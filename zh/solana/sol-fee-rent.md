[English](../../en/solana/sol-fee-rent.md) · **简体中文** · [← 文档总览](../index.md)

# Compute / Fee / Rent · Solana

> 本地估算 Solana 交易的 Compute Unit、签名费、优先费，以及账户免租余额（Rent Exemption），无需连网。

## 什么时候用

- 想估算一笔交易的总费用：基础签名费 + 优先费（priority fee）。
- 设置 Compute Budget（CU Limit / CU Price）时，先算清对应的优先费成本。
- 建账户前，想知道达到 Rent Exemption 需要预存多少 lamports。

## 使用步骤

### 交易费用

1. 填 **签名数**（默认 1）——每个签名收取固定的基础费。
2. 填 **CU Limit**（0 – 1,400,000，默认 200000）。
3. 填 **CU Price**（micro-lamports / CU，默认 0）——即每个 Compute Unit 的优先费单价。
4. 结果区给出估算的签名费、优先费与合计（lamports / SOL）。

> 通过 `getRecentPrioritizationFees` 获取实时优先费需只读 RPC，为**即将支持**功能。

### 账户免租（Rent Exemption）

1. 填 **Account Size**（字节，默认 165，即 SPL Token 账户大小）。
2. 结果区给出该大小账户达到免租所需的最低余额。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 签名数 | 交易签名个数，默认 1 |
| CU Limit | 0 – 1,400,000，默认 200000 |
| CU Price | micro-lamports / CU，默认 0（无优先费） |
| Account Size | 账户字节数，默认 165（SPL Token 账户） |
| 输出 | 签名费 / 优先费 / 合计；免租最低余额（lamports 与 SOL） |

## 注意事项 & 常见坑

- **单位换算**：1 SOL = 1,000,000,000 lamports；优先费单价按 **micro-lamports / CU** 计（1 lamport = 10⁶ micro-lamports），别把两个单位搞混。
- **优先费 = CU Limit × CU Price**：CU Price 为 0 时没有优先费，只有基础签名费。
- **CU Limit 上限**：单笔交易的 Compute Unit 上限为 1,400,000。
- **免租按大小算**：Rent Exemption 最低余额随 Account Size 变化；账户越大预存越多。
- **本地估算**：为无需连网的静态估算，实时优先费与链上实际费率可能有差异。

## 相关工具

- [Instruction 编解码](./sol-instruction.md) — 依 IDL 编解码 Instruction Data
- [PDA / ATA 计算](./sol-address.md) — 计算 PDA 与 ATA
- [Program IDL 浏览器](./sol-idl.md) — 结构化浏览 Anchor IDL
- [安全模型](../security.md)

---

> 免责声明：以上为本地静态估算，实际上链费用以网络当时状态为准。
