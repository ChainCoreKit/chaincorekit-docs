**English** · [简体中文](../../zh/evm/sig-verify.md) · [← Overview](../index.md)

# Signature Verifier · EVM

> Compute the signing digest, recover the signer from a signature, and compare it against
> an expected address. Supports EIP-191 messages and EIP-712 typed data. Everything is
> computed locally — no wallet, no chain lookup.

## When to use it

- You have a signature and want to confirm which address actually produced it.
- `ecrecover` in your contract returns an unexpected address and you want to nail down the
  digest off-chain first.
- You're integrating EIP-712 (Permit, order signing, …) and the front-end and contract
  hashes disagree — you need to find which layer is wrong.

## Steps

### Message (EIP-191)

1. Enter the **message**; the signing digest appears immediately.
2. Paste the **signature** (`0x`-prefixed, 65 bytes); the recovered signer is shown below.
3. (Optional) Enter an **expected signer address** to get a match / no-match verdict.

### Typed data (EIP-712)

1. Paste the full **typed data JSON** (`types`, `primaryType`, `domain`, `message`).
2. Each level is shown: the raw `encodeType` string, `typeHash`, `domainSeparator`,
   `hashStruct` and the final `digest`.
3. A signature can be pasted and compared the same way.

## Inputs / outputs

| Item | Meaning / format |
| --- | --- |
| Message | Any text; the prefix counts its length in **UTF-8 bytes** |
| Signature | `0x`-prefixed, 65 bytes (r ‖ s ‖ v); v may be 0/1 or 27/28 |
| Typed data | Standard EIP-712 JSON; when `EIP712Domain` is omitted it is inferred from the fields present in `domain` |
| Digest | The final 32 bytes the wallet actually signs |

## Notes & gotchas

- **This verifies EOA signatures.** Contract wallets such as Safe use ERC-1271 and can only
  be verified by calling `isValidSignature` on-chain — their signatures will never verify
  locally, and **that does not mean they're invalid**.
- **A successful recovery does not mean the content is trustworthy.** A signature always
  recovers *some* address: change one character in the message and you get a different
  address, not an error. So "the recovered address equals the one I expected" is the
  meaningful conclusion; "recovery succeeded" on its own says nothing.
- **EIP-712 problems are almost never cryptographic — they're schema mismatches.** One
  difference in field order, type or name versus the contract produces a different, equally
  plausible-looking hash. The `encodeType` string shown here can be compared character by
  character against your Solidity source, which beats staring at a 32-byte hash.
- **Message length is counted in bytes.** Counting characters for CJK or emoji yields a
  completely different digest — `中文消息` is 4 characters but 12 bytes.
- **Dependency ordering matters**: in `encodeType` the primary type comes first and the
  remaining dependencies are sorted alphabetically. Get the order wrong and `typeHash` is wrong.

## Related tools

- [ABI Codec](./abi-codec.md) — constructor args, event logs, revert errors
- [Hash Tool](./hash-tool.md) — keccak-256 and other common hashes
- [Transaction Decoder](./tx-decode.md) — raw transactions and RLP
- [Security model](../security.md)

---

> Disclaimer: verification only establishes the link between a signature and an address; it
> is not an endorsement of what was signed.
