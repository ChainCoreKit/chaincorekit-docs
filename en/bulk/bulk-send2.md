**English** · [简体中文](../../zh/bulk/bulk-send2.md) · [← Overview](../index.md)

# Multi-key Send

> Import private-key wallets and batch-send native coins or ERC-20 in concurrent
> batches, with failure retries and custom gas.

## When to use it

- You hold a set of private-key wallets and need to batch-pay many addresses from
  one of them.
- The list is large and you want concurrent batches for throughput with automatic
  retries.
- You need custom Gas Limit, batch size, and max retries.

> ⚠️ Keys and mnemonics are used in local memory for this session only —
> **never uploaded, stored, or sent off your device**. Read the
> [security model](../security.md) first.

## Steps

1. Choose the **data source**: **Follow wallet** (use the connected wallet's
   network) or **Custom RPC** (enter an RPC URL; the ChainId is detected
   automatically).
2. Paste **private keys** in the key box (`0x` + 64 hex, one per line, batch paste
   supported) and click **Import keys**; use the eye icon to reveal / hide.
3. After import, pick which wallet pays from the **Sender wallet** dropdown.
4. Enter the **token**: blank = native coin; a `0x…` ERC-20 contract address =
   send that token.
5. Set parameters: **batch size** (concurrent sends), **max retries**, and
   **Gas Limit** (native ≈ 21k).
6. Add the recipient list: one "address,amount" per line (comma or space
   separated), then **Add**. You can also use **Sample**, **Import Excel / CSV**,
   or the **template**.
7. Click **Send**. In the confirmation dialog, verify the send network, sender
   wallet, asset, recipient count, batch / retries, Gas Limit, estimated gas, and
   total, then run. Failed rows can be **retried**, and results **exported**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Data source | follow wallet / custom RPC (ChainId auto-detected) |
| Private keys | `0x` + 64 hex, one per line |
| Sender wallet | one of the imported keys, as the payer |
| Token | blank = native coin; `0x…` = ERC-20 contract |
| Batch size / max retries / Gas Limit | concurrency / retry cap / per-tx gas cap |
| List | one "address,amount" per line, comma / space separated |
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
- **Retrying after changing the network, sending wallet or asset is blocked**, with a
  prompt to restore it. A transfer's identity is all three together: a row that failed
  on chain A becomes a brand-new payment — in a different coin — if resent on chain B,
  and a different sending wallet quietly pays from another address. Restore and retry.

## Notes & gotchas

- **Sender needs native coin for gas**: sending ERC-20 still costs native coin for
  gas — a row fails if the balance is too low.
- **Match Gas Limit to the op**: native ≈ 21k, ERC-20 needs more; too low a Gas
  Limit makes the tx fail.
- **Don't over-parallelize**: too large a batch size may hit RPC rate limits — mind
  the node's capacity, especially on a custom RPC.
- **Amount precision**: ERC-20 amounts are scaled by the token's `decimals`.
- **Double-check addresses**: transfers are irreversible; a wrong address means lost
  funds.
- **Native coins differ per chain**: Ethereum/Arbitrum/Base/Optimism = ETH,
  BNB Chain = BNB, Polygon = POL, Avalanche = AVAX, Sepolia = SepoliaETH.

## Security

- The key box is masked; click the eye icon to reveal, and operate only in a
  **safe environment**.
- Keys are used for this signing session only, never written to localStorage, and
  cleared from memory on close.
- Before a large run, validate the flow with 1–2 addresses and a small amount.

## Related tools

- [Per-wallet Send](./bulk-send.md) — send from the connected wallet
- [Disperse](./disperse.md) — one-to-many distribution in a single tx
- [Sweep](./bulk-collect.md) — consolidate assets from many wallets into one
- [Balance Checker](./bulk-query-balance.md) — batch balance lookups
- [Security model](../security.md)

---

> Disclaimer: batch sends are real, irreversible on-chain transactions — verify the
> recipient, asset, and network before running.
