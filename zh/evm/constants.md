[English](../../en/evm/constants.md) · **简体中文** · [← 文档总览](../index.md)

# 常用常量（EVM Constants）

> 写合约、拼 calldata、排查问题时反复要用的固定值：特殊地址、多链同址合约、整数边界、常见哈希。每一条都可一键复制。

## 什么时候用

- 需要零地址、销毁地址作为参数，或在日志里认出它们。
- 无限授权要填 `max uint256`，Permit2 授权上限要填 `max uint160`。
- 写脚本或测试时要用 Multicall3、Permit2、ERC-4337 EntryPoint 等常见合约地址。
- 排查时看到 `0xc5d2…a470`、`0x56e8…b421` 这类值，想确认它们代表什么。

## 包含哪些值

| 分组 | 条目 |
| --- | --- |
| 特殊地址 | 零地址、常用销毁地址 `0x…dEaD` |
| 多链同址合约 | Multicall3、Permit2（Uniswap）、CREATE2 部署器（Arachnid）、ERC-4337 EntryPoint v0.7 / v0.6 |
| 整数边界 | max uint256（hex 与十进制）、max uint160 / uint128 / uint64、max / min int256 |
| 哈希与字节 | bytes32 零值、keccak256(空字节)、空 MPT 根 |

地址一律以 EIP-55 校验和格式给出，可直接粘贴到钱包或区块浏览器。

## 注意事项 & 常见坑

- **多链同址 ≠ 每条链都有**。这些合约在多数 EVM 链上地址相同，但新链、私有链或部分 L2 可能尚未部署。使用前在目标链的区块浏览器确认该地址有合约代码。
- **EntryPoint 有多个版本**，v0.6 与 v0.7 的接口不兼容，按你的智能账户实现选择。
- **销毁地址只是约定**：`0x…dEaD` 没有已知私钥，但它不是协议层面的特殊地址；转进去的资产无法取回。
- `max uint256` 用作无限授权时，对方合约可以随时转走你在该代币上的**全部**余额，授权前请确认合约可信，授权后可在 [授权管理](./approvals.md) 撤销。

## 相关工具

- [时间戳换算](./timestamp.md) — Unix 时间戳与日期互转
- [单位换算](./unit-convert.md) — Wei / Gwei / ETH 与代币精度换算
- [Hash 工具](./hash-tool.md) — 计算任意输入的 keccak-256
- [合约检查](./contract-check.md) — 确认某个地址上是否有合约代码
