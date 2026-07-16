**English** · [简体中文](../../zh/solana/sol-address.md) · [← Overview](../index.md)

# PDA / ATA · Solana

> Compute a Program Derived Address (PDA + canonical bump) and an Associated Token
> Account (ATA) locally, distinguishing Token Program from Token-2022.

## When to use it

- While building an Anchor / native program, you need the PDA and bump for a set of
  seeds ahead of time.
- You want the ATA address for an owner under a given mint (to verify before a
  transfer or account creation).
- You need to tell apart the ATAs derived under Token Program vs Token-2022 for the
  same mint.

## Steps

### PDA mode

1. Switch to **PDA** at the top.
2. Enter the **Program ID** (base58).
3. Add **Seeds** one by one: each ≤ 32 bytes, up to 15; integers are treated as
   little-endian.
4. The result shows the derived PDA address and the canonical **bump**.

### ATA mode

1. Switch to **ATA** at the top.
2. Enter the **Owner** (base58 owner pubkey) and **Mint** (base58 mint pubkey).
3. Choose the **Token Program**: `Token Program` or `Token-2022`.
4. The result shows the corresponding ATA address.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Program ID | base58 program pubkey (PDA mode) |
| Seeds | each ≤ 32 bytes, up to 15; integers little-endian |
| Owner | base58 owner pubkey (ATA mode) |
| Mint | base58 mint pubkey (ATA mode) |
| Token Program | `Token Program` / `Token-2022` |
| Output | PDA address + canonical bump (PDA); ATA address (ATA) |

## Notes & gotchas

- **Canonical bump**: a PDA uses the largest bump that pushes the derivation off the
  ed25519 curve (the canonical bump); a different bump gives a different address.
- **Seed encoding must match**: integers default to little-endian, strings to their
  raw bytes. This must match exactly how your on-chain program encodes seeds, or the
  address won't line up.
- **Wrong Token Program = wrong address**: Token and Token-2022 are different program
  ids, so the same owner/mint derives **different** ATAs. Pick the one the mint
  actually belongs to.
- **Each seed ≤ 32 bytes**: hash an over-long seed yourself first, then use the hash.

## Related tools

- [Instruction Codec](./sol-instruction.md) — encode/decode instruction data via IDL
- [Program IDL](./sol-idl.md) — browse an Anchor IDL structurally
- [Generate Wallet](./sol-wallet.md) — generate / import wallets locally
- [Security model](../security.md)

---

> Disclaimer: derivation depends on the Program ID / seeds / Token Program you
> provide — verify they match the chain yourself.
