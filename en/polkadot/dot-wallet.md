**English** · [简体中文](../../zh/polkadot/dot-wallet.md) · [← Overview](../index.md)

# Polkadot Wallet Generator · Polkadot

> Generate Substrate wallets locally (BIP39 + SS58), or import a mnemonic / key.
> Keys and mnemonics never leave your device.

## When to use it

- You need a batch of Substrate test wallets for development, testing, or rehearsals.
- You want many Substrate addresses derived from one BIP39 mnemonic, backed up
  together.
- You have a mnemonic or secret seed and want to recover its address.

> ⚠️ Mnemonics / keys are generated in memory only — never uploaded or stored, and
> cleared on refresh. Back up offline and never share them. Read the
> [security model](../security.md) first.

## Steps

### Option A — Random bulk generation

1. Choose a **key type**: `sr25519` (the default, matching Polkadot wallets),
   `ed25519`, or `ecdsa`.
2. Choose an **SS58 prefix**: Polkadot (0) / Kusama (2) / Generic Substrate (42),
   which sets the prefix of the generated addresses.
3. Choose a **generation mode**:
   - **Derive from mnemonic**: one mnemonic derives many accounts by index.
   - **Independent**: each wallet gets its own mnemonic.
4. Choose the **mnemonic length**: 12 / 15 / 18 / 21 / 24 words.
5. Set the **count** (1–100).
6. (Optional) Set a **derivation URI**: leave it blank with count > 1 to derive by
   index `//0` `//1` …; enter a URI (e.g. `//hard`, `/soft`, `///password`) for a
   single account.
7. Click **Generate**. The results table lists address and private key (masked by
   default).

### Option B — Import a mnemonic / key

1. In the **Import** card, paste a **BIP39 mnemonic** (optionally with
   `//derivation-path` `///password`), or a 32-byte **secret seed** (`0x…`).
2. Click **Import** to recreate the wallet.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Key type | `sr25519` (default) / `ed25519` / `ecdsa` |
| SS58 prefix | Polkadot (0) / Kusama (2) / Generic Substrate (42) |
| Generation mode | derive from mnemonic / independent |
| Mnemonic length | 12 / 15 / 18 / 21 / 24 words (BIP39) |
| Count | 1–100 |
| Derivation URI (optional) | e.g. `//hard`, `/soft` (sr25519 only), `///password`; blank with count > 1 derives by index `//0` `//1` … |
| Import | BIP39 mnemonic (optionally `//path` `///password`), or 32-byte secret seed (`0x…`) |
| Output | address, private key (masked by default); export addresses or export with keys |

## Notes & gotchas

- **Changing the key type gives you a different account**: Polkadot wallets
  (polkadot-js, Talisman, SubWallet, Ledger) all default to sr25519, and so does this
  tool — the same mnemonic yields the same address your wallet shows.
  Switch to `ed25519` or `ecdsa` and that mnemonic resolves to **a different
  account**; the page warns you when you do. Make sure the type matches before
  verifying or receiving funds.
- **Max 100** wallets per run.
- **Soft derivation (a single `/`) is sr25519-only**: it is a capability unique to
  sr25519. Under `ed25519` / `ecdsa` a `/xxx` path prompts you to switch the key type
  to sr25519, or to use hard derivation (`//`) instead.
- **The SS58 prefix only affects the address text**: the underlying AccountId is
  unchanged; a new prefix isn't a new account. Switching the prefix **re-encodes
  the rows you already generated** in place — the addresses change, the AccountId
  doesn't, and the explorer links follow to the matching chain. No need to
  regenerate.
- **Switching the key type does not clear existing results**: it is a different
  key set, so regenerate before using the new type. Results aren't cleared
  automatically because a mnemonic can't be recovered once the page is left —
  brushing a dropdown shouldn't destroy it.
- Results are **lost on leave/refresh** — export or write them down first.

## Security

- Keys/mnemonics are masked; click the eye icon to reveal, only in a **safe
  environment**.
- **Exporting a table with keys** writes a plaintext file — anyone who gets it fully
  controls those wallets. Store and delete it carefully.
- Sensitive data is never written to localStorage and is cleared from memory on
  close.
- **Keys never leave your device**: everything is generated locally in the browser —
  never uploaded or stored.

## Related tools

- [SS58 Convert](./dot-ss58.md) — SS58 ↔ AccountId32
- [Substrate Hash / Storage Key](./dot-hash-storage.md) — derive a storage key from an AccountId
- [SCALE Codec](./dot-scale.md) — encode / decode by type expression
- [DOT Units](./dot-unit.md) — Planck ↔ main unit
- [Security model](../security.md)

---

> Disclaimer: lost keys cannot be recovered — always back up offline. This tool
> assumes no liability for asset loss.
