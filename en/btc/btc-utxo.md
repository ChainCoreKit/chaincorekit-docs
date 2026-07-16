**English** · [简体中文](../../zh/btc/btc-utxo.md) · [← Overview](../index.md)

# UTXO Lookup · BTC

> Inspect the unspent outputs (UTXOs) of a Bitcoin address on mainnet or testnet,
> up to 20 addresses per run.

## When to use it

- You want to see an address's current UTXOs to build a transaction or estimate
  spendable value.
- You're checking fund composition — one large UTXO vs. many small ones.
- You need to review UTXOs across several addresses at once.

## Steps

1. Choose the network: **Mainnet** or **Testnet**.
2. Paste addresses in the box, **one per line**, up to 20 per run.
3. Click **Look up**. UTXO details appear in the results area below.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Mainnet / Testnet |
| Address | one per line (Legacy / SegWit / Taproot), ≤ 20 per run |
| Output | a list of UTXO details per address |

## Notes & gotchas

- **Max 20 addresses** per run — split larger sets into batches.
- Don't mix mainnet and testnet addresses; pick the right network first.
- UTXOs are an on-chain snapshot — re-run after new confirmations to refresh.

## Related tools

- [Balance Checker](./btc-balance.md) — balance totals only
- [PSBT Decode](./btc-psbt.md) — inspect an unsigned transaction
- [Generate BTC Wallet](./btc-wallet.md) — generate addresses locally
- [Security model](../security.md)

---

> Disclaimer: results rely on public on-chain data and are for reference only.
