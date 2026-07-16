[English](../../en/polkadot/dot-ss58.md) · **简体中文** · [← 文档总览](../index.md)

# SS58 地址转换（SS58 Convert）

> SS58 地址 ↔ AccountId32，在不同网络前缀间转换并校验；同一 AccountId32、不同前缀只是地址表示不同。

## 什么时候用

- 拿到一个 Polkadot 地址，想看它在 Kusama 或通用 Substrate 前缀下的写法。
- 手上有 AccountId32 / Public Key（`0x` + 64 hex），需要还原成可读的 SS58 地址。
- 想校验一个 SS58 地址是否合法（校验位是否正确）。

> ⚠️ 前缀转换只改变地址的文本表示，底层 AccountId32 不变；**这不等于跨链可直接转账**。

## 使用步骤

1. 在输入框粘贴 **SS58 地址**（如 `5Grwva…`）或 **AccountId32 / Public Key**（`0x` + 64 hex）。
2. 选择**目标 SS58 前缀**：
   - **Polkadot (0)**
   - **Kusama (2)**
   - **Substrate 通用 (42)**
   - **自定义**：选中后填入前缀整数（0–16383）。
3. 结果区自动给出目标前缀下的 SS58 地址及对应的 AccountId32。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 输入 | SS58 地址，或 AccountId32 / Public Key（`0x` + 64 hex） |
| 目标 SS58 前缀 | Polkadot (0) / Kusama (2) / Substrate 通用 (42) / 自定义 |
| 自定义前缀 | 前缀整数，范围 0–16383 |
| 输出 | 目标前缀下的 SS58 地址与底层 AccountId32 |

## 注意事项 & 常见坑

- **前缀 ≠ 账户不同**：Polkadot、Kusama、Substrate 地址底层是同一个 AccountId32，只是前缀不同导致文本不同。
- **换前缀不等于跨链**：把地址转成 Kusama 前缀，并不代表 Polkadot 上的资产能直接转到 Kusama，跨链需走桥或 XCM。
- **SS58 自带校验位**：粘贴错一个字符通常会校验失败，转换前会先校验合法性。
- **前缀范围 0–16383**：自定义前缀请填这一区间内的整数，Polkadot=0、Kusama=2、通用 Substrate=42 是最常见的几个。

## 相关工具

- [Polkadot 钱包生成](./dot-wallet.md) — 本地生成 Substrate 钱包
- [Substrate Hash / Storage Key](./dot-hash-storage.md) — 由 AccountId 推导 Storage Key
- [DOT 单位换算](./dot-unit.md) — Planck ↔ 主单位
- [SCALE 编解码](./dot-scale.md) — 按类型表达式编 / 解码
- [安全模型](../security.md)

---

> 免责声明：地址转换仅改变文本表示，转账前请确认目标链与地址无误。
