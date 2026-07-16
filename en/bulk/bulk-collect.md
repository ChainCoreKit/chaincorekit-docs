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
