[English](../../en/btc/btc-addr-convert.md) · **简体中文** · [← 文档总览](../index.md)

# BTC 地址类型转换（Address Format Convert）· BTC

> 输入一个地址或压缩公钥，换算出 Legacy / Nested SegWit / Native SegWit / Taproot 各形态。

## 什么时候用

- 拿到一个地址，想看它对应的其他类型形态（如从 Legacy 看 Native SegWit）。
- 有一段压缩公钥，想直接推出它在各类型下的地址。
- 核对不同格式其实指向同一把密钥。

## 使用步骤

1. 选择网络：**主网** 或 **测试网**。
2. 在输入框填入地址（`1` / `3` / `bc1q` / `bc1p…`）或压缩公钥（`02` / `03…`，66 位 hex）。
3. 转换结果自动显示各形态地址。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 网络 | 主网 / 测试网 |
| 输入 | 地址（Legacy / Nested SegWit / Native SegWit / Taproot）或压缩公钥（`02` / `03` + 64 hex，共 66 位） |
| 输出 | Legacy / Nested SegWit / Native SegWit / Taproot 各形态地址 |

## 注意事项 & 常见坑

- **不同形态 ≠ 不同资金**：它们由同一把密钥推导，但链上是不同地址，余额各自独立。
- 仅接受**压缩公钥**（`02` / `03` 开头、66 位 hex）作为公钥输入。
- 选对网络：主网与测试网前缀不同，结果不能跨网通用。
- 转换只做形态换算，不涉及私钥，也不查询余额。

## 相关工具

- [生成 BTC 钱包](./btc-wallet.md) — 本地生成各类型地址
- [BTC 余额批量查询](./btc-balance.md) — 查各形态地址余额
- [UTXO 查询](./btc-utxo.md) — 查看未花费输出
- [安全模型](../security.md)

---

> 免责声明：不同形态为独立链上地址，向哪种形态收款请以对方指定为准。
