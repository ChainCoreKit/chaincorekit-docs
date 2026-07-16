**English** · [简体中文](../../zh/solana/sol-wallet.md) · [← Overview](../index.md)

# Generate Wallet · Solana

> Generate Ed25519 wallets locally (BIP39 mnemonic + SLIP-0010 derivation), or
> import a Base58 key / mnemonic / CLI JSON array to recreate them.

## When to use it

- You need a batch of Solana test wallets for development, testing, or airdrop
  rehearsals.
- You want many addresses derived from one mnemonic via SLIP-0010, backed up
  together.
- You have a Base58 key, a mnemonic, or an `id.json`, and want to recover its
  address(es).

> ⚠️ Mnemonics and keys are used in local memory for this session only —
> **never uploaded or stored, and cleared on refresh**. Read the
> [security model](../security.md) first.

## Steps

### Option A — Random bulk generation

1. Choose a **generation mode**:
   - **Mnemonic derivation**: one BIP39 mnemonic derives many addresses via
     SLIP-0010; backing up that single phrase restores all of them.
   - **Independent**: each wallet gets its own unrelated mnemonic and must be
     backed up separately.
2. Choose the **mnemonic length**: 12 / 15 / 18 / 21 / 24 words (more words = more
   entropy).
3. Set the **count** (1–100). In derivation mode this is how many addresses are
   derived consecutively along the path.
4. Click **Generate**. The results table lists address, private key, and mnemonic
   (masked by default).

The derivation path is `m/44'/501'/i'/0'` (all hardened, the Phantom convention).

### Option B — Import a key / mnemonic

1. In the **Import** box paste: a BIP39 mnemonic, a Base58 private key (64-byte
   secretKey), or a Solana CLI JSON array (`id.json`).
2. If you imported a mnemonic, set the **derivation count** (1–100).
3. Click **Import** to recreate the wallets.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Generation mode | `Mnemonic derivation` / `Independent` |
| Mnemonic length | 12 / 15 / 18 / 21 / 24 words (BIP39) |
| Count | 1–100 |
| Derivation path | `m/44'/501'/i'/0'` (all hardened) |
| Import | mnemonic / Base58 key (64-byte secretKey) / CLI JSON array (`id.json`) |
| Output | address, key, mnemonic; export addresses, export with keys |

## Notes & gotchas

- **Path conventions differ**: Phantom uses `m/44'/501'/i'/0'`; Solflare / Ledger /
  solana-keygen commonly use `m/44'/501'/i'`. If an address doesn't match your own
  wallet, it's usually a path difference.
- **Max 100** addresses per run.
- **Importing a key ≠ derivation**: a raw Base58 key is independent and carries no
  derivation info.
- Results are **lost on leave/refresh** — export or write them down first.

## Security

- Keys/mnemonics are masked; click the eye icon to reveal, only in a **safe
  environment**.
- **Exporting a table with keys** writes a plaintext file — anyone who gets it
  fully controls those wallets. Store and delete it carefully.
- Sensitive data is never written to localStorage and is cleared from memory on
  close.

## Related tools

- [PDA / ATA](./sol-address.md) — compute PDAs and ATAs
- [Instruction Codec](./sol-instruction.md) — encode/decode instruction data via IDL
- [Compute / Fee / Rent](./sol-fee-rent.md) — estimate fees and rent exemption
- [Security model](../security.md)

---

> Disclaimer: lost keys cannot be recovered — always back up offline. This tool
> assumes no liability for asset loss.
