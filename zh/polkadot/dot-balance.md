[English](../../en/polkadot/dot-balance.md) · **简体中文** · [← 文档总览](../index.md)

# Polkadot 余额查询（Polkadot Balance）

> 按 SS58 地址查询 Polkadot / Kusama 账户余额，可转账、冻结、保留分开列出。

## 什么时候用

- 想知道某个账户**现在能动多少钱**（而不只是链上总额）。
- 转账前确认可转账余额够不够 —— 质押、治理投票、vesting 都会冻住一部分。
- 需要账户的当前 nonce（构造离线交易时用）。
- 对着自建节点查询，而不想依赖第三方浏览器。

## 使用步骤

1. 选择**网络**（Polkadot / Kusama / Westend 测试网）。
2. （可选）填**自定义 RPC**。填 https 端点即可 —— 本工具走 HTTP JSON-RPC，
   不需要 WebSocket。
3. 粘贴 **SS58 地址**，点**查询**。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 网络 | Polkadot / Kusama / Westend |
| 自定义 RPC（可选） | https JSON-RPC 端点，留空用公共节点 |
| 账户地址 | SS58 格式，实时校验校验和 |
| 可转账 | `free − max(frozen − reserved, 0)`，**这才是现在能动的钱** |
| 自由余额 free | 未被保留的余额，但其中可能有一部分被冻结 |
| 保留 reserved | 被链上功能锁定的押金（如身份、代理、多签） |
| 冻结 frozen | 被质押 / 投票 / vesting 锁住的量 |
| 总额 | free + reserved |
| Nonce | 该账户已发出的交易数 |

## 注意事项 & 常见坑

- **可转账 ≠ free。** 这是这一页最重要的一件事。质押、治理投票、vesting 都会冻住
  一部分 free，直接把 free 当成「我有多少钱」会高估 —— 发起转账时才发现不够。
  所以可转账排在第一行。
- **SS58 前缀不同不影响查询。** 同一个 AccountId 在所有 Substrate 链上都有效，
  只是地址的显示格式不同。用 Kusama 格式的地址查 Polkadot 余额是合理的，
  页面会提示一句而不会拦住你。
- **「链上没有这个账户」不是查询失败。** 它意味着该地址从未收到过资产，
  或者余额曾低于**存在性押金**而被链上清除（Substrate 特有机制：余额低于门槛的账户
  会被删除以回收存储）。
- **「冻结」的含义随运行时版本而变**：新版运行时指质押 / 投票 / vesting 锁定量，
  旧版该字段是 `miscFrozen`。两者字节布局完全相同，本地分辨不出来 ——
  Polkadot 与 Kusama 目前都是新版。
- **这是只读查询**，不需要连接钱包，也不会要求任何私钥。

## 相关工具

- [SS58 地址转换](./dot-ss58.md) — SS58 ↔ AccountId32
- [Polkadot 钱包生成](./dot-wallet.md) — 本地生成 Substrate 钱包
- [DOT 单位换算](./dot-unit.md) — Planck ↔ 主单位
- [Substrate Hash / Storage Key](./dot-hash-storage.md) — 由 AccountId 推导存储键
- [安全模型](../security.md)
