**English** · [简体中文](../../zh/evm/hash-tool.md) · [← Overview](../index.md)

# Hash Tools

> Compute keccak-256 / SHA3-256 / SHA-256 over an input string in real time, or
> Base64 / Hex encode it — switch algorithms to recompute instantly.

## When to use it

- Compute the keccak-256 used by function selectors / event TopicIDs / EIP-55.
- Need a general-purpose SHA3-256 or SHA-256 digest of a string.
- Base64- or Hex(UTF-8)-encode a string.

## Steps

1. Pick an algorithm at the top: **keccak-256 / SHA3-256 / SHA-256 / Base64 /
   Hex(UTF-8)**.
2. Type the string in **Input**.
3. The **Result** shows live below — click copy. Switching algorithms recomputes
   instantly.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Algorithm | keccak-256 / SHA3-256 / SHA-256 / Base64 / Hex(UTF-8) |
| Input | any string (treated as UTF-8) |
| Result | the hash or encoding for the chosen algorithm, copyable |

## Notes & gotchas

- **keccak-256 ≠ SHA3-256** — Ethereum uses keccak-256, which differs from the
  finalized SHA3-256. Use keccak-256 for selectors / TopicIDs / EIP-55.
- **Input is treated as a string** — it hashes UTF-8 text, not a raw hex byte array;
  mind the difference.
- **Base64 / Hex are encodings, not hashes** — reversible, not for digests.
- Everything runs locally; input is never uploaded.

## Related tools

- [Selector Lookup](./query-selector.md) — first 4 bytes of keccak-256 = selector
- [Event TopicID](./topic-id.md) — keccak-256 of an event signature
- [Address & ENS](./address.md) — EIP-55 checksum (keccak-256 based)
- [Calldata Codec](./calldata.md) — encode / decode call data
- [Security model](../security.md)

---

> Disclaimer: results are for development reference — verify the algorithm and input
> encoding yourself.
