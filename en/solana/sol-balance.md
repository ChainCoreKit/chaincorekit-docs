**English** · [简体中文](../../zh/solana/sol-balance.md) · [← Docs home](../index.md)

# Solana Balance

> Fetch an address's SOL balance and every token holding (Token-2022 included) in one go, with amounts shown both converted and in raw base units.

## When to use it

- Get a quick picture of how much SOL an address holds and which tokens it owns.
- Reconcile accounts where you need the **raw base-unit integer**, not the rounded figure a wallet displays.
- Investigate a token that shows up in your wallet but not in other tools — usually Token-2022.
- Find out how many empty token accounts you could close to reclaim their rent.

## Steps

1. Pick a **network** (Mainnet Beta / Devnet / Testnet).
2. (Optional) Enter a **custom RPC**. Solana's public nodes rate-limit hard; use your own endpoint for repeated lookups.
3. Paste a **wallet address** (base58 public key) and click **Look up**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Mainnet Beta / Devnet / Testnet |
| Custom RPC (optional) | Blank uses a public node |
| Wallet address | Solana base58 public key |
| SOL | Converted SOL, with the raw lamports alongside |
| Token holdings | Mint, amount (converted + base units), owning program |

## Notes & gotchas

- **Token-2022 is a separate program.** Solana token accounts are keyed by program, so classic
  SPL Token and Token-2022 have to be queried separately. This page queries both — a tool that
  queries only one **silently drops** half your holdings, and those holdings are visible in your
  wallet. Each row is tagged with the program it belongs to.
- **Amounts appear in two forms.** The converted figure is for reading; the raw base-unit integer
  is the on-chain fact. Use the raw value when reconciling, sending transactions, or filling in
  contract arguments.
- **Zero-balance token accounts are counted but not listed.** They still hold rent (about 0.002 SOL
  each) which you can reclaim by closing them in your wallet. Omitting the count entirely would
  leave you assuming you have none.
- **This is a read-only lookup.** No wallet connection, no private key.

## Related tools

- [Solana Token Inspector](./sol-token-inspector.md) — inspect a mint's decimals and authorities
- [Solana Address Tools](./sol-address.md) — PDA / ATA derivation
- [Solana Fees & Rent](./sol-fee-rent.md) — rent and fee estimation
- [Security model](../security.md)
