[English](../../en/evm/topic-id.md) · **简体中文** · [← 文档总览](../index.md)

# 事件主题 TopicID（Event TopicID）

> 事件签名实时计算 TopicID（keccak-256），并支持基于本地词典的反向查询。

## 什么时候用

- 有事件签名，想算出它在日志 `topics[0]` 里的 TopicID。
- 拿到一串 32 字节的 TopicID，想知道对应的是哪个事件。
- 解析交易日志、过滤事件时快速对照事件签名与 TopicID。

## 使用步骤

### 事件签名 → TopicID

1. 在**事件签名**框填入事件定义，可直接粘贴带 `indexed` / 参数名的形式（如 `Transfer(address indexed from, address indexed to, uint256 value)`），会自动剥离并按规范签名计算。
2. 下方 **TopicID** 实时给出结果，点复制按钮复制。

### TopicID → 事件名

1. 在**主题 ID**（32 字节）框填入 `0x` + 64 位 hex。
2. **事件签名**返回本地词典中的匹配结果，点复制按钮复制。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 事件签名 | `Event(type1,type2,…)`，允许带 `indexed` / 参数名（自动剥离） |
| TopicID | `keccak-256(规范事件签名)`，`0x` + 64 位 hex |
| 主题 ID（反查输入） | `0x` + 64 位 hex |
| 事件签名（反查输出） | 本地词典命中的事件签名 |

## 注意事项 & 常见坑

- **TopicID = keccak-256(规范事件签名)**：仅取类型列表，`indexed`、参数名会被自动剥离，不参与计算。
- **规范类型很重要**：`uint` 视为 `uint256`；写别名会算出不同 TopicID。
- **仅 `indexed` 事件才有 topics**：匿名事件（`anonymous`）不产生 `topics[0]`，此工具计算的是常规事件签名的哈希。
- **反查基于本地词典**，只返回收录的常用事件，未收录的需自行以签名计算。

## 相关工具

- [签名选择器查询](./query-selector.md) — 函数签名 ↔ 4 字节选择器
- [Hash 工具](./hash-tool.md) — keccak-256 等哈希与编码
- [交易分析](./trace-view.md) — 解析交易的事件日志
- [Calldata 编解码](./calldata.md) — 解码 / 编码调用数据
- [安全模型](../security.md)

---

> 免责声明：反查结果来自本地词典，可能不完整，请结合上下文核对。
