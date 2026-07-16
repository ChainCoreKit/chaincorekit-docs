[English](../../en/nft/nft-preview.md) · **简体中文** · [← 文档总览](../index.md)

# NFT 预览（NFT Preview）

> 输入合约地址与 Token ID，预览 NFT 的媒体与元数据，无需连接钱包。

## 什么时候用

- 想在铸造或购买前，快速核对某个 Token ID 的图片与属性。
- 元数据托管在 IPFS，需要通过网关把 `ipfs://` 链接渲染出来看效果。
- 部署合约、设置 Base URI 后，验证 `tokenURI` 是否指向了正确的元数据。

## 使用步骤

1. 选择**网络**：Ethereum / Polygon / Arbitrum One / Base。
2. 选择 **IPFS 网关**：ipfs.io / Pinata / dweb.link（用于加载 `ipfs://` 资源）。
3. 填写**合约地址**（`0x…`，实时做 EIP-55 校验）。
4. 填写 **Token ID**（如 3749）。
5. 点击**预览**读取链上 `tokenURI` 并渲染媒体与元数据；或点**示例**载入一组样本快速体验。
6. 结果卡顶部显示标准徽标（ERC-721）；可在弹窗中**查看原始元数据 JSON**并**复制 JSON**。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 网络 | Ethereum / Polygon / Arbitrum One / Base |
| IPFS 网关 | ipfs.io / Pinata / dweb.link，加载 `ipfs://` 资源 |
| 合约地址 | `0x` + 40 位十六进制，实时 EIP-55 校验 |
| Token ID | 该 NFT 的整数 ID |
| 输出 | NFT 媒体、元数据字段、原始 JSON（可复制） |

## 注意事项 & 常见坑

- **只读工具**：预览不发交易、不需连接钱包，安全无副作用。
- **当前支持 ERC-721** 元数据预览，ERC-1155 即将支持。
- **网关差异**：某个 IPFS 网关加载慢或超时，可切换到另一个网关重试。
- **元数据缺失**：合约未设置 `tokenURI` 或指向的路径为空时，媒体无法渲染，请核对 Base URI 与元数据上传路径。
- **网络要对应**：合约地址与所选网络要一致，否则读不到该 Token。

## 相关工具

- [NFT 发行 / 铸造](./nft-issuance.md) — 部署 ERC-721、设置 Base URI 并铸造
- [ABI 可视化调用](../evm/abi.md) — 图形化读写合约
- [安全模型](../security.md)

---

> 免责声明：预览为只读操作，媒体与元数据由第三方托管，展示内容以链上数据为准。
