**English** · [简体中文](../../zh/evm/batch-read.md) · [← Docs home](../index.md)

# Batch Contract Read · EVM

> Query different read-only functions across many contracts at once. All calls are pinned to the same block, and every success and failure is reported per row.

## When to use it

- Pull `symbol` / `decimals` / `totalSupply` from dozens of contracts in one pass for reconciliation.
- Compare several pools or tokens side by side as of the same moment.
- Hit a set of view functions while debugging, instead of clicking through them one at a time.

> How this differs from [Balance Checker](../bulk/bulk-query-balance.md): that tool runs **one function across many addresses**; this one runs **a different function per contract**.

## Steps

1. Pick the **network**.
2. Put one call per line:

   ```
   address  signature->returnTypes  args…
   ```

   For example:

   ```
   0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48 symbol()->string
   0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48 balanceOf(address)->uint256 0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045
   ```

   Fields are separated by whitespace or commas; lines starting with `#` are ignored; 50 calls max.
3. Hit **Run**. Results export to CSV with the block number and network included.

## Input / output notes

| Item | Notes |
| --- | --- |
| Return types | Go after `->`; wrap multiple values in parentheses: `getReserves()->(uint112,uint112,uint32)` |
| Return types are optional | Omit them and you get the raw return data — the tool will **not guess the type** |
| Unparseable lines | Listed with line number and reason — never silently dropped |
| A failed call | Affects only that row; the rest still run, and the failure count shows in the summary |

## Gotchas

- **Every call is pinned to the same block height.** If calls landed on different blocks you would be holding snapshots from different moments, and comparing them would be wrong — especially for balances and prices. The tool reads the block number once up front, uses it for every call, and displays it.
- **No Multicall aggregation.** Aggregating is faster, but it replaces the `msg.sender` the target contract sees with the Multicall contract's address. Any view function that reads `msg.sender` can return a different value under aggregation, and that difference raises no error. So calls are sent individually here.
- **Return types must match the contract.** If you get them wrong the decode fails and you see the raw data — not a plausible-looking wrong value.
- **Read-only.** No transactions, no wallet connection needed.

## Related tools

- [Contract Interaction](./abi.md) — interactive read/write against a single contract
- [ABI Encoder / Decoder](./abi-codec.md) — manual encoding and decoding
- [Balance Checker](../bulk/bulk-query-balance.md) — one function across many addresses

---

> Disclaimer: results reflect on-chain state at the selected block height. Check the block number before exporting.
