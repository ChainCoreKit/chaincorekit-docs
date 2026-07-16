[English](../../en/evm/unit-convert.md) · **简体中文** · [← 文档总览](../index.md)

# 单位换算（Unit Converter）

> 输入任一以太单位，其余单位实时联动换算，每格都可一键复制。

## 什么时候用

- 在 Wei / Gwei / Ether 之间来回换算金额或 Gas 价格。
- 核对合约里的 uint256 原始 Wei 值对应多少 ETH。
- 需要更细分的单位（Kwei、Szabo、Finney、Kether 等）做换算。

## 使用步骤

1. 在**常用**区（Ether / Gwei / Wei）任一输入框填入数值。
2. 其余单位**实时联动**换算，点每格旁的复制按钮即可复制该单位的值。
3. 需要更多单位时展开**更多单位**（Kwei · Mwei · Szabo · Finney · Kether · Mether · Gether · Tether）。
4. 也可用**快捷填入**（1 ETH / 0.1 ETH / 1 Gwei / 100 Gwei）快速赋值；右上角按钮可**重置为 1 ETH**。

## 输入 / 输出说明

| 单位 | 相对 Ether 的量级 |
| --- | --- |
| Wei | 10⁻¹⁸（最小单位） |
| Kwei | 10⁻¹⁵ |
| Mwei | 10⁻¹² |
| Gwei | 10⁻⁹（Gas 常用） |
| Szabo | 10⁻⁶ |
| Finney | 10⁻³ |
| Ether | 1 |
| Kether / Mether / Gether / Tether | 10³ / 10⁶ / 10⁹ / 10¹² |

## 注意事项 & 常见坑

- **1 ETH = 10¹⁸ Wei**；支付 Gas 时价格常以 Gwei 计。
- **Wei 是整数单位**：小于 1 Wei 的数值没有意义，换算到 Wei 会取整。
- **别把原始 Wei 当人类可读数值**：合约里的 uint256 金额通常是最小单位，展示前需按单位换算。
- 这里换算的是**以太原生单位**；ERC-20 代币各有自己的 `decimals`（如 USDC=6），不要混用。

## 相关工具

- [ABI 可视化调用](./abi.md) — 调用合约时辅助金额单位切换
- [Calldata 编解码](./calldata.md) — 编码 / 解码调用参数
- [地址转换与 ENS](./address.md) — 地址校验与解析
- [安全模型](../security.md)

---

> 免责声明：换算仅供参考，签名前请核对实际金额与单位。
