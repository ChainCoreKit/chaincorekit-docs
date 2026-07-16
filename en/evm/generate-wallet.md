**English** · [简体中文](../../zh/evm/generate-wallet.md) · [← Overview](../index.md)

# Generate Wallet · EVM

> Generate EVM wallets locally in bulk — derive from a mnemonic, or import an
> existing key/mnemonic to recreate wallets.

## When to use it

- You need a batch of test wallets for development, testing, or airdrop rehearsals.
- You want many addresses derived from one mnemonic via BIP44, backed up together.
- You have a private key/mnemonic and want to recover its address(es).

> ⚠️ Keys and mnemonics are used in local memory for this session only —
> **never uploaded, stored, or sent off your device**. Read the
> [security model](../security.md) first.

## Steps

### Option A — Random bulk generation

1. Choose a **generation mode**:
   - **Same mnemonic (HD)**: one BIP39 mnemonic derives many addresses; backing up
     that single phrase restores all of them. A leaked key affects only its address.
   - **Independent mnemonics**: each wallet gets its own unrelated mnemonic and must
     be backed up separately.
2. Choose the **mnemonic length**: 12 / 15 / 18 / 21 / 24 words (more words = more
   entropy).
3. Set the **count** (≤ 100). In HD mode this is how many addresses are derived
   consecutively along the path.
4. (Optional) Expand **Advanced · derivation path** to set `account` and the
   starting `index`. The path follows BIP44: `m / 44' / 60' / account' / 0 / index`.
5. Click **Generate**. The results table lists address, private key, and mnemonic
   (masked by default).

### Option B — Import a key / mnemonic

1. Switch to the **Import key / mnemonic** tab.
2. Enter keys or mnemonics, **one per line** (batch paste supported).
3. Click **Create** to recreate the wallets.

> When importing by private key, the HD options ("count", "derivation path") are
> unavailable — a raw key carries no derivation info.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Generation mode | `Same mnemonic (HD)` / `Independent mnemonics` |
| Mnemonic length | 12 / 15 / 18 / 21 / 24 words (BIP39) |
| Count | 1–100 |
| Account | the `account'` segment of the BIP44 path, default 0 |
| Start index | the starting value of the path's last segment, default 0 |
| Import | private key (`0x` + 64 hex) or BIP39 mnemonic, one per line |
| Output | address, key, mnemonic, path; copy, export, QR detail |

## Notes & gotchas

- **Max 100** addresses per run.
- **QR codes contain the address only** — safe for receiving test coins.
  **Never** generate a QR of a private key.
- **Importing a key ≠ HD derivation**: imported keys are independent; no count/path.
- Results are **lost on leave/refresh** — export or write them down first.

## Security

- Keys/mnemonics are masked; click the eye icon to reveal, only in a **safe
  environment**.
- **Exporting a table with keys** writes a plaintext file — anyone who gets it
  fully controls those wallets. There's a confirmation step; store and delete it
  carefully.
- Sensitive data is never written to localStorage and is cleared from memory on
  close.

## Related tools

- [Vanity Address](./vanity.md) — addresses with a chosen prefix/suffix
- [Address & ENS](./address.md) — checksum addresses, resolve ENS
- [Faucets](./faucet.md) — get test coins for a new wallet
- [Security model](../security.md)

---

> Disclaimer: lost keys cannot be recovered — always back up offline. This tool
> assumes no liability for asset loss.
