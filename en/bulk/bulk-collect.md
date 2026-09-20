**English** · [简体中文](../../zh/bulk/bulk-collect.md) · [← Overview](../index.md)

# Sweep

> Consolidate native coins or ERC-20 tokens from many wallets into one
> destination address, in a single run.

## When to use it

- Gather assets scattered across many wallets into one main address after an
  airdrop or testing.
- Empty the balances of a group of test wallets in bulk.
- Sweep under different strategies: send all, a fixed amount, or keep a reserve.

> ⚠️ Source keys are used in local memory for this session only —
> **never uploaded, stored, or sent off your device**. Read the
> [security model](../security.md) first.

## Steps

1. Choose the **data source**:
   - **Follow wallet**: use the connected wallet's current network.
   - **Custom RPC**: enter an RPC URL; the ChainId is detected automatically.
2. Enter the **destination address** (assets are swept here).
3. Enter the **token**: leave blank for the native coin; enter a `0x…` ERC-20
   contract address to sweep that token.
4. Choose the **sweep mode**:
   - **Send all**: send the whole balance after reserving gas.
   - **Fixed amount**: send a set amount from each wallet.
   - **Keep balance**: keep a set amount in each wallet and send the rest.
5. Paste **source private keys** in the bottom box (`0x` + 64 hex, one per line,
   batch paste supported) and click **Import keys**.
6. After import, the table lists each address and balance. You can **refresh
   balances**, select/invert/delete rows, and **filter** by address.
7. Click **Sweep**. In the confirmation dialog, verify the network, destination,
   asset, mode, wallet count, total reserved gas, and estimated total, then run.
   Failed rows can be **retried**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Data source | follow wallet / custom RPC |
| Destination | `0x…`, the sweep target |
| Token | blank = native coin; `0x…` = ERC-20 contract |
| Sweep mode | send all / fixed amount / keep balance |
| Source keys | `0x` + 64 hex, one per line |
| Output | per-row status, estimated total, exportable results |

## Retrying failed rows: the chain is checked first

**"Failed" means two very different things.** Either the transfer never went out
(rejected in the wallet, not enough balance, gas estimation failed), or it **was
broadcast and simply never got a receipt** — common when the network is busy.
Blindly resending the second kind sweeps the same wallet twice: once the first one
lands, the second either carries off the gas that just arrived or burns a fee for
nothing. There is no undo on-chain.

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
  success does not mean the sweep happened — that wallet's balance never moved.
- **Retrying after changing the network, asset or destination is blocked**, with a
  prompt to restore it. A sweep's identity is all three together: a row that failed on
  chain A becomes a brand-new sweep — of a different coin — if resent on chain B, and a
  changed destination simply sends the funds to someone else. Restore and retry as usual.

## Notes & gotchas

- **Gas reserve**: sweeping the native coin reserves gas per wallet, so "send all"
  actually sends "balance − reserved gas".
- **Native vs token**: sweeping an ERC-20 doesn't spend the token on gas, but each
  source wallet still needs native coin for gas — otherwise that row fails.
- **Double-check the destination**: sweeping is irreversible; a wrong address means
  lost funds.
- **Network consistency**: make sure a custom RPC's ChainId is the chain you expect,
  to avoid sending on the wrong network.
- Native/pricing coins differ per chain: Ethereum/Arbitrum/Base/Optimism = ETH,
  BNB Chain = BNB, Polygon = POL, Avalanche = AVAX, Sepolia = SepoliaETH.

## Security

- The key box is masked; click the eye icon to reveal, and operate only in a
  **safe environment**.
- Keys are used for this signing session only, never written to localStorage, and
  cleared from memory on close.
- Before a large run, validate the flow with 1–2 wallets and a small amount.

## Related tools

- [Per-wallet Send](./bulk-send.md) — send from the connected wallet
- [Multi-key Send](./bulk-send2.md) — import many keys and batch-send
- [Balance Checker](./bulk-query-balance.md) — batch balance lookups
- [Disperse](./disperse.md) — one-to-many distribution
- [Security model](../security.md)

---

> Disclaimer: a sweep is a real, irreversible on-chain transfer — verify the
> destination, asset, and network before running.
