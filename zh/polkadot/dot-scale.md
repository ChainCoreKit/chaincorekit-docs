[English](../../en/polkadot/dot-scale.md) · **简体中文** · [← 文档总览](../index.md)

# SCALE 编解码（SCALE Codec）

> 按类型表达式对 SCALE 数据编 / 解码（Compact / Option / Vec / Tuple / 定长数组 / 嵌套）。

## 什么时候用

- 想把一个值按某个类型编码成 SCALE 十六进制，用于构造 extrinsic 参数。
- 拿到一段 SCALE hex，需要按类型表达式解码回可读的值。
- 调试 Substrate 数据结构，验证嵌套类型（Vec、Tuple、Option、定长数组）的编码是否正确。

## 使用步骤

1. 在**类型表达式**框填入类型，如 `Compact<u128>`、`Vec<(u8, bool)>`、`Option<u32>`、`[u8; 4]`。
2. 用开关选择**编码**或**解码**：
   - **编码**：在**值**（JSON）框填入 JSON 形式的值（如 `42` / `true` / `[[1, true], [2, false]]` / `"hello"`），点**编码**。
   - **解码**：在 **SCALE 数据（hex）** 框填入 `0x…`，点**解码**。
3. 结果区显示编码后的 hex 或解码后的值。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 类型表达式 | 如 `Compact<u128>`、`Vec<(u8, bool)>`、`Option<u32>`、`[u8; 4]` |
| 模式 | `编码` / `解码` |
| 值（JSON） | 编码模式下的输入，JSON 形式的值 |
| SCALE 数据（hex） | 解码模式下的输入，`0x…` |
| 输出 | 编码后的 SCALE hex，或解码后的值 |

## 注意事项 & 常见坑

- **类型表达式要匹配数据**：类型与实际数据不符会解出错误或失败，`Compact` 与普通整数编码不同，别混用。
- **值用 JSON 表示**：Tuple 写成数组（如 `[1, true]`），字符串带引号（如 `"hello"`），Option 的空值按 SCALE 语义处理。
- **定长数组要够长**：`[u8; 4]` 需正好 4 个元素，多了少了都会报错。
- **绑定 Runtime Metadata 的命名类型解码需 WSS**，属即将支持；当前仅支持类型表达式明确写出的结构。

## 相关工具

- [Substrate Hash / Storage Key](./dot-hash-storage.md) — Storage Key 推导
- [SS58 地址转换](./dot-ss58.md) — SS58 ↔ AccountId32
- [DOT 单位换算](./dot-unit.md) — Planck ↔ 主单位
- [Polkadot 钱包生成](./dot-wallet.md) — 本地生成 Substrate 钱包
- [安全模型](../security.md)

---

> 免责声明：编解码结果仅供开发调试参考，构造交易前请再核对类型与数据。
