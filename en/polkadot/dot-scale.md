**English** · [简体中文](../../zh/polkadot/dot-scale.md) · [← Overview](../index.md)

# SCALE Codec

> Encode / decode SCALE data by a type expression (Compact / Option / Vec / Tuple /
> fixed-size array / nesting).

## When to use it

- You want to encode a value under some type into SCALE hex to build an extrinsic
  parameter.
- You have SCALE hex and need to decode it back to a readable value under a type
  expression.
- You're debugging Substrate data structures and want to verify how nested types
  (Vec, Tuple, Option, fixed-size arrays) encode.

## Steps

1. Enter a type in the **type expression** box, e.g. `Compact<u128>`,
   `Vec<(u8, bool)>`, `Option<u32>`, `[u8; 4]`.
2. Use the toggle to pick **encode** or **decode**:
   - **Encode**: put a JSON value in the **value (JSON)** box
     (e.g. `42` / `true` / `[[1, true], [2, false]]` / `"hello"`) and click **Encode**.
   - **Decode**: put `0x…` in the **SCALE data (hex)** box and click **Decode**.
3. The result panel shows the encoded hex or the decoded value.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Type expression | e.g. `Compact<u128>`, `Vec<(u8, bool)>`, `Option<u32>`, `[u8; 4]` |
| Mode | `encode` / `decode` |
| Value (JSON) | the input in encode mode, a JSON value |
| SCALE data (hex) | the input in decode mode, `0x…` |
| Output | the encoded SCALE hex, or the decoded value |

## Notes & gotchas

- **The type expression must match the data**: a mismatched type decodes wrong or
  fails; `Compact` encodes differently from a plain integer — don't mix them up.
- **Values are JSON**: write a Tuple as an array (e.g. `[1, true]`), strings in
  quotes (e.g. `"hello"`), and let Option follow SCALE semantics.
- **Fixed-size arrays need the exact length**: `[u8; 4]` requires exactly 4
  elements — too many or too few errors out.
- **Decoding named types bound to runtime metadata needs WSS** — that's coming soon;
  for now only types written out explicitly in the expression are supported.

## Related tools

- [Substrate Hash / Storage Key](./dot-hash-storage.md) — storage-key derivation
- [SS58 Convert](./dot-ss58.md) — SS58 ↔ AccountId32
- [DOT Units](./dot-unit.md) — Planck ↔ main unit
- [Generate Wallet](./dot-wallet.md) — generate a Substrate wallet locally
- [Security model](../security.md)

---

> Disclaimer: codec results are for development and debugging reference — re-check
> the type and data before building a transaction.
