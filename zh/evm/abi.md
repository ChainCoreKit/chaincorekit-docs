[English](../../en/evm/abi.md) · **简体中文** · [← 文档总览](../index.md)

# ABI 可视化调用（ABI Console）

> 导入 ABI 自动生成函数列表，图形化读写合约；支持多合约管理，按 Read / Write 分组。

## 什么时候用

- 想像 Etherscan「Contract」页那样，不写代码就调用合约的读/写函数。
- 手上有合约 ABI（自己部署的或第三方的），需要快速交互调试。
- 需要同时管理多个合约，在它们之间切换调用。

## 使用步骤

1. 点击左侧**添加合约**，在弹窗中填写：
   - **合约名称**（如 USDC、MyToken）。
   - **区块链网络**：当前连接网络 / Ethereum / Arbitrum One / Base 等（决定区块浏览器链接与调用网络）。
   - **合约地址**（`0x…`，实时做 EIP-55 校验）。
   - **ABI 来源**：粘贴 ABI / 上传 ABI 文件（「从区块浏览器获取」「常见 ABI」为即将支持）。
2. 添加后，合约出现在左侧列表；点击选中，右侧展示函数区。
3. 用顶部分组切换 **全部 / Read / Write**（各带数量），或用**筛选函数名**输入框过滤。
4. 展开某个函数，填入参数：
   - **读函数（Read）**：填参数后调用即可看到返回值。
   - **写函数（Write）**：需连接钱包，走参数预览 → Gas 预估 → 确认 → 签名 → pending → 结果。
   - 涉及金额的参数可用右上角 **Wei / Gwei / Ether** 单位切换辅助输入。
5. 顶部操作栏可**查看 ABI**、跳**区块浏览器**、**编辑**合约，或在 `···` 菜单里**分享链接 / 删除合约**。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 合约名称 | 自定义标识，仅用于列表展示 |
| 区块链网络 | 决定区块浏览器 URL 与调用所在链 |
| 合约地址 | `0x` + 40 位十六进制，实时 EIP-55 校验 |
| ABI 来源 | 粘贴 ABI JSON 数组 / 上传文件 |
| 单位切换 | Wei / Gwei / Ether，仅辅助金额类参数输入 |
| 函数分组 | 全部 / Read（只读）/ Write（写入） |

## 注意事项 & 常见坑

- **Read vs Write**：`view` / `pure` 归 Read（免费、无需签名）；`nonpayable` / `payable` 归 Write（需签名、上链）。
- **payable 函数**要额外填 ETH value；请注意单位（Wei/Gwei/Ether）。
- **金额精度**：uint256 金额按代币 `decimals` 换算（USDC=6，多数 ERC-20=18），别把原始 Wei 数当成人类可读数值。
- **参数类型**：`uint` 等价 `uint256`、`int` 等价 `int256`、`byte` 等价 `bytes1`；`bytes/bytes32` 需 `0x` 前缀 hex。
- **合约未在区块浏览器验证**时，ABI 来源不可信要留意风险，别盲目相信第三方给的 ABI。
- 高危写函数（`transferOwnership`、`selfdestruct`、`upgrade`）应格外谨慎，通常需二次确认。

## 相关工具

- [Calldata 编解码](./calldata.md) — 手动编解码调用数据
- [签名选择器查询](./query-selector.md) — 选择器 ↔ 函数签名
- [事件主题 TopicID](./topic-id.md) — 计算事件 TopicID
- [单位换算](./unit-convert.md) — Wei / Gwei / Ether
- [安全模型](../security.md)

---

> 免责声明：写操作会真实上链且不可逆，签名前请核对地址、金额与网络。
