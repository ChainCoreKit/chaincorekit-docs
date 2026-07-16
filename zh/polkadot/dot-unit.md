[English](../../en/polkadot/dot-unit.md) · **简体中文** · [← 文档总览](../index.md)

# DOT 单位换算（DOT Units）

> Planck 与 DOT / KSM / PAS 等主单位精确互转，支持自定义 decimals，无需连网。

## 什么时候用

- 链上金额都以最小单位 Planck 计价，需要换算成人类可读的 DOT / KSM 才能核对。
- 手上有一个 DOT 数值，想算出对应多少 Planck 再填进交易或 extrinsic。
- 面对 Kusama、Paseo 或其它 Substrate 链时，decimals 各不相同，需要按链切换。

## 使用步骤

1. 在**数值**框输入金额（如 `1.5` 或 `15000000000`）。
2. 选择**链 / decimals**：
   - **Polkadot · DOT**（decimals 10）
   - **Kusama · KSM**（decimals 12）
   - **Paseo · PAS**（decimals 10）
   - **自定义 decimals**：选中后填入目标链的 decimals。
3. 用下方开关选择输入的是**按主单位输入**还是**按 Planck 输入**。
4. 结果区自动给出另一单位的换算值，无需点击。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 数值 | 待换算金额，可为小数（主单位）或整数（Planck） |
| 链 / decimals | DOT (10) / KSM (12) / PAS (10) / 自定义 |
| 自定义 decimals | 目标链的小数位数（选「自定义」时可填） |
| 输入模式 | `按主单位输入` / `按 Planck 输入` |
| 输出 | 对应的主单位与 Planck 数值 |

## 注意事项 & 常见坑

- **Planck 是最小单位**：1 DOT = 10,000,000,000 Planck（10 位 decimals），KSM 则是 12 位，切勿套用同一倍数。
- **decimals 因链而异**：跨到非默认链前，先确认该链真实 decimals，自定义时填错会整体差几个数量级。
- **Planck 必须是整数**：主单位小数位超过 decimals 的部分无法表示为整数 Planck，注意精度截断。
- **读取链上 symbol / decimals（metadata）需只读 RPC**，属即将支持，当前以内置常量换算。

## 相关工具

- [SS58 地址转换](./dot-ss58.md) — SS58 ↔ AccountId32
- [Substrate Hash / Storage Key](./dot-hash-storage.md) — Blake2 / XXHash 与 Storage Key
- [SCALE 编解码](./dot-scale.md) — 按类型表达式编 / 解码
- [Polkadot 钱包生成](./dot-wallet.md) — 本地生成 Substrate 钱包
- [安全模型](../security.md)

---

> 免责声明：换算结果仅供参考，提交交易前请再次核对金额与单位。
