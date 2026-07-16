[English](../../en/solana/sol-address.md) · **简体中文** · [← 文档总览](../index.md)

# PDA / ATA 计算（PDA / ATA）· Solana

> 本地计算 Program Derived Address（PDA + 规范 bump）与 Associated Token Account（ATA），并区分 Token Program 与 Token-2022。

## 什么时候用

- 开发 Anchor / 原生 program 时，需要预先算出某组 seeds 对应的 PDA 与 bump。
- 要确定某个 owner 在某个 mint 下的 ATA 地址（转账、建账前核对）。
- 分辨同一 mint 在 Token Program 与 Token-2022 下派生出的不同 ATA。

## 使用步骤

### PDA 模式

1. 在顶部切到 **PDA**。
2. 填入 **Program ID**（base58）。
3. 逐条添加 **Seeds**：单条 ≤ 32 字节，最多 15 条；整数按 little-endian 处理。
4. 结果区展示派生出的 PDA 地址与规范 **bump**。

### ATA 模式

1. 在顶部切到 **ATA**。
2. 填入 **Owner**（base58 owner pubkey）与 **Mint**（base58 mint pubkey）。
3. 选择 **Token Program**：`Token Program` 或 `Token-2022`。
4. 结果区展示对应的 ATA 地址。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| Program ID | base58 编码的 program 公钥（PDA 模式） |
| Seeds | 单条 ≤ 32 字节，最多 15 条；整数按 little-endian |
| Owner | base58 owner pubkey（ATA 模式） |
| Mint | base58 mint pubkey（ATA 模式） |
| Token Program | `Token Program` / `Token-2022` |
| 输出 | PDA 地址 + 规范 bump（PDA）；ATA 地址（ATA） |

## 注意事项 & 常见坑

- **规范 bump**：PDA 用「让派生落在 ed25519 曲线之外」的最大 bump（规范 bump）；换 bump 会得到不同地址。
- **Seed 类型要一致**：整数默认 little-endian，字符串按原始字节。与链上 program 里的 seed 编码方式必须完全一致，否则地址对不上。
- **Token Program 选错 = 地址错**：Token 与 Token-2022 是不同的 program id，同一 owner/mint 会派生出**不同**的 ATA，务必按 mint 实际所属选择。
- **单条 seed ≤ 32 字节**：超长 seed 需先自行哈希再作为 seed。

## 相关工具

- [Instruction 编解码](./sol-instruction.md) — 依 IDL 编解码 Instruction Data
- [Program IDL 浏览器](./sol-idl.md) — 结构化浏览 Anchor IDL
- [Solana 钱包生成](./sol-wallet.md) — 本地生成 / 导入钱包
- [安全模型](../security.md)

---

> 免责声明：地址派生依赖你提供的 Program ID / seeds / Token Program，请自行核对与链上一致。
