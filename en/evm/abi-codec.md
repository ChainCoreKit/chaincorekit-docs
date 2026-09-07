**English** · [简体中文](../../zh/evm/abi-codec.md) · [← Overview](../index.md)

# ABI Codec · EVM

> Encode constructor arguments, decode event logs, decode revert errors — the three
> things that surround a contract call. All computed locally: no network, no wallet.

## When to use it

- You deployed a contract and need the "constructor arguments" field to verify its
  source on a block explorer.
- You have a log's `topics` and `data` and want to know which event it is and what
  the arguments were.
- A transaction failed and the explorer only shows `0x08c379a0…` — you want to know
  why it actually reverted.

## Steps

### Constructor arguments

1. Enter the **constructor signature**, e.g. `constructor(string,string,uint8)`.
2. Put **one argument per line**, in signature order. Arrays go on one line, brackets
   optional: `[1,2,3]` or `1,2,3`.
3. Copy the result straight into the explorer's constructor-arguments field.

> The only difference from encoding in [Calldata Codec](./calldata.md) is the missing
> **4-byte selector**: this blob goes after the bytecode, which is exactly what
> verification asks for separately.

### Event log

1. Enter the **event signature**, keeping the `indexed` markers:
   `Transfer(address indexed from, address indexed to, uint256 value)`.
2. Put **one topic per line**, including `topic0`; put the non-indexed data area in **Data**.
3. The table lists each parameter's name, type and value, with `indexed` ones tagged.

> If the `topic0` you pasted doesn't match the one derived from the signature, you get a
> warning but decoding **still follows your signature** — the judgement is yours, the tool
> won't silently "fix" it.

### Revert error

1. Paste the **revert data** (the hex blob shown on a failed transaction).
2. Standard `Error(string)` and `Panic(uint256)` decode directly; panics also get their
   meaning (overflow, division by zero, out-of-bounds, …).
3. **Custom errors need a signature from you** (one per line); they're matched by
   4-byte selector.

## Inputs / outputs

| Item | Meaning / format |
| --- | --- |
| Constructor signature | `constructor(type1,type2,…)`; the `constructor` keyword may be omitted |
| Event signature | Keep `indexed`; parameter names are allowed |
| Topics | One 32-byte value per line; the first line is `topic0` |
| Data | `0x`-prefixed hex; use `0x` when there are no non-indexed params |
| Revert data | `0x`-prefixed hex |
| Custom error signature | e.g. `InsufficientBalance(address,uint256)`, one per line |

## Notes & gotchas

- **Indexed dynamic types are hash-only**: when `string` / `bytes` / arrays are `indexed`,
  the topic stores a keccak hash, **not the value**. The original cannot be recovered.
  That's how the ABI spec works, so the tool labels it "hash only" rather than passing the
  hash off as a value.
- **Indexed count must line up**: one missing topic shifts everything, so the tool errors
  out instead of handing you plausible-looking wrong values.
- **Tuples aren't encodable yet**: you get a clear error rather than wrong bytes.
- Custom errors have **no global registry** — the tool cannot recognise them on its own,
  so you must supply the signature.

## Related tools

- [Calldata Codec](./calldata.md) — decode transaction input data
- [Event TopicID](./topic-id.md) — derive topic0 from an event signature
- [Transaction Tracer](./trace-view.md) — full call tree and events for a transaction
- [Selector Lookup](./query-selector.md) — selector ⇄ signature

---

> Disclaimer: decoded results are for reference; always defer to the raw on-chain data.
