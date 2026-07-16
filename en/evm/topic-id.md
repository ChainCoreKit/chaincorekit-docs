**English** · [简体中文](../../zh/evm/topic-id.md) · [← Overview](../index.md)

# Event TopicID

> Compute a TopicID (keccak-256) from an event signature in real time, and look one
> up against a local dictionary.

## When to use it

- You have an event signature and need its TopicID (the `topics[0]` of a log).
- You have a 32-byte TopicID and want to know which event it is.
- You're parsing logs or filtering events and need signature ↔ TopicID.

## Steps

### Signature → TopicID

1. Enter the event definition — you can paste it with `indexed` / param names (e.g.
   `Transfer(address indexed from, address indexed to, uint256 value)`); it strips
   them and computes over the canonical signature.
2. The **TopicID** appears live below — click copy.

### TopicID → event name

1. Enter `0x` + 64 hex in **Topic ID (32 bytes)**.
2. **Event signature** returns a match from the local dictionary; click to copy.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Event signature | `Event(type1,type2,…)`; `indexed` / names allowed (auto-stripped) |
| TopicID | `keccak-256(canonical signature)`, `0x` + 64 hex |
| Topic ID (reverse input) | `0x` + 64 hex |
| Event signature (reverse output) | a dictionary hit |

## Notes & gotchas

- **TopicID = keccak-256(canonical event signature)** — only the type list; `indexed`
  and param names are stripped and don't affect the hash.
- **Canonical types matter**: `uint` means `uint256`; aliases yield a different
  TopicID.
- **Only non-anonymous events have topics** — `anonymous` events produce no
  `topics[0]`; this computes the hash of a regular event signature.
- **Reverse lookup uses a local dictionary** — it returns common events only;
  uncovered ones must be computed from the signature.

## Related tools

- [Selector Lookup](./query-selector.md) — signature ↔ 4-byte selector
- [Hash Tools](./hash-tool.md) — keccak-256 and other hashes / encodings
- [Transaction Tracer](./trace-view.md) — parse a transaction's event logs
- [Calldata Codec](./calldata.md) — decode / encode call data
- [Security model](../security.md)

---

> Disclaimer: reverse results come from a local dictionary and may be incomplete —
> verify against context.
