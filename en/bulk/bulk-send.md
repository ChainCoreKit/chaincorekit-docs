**English** · [简体中文](../../zh/bulk/bulk-send.md) · [← Overview](../index.md)

# Bulk Send (Wallet)

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
   failed rows can be **retried** — retrying checks the chain first rather than
   resending blindly (see the section below) — and results can be **exported**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Send network | follows the connected wallet's network |
| Token | blank = native coin; `0x…` = ERC-20 contract |
| List | one "address,amount" per line, comma / space separated |
| Import | Excel / CSV, or the template filled in |
| Output | per-row status, retry failures, exportable results |

## Retrying failed rows: the chain is checked first

**"Failed" means two very different things.** Either the transfer never went out
(rejected in the wallet, not enough balance, gas estimation failed), or it **was
broadcast and simply never got a receipt** — common when the network is busy.
Blindly resending the second kind pays the same recipient twice, and there is no
undo on-chain.

So retrying first **asks the chain about every row** before deciding. You will see:

- **A "triaging 3/12" progress line** — these are sequential lookups, so a long list
  takes a moment; a stop button sits next to it.
- **Some rows are deliberately not resent**:
  - already confirmed on-chain → the row is corrected back to success, nothing is sent;
  - still in flight (the node has it, not yet mined) → skipped; check back shortly;
  - dropped by the node (usually gas priced too low) → unlocked and the hash cleared,
    so **clicking retry once more** actually resends it;
  - status unknown (node throttling / network error) → no verdict, no resend; try a
    different endpoint later.

Two more cases are held back:

- **A transaction you cancelled or replaced in the wallet counts as failed.** The
  "cancel" your wallet sends is itself a transaction that succeeds on-chain, so its
  success does not mean the transfer happened — the money never moved.
- **Retrying after switching networks is blocked**, with a prompt to switch back. A
  transaction's identity includes its chain: a row that failed on chain A becomes a
  brand-new payment — in a different coin — if resent on chain B. Switch back and
  retry as usual.

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
