<div align="center">

# ChainCore Kit · 文档

**面向 Web3 开发者的本地优先多链工具箱。**
生成钱包、解码 Calldata、可视化调用合约、批量操作——私钥全程不出本机。

[English](./README.md) · 简体中文

</div>

---

> [!IMPORTANT]
> 本仓库**仅包含文档**。ChainCore Kit 应用本身为专有软件，未在此发布。本仓库不授予应用源代码的任何许可。详见 [LICENSE](./LICENSE)。

## ChainCore Kit 是什么？

ChainCore Kit 是一个浏览器端开发者工具箱，覆盖 **EVM、Bitcoin、NFT、Solana、Polkadot** 多个生态。助记词与私钥生成、钱包派生、交易签名等敏感操作全部在你的浏览器本地完成，**私钥与助记词不上传、不存储、不出本机**。

本文档说明每个工具的用途、用法，以及背后的 Web3 概念。

## 文档索引

完整索引：[中文](./zh/index.md) · [English](./en/index.md)

| 分类 | 工具 |
| --- | --- |
| **EVM** | 测试币水龙头 · 生成钱包 · 靓号地址 · ABI 可视化调用 · 签名选择器查询 · 单位换算 · 交易分析 · 地址转换与 ENS · 事件主题 TopicID · Hash 工具 · Calldata 编解码 · Token 发行 |
| **Bitcoin** | 生成钱包 · 地址类型转换 · 余额批量查询 · UTXO 查询 · PSBT 解码 |
| **NFT** | 预览 · 发行 |
| **Solana** | 钱包生成 · PDA / ATA 计算 · Instruction 编解码 · Program IDL · Compute / Fee / Rent |
| **Polkadot** | 钱包生成 · SS58 地址转换 · DOT 单位换算 · Hash / Storage Key · SCALE 编解码 |
| **批量操作** | Disperse 分发 · 钱包逐笔转账 · 私钥批量转账 · 私钥归集 Sweep · 余额批量查询 |

## 快速链接

- 快速开始：[zh/index.md](./zh/index.md)
- 安全模型：[zh/security.md](./zh/security.md)
- 常见问题：[zh/faq.md](./zh/faq.md)
- 术语表：[zh/glossary.md](./zh/glossary.md)

## 参与贡献

欢迎修正文档与提交翻译。请先阅读 [CONTRIBUTING.md](./CONTRIBUTING.md) 与[行为准则](./CODE_OF_CONDUCT.md)。

## 安全披露

发现文档中的安全问题（如危险或误导性指引）？见 [SECURITY.md](./SECURITY.md)。应用本身的问题请通过应用内反馈渠道提交。

## 免责声明

ChainCore Kit 及本文档按**「现状」提供，不附带任何形式的担保**。你需自行妥善保管私钥与助记词，并对自己签署、广播的任何交易负全部责任。本文档不构成任何金融、法律或投资建议。签名前请务必核对地址、金额与网络。**私钥丢失或误操作导致的损失不可逆。**

## 许可证

正文与图片采用 [CC BY 4.0](./LICENSE) 许可；文档内嵌的代码片段额外以 MIT 许可提供。本许可仅覆盖文档，**不含** ChainCore Kit 应用。
