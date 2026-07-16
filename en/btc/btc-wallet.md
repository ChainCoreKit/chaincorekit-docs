**English** · [简体中文](../../zh/btc/btc-wallet.md) · [← Overview](../index.md)

# Generate BTC Wallet · BTC

> Generate Bitcoin wallets locally in bulk across four address types — Legacy,
> Nested SegWit, Native SegWit, and Taproot — or import existing WIF keys. Keys
> never leave your device.

## When to use it

- You need a batch of Bitcoin addresses for development, testing, or rehearsals.
- You want many addresses of a chosen type at once (e.g. Native SegWit `bc1q…` or
  Taproot `bc1p…`).
- You have a WIF private key and want to recover its address.

> ⚠️ Keys are used in local memory for this session only — **never uploaded,
> stored, or sent off your device**. Read the [security model](../security.md) first.

## Steps

### Option A — Random bulk generation

1. Choose a **generation mode**:
   - **Bulk generate addresses**: create many addresses at once; each holds its own
     independent WIF key.
   - **Independent keys**: likewise one independent key per address, all unrelated.
2. Choose the **address type**:
   - **Native SegWit (`bc1q…`)**: today's mainstream format — low fees, broad
     compatibility. Pick this if unsure.
   - **Taproot (`bc1p…`)**: newer format with better privacy and scripting.
   - **Nested SegWit (`3…`)**: a transitional format compatible with older wallets.
   - **Legacy (`1…`)**: the oldest format — widest compatibility but higher fees.
3. Set the **count** (≤ 100).
4. (Optional) Expand **Advanced · derivation path** to set `account` and the
   starting `index`. The prefix follows the address type: Legacy `m/44'`, Nested
   SegWit `m/49'`, Native SegWit `m/84'`, Taproot `m/86'`.
5. Click **Generate**. The results table lists address and private key (masked by
   default).

> The path shown here is a **BIP structural illustration** only — not a real
> derivation and not a recovery credential. Each address's recovery credential is
> its own **WIF key**; back them up individually.

### Option B — Import a private key

1. Switch to the **Import private key** tab.
2. Enter WIF keys, **one per line** (batch paste supported).
3. Click **Create** to recover the addresses.

> Only **WIF keys** are accepted for import; HD options ("count", "derivation
> path") are unavailable afterward.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Generation mode | `Bulk generate addresses` / `Independent keys` |
| Address type | Native SegWit (bc1q) / Taproot (bc1p) / Nested SegWit (3) / Legacy (1) |
| Count | 1–100 |
| Account | the `account'` path segment, default 0 (illustration only) |
| Start index | the path's last-segment start, default 0 (illustration only) |
| Import | WIF private keys, one per line |
| Output | address, WIF key; copy, export (address-only / with keys), multi-select |

## Notes & gotchas

- **Max 100** addresses per run.
- **Path is illustrative only**: each address stands alone; recovery relies on its
  own WIF key, not on the path.
- **Import accepts WIF only**; other formats aren't handled.
- Results are **lost on leave/refresh** — export or write them down first.
- On mainnet, confirm the address type before receiving real funds — a wrong
  format can make funds unrecoverable.

## Security

- Keys are masked; click the eye icon to reveal, only in a **safe environment**.
- **Exporting a table with keys** writes a plaintext file — anyone who gets it
  fully controls those wallets. There's a confirmation step; store and delete it
  carefully.
- Sensitive data is never written to localStorage and is cleared from memory on
  close.

## Related tools

- [UTXO Lookup](./btc-utxo.md) — view an address's unspent outputs
- [Balance Checker](./btc-balance.md) — check balances in bulk
- [Address Format Convert](./btc-addr-convert.md) — convert between address forms
- [Security model](../security.md)

---

> Disclaimer: lost keys cannot be recovered — always back up offline. This tool
> assumes no liability for asset loss.
