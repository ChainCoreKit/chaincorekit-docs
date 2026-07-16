[English](../../en/polkadot/dot-hash-storage.md) · **简体中文** · [← 文档总览](../index.md)

# Substrate Hash / Storage Key（Hash / Storage Key）

> Blake2 / XXHash 哈希，以及 Storage Key 推导（twox128(pallet) ‖ twox128(storage) [‖ hashed(map key)]）。

## 什么时候用

- 想对一段文本或 hex 计算 Blake2 / XXHash 哈希。
- 需要按 Substrate 规则算出某个 storage item 的 storage key，用于 RPC `state_getStorage` 等查询。
- 调试 pallet 存储时，要手动还原 map 条目的完整 key。

## 使用步骤

### 模式一：Hash

1. 顶部**模式**选 **Hash**。
2. 在**输入**框填入内容，用下方开关选择**文本**还是 **hex**（hex 需 `0x` 前缀）。
3. 结果区自动列出各算法的哈希值。

### 模式二：Storage Key

1. 顶部**模式**选 **Storage Key**。
2. 填 **Pallet**（如 `System`）与 **Storage**（如 `Account`）。
3. 如需 map 条目，填 **Map key** 并选 **Key 类型**：
   - **SS58 / AccountId**：按 32 字节 AccountId32 处理。
   - **hex**：视为已 SCALE 编码的 key 原始字节。
   - **文本**：按 Text（含 compact 长度前缀）编码。
4. 选 **Hasher**：`Blake2_128Concat` / `Twox64Concat` / `Blake2_128` / `Twox128` / `Identity`。
5. 结果区自动给出推导出的 storage key。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 模式 | `Hash` / `Storage Key` |
| Hash 输入 | 文本，或 `0x` + hex |
| 输入类型 | 文本 / hex |
| Pallet | pallet 名，如 `System` |
| Storage | storage item 名，如 `Account` |
| Map key（可选） | `0x…` / 文本 / SS58 |
| Key 类型 | SS58 / AccountId、hex、文本 |
| Hasher | Blake2_128Concat / Twox64Concat / Blake2_128 / Twox128 / Identity |
| 输出 | 哈希值，或推导出的 storage key |

## 注意事项 & 常见坑

- **Storage key 结构**：`twox128(pallet) ‖ twox128(storage)`，map 再拼上 `hashed(map key)`。
- **Map key 先 SCALE 编码再哈希**：文本按 Text（含 compact 长度前缀）；SS58 / AccountId 按 32 字节 AccountId32；hex 视为已 SCALE 编码的原始字节，别重复编码。
- **Hasher 要选对**：不同 storage item 用的 hasher 不同（常见 `Blake2_128Concat` / `Twox64Concat`），选错算出的 key 无效。
- **单 Map 只填一个 key**：DoubleMap / NMap 需按段自行拼接，本工具一次处理单 map 的一个 key。

## 相关工具

- [SS58 地址转换](./dot-ss58.md) — 由 SS58 得到 AccountId32
- [SCALE 编解码](./dot-scale.md) — 手动处理 SCALE 编码
- [DOT 单位换算](./dot-unit.md) — Planck ↔ 主单位
- [Polkadot 钱包生成](./dot-wallet.md) — 本地生成 Substrate 钱包
- [安全模型](../security.md)

---

> 免责声明：计算结果仅供开发调试参考，请以链上运行时实际编码为准。
