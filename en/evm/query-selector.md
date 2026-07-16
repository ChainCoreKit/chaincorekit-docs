**English** · [简体中文](../../zh/evm/query-selector.md) · [← Overview](../index.md)

# Selector Lookup

> Compute a 4-byte selector from a function signature in real time, and look up a
> selector against a local dictionary.

## When to use it

- You have a function signature and need its 4-byte selector (e.g. to match the
  first 4 bytes of calldata).
- You see a `0x` 4-byte selector and want to know which function it is.
- You're debugging a call or cross-checking an ABI and need selector ↔ signature.

## Steps

### Signature → selector

1. Enter a canonical signature like `transfer(address,uint256)`.
2. The **4-byte selector** is computed live below — click copy to grab it.

### Selector → signature

1. Enter `0x` + 8 hex, e.g. `0x70a08231`.
2. **Matched signature** returns one hit from the local dictionary; click to copy.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Function signature | canonical `name(type1,type2,…)`, comma-separated, no spaces |
| 4-byte selector | first 4 bytes of `keccak-256(signature)`, `0x` + 8 hex |
| Selector (reverse input) | `0x` + 8 hex |
| Matched signature | a dictionary hit (may not be unique) |

## Notes & gotchas

- **Selector = first 4 bytes of keccak-256(signature)** — over the signature string
  only; no return types, param names, or `indexed` modifiers.
- **Use canonical types**: `uint` means `uint256`, `int` means `int256`. Aliases
  produce a different selector — always use canonical forms.
- **Reverse lookup uses a local dictionary** — it returns one match; a 4-byte
  selector can in theory map to several signatures, so treat results as a hint.
- **No spaces between params**: `transfer(address, uint256)` differs from
  `transfer(address,uint256)`.

## Related tools

- [Event TopicID](./topic-id.md) — compute a TopicID from an event signature
- [Calldata Codec](./calldata.md) — decode / encode call data by signature
- [Hash Tools](./hash-tool.md) — keccak-256 and other hashes / encodings
- [ABI Console](./abi.md) — call contracts visually
- [Security model](../security.md)

---

> Disclaimer: reverse results come from a local dictionary and may not be unique —
> verify against context.
