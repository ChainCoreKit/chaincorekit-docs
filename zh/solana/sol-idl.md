[English](../../en/solana/sol-idl.md) · **简体中文** · [← 文档总览](../index.md)

# Program IDL 浏览器（Program IDL）· Solana

> 上传或粘贴 Anchor IDL，结构化浏览指令、账户、类型、事件与错误；不依赖链上一定存在 IDL。

## 什么时候用

- 拿到一份 Anchor IDL，想快速看清它有哪些指令、账户、类型、事件和错误码。
- program 链上没有发布 IDL，但你手上有 JSON 文件，想离线阅读其结构。
- 编解码指令前，先浏览一遍 IDL 结构确认字段。

## 使用步骤

1. 在 **Anchor IDL** 卡片：
   - 直接粘贴 IDL JSON；或点击**选择 IDL 文件**上传 `.json`；或点击**载入示例 IDL**。
2. 载入后，**IDL 内容**卡片会结构化列出：指令、账户、类型、事件与错误。
3. 未载入时显示空状态引导；载入成功后自动填充。

> 通过 Program ID 从链上拉取 IDL 需只读 RPC，为**即将支持**功能。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| Anchor IDL | 粘贴 IDL JSON、上传 `.json` 文件，或载入示例 |
| Program ID | 链上拉取 IDL 的入口（即将支持） |
| 输出 | 结构化的指令 / 账户 / 类型 / 事件 / 错误列表 |

## 注意事项 & 常见坑

- **纯本地解析**：仅解析你提供的 JSON，不联网、不校验链上是否存在同名 program。
- **IDL 版本要对**：不同版本的 program 对应不同 IDL，用错版本会看到过期的指令 / 字段。
- **链上拉取暂未开放**：目前只能粘贴或上传 IDL，Program ID 拉取为即将支持。

## 相关工具

- [Instruction 编解码](./sol-instruction.md) — 依同一份 IDL 编解码 Instruction Data
- [PDA / ATA 计算](./sol-address.md) — 计算 program 用到的 PDA / ATA
- [Compute / Fee / Rent](./sol-fee-rent.md) — 估算交易费用
- [安全模型](../security.md)

---

> 免责声明：展示内容完全来自你提供的 IDL，请自行确认其与目标 program 一致。
