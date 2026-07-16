**English** · [简体中文](../../zh/polkadot/dot-wallet.md) · [← Overview](../index.md)

# Generate Wallet · Polkadot

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

1. Choose a **key type**: `ed25519` or `ecdsa` (`sr25519` coming soon).
2. Choose an **SS58 prefix**: Polkadot (0) / Kusama (2) / Generic Substrate (42),
   which sets the prefix of the generated addresses.
3. Choose a **generation mode**:
   - **Derive from mnemonic**: one mnemonic derives many accounts by index.
   - **Independent**: each wallet gets its own mnemonic.
4. Choose the **mnemonic length**: 12 / 15 / 18 / 21 / 24 words.
5. Set the **count** (1–100).
6. (Optional) Set a **derivation URI**: leave it blank with count > 1 to derive by
   index `//0` `//1` …; enter a URI (e.g. `//hard` or `///password`) for a single
   account.
7. Click **Generate**. The results table lists address and private key (masked by
   default).

### Option B — Import a mnemonic / key

1. In the **Import** card, paste a **BIP39 mnemonic** (optionally with
   `//derivation-path` `///password`), or a 32-byte **secret seed** (`0x…`).
2. Click **Import** to recreate the wallet.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Key type | `ed25519` / `ecdsa` (`sr25519` coming soon) |
| SS58 prefix | Polkadot (0) / Kusama (2) / Generic Substrate (42) |
| Generation mode | derive from mnemonic / independent |
| Mnemonic length | 12 / 15 / 18 / 21 / 24 words (BIP39) |
| Count | 1–100 |
| Derivation URI (optional) | e.g. `//hard` or `///password`; blank with count > 1 derives by index `//0` `//1` … |
| Import | BIP39 mnemonic (optionally `//path` `///password`), or 32-byte secret seed (`0x…`) |
| Output | address, private key (masked by default); export addresses or export with keys |

## Notes & gotchas

- **Key type differs from mainstream wallets**: Polkadot-ecosystem wallets derive
  with sr25519 by default; this tool currently supports only ed25519 / ecdsa, so the
  address from the same mnemonic here differs from what a mainstream (sr25519)
  wallet shows — **don't use it to verify or receive assets**.
- **Max 100** wallets per run.
- **Derivation URI**: blank with count > 1 derives by index `//0` `//1` …; a URI
  derives a single account (sr25519 soft derivation coming soon).
- **The SS58 prefix only affects the address text**: the underlying AccountId is
  unchanged; a new prefix isn't a new account.
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
