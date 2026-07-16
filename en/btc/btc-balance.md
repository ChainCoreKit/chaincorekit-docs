**English** · [简体中文](../../zh/btc/btc-balance.md) · [← Overview](../index.md)

# Balance Checker · BTC

> Paste many Bitcoin addresses and check their balances in one pass, on mainnet or
> testnet, up to 200 addresses per run.

## When to use it

- You have a batch of addresses and want to verify each balance quickly.
- Before a sweep or an audit, you want to see which addresses hold funds.
- Reconciliation — confirm that generated or imported addresses received funds.

## Steps

1. Choose the network: **Mainnet** or **Testnet**.
2. Paste addresses in the box, **one per line**, up to 200 per run.
3. Click **Look up**. Balances appear in the results area below.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Mainnet / Testnet |
| Address | one per line (Legacy / SegWit / Taproot), ≤ 200 per run |
| Output | the balance for each address |

## Notes & gotchas

- **Max 200 addresses** per run — split larger sets into batches.
- Don't mix mainnet and testnet addresses; pick the right network first.
- Balances are an on-chain snapshot — unconfirmed transactions may be excluded;
  re-run after confirmation to refresh.

## Related tools

- [UTXO Lookup](./btc-utxo.md) — view unspent-output details
- [Generate BTC Wallet](./btc-wallet.md) — generate addresses locally
- [Address Format Convert](./btc-addr-convert.md) — convert between address forms
- [Security model](../security.md)

---

> Disclaimer: results rely on public on-chain data and are for reference only.
