**English** · [简体中文](../../zh/btc/btc-tx-decode.md) · [← Docs home](../index.md)

# Raw Transaction Decoder

> Paste signed BTC raw transaction hex to decode the TXID, inputs, outputs, size and RBF signal locally; fetch the fee with one click.

## When to use it

- You have transaction hex (exported from a wallet, sent by someone, pulled from a node) and want to see what it does **before** broadcasting.
- You want the TXID ahead of broadcast so you can track it later.
- As a recipient, you need to know whether the transaction is **replaceable** (RBF) — that decides whether you should deliver before confirmation.
- You want the fee rate (sat/vB) to judge whether it will stick in the mempool.

## Steps

1. Pick a **network**. A raw transaction carries no network marker, and the wrong choice
   re-encodes mainnet outputs as testnet addresses with a **perfectly valid checksum** —
   confirm it first.
2. Paste the **raw transaction hex** (`0100…` or `0x0100…`). Decoding happens locally; no
   network access required.
3. Click **Fetch upstream** when you need the fee — see below.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Mainnet / testnet; affects address encoding |
| Raw transaction | Signed transaction hex (not a PSBT) |
| TXID | Transaction hash, linked to the block explorer |
| Size | vsize (virtual size) · bytes · weight |
| Version / locktime | nVersion and nLockTime |
| Inputs | Referenced output, sequence, witness item count, RBF flag |
| Outputs | Address, amount (BTC and sat), script type |

## Why the fee is a separate step

**A raw transaction doesn't carry its input amounts.** They live in the upstream UTXOs, not in
this hex — so the fee **cannot be computed locally**. Only the output total can.

"Fetch upstream" queries the block explorer for each referenced transaction, then derives the fee
and the sat/vB rate. **If any one lookup fails the whole calculation is discarded** rather than
reporting a too-low figure: missing one input makes the fee look smaller, and that smaller number
appears perfectly normal with nothing to signal it's wrong.

Switching to a different transaction automatically invalidates the previously fetched amounts —
they no longer correspond to what's on screen.

## Notes & gotchas

- **RBF is the single most important bit for a recipient.** A transaction signalling RBF
  (BIP-125) can be replaced by the sender with a higher-fee version until it confirms —
  **including one that doesn't pay you**. It hides in the `sequence` field (`< 0xfffffffe` means
  replaceable), invisible among the hex, so this page calls it out explicitly. If you see RBF,
  wait for confirmation before delivering.
- **This is a raw transaction, not a PSBT.** The formats differ: a PSBT is an unfinished template
  (which does carry input amounts), a raw transaction is the signed result. Pasting the wrong one
  shows an error — use the [PSBT decoder](./btc-psbt.md) instead.
- **vsize is exact here.** The transaction is signed, so there's nothing to estimate the way a
  PSBT requires, and the fee rate is exact too.
- **OP_RETURN and non-standard outputs have no address** — the field is left blank rather than
  fabricating one.

## Related tools

- [PSBT Decoder](./btc-psbt.md) — unsigned transaction templates, checked before signing
- [UTXO Lookup](./btc-utxo.md) — unspent outputs for an address
- [Balance](./btc-balance.md) — address balance and transaction count
- [Security model](../security.md)
