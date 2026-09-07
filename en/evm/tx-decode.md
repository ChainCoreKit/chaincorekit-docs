**English** · [简体中文](../../zh/evm/tx-decode.md) · [← Overview](../index.md)

# Transaction Decoder · EVM

> Turn a `0x02f8…` blob back into fields: type, fees, access list, blobs, authorization
> list — and recover the sender from the signature. Covers Legacy plus EIP-2930 / 1559 /
> 4844 / 7702. Everything is computed locally.

## When to use it

- You signed a transaction offline and want to check the recipient, amount and nonce
  before broadcasting.
- You found an unidentified transaction blob in a log or a capture.
- You're debugging the wire format: a transaction *is* RLP inside, so when decoding
  fails you can switch to the RLP tab and look at the raw structure.

## Steps

### Raw transaction

1. Paste the **`0x`-prefixed raw signed transaction**.
2. The top shows the **transaction hash** and the **sender recovered from the signature**.
3. The table below lists the fields, which vary by type (`gasPrice` only for type 0/1,
   `maxFeePerBlobGas` only for type 3, `authorizationList` only for type 4).

### RLP

1. Paste **`0x`-prefixed RLP data**.
2. Byte strings and list lengths are shown by nesting depth.

## Inputs / outputs

| Item | Meaning / format |
| --- | --- |
| Raw transaction | Complete `0x`-prefixed signed transaction |
| Transaction type | `0` Legacy / `1` EIP-2930 / `2` EIP-1559 / `3` EIP-4844 / `4` EIP-7702 |
| Sender | Recovered from `r`, `s`, `yParity`; left empty when recovery fails |
| RLP data | `0x`-prefixed hex |

## Notes & gotchas

- **EIP-4844 has two shapes**: blocks store the *payload body*, while
  `eth_sendRawTransaction` takes the **network wrapper** (payload body + blobs +
  commitments + proofs). Both start with `0x03` and are easy to mix up — when a wrapper
  is detected the tool says so explicitly instead of decoding its first element as a
  whole transaction and producing nonsense.
- **A field-count mismatch is a hard error**: one missing item shifts every field after
  it, and each shifted value still *looks* plausible. Better to refuse than to hand you a
  suspicious result.
- **The sender is left empty when recovery fails**: no fallback to a wrong address. This
  happens when the signature has been altered, or was never valid.
- **RLP carries no type information**: decoding yields nested byte strings only. Whether
  an item is a `nonce` or a `gasPrice` is decided by the enclosing structure — so the RLP
  view shows shape and leaves interpretation to you.
- **Trailing bytes are an error**: they usually mean the input was truncated or something
  extra was pasted in. Ignoring them silently would let you believe you're seeing it all.

## Related tools

- [Calldata Codec](./calldata.md) — decode a transaction's `data` field
- [ABI Codec](./abi-codec.md) — constructor args, event logs, revert errors
- [Transaction Tracer](./trace-view.md) — call tree for an on-chain transaction
- [Unit Converter](./unit-convert.md) — wei / gwei / ether

---

> Disclaimer: decoded results are for reference; always defer to the raw on-chain data.
