**English** · [简体中文](../../zh/solana/sol-fee-rent.md) · [← Overview](../index.md)

# Compute / Fee / Rent · Solana

> Estimate a Solana transaction's Compute Units, signature fee, and priority fee,
> plus an account's rent-exemption balance — all locally, no network.

## When to use it

- You want to estimate a transaction's total cost: base signature fee + priority fee.
- While setting a Compute Budget (CU Limit / CU Price), you want to work out the
  priority-fee cost up front.
- Before creating an account, you want to know how many lamports to pre-fund to reach
  rent exemption.

## Steps

### Transaction fee

1. Enter the **number of signatures** (default 1) — each signature has a fixed base
   fee.
2. Enter the **CU Limit** (0 – 1,400,000, default 200000).
3. Enter the **CU Price** (micro-lamports / CU, default 0) — the priority-fee price
   per Compute Unit.
4. The result shows the estimated signature fee, priority fee, and total (lamports /
   SOL).

> Fetching a live priority fee via `getRecentPrioritizationFees` needs read-only RPC
> and is **coming soon**.

### Rent exemption

1. Enter the **Account Size** (bytes, default 165 — the SPL Token account size).
2. The result shows the minimum balance for an account of that size to be rent-exempt.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Signatures | number of transaction signatures, default 1 |
| CU Limit | 0 – 1,400,000, default 200000 |
| CU Price | micro-lamports / CU, default 0 (no priority fee) |
| Account Size | account bytes, default 165 (SPL Token account) |
| Output | signature fee / priority fee / total; min rent-exempt balance (lamports and SOL) |

## Notes & gotchas

- **Units**: 1 SOL = 1,000,000,000 lamports; the priority-fee price is in
  **micro-lamports / CU** (1 lamport = 10⁶ micro-lamports) — don't mix the two.
- **Priority fee = CU Limit × CU Price**: when CU Price is 0 there's no priority fee,
  only the base signature fee.
- **CU Limit cap**: a single transaction is capped at 1,400,000 Compute Units.
- **Rent scales with size**: the minimum rent-exempt balance grows with Account Size
  — larger accounts pre-fund more.
- **Local estimate**: this is a static, offline estimate; live priority fees and
  actual on-chain rates may differ.

## Related tools

- [Instruction Codec](./sol-instruction.md) — encode/decode instruction data via IDL
- [PDA / ATA](./sol-address.md) — compute PDAs and ATAs
- [Program IDL](./sol-idl.md) — browse an Anchor IDL structurally
- [Security model](../security.md)

---

> Disclaimer: these are local, static estimates; actual on-chain costs depend on
> network conditions at the time.
