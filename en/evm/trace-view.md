**English** · [简体中文](../../zh/evm/trace-view.md) · [← Overview](../index.md)

# Transaction Tracer

> Parse an EVM transaction's internal call stack — overview, CallTraces, fund flow,
> asset changes, event logs, and gas analysis — with address / function aliases.

## When to use it

- You want to see exactly which contracts a transaction called and what happened.
- A transaction reverted and you need to find the failing call and its reason.
- You need the fund flow, net asset changes, emitted events, and per-call gas share.

## Steps

1. Pick the transaction's **network** (Ethereum / Arbitrum One / Base / Optimism /
   BNB Chain / Polygon / Avalanche / Sepolia).
2. Paste the **transaction hash** and click **Analyze** — or try **Success example /
   Failure example**.
3. (Optional) Expand **Advanced · aliases** to render `0x` addresses / selectors as
   readable names (e.g. `WETH.deposit()`). Use **Fill example**, or add them under
   **address** / **function** mappings.
4. Review the results: **Overview**, **CallTraces** (collapse all), **Fund flow**,
   **Asset changes**, **Event logs**, **Gas analysis**; open it in the block
   explorer from the overview.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | drives the alias library and explorer link — unrelated to your wallet |
| Transaction hash | `0x` + 64 hex |
| Aliases | address / function → readable name; display only, not the analysis |
| Overview | basic info and a revert notice |
| CallTraces | internal call tree; reverted calls highlighted red with the reason |
| Fund flow / Asset changes | fund-flow graph + net per-address balance |
| Event logs / Gas analysis | emitted events and per-call gas share |

## Notes & gotchas

- **Network only affects the alias library and explorer link** — it's not your
  wallet's connected network. Don't pick the wrong chain.
- **Aliases are display-only** — swapping `0x` codes for readable names doesn't
  change the analysis; hover to see the raw `0x`.
- **Reverts are highlighted red** with a reason — walk the tree to find the failure.
- **Dynamic / complex types** in the trace may show as raw encoding; combine aliases
  and the Calldata tool to dig in.

## Related tools

- [Calldata Codec](./calldata.md) — decode Input data from the trace
- [Selector Lookup](./query-selector.md) — 4-byte selector ↔ signature
- [Event TopicID](./topic-id.md) — event signature ↔ TopicID
- [ABI Console](./abi.md) — call contracts visually
- [Security model](../security.md)

---

> Disclaimer: analysis is for reference — the block explorer and on-chain data are
> authoritative.
