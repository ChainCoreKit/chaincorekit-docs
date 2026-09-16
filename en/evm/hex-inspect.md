**English** · [简体中文](../../zh/evm/hex-inspect.md) · [← Docs home](../index.md)

# Hex Inspector

> Paste any `0x` string to see what it might be, with a direct link to the right decoder.

## When to use it

- You copied a `0x…` string out of a log, an explorer or an error message and **don't know what it is**.
- You think it's calldata but want to confirm before decoding.
- You want to tell quickly whether 32 bytes is a transaction hash, an event TopicID or a storage slot value.

## Steps

1. Paste the `0x` string into the input (a missing `0x` prefix and mixed case are both tolerated).
2. The results table lists candidates by confidence, with a link to the matching tool on the right.
3. If the first 4 bytes hit the built-in dictionary, the function signature is reported directly —
   jumping from "might be a selector" to "this is `transfer(address,uint256)`".

## How it decides

| Feature | Could be | Where to check |
| --- | --- | --- |
| 4 bytes | Function selector | Signature Lookup |
| 20 bytes | EVM address | Address & ENS |
| 32 bytes | Transaction hash / block hash / event TopicID / storage slot / bytes32 text | Hash Tool |
| 65 bytes | ECDSA signature (r + s + v) | Signature Verify |
| 4 + 32n bytes | Contract calldata | Calldata Decoder |
| A multiple of 32 | ABI-encoded parameters | ABI Codec |
| Starts `0x60806040…` | Contract bytecode | Contract Check |
| RLP list or `0x01/02/03` | Raw transaction | Transaction Tracer |

## Notes & gotchas

- **These are candidates, not a verdict.** The same bytes mean different things in different
  contexts — 32 bytes could be a transaction hash or a storage slot value, and guessing one would
  send you the wrong way. They're ordered by confidence; follow the link for real decoding.
- **32 bytes might be a private key.** A hash and a private key are indistinguishable by appearance.
  Everything here runs in your browser and nothing is uploaded, but make it a habit:
  **never paste a private key into any online tool.** The page warns you on 32-byte input.
- **This page doesn't decode anything** — it identifies and dispatches. For parameters or
  transaction contents, use the linked tool.
- **Length is the most reliable clue**, which is why the byte count sits in the result header.

## Related tools

- [Signature Lookup](./signature-lookup.md) — selector / TopicID ⇄ signature
- [Calldata Decoder](./calldata.md) — decode full parameters from a selector
- [ABI Codec](./abi-codec.md) — encode and decode parameters
- [Hash Tool](./hash-tool.md) — keccak-256 / sha256 and friends
- [Transaction Tracer](./trace-view.md) — a transaction's calls and events
