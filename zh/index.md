[English](../en/index.md) · **简体中文** · [← 仓库首页](../README.zh-CN.md)

# ChainCore Kit 文档总览

ChainCore Kit 是一个浏览器端的多链开发者工具箱，覆盖 **EVM、Bitcoin、NFT、Solana、Polkadot** 生态。助记词/私钥生成、钱包派生、交易签名等敏感操作全部在本地完成——**私钥与助记词不上传、不存储、不出本机**。

> 先读一遍[安全模型](./security.md)，再动手用涉及私钥的工具。

## 快速开始

1. 打开 ChainCore Kit 应用，顶部选择生态（EVM / BTC / NFT / Solana / Polkadot / 批量操作），或用左侧边栏 / `⌘K` 搜索工具。
2. **只读工具**（换算、解码、查询等）无需连接钱包即可使用。
3. **写操作 / 签名工具**需先连接钱包；未连接时按钮显示「连接钱包后可用」，点击即拉起连接。
4. 涉及私钥/助记词的结果默认打码，点击眼睛图标才显示，请在安全环境下查看与保存。

## 工具索引

### EVM 工具

| 工具 | 说明 |
| --- | --- |
| [测试币水龙头](./evm/faucet.md) | 汇总各测试网水龙头入口 |
| [生成钱包](./evm/generate-wallet.md) | 本地批量生成 EVM 钱包，支持助记词/私钥导入 |
| [靓号地址](./evm/vanity.md) | 生成带指定前后缀的地址 |
| [ABI 可视化调用](./evm/abi.md) | 导入 ABI 图形化读写合约 |
| [签名选择器查询](./evm/query-selector.md) | 4byte 选择器 ↔ 函数签名互查 |
| [单位换算](./evm/unit-convert.md) | Wei / Gwei / Ether 换算 |
| [交易分析](./evm/trace-view.md) | 解析交易的资金流、事件与调用 |
| [地址转换与 ENS](./evm/address.md) | EIP-55 校验、ENS 解析 |
| [事件主题 TopicID](./evm/topic-id.md) | 计算事件签名的 TopicID |
| [Hash 工具](./evm/hash-tool.md) | keccak-256 等哈希计算 |
| [Calldata 编解码](./evm/calldata.md) | 编码/解码交易 Calldata |
| [ABI 编解码](./evm/abi-codec.md) | 构造函数参数编码、事件日志与 revert 错误解码 |
| [交易数据解码](./evm/tx-decode.md) | 原始已签名交易与 RLP 解码，支持到 EIP-4844 / 7702 |
| [签名验证](./evm/sig-verify.md) | EIP-191 消息与 EIP-712 结构化数据的哈希与验签 |
| [RPC 诊断](./evm/rpc-check.md) | 检查端点连通、chainId、区块高度、响应时间与只读能力 |
| [合约检查](./evm/contract-check.md) | 字节码、代理实现、管理员槽与 EIP-7702 委托 |
| [授权管理](./evm/approvals.md) | 查询指定 Token / spender 的授权额度并撤销 |
| [Token 发行](./evm/token-issuance.md) | 部署 ERC-20 代币 |

### Bitcoin 工具

| 工具 | 说明 |
| --- | --- |
| [生成 BTC 钱包](./btc/btc-wallet.md) | 本地生成 BTC 钱包 |
| [地址类型转换](./btc/btc-addr-convert.md) | Legacy / SegWit / Taproot 互转 |
| [余额批量查询](./btc/btc-balance.md) | 批量查询 BTC 地址余额 |
| [UTXO 查询](./btc/btc-utxo.md) | 查询地址的 UTXO 列表 |
| [PSBT 解码](./btc/btc-psbt.md) | 解析 PSBT 内容 |

### NFT 工具

| 工具 | 说明 |
| --- | --- |
| [NFT 预览](./nft/nft-preview.md) | 预览 NFT 元数据与媒体 |
| [NFT 发行](./nft/nft-issuance.md) | 部署 NFT 合约 |

### Solana 工具

| 工具 | 说明 |
| --- | --- |
| [钱包生成](./solana/sol-wallet.md) | 本地生成 Solana 钱包 |
| [PDA / ATA 计算](./solana/sol-address.md) | 派生 PDA 与关联代币账户 |
| [Instruction 编解码](./solana/sol-instruction.md) | 编码/解码指令数据 |
| [Program IDL 浏览器](./solana/sol-idl.md) | 浏览 Anchor IDL |
| [Compute / Fee / Rent](./solana/sol-fee-rent.md) | 估算计算单元、手续费与租金 |

### Polkadot 工具

| 工具 | 说明 |
| --- | --- |
| [钱包生成](./polkadot/dot-wallet.md) | 本地生成 Polkadot 钱包 |
| [SS58 地址转换](./polkadot/dot-ss58.md) | 不同链前缀间转换 SS58 地址 |
| [DOT 单位换算](./polkadot/dot-unit.md) | Planck / DOT 换算 |
| [Hash / Storage Key](./polkadot/dot-hash-storage.md) | 计算 storage key |
| [SCALE 编解码](./polkadot/dot-scale.md) | SCALE 编码/解码 |

### 批量操作

| 工具 | 说明 |
| --- | --- |
| [Disperse 合约分发](./bulk/disperse.md) | 通过合约一对多分发 |
| [钱包逐笔转账](./bulk/bulk-send.md) | 当前钱包逐笔发送 |
| [私钥批量转账](./bulk/bulk-send2.md) | 导入多私钥批量发送 |
| [私钥归集 · Sweep](./bulk/bulk-collect.md) | 多钱包资产归集到一个地址 |
| [余额批量查询](./bulk/bulk-query-balance.md) | 批量查询地址余额 |

## 相关文档

- [Corbit 端点跨域（CORS）配置](./ai/corbit-cors.md)
- [安全模型](./security.md)
- [常见问题 FAQ](./faq.md)
- [术语表](./glossary.md)

---

> 免责声明：本文档及工具按「现状」提供，不附带任何担保。你需自行保管私钥并对签署的交易负责。签名前务必核对地址、金额与网络。损失不可逆。
