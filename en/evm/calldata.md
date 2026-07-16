**English** · [简体中文](../../zh/evm/calldata.md) · [← Overview](../index.md)

# Calldata Codec

> Decode / encode transaction Input calldata in real time, auto-detecting common
> selectors and accepting your own function signatures.

## When to use it

- You have a `0x` transaction Input and want to recover the function and its params.
- You want to encode calldata by hand from a signature and params.
- The local dictionary doesn't cover a selector and you want to decode arbitrary
  calldata via your own signature.

## Steps

### Decode calldata

1. On the **Decode** tab, paste `0x` + calldata (the sample is a `transfer` call).
2. It **matches the first 4 bytes against the local dictionary**; on a hit it decodes
   by that signature.
3. If uncovered, enter a signature in **Canonical function signature (optional)**
   (e.g. `transfer(address,uint256)`) to override the auto-match.
4. The table lists **param / type / value** per row.

### Encode calldata

1. Switch to the **Encode** tab and enter a **function signature**.
2. Put one param per line in **Params**, in signature order.
3. The **Calldata result** builds live — click copy.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Input calldata | `0x` + selector + encoded params |
| Canonical signature (decode, optional) | overrides auto-match, e.g. `transfer(address,uint256)` |
| Decode result | param / type / value table |
| Function signature (encode) | `name(type1,type2,…)` |
| Params (encode) | one per line, in signature order |
| Calldata result | the encoded `0x` data |

## Notes & gotchas

- **Decoding handles dynamic types** — with a signature it decodes string / bytes /
  arrays via head-tail offsets; tuples and similar may show as raw 32-byte words.
- **Encoding is static types for now** — local encoding for address / uint / bool /
  bytesN, etc.
- **Type aliases normalize**: `uint` = `uint256`, `int` = `int256`, `byte` =
  `bytes1`; normalization applies to params inside the parentheses, not the name.
- **Amounts are smallest-unit** — enter uint256 params in Wei / the token's smallest
  unit, not human-readable values.
- `bytes/bytesN` params need `0x`-prefixed hex; wrong param order yields wrong
  decode / encode.

## Related tools

- [Selector Lookup](./query-selector.md) — 4-byte selector ↔ signature
- [Unit Converter](./unit-convert.md) — Wei / Gwei / Ether
- [Transaction Tracer](./trace-view.md) — parse internal calls and Input
- [ABI Console](./abi.md) — call contracts visually
- [Security model](../security.md)

---

> Disclaimer: codec output is for reference — verify the function, params, and units
> before going on-chain.
