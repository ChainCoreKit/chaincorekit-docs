**English** · [简体中文](../../zh/evm/signature-lookup.md) · [← Docs home](../index.md)

# Signature Lookup

> Function / event signature ⇄ 4-byte selector and 32-byte TopicID, both directions from one page.

## When to use it

- You have a `0x…` string and want to know which function or event it maps to — **without knowing which kind it is yet**.
- You need an event's TopicID for a test or a log filter.
- You want to check whether calldata's first four bytes are the function you think they are.
- You want to see what a signature with parameter names and `indexed` looks like once canonicalised.

## Steps

### Signature → hash

Enter a function or event signature on the left (e.g. `transfer(address,uint256)`) and you get
**both** results below:

- **Function selector** — the first 4 bytes of the signature's keccak-256 hash
- **Event TopicID** — all 32 bytes of the same hash

Showing both isn't redundant: they are slices of the same hash. And a signature like
`Transfer(address,address,uint256)` is **syntactically indistinguishable** between a function and
an event (the capital letter is a naming convention, not a language rule), so you aren't asked to
pick one first.

Type aliases (`uint` → `uint256`) and Etherscan-style leniency are supported — paste a definition
with parameter names and `indexed` and they'll be stripped before hashing. When the canonical form
differs from what you typed, it's shown below the result.

### Hash → signature

Paste a hex string on the right and the tool **routes it by length**:

- 4 bytes (8 hex characters) → function selector dictionary
- 32 bytes (64) → event TopicID dictionary

A missing `0x` prefix and uppercase letters are both tolerated. Which kind it was recognised as is
shown explicitly as a tag.

## Notes & gotchas

- **Hashes are one-way.** Every reverse lookup depends on a known signature table, so no match does
  **not** mean the selector is invalid. This tool ships an offline dictionary covering the common
  standard interfaces (ERC-20 / ERC-721 / ERC-1155 and friends); for a fuller database try
  openchain.xyz or 4byte.directory.
- **One selector can in principle map to several signatures** — 4 bytes is only ~4 billion
  possibilities, and collisions can be constructed deliberately. A reverse lookup returns one match
  from the dictionary, not the only possible answer.
- **"Wrong length" and "not in the dictionary" are different things.** The first means your input
  needs fixing, the second is the dictionary's boundary — they're reported separately.
- **Canonicalisation changes the hash.** `transfer(address,uint)` and `transfer(address,uint256)`
  are the same signature (the former is an alias), but a stray space in `transfer(address ,uint256)`
  would hash to something entirely different if it weren't stripped — which is why this page
  canonicalises. If you want the raw hash with **no** normalisation, use the
  [hash tool](./hash-tool.md).

## Related tools

- [Hash Tool](./hash-tool.md) — keccak-256 / sha256 and friends, with **no** input normalisation
- [Calldata Decoder](./calldata.md) — decode full parameters from a selector
- [ABI Codec](./abi-codec.md) — encode and decode parameters
- [Transaction Tracer](./trace-view.md) — a transaction's calls and events
