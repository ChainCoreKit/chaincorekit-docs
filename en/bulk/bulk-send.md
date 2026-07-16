**English** · [简体中文](../../zh/bulk/bulk-send.md) · [← Overview](../index.md)

# Per-wallet Send

> Send native coins or ERC-20 to many recipients one transfer at a time from the
> connected wallet — no contract, fully self-custodial.

## When to use it

- Send one transfer each to a batch of addresses, confirming every one in your
  wallet for full control.
- Avoid a distributor contract (no approve, no trusting a third-party contract).
- The list is small or amounts vary, so per-wallet sending is enough.

## Steps

1. Connect your wallet (top right). While disconnected, the button shows
   **"🔒 Connect wallet to continue"** — clicking opens the connect dialog.
2. The **send network** follows the connected wallet's current network.
3. Enter the **token**: blank = native coin; a `0x…` ERC-20 contract address =
   send that token (token info is shown).
4. Add the list in the bottom box: one "address,amount" per line (comma or space
   separated), then click **Add**. You can also use **Sample**, **Import
   Excel / CSV**, or download the **template** and import it filled in.
5. The table lists each row's address and amount; you can select / **invert** /
   **delete selected** / **clear**, and **filter** by address.
6. Click **Send**. In the confirmation dialog, verify the send network, payer
   address, asset, recipient count, estimated gas, and total, then run.
7. Each transfer is confirmed individually in the wallet and lands one by one;
   failed rows can be **retried**, and results can be **exported**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Send network | follows the connected wallet's network |
| Token | blank = native coin; `0x…` = ERC-20 contract |
| List | one "address,amount" per line, comma / space separated |
| Import | Excel / CSV, or the template filled in |
| Output | per-row status, retry failures, exportable results |

## Notes & gotchas

- **One at a time**: every transfer needs its own wallet confirmation; for a large
  list with fewer signatures, use [Disperse](./disperse.md).
- **Payer needs native coin for gas**: sending ERC-20 still costs native coin for
  gas — a row fails if the balance is too low.
- **Amount precision**: ERC-20 amounts are scaled by the token's `decimals` — don't
  read a raw Wei value as human-readable.
- **Double-check addresses**: transfers are irreversible; a wrong address means lost
  funds.
- **Native coins differ per chain**: Ethereum/Arbitrum/Base/Optimism = ETH,
  BNB Chain = BNB, Polygon = POL, Avalanche = AVAX, Sepolia = SepoliaETH.

## Related tools

- [Disperse](./disperse.md) — one-to-many distribution in a single tx, fewer signs
- [Multi-key Send](./bulk-send2.md) — import many keys and batch-send concurrently
- [Sweep](./bulk-collect.md) — consolidate assets from many wallets into one
- [Balance Checker](./bulk-query-balance.md) — batch balance lookups
- [Security model](../security.md)

---

> Disclaimer: per-wallet sends are real, irreversible on-chain transactions —
> verify the recipient, asset, and network before running.
