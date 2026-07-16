**English** · [简体中文](../../zh/bulk/bulk-query-balance.md) · [← Overview](../index.md)

# Balance Checker

> Batch-check native or ERC-20 balances across many addresses — follow wallet or a
> custom RPC, with Multicall support.

## When to use it

- You have a large set of addresses and want each one's native coin or a specific
  token balance in one run.
- Reconcile a list before/after an airdrop, or monitor a group of wallets.
- You want Multicall aggregation to cut RPC calls and speed up the batch.

## Steps

1. Choose the **data source**: **Follow wallet** (use the connected wallet's
   network) or **Custom RPC** (enter an RPC URL; the ChainId is detected
   automatically).
2. Enter the **token**: blank = native coin; a `0x…` ERC-20 contract address =
   query that token's balance (token info is shown).
3. Set parameters: **preset** (Normal / Fast), **concurrency**; enabling
   **Multicall** exposes **batch size** and a **custom Multicall address**.
4. Add addresses: one per line, or comma / space separated, then **Add**. You can
   also use **Sample**, **Import Excel / CSV**, or the **template**.
5. The table supports select / **invert** / **delete selected** / **clear**, and
   **filter** by address.
6. Click **Run** to fetch balances in bulk; failed rows can be **retried**, and
   results **exported**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Data source | follow wallet / custom RPC (ChainId auto-detected) |
| Token | blank = native coin; `0x…` = ERC-20 contract |
| Preset / concurrency | Normal / Fast; number of simultaneous queries |
| Multicall | aggregation toggle, with batch size and custom contract address |
| Address list | one per line, or comma / space separated |
| Output | per-address balance, status, retry failures, exportable results |

## Notes & gotchas

- **Read-only tool**: queries send no transaction, need no signing, and require no
  private keys.
- **Multicall auto-fallback**: when enabled, it detects whether the chain has
  Multicall3 (`eth_getCode`); if not, it falls back to per-address concurrent
  queries.
- **Default Multicall3 shares one address across chains**:
  `0xcA11bde05977b3631167028862bE2a173976CA11`; click "check" to verify a custom
  address first.
- **Don't over-parallelize**: too high a concurrency / batch size may hit RPC rate
  limits — mind the node's capacity on a custom RPC.
- **Amount precision**: ERC-20 balances are scaled by the token's `decimals` — don't
  read a raw Wei value as human-readable.
- **Native coins differ per chain**: Ethereum/Arbitrum/Base/Optimism = ETH,
  BNB Chain = BNB, Polygon = POL, Avalanche = AVAX, Sepolia = SepoliaETH.

## Related tools

- [Per-wallet Send](./bulk-send.md) — send from the connected wallet
- [Disperse](./disperse.md) — one-to-many distribution in a single tx
- [Multi-key Send](./bulk-send2.md) — import many keys and batch-send concurrently
- [Sweep](./bulk-collect.md) — consolidate assets from many wallets into one
- [Security model](../security.md)

---

> Disclaimer: checking is read-only; balances reflect on-chain data from the chosen
> data source.
