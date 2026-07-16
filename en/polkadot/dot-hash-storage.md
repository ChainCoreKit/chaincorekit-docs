**English** · [简体中文](../../zh/polkadot/dot-hash-storage.md) · [← Overview](../index.md)

# Substrate Hash / Storage Key

> Blake2 / XXHash hashing, plus storage-key derivation
> (twox128(pallet) ‖ twox128(storage) [‖ hashed(map key)]).

## When to use it

- You want a Blake2 / XXHash hash of some text or hex.
- You need a storage item's storage key, following Substrate rules, to query it via
  RPC such as `state_getStorage`.
- You're debugging pallet storage and want to reconstruct a map entry's full key by
  hand.

## Steps

### Mode A — Hash

1. Set **mode** to **Hash**.
2. Enter content in the **input** box and use the toggle to pick **text** or **hex**
   (hex needs a `0x` prefix).
3. The result panel lists the hash under each algorithm automatically.

### Mode B — Storage Key

1. Set **mode** to **Storage Key**.
2. Fill in **Pallet** (e.g. `System`) and **Storage** (e.g. `Account`).
3. For a map entry, fill **Map key** and pick its **key type**:
   - **SS58 / AccountId**: treated as a 32-byte AccountId32.
   - **hex**: treated as already-SCALE-encoded raw key bytes.
   - **text**: encoded as Text (with a compact length prefix).
4. Pick a **hasher**: `Blake2_128Concat` / `Twox64Concat` / `Blake2_128` /
   `Twox128` / `Identity`.
5. The result panel shows the derived storage key automatically.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Mode | `Hash` / `Storage Key` |
| Hash input | text, or `0x` + hex |
| Input type | text / hex |
| Pallet | pallet name, e.g. `System` |
| Storage | storage item name, e.g. `Account` |
| Map key (optional) | `0x…` / text / SS58 |
| Key type | SS58 / AccountId, hex, text |
| Hasher | Blake2_128Concat / Twox64Concat / Blake2_128 / Twox128 / Identity |
| Output | the hash, or the derived storage key |

## Notes & gotchas

- **Storage key layout**: `twox128(pallet) ‖ twox128(storage)`, with a map appending
  `hashed(map key)`.
- **Map key is SCALE-encoded before hashing**: text as Text (with a compact length
  prefix); SS58 / AccountId as a 32-byte AccountId32; hex as already-SCALE-encoded
  raw bytes — don't double-encode.
- **Pick the right hasher**: storage items use different hashers (commonly
  `Blake2_128Concat` / `Twox64Concat`); the wrong one yields an invalid key.
- **One key per single map**: DoubleMap / NMap must be concatenated segment by
  segment; this tool handles one key of a single map at a time.

## Related tools

- [SS58 Convert](./dot-ss58.md) — get an AccountId32 from an SS58 address
- [SCALE Codec](./dot-scale.md) — handle SCALE encoding by hand
- [DOT Units](./dot-unit.md) — Planck ↔ main unit
- [Generate Wallet](./dot-wallet.md) — generate a Substrate wallet locally
- [Security model](../security.md)

---

> Disclaimer: results are for development and debugging reference — defer to the
> runtime's actual on-chain encoding.
