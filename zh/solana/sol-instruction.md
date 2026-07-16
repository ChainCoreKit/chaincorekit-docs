[English](../../en/solana/sol-instruction.md) · **简体中文** · [← 文档总览](../index.md)

# Instruction 编解码（Instruction Codec）· Solana

> 依 Anchor IDL 编码 / 解码 Instruction Data（discriminator + Borsh 参数）。

## 什么时候用

- 想手动构造某条 Anchor 指令的 Instruction Data，检查参数序列化是否正确。
- 拿到一段 hex / base58 的 Instruction Data，想反查它对应哪条指令、参数是什么。
- 调试交易时核对 discriminator 与 Borsh 编码结果。

## 使用步骤

1. 在 **Anchor IDL** 卡片粘贴 IDL JSON，或点击**载入示例 IDL**。
2. 在**编解码**卡片选择模式：

   ### 编码
   - 从**指令**下拉选择一条指令。
   - 按提示填入各**参数**（Borsh 类型）与相关**账户**。
   - 点击**编码为 Instruction Data**，结果区给出编码后的字节。

   ### 解码
   - 在 **Instruction Data** 框粘贴 `0x…` hex 或 base58 数据。
   - 点击**解码**，按 IDL 匹配 discriminator 并还原参数。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| Anchor IDL | Anchor IDL JSON（粘贴或载入示例） |
| 模式 | `编码` / `解码` |
| 指令 | 编码模式下从 IDL 指令列表选择 |
| 参数 | 按指令定义的 Borsh 类型逐项填入 |
| Instruction Data | 解码模式输入，`0x…` hex 或 base58 |
| 输出 | 编码后的 Instruction Data；或解码出的指令名与参数 |

## 注意事项 & 常见坑

- **discriminator 前缀**：Anchor 指令数据以 8 字节 discriminator 开头，其后才是 Borsh 参数；解码依赖 IDL 中的定义匹配。
- **IDL 要对得上 program**：用错版本的 IDL 会导致 discriminator 匹配不到或参数错位。
- **hex / base58 二选一**：解码输入按 `0x` 前缀识别 hex，否则按 base58 解析，注意别混用。
- **复杂类型**：嵌套 struct / enum 等按 IDL 定义序列化，填参时类型要与定义一致。

## 相关工具

- [Program IDL 浏览器](./sol-idl.md) — 先结构化浏览 IDL 再编解码
- [PDA / ATA 计算](./sol-address.md) — 计算指令用到的 PDA / ATA
- [Compute / Fee / Rent](./sol-fee-rent.md) — 估算交易费用
- [安全模型](../security.md)

---

> 免责声明：编解码结果依赖你提供的 IDL 是否与目标 program 一致，请自行核对。
