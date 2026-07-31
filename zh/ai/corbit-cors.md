[English](../../en/ai/corbit-cors.md) · **简体中文** · [← 文档总览](../index.md)

# Corbit 端点跨域（CORS）配置

> Corbit 提示「该端点未允许浏览器跨域访问（CORS）」时，按本文配置你的端点。

Corbit 是**浏览器直连**你自己填的 OpenAI 兼容端点：请求与 API Key 从浏览器直接发往该端点，不经过 ChainCore Kit 的任何服务器。这也是 Key 不会落到第三方手里的原因。

代价是浏览器的同源策略会介入——端点必须在响应里声明「允许这个网页调用我」，否则请求会被浏览器拦下。这一步只能在端点侧完成，应用本身无法代劳。

先判断你属于哪种情况：

| 情况                               | 怎么做                 | 要不要额外部署程序 |
| ---------------------------------- | ---------------------- | ------------------ |
| 端点是你自建 / 可改配置的网关      | 方案 A：加 CORS 响应头 | 不需要             |
| 端点是第三方中转站，改不了它的响应 | 方案 B：自建一个中转   | 需要（很轻）       |

---

## 先确认确实是跨域问题

浏览器把「跨域被拦」和「网络不通」报成同一种失败，所以要看浏览器开发者工具：

- Console 出现 `blocked by CORS policy` 或 `No 'Access-Control-Allow-Origin' header` → 是跨域，按本文处理。
- Network 面板里那条请求显示 `(failed)`、且没有任何响应头 → 大概率也是跨域（预检就被拒了）。
- 能看到 401 / 429 等状态码 → 不是跨域，是鉴权或限流问题。

一个容易被忽略的点：Corbit 发的是带 `Authorization` 头的 JSON 请求，**浏览器一定会先发一个 `OPTIONS` 预检**。只配了 `Access-Control-Allow-Origin` 却没处理 `OPTIONS`，照样会被拦。

---

## 方案 A：端点是你自建的（推荐）

在网关本身、或它前面的反向代理上补齐响应头即可，**不需要部署任何新程序**。

### 需要的响应头

```
Access-Control-Allow-Origin: <你的站点域名>
Access-Control-Allow-Headers: authorization, content-type
Access-Control-Allow-Methods: GET, POST, OPTIONS
```

`Access-Control-Allow-Origin` 建议填具体域名而不是 `*`，只在调试期用 `*`。

### nginx

```nginx
location /v1/ {
    if ($request_method = OPTIONS) {
        add_header Access-Control-Allow-Origin  $http_origin always;
        add_header Access-Control-Allow-Headers "authorization, content-type" always;
        add_header Access-Control-Allow-Methods "GET, POST, OPTIONS" always;
        add_header Access-Control-Max-Age      86400 always;
        return 204;
    }

    add_header Access-Control-Allow-Origin  $http_origin always;
    add_header Access-Control-Allow-Headers "authorization, content-type" always;
    add_header Access-Control-Allow-Methods "GET, POST, OPTIONS" always;

    proxy_pass http://127.0.0.1:3000;   # 你的网关地址
    proxy_buffering off;                # 关掉缓冲，否则流式回复会被攒成一坨再吐出来
}
```

两个高频踩坑点：

- **`always` 不能省**。不带 `always` 时 nginx 只在 2xx / 3xx 响应上加头；端点报 500 时头就没了，浏览器只显示跨域错误，把真正的报错盖掉。
- **`OPTIONS` 要单独 204 返回**，别让预检穿透到后端——后端多半不认识 `OPTIONS`，会返回 404 / 405，预检即失败。

### Caddy

```caddyfile
your-gateway.example.com {
    @preflight method OPTIONS
    handle @preflight {
        header {
            Access-Control-Allow-Origin  "{http.request.header.Origin}"
            Access-Control-Allow-Headers "authorization, content-type"
            Access-Control-Allow-Methods "GET, POST, OPTIONS"
            Access-Control-Max-Age       "86400"
        }
        respond 204
    }

    header {
        Access-Control-Allow-Origin  "{http.request.header.Origin}"
        Access-Control-Allow-Headers "authorization, content-type"
        Access-Control-Allow-Methods "GET, POST, OPTIONS"
    }
    reverse_proxy 127.0.0.1:3000
}
```

### Traefik（动态配置）

```yaml
http:
  middlewares:
    corbit-cors:
      headers:
        accessControlAllowOriginList:
          - https://your-site.example.com
        accessControlAllowHeaders:
          - authorization
          - content-type
        accessControlAllowMethods:
          - GET
          - POST
          - OPTIONS
        accessControlMaxAge: 86400
        addVaryHeader: true
```

把 `corbit-cors` 挂到对应 router 的 `middlewares` 上即可。Traefik 会自行处理预检，不需要额外的 `OPTIONS` 规则。

### one-api / new-api / LiteLLM 等网关

