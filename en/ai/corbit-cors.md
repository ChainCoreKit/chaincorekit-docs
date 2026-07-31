**English** · [简体中文](../../zh/ai/corbit-cors.md) · [← Docs home](../index.md)

# Corbit endpoint CORS setup

> Read this when Corbit says "This endpoint doesn't allow browser requests (CORS)".

Corbit talks to the OpenAI-compatible endpoint you configure **straight from the browser**: the request and your API key go to that endpoint directly, never through a ChainCore Kit server. That is also why your key never reaches a third party.

The trade-off is the browser's same-origin policy — the endpoint has to state in its response that this page is allowed to call it, otherwise the browser blocks the request. Only the endpoint side can do that; the app cannot do it for you.

Start by working out which case you're in:

| Case                                                        | What to do                    | Anything to deploy? |
| ----------------------------------------------------------- | ----------------------------- | ------------------- |
| You run the endpoint, or can change its config               | Option A: add CORS headers    | No                  |
| It's a third-party relay whose responses you can't change    | Option B: run your own relay  | Yes (a small one)   |

---

## First, confirm it really is CORS

The browser reports "blocked by CORS" and "host unreachable" as the same failure, so check DevTools:

- Console shows `blocked by CORS policy` or `No 'Access-Control-Allow-Origin' header` → it's CORS, keep reading.
- The request shows up as `(failed)` in the Network panel with no response headers → most likely CORS too (the preflight was rejected).
- You can see a 401 / 429 status → not CORS, that's auth or rate limiting.

One thing people miss: Corbit sends JSON with an `Authorization` header, so **the browser always sends an `OPTIONS` preflight first**. Setting `Access-Control-Allow-Origin` but not handling `OPTIONS` still gets you blocked.

---

## Option A: you run the endpoint (recommended)

Add the response headers on the gateway itself, or on the reverse proxy in front of it. **Nothing extra to deploy.**

### Headers you need

```
Access-Control-Allow-Origin: <your-site-origin>
Access-Control-Allow-Headers: authorization, content-type
Access-Control-Allow-Methods: GET, POST, OPTIONS
```

Prefer an explicit origin over `*`; keep `*` for debugging only.

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

    proxy_pass http://127.0.0.1:3000;   # your gateway
    proxy_buffering off;                # keep streaming replies streaming
}
```

Two things that bite people:

- **Don't drop `always`.** Without it nginx only attaches the headers to 2xx / 3xx responses, so when the endpoint returns a 500 the headers vanish and the browser shows a CORS error that hides the real one.
- **Answer `OPTIONS` with a 204 yourself.** Don't let the preflight reach the backend — it usually doesn't know `OPTIONS` and answers 404 / 405, which fails the preflight.

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

### Traefik (dynamic config)

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

Attach `corbit-cors` to the router's `middlewares`. Traefik answers the preflight itself, so no extra `OPTIONS` rule is needed.

### Gateways like one-api, new-api, LiteLLM

These ship their own CORS settings — use those instead of layering a second set on top. Configuring both produces duplicate `Access-Control-Allow-Origin` headers, which browsers also reject:

- **one-api / new-api**: the admin panel has an allowed-origins setting; some builds take it as an environment variable or start-up flag — check the CORS section of that version's docs.
- **LiteLLM Proxy**: set the allowed origins under `general_settings` in `config.yaml`, or use the CORS environment variables from the official image.

### Verify

Reload the config (`nginx -s reload`, restart the container), then confirm the preflight actually passes:

```bash
curl -i -X OPTIONS 'https://your-gateway.example.com/v1/chat/completions' \
  -H 'Origin: https://your-site.example.com' \
  -H 'Access-Control-Request-Method: POST' \
  -H 'Access-Control-Request-Headers: authorization, content-type'
```

You want a `204` (or `200`) plus the three `Access-Control-Allow-*` headers. Then hit "Test connection" in Corbit's settings.

---

## Option B: the endpoint isn't yours

Only the responder can send CORS headers. If the third party won't, your only move is to send the request somewhere you control and have that forward it.

This means running a relay of your own — yours, unrelated to ChainCore Kit. The app itself proxies nothing.

### Cloudflare Worker (quickest, free tier)

1. Cloudflare Dashboard → Workers & Pages → Create → Worker.
2. Paste the code below, then edit the `UPSTREAM` and `ALLOW_ORIGIN` constants.
3. Deploy and copy the `https://xxx.workers.dev` URL.
4. Back in Corbit's settings, set the API endpoint to `https://xxx.workers.dev/v1` and keep your existing API key.

```js
// Cloudflare Worker — CORS relay for an OpenAI-compatible endpoint.
// UPSTREAM is fixed here on purpose: the moment the caller can pick the target,
// this Worker becomes an open proxy anyone can ride for free.
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
    // Preflight: answer 204 here, never forward it upstream.
    if (request.method === 'OPTIONS') {
      return new Response(null, { status: 204, headers: CORS });
    }

    const url = new URL(request.url);
    const target =
      UPSTREAM.replace(/\/+$/, '') + url.pathname.replace(/^\/v1/, '') + url.search;

    // Pass bodies through untouched so SSE streaming isn't buffered or cut off.
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

Notes:

- **Your key only ever passes through your own Worker**, never a ChainCore Kit server. The code above logs nothing and stores nothing — keep it that way.
- The `Authorization` header is forwarded as-is; the Worker neither needs nor should hardcode your key.
- To tighten it further, reject requests whose `Origin` isn't `ALLOW_ORIGIN` with a 403 at the top of `fetch`.

### Already have a server? An nginx reverse proxy does the same

```nginx
location /relay/ {
    proxy_pass https://your-endpoint.example.com/;   # the trailing / strips the /relay prefix
    proxy_set_header Host your-endpoint.example.com;
    proxy_buffering off;

    add_header Access-Control-Allow-Origin  $http_origin always;
    add_header Access-Control-Allow-Headers "authorization, content-type" always;
    add_header Access-Control-Allow-Methods "GET, POST, OPTIONS" always;

    if ($request_method = OPTIONS) { return 204; }
}
```

Then use `https://your-server.example.com/relay/v1` as the endpoint.

---

## Don't do this

- **Don't use a public CORS proxy** (`cors-anywhere` and friends). Your API key travels in the clear through a stranger's server.
- **Don't let the caller choose the relay target.** That's an anonymous open proxy for the whole internet, billed to you.
- **Don't disable browser security to get around it** (`--disable-web-security` and similar). It only "works" on your machine, and it strips protection from every site you visit.

---

## Related

- [Security model](../security.md)
- [FAQ](../faq.md)
