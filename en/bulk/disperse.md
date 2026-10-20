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
  of the total amount. The balance pre-check **now includes the fee** — meaning
  "disperse my entire balance" is caught up front as insufficient funds rather than
  failing in your wallet at signing time. When the fee can't be estimated (a
  rate-limited node, say) the check falls back to comparing the total alone: better to
  let a legitimate dispersal through than to block it on a guess.
- **The zero address is rejected**: a line holding `0x0000…0000` is treated as a
  malformed address, skipped, and written back into the input box. Native coin sent
  there lands on-chain and is **burned permanently**; most ERC-20 implementations
  revert instead — and since a dispersal is **one transaction for every row**, a single
  zero address makes **the whole batch fail and wastes all the gas**.
- **Transaction links follow the chain the transaction is on**: if you switch networks
  in your wallet after dispersing, the hash in the results still links to the block
  explorer for the chain the transaction actually landed on, not the one you switched to.
- **The contract check has four outcomes, each handled differently**:
  - **Contract deployed** — the address holds the canonical Disperse, or a build of
    this page's "Deploy in Remix" source; you can disperse right away.
  - **No contract** — nothing is deployed at this address on the current network,
    so dispersing is disabled (sending to a codeless address loses all funds). Deploy
    one via Remix as prompted and enter it as the custom contract address.
  - **Unrecognized contract** — there is a contract, but not a known Disperse
    implementation. If it has a payable fallback it will keep the funds and no
    recipient gets paid. Check its source on a block explorer, confirm it's the
    Disperse contract you deployed, then tick the confirmation; it only applies to
    this address on this network — switching either requires confirming again.
  - **Check failed** — the RPC request errored, which **doesn't mean the contract is
    missing**. Dispersing pauses; check your connection and click "Check again"
    instead of redeploying.
- **Switching networks while the confirm dialog is open closes it** with "Network
  changed — this run was aborted". The network, contract and allowance shown there
  only hold for the chain it was opened on; start again on the new network.
- **Amount precision**: ERC-20 amounts are scaled by the token's `decimals`.
- **Native coins differ per chain**: Ethereum/Arbitrum/Base/Optimism = ETH,
  BNB Chain = BNB, Polygon = POL, Avalanche = AVAX, Sepolia = SepoliaETH.
- **Tokens like USDT need the allowance reset to 0 first**: they won't change a non-zero allowance straight to another non-zero value. The tool simulates the change first; when a reset is really needed, the button becomes "① Reset approval to 0", and after it confirms you approve the new total. It's one extra signature, but the only way forward. Standard tokens are unaffected.
- **If you deploy your own Disperse contract, use the source shown on the page**: since October 2026 it's v2 — it refunds only the unspent part of what you sent and rejects re-entry from recipient contracts. With the older v1, if your recipients included an untrusted contract, the last one could take your change during its callback. Already-deployed v1 contracts are still recognised, and they're fine when all recipients are ordinary addresses.

## Related tools

- [Per-wallet Send](./bulk-send.md) — sign each transfer, fully self-custodial
- [Multi-key Send](./bulk-send2.md) — import many keys and batch-send concurrently
- [Sweep](./bulk-collect.md) — consolidate assets from many wallets into one
- [Balance Checker](./bulk-query-balance.md) — batch balance lookups
- [Security model](../security.md)

---

> Disclaimer: distribution is a real, irreversible on-chain transaction — verify the
> recipient list, asset, contract, and network before running.