这类网关通常自带 CORS 配置，优先用它们的开关，别在外面再叠一层——两边都加会产生重复的 `Access-Control-Allow-Origin` 头，浏览器同样判定失败：

- **one-api / new-api**：后台「系统设置」里有允许跨域来源的配置项；部分版本走环境变量或启动参数，查对应版本文档的 CORS / 跨域一节。
- **LiteLLM Proxy**：`config.yaml` 的 `general_settings` 下配置允许的来源，或用官方镜像提供的 CORS 环境变量。

### 验证

改完重载配置（`nginx -s reload` / 重启容器），用这条命令确认预检真的通了：

```bash
curl -i -X OPTIONS 'https://your-gateway.example.com/v1/chat/completions' \
  -H 'Origin: https://your-site.example.com' \
  -H 'Access-Control-Request-Method: POST' \
  -H 'Access-Control-Request-Headers: authorization, content-type'
```

期望看到 `204`（或 `200`）以及三个 `Access-Control-Allow-*` 头。然后回到 Corbit 设置点「测试连接」。

---

## 方案 B：端点不可控（第三方中转站）

跨域响应头只能由**响应方**给。第三方不给，你就只能让请求先打到一个你能控制的地方，由它转发。

这条路需要你自己部署一个中转——是你自己的，与 ChainCore Kit 无关，应用本身不代理任何请求。

### Cloudflare Worker（最省事，免费）

1. 登录 Cloudflare Dashboard → Workers & Pages → Create → Worker。
2. 把下面的代码粘进编辑器，改掉 `UPSTREAM` 和 `ALLOW_ORIGIN` 两个常量。
3. Deploy，拿到形如 `https://xxx.workers.dev` 的地址。
4. 回到 Corbit 设置，把「API 端点」改成 `https://xxx.workers.dev/v1`，API Key 保持原来那个。

```js
// Cloudflare Worker —— OpenAI 兼容端点的 CORS 中转。
// UPSTREAM 必须写死在代码里：一旦允许请求方指定转发目标，
// 这个 Worker 就变成了谁都能白嫖的开放代理。
const UPSTREAM = 'https://your-endpoint.example.com/v1';
const ALLOW_ORIGIN = 'https://your-site.example.com';

const CORS = {
  'Access-Control-Allow-Origin': ALLOW_ORIGIN,
  'Access-Control-Allow-Headers': 'authorization, content-type',
  'Access-Control-Allow-Methods': 'GET, POST, OPTIONS',
  'Access-Control-Max-Age': '86400',
};

export default {
  async fetch(request) {
    // 预检：直接 204，不要转发到上游。
    if (request.method === 'OPTIONS') {
      return new Response(null, { status: 204, headers: CORS });
    }

    const url = new URL(request.url);
    const target =
      UPSTREAM.replace(/\/+$/, '') + url.pathname.replace(/^\/v1/, '') + url.search;

    // 请求体与响应体原样透传，流式回复（SSE）才不会被截断或攒批。
    const upstream = await fetch(target, {
      method: request.method,
      headers: request.headers,
      body: request.body,
    });

    const headers = new Headers(upstream.headers);
    for (const [k, v] of Object.entries(CORS)) headers.set(k, v);
    return new Response(upstream.body, { status: upstream.status, headers });
  },
};
```

几点说明：

- **Key 只经过你自己的 Worker**，不进入 ChainCore Kit 的任何服务器。上面的代码不打日志、不落存储，请保持这一点。
- `Authorization` 头随请求原样透传，Worker 不需要也不应该硬编码你的 Key。
- 想更严一点，可以在 `fetch` 开头校验 `request.headers.get('Origin') === ALLOW_ORIGIN`，非本站来源直接 403。

### 已有服务器的话，nginx 反代同样可以

```nginx
location /relay/ {
    proxy_pass https://your-endpoint.example.com/;   # 结尾的 / 会剥掉 /relay 前缀
    proxy_set_header Host your-endpoint.example.com;
    proxy_buffering off;

    add_header Access-Control-Allow-Origin  $http_origin always;
    add_header Access-Control-Allow-Headers "authorization, content-type" always;
    add_header Access-Control-Allow-Methods "GET, POST, OPTIONS" always;

    if ($request_method = OPTIONS) { return 204; }
}
```

端点填 `https://your-server.example.com/relay/v1`。

---

## 不要这么做

- **不要用公共 CORS 代理**（`cors-anywhere` 及各类 `corsproxy` 服务）。你的 API Key 会明文经过一个陌生人的服务器。
- **不要把中转做成「目标由请求方指定」**。那等于对全网开放一个匿名代理，账单和封禁都算在你头上。
- **不要靠关闭浏览器安全策略绕过**（`--disable-web-security` 之类）。那只在你这台机器上「有效」，且会让浏览器里所有网站都失去保护。

---

## 相关文档

- [安全模型](../security.md)
- [常见问题 FAQ](../faq.md)
