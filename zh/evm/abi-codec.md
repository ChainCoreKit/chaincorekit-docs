[English](../../en/evm/abi-codec.md) · **简体中文** · [← 文档总览](../index.md)

# ABI 编解码（ABI Codec）· EVM

> 构造函数参数编码、事件日志解码、revert 错误解码——合约调用周边的三件事。全部本地计算，不联网、不连钱包。

## 什么时候用

- 部署完合约要在区块浏览器验证源码，需要填「构造函数参数」那一栏。
- 手上有一条事件日志的 `topics` 和 `data`，想知道是什么事件、参数是什么。
- 交易失败了，区块浏览器只给一串 `0x08c379a0…`，想看懂到底为什么回滚。

## 使用步骤

### 构造函数参数

1. 填**构造函数签名**，如 `constructor(string,string,uint8)`。
2. **参数每行一个**，顺序与签名一致。数组写在一行，方括号可省：`[1,2,3]` 或 `1,2,3`。
3. 结果即可直接复制到区块浏览器的构造函数参数栏。

> 与 [Calldata 编解码](./calldata.md) 的编码唯一差别是**不带 4 字节选择器**：这段拼在字节码后面，正是验证合约时单独要填的那一栏。

### 事件日志

1. 填**事件签名**，`indexed` 标记要保留：`Transfer(address indexed from, address indexed to, uint256 value)`。
2. **Topics 每行一个**，包含 `topic0`；**Data** 填非 indexed 参数的数据区。
3. 表格逐行列出参数名、类型、值，`indexed` 的参数带标记。

> 若填入的 `topic0` 与签名算出的不一致，会给出告警但**仍按你的签名解**——判断留给你，工具不替你改。

### revert 错误

1. 把 **revert data** 粘进来（区块浏览器上失败交易里那串 hex）。
2. 标准的 `Error(string)` 与 `Panic(uint256)` 直接解出来，Panic 还会给出语义（溢出、除零、越界等）。
3. **自定义 error 需要你提供签名**（每行一个），按 4 字节选择器匹配。

## 输入 / 输出说明

| 项 | 含义 / 格式 |
| --- | --- |
| 构造函数签名 | `constructor(type1,type2,…)`，也接受省略 `constructor` 的写法 |
| 事件签名 | 保留 `indexed`，可带参数名 |
| Topics | 每行一个 32 字节值，首行是 `topic0` |
| Data | `0x` 开头的十六进制；无非 indexed 参数时填 `0x` |
| revert data | `0x` 开头的十六进制 |
| 自定义 error 签名 | 如 `InsufficientBalance(address,uint256)`，每行一个 |

## 注意事项 & 常见坑

- **indexed 的动态类型只有哈希**：`string` / `bytes` / 数组做 `indexed` 时，链上 topic 里存的是 keccak 哈希而**不是值本身**，原值无法还原。这是 ABI 规范的性质，工具会如实标注为「仅哈希」，不拿哈希冒充值。
- **indexed 数量必须对得上**：topics 少一个就会整体错位，工具会直接报错而不是给你一组看着正常的错值。
- **tuple 暂不支持编码**：遇到会明确报错，不会编出错的字节。
- 自定义 error **没有全局注册表**，工具无法凭空认出——必须由你提供签名。

## 相关工具

- [Calldata 编解码](./calldata.md) — 解码交易输入数据
- [事件 TopicID](./topic-id.md) — 由事件签名算 topic0
- [交易堆栈 Trace 分析](./trace-view.md) — 完整交易的调用树与事件
- [函数签名查询](./query-selector.md) — 选择器与签名互查

---

> 免责声明：解码结果仅供参考，请以链上原始数据为准。
