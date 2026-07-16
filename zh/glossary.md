[English](../en/glossary.md) · **简体中文** · [← 文档总览](./index.md)

# 术语表

按主题分组，术语保留英文原样，解释用中文。

## 通用 / EVM

- **ABI**（Application Binary Interface）：合约的接口描述（函数、事件、参数类型），用于编码调用数据与解码返回值。
- **Calldata**：交易 `data` 字段的十六进制内容，= 4 字节函数选择器 + ABI 编码后的参数。
- **Selector（函数选择器）**：函数签名 keccak-256 哈希的前 4 字节，如 `transfer(address,uint256)` → `0xa9059cbb`。
- **TopicID / Event Topic**：事件签名的 keccak-256 哈希（32 字节），用于日志过滤。
- **keccak-256**：以太坊使用的哈希算法，用于函数选择器、事件 TopicID、EIP-55 校验等。
- **EIP-55**：地址大小写校验和格式，可检测地址输入错误。
- **ENS**：Ethereum Name Service，把 `vitalik.eth` 之类域名解析为地址。
- **Wei / Gwei / Ether**：ETH 的单位。1 Ether = 10⁹ Gwei = 10¹⁸ Wei；Gas 价格常用 Gwei。
- **Gas**：执行交易消耗的计算量；费用 = Gas 用量 × Gas 价格。
- **ERC-20 / ERC-721**：同质化代币 / NFT 的标准接口。
- **decimals**：代币精度，如 USDC=6、多数 ERC-20=18；展示金额时需按此换算。
- **payable / nonpayable / view / pure**：函数可变性。`payable` 可随调用发送 ETH；`view`/`pure` 为只读。
- **approve / allowance**：ERC-20 授权机制，允许某地址在额度内转走你的代币。

## 钱包 / 派生

- **BIP39**：助记词标准（12/15/18/21/24 词）。
- **BIP44**：分层确定性钱包的路径标准，EVM 常用 `m/44'/60'/account'/0/index`。
- **HD Wallet**：分层确定性钱包，由一条种子/助记词派生出多个地址。

## Bitcoin

- **UTXO**：未花费交易输出，比特币的记账模型。
- **PSBT**（Partially Signed Bitcoin Transaction）：部分签名交易格式，便于多方协作签名。
- **Legacy / SegWit / Taproot**：BTC 地址类型（`1...` / `bc1q...` / `bc1p...`）。

## Solana

- **PDA**（Program Derived Address）：由程序派生、无私钥的账户地址。
- **ATA**（Associated Token Account）：某钱包持有某代币的关联账户。
- **IDL**（Interface Definition Language）：Anchor 程序的接口描述，类似 EVM 的 ABI。
- **Rent**：Solana 账户占用链上存储需缴纳的租金。
- **Compute Units**：Solana 交易的计算预算单位。

## Polkadot

- **SS58**：Polkadot/Substrate 的地址编码，前缀区分不同链。
- **Planck / DOT**：DOT 的单位，1 DOT = 10¹⁰ Planck。
- **SCALE**：Substrate 的紧凑编码格式。
- **Storage Key**：链上存储项的键，由模块与项名哈希得到。

---

[← 返回文档总览](./index.md)
