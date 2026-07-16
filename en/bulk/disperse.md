**English** · [简体中文](../../zh/bulk/disperse.md) · [← Overview](../index.md)

# Disperse

> Distribute native coins or ERC-20 to many addresses in a single transaction via
> the Disperse contract — save gas, sign less.

## When to use it

- Pay many addresses at once, merging many transfers into one transaction to save
  gas and cut confirmations.
- One-to-many distribution: airdrops, batch payroll, event rewards.
- You care about overall efficiency and signature count more than per-wallet
  control.

## Steps

1. Connect your wallet (top right). While disconnected, the button shows
   **"🔒 Connect wallet to continue"** — clicking opens the connect dialog.
2. The **send network** follows the connected wallet's network; the card shows the
   **Disperse contract** address in use (copyable, with an explorer link).
3. Enter the **token**: blank = native coin; a `0x…` ERC-20 contract address =
   distribute that token.
4. For ERC-20, first click **① Approve** to let the Disperse contract move your
   tokens.
5. Add the list: one "address,amount" per line (comma or space separated), then
   **Add**. You can also use **Sample**, **Import Excel / CSV**, or the
   **template**.
6. The table supports select / **invert** / **delete selected** / **clear**, and
   **filter** by address.
7. Click **Disperse**. In the confirmation dialog, verify the send network, payer
   address, asset, Disperse contract, recipient count, estimated gas, and total,
   then run. Results can be **exported**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Send network | follows the connected wallet's network |
| Token | blank = native coin; `0x…` = ERC-20 contract |
| Disperse contract | the distributor address shown on the card (verify on explorer) |
| Approve | the approval step before distributing ERC-20 |
| List | one "address,amount" per line, comma / space separated |
| Output | distribution results, export |

## Notes & gotchas

- **ERC-20 needs Approve first**: distribution fails without allowance; complete
  ① Approve if the allowance is insufficient.
- **One on-chain transaction**: distribution completes in a single tx with one
  signature, but total gas grows with recipient count.
- **Payer needs native coin for gas**: distributing native coin requires gas on top
  of the total amount.
- **Verify the Disperse contract**: check it on the block explorer before writing,
  confirming it's the trusted distributor contract.
- **Amount precision**: ERC-20 amounts are scaled by the token's `decimals`.
- **Native coins differ per chain**: Ethereum/Arbitrum/Base/Optimism = ETH,
  BNB Chain = BNB, Polygon = POL, Avalanche = AVAX, Sepolia = SepoliaETH.

## Related tools

- [Per-wallet Send](./bulk-send.md) — sign each transfer, fully self-custodial
- [Multi-key Send](./bulk-send2.md) — import many keys and batch-send concurrently
- [Sweep](./bulk-collect.md) — consolidate assets from many wallets into one
- [Balance Checker](./bulk-query-balance.md) — batch balance lookups
- [Security model](../security.md)

---

> Disclaimer: distribution is a real, irreversible on-chain transaction — verify the
> recipient list, asset, contract, and network before running.
