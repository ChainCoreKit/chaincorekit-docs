**English** · [简体中文](../../zh/btc/btc-wallet.md) · [← Overview](../index.md)

# Generate BTC Wallet · BTC

> Generate Bitcoin wallets locally in bulk: one BIP39 mnemonic derives many
> addresses along the BIP path for the chosen address type — Legacy, Nested
> SegWit, Native SegWit, or Taproot — or import existing WIF keys. Keys never
> leave your device.

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
   - **Derive from one mnemonic**: one BIP39 mnemonic derives consecutive
     addresses along the path for the chosen type. Back up **that single
     mnemonic** to restore every address.
   - **Independent mnemonics**: each wallet gets its own mnemonic and key, all
     unrelated — back up **every mnemonic separately**.
2. Choose the **address type**:
   - **Native SegWit (`bc1q…`)**: today's mainstream format — low fees, broad
     compatibility. Pick this if unsure.
   - **Taproot (`bc1p…`)**: newer format with better privacy and scripting.
   - **Nested SegWit (`3…`)**: a transitional format compatible with older wallets.
   - **Legacy (`1…`)**: the oldest format — widest compatibility but higher fees.
3. Set the **count** (≤ 100).
4. (Optional) Expand **Advanced · derivation path** to set `account`, the
   starting `index`, and an optional BIP39 passphrase. The prefix follows the
   address type: Legacy `m/44'` (BIP44), Nested SegWit `m/49'` (BIP49), Native
   SegWit `m/84'` (BIP84), Taproot `m/86'` (BIP86).
   All four are **real BIP32 derivations** — including BIP86 for Taproot — so the
   same mnemonic restores identical addresses in any compatible wallet.
5. Click **Generate**. The results table lists address and private key (masked by
   default).

> **The mnemonic is the recovery credential.** In the derive-from-one-mnemonic
> mode, writing down that single mnemonic (plus any passphrase you set) restores
> every address in any compatible wallet. WIF keys can be backed up separately,
> but leaking one only affects that single address.

### Option B — Import a private key

1. Switch to the **Import private key** tab.
2. Enter WIF keys, **one per line** (batch paste supported).
3. Click **Create** to recover the addresses.

> Only **WIF keys** are accepted for import; HD options ("count", "derivation
> path") are unavailable afterward.

> **BIP39 passphrase (optional)** — also known as the 25th word. Leaving it empty
> matches standard derivation. Once set, the same mnemonic derives a **completely
> different and unrelated** set of wallets. A typo fails silently — you simply get
> other addresses. Store it **separately** from the mnemonic; without it the
> mnemonic alone cannot recover your funds.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Generation mode | `Derive from one mnemonic` / `Independent mnemonics` |
| Address type | Native SegWit (bc1q) / Taproot (bc1p) / Nested SegWit (3) / Legacy (1) |
| Count | 1–100 |
| Account | the `account'` path segment, default 0 |
| Start index | the path's last-segment start, default 0 |
| BIP39 passphrase | optional. Empty means standard derivation; setting one gives a different set of wallets and must be stored separately from the mnemonic |
| Import | WIF private keys, one per line |
| Output | address, WIF key; copy, export (address-only / with keys), multi-select |

## Notes & gotchas

- **Max 100** addresses per run.
- **A passphrase is part of the seed**: a different passphrase gives you a
  completely different set of wallets, and a typo fails silently — you just get
  other addresses. Lose it and the mnemonic alone cannot recover your funds.
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
