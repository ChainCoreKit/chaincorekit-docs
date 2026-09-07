**English** · [简体中文](../../zh/evm/rpc-check.md) · [← Overview](../index.md)

# RPC Diagnostics · EVM

> Probe RPC endpoints from your current network: can it connect, is it the right chain, how
> far behind is it, and which read capabilities does it support.

## When to use it

- A tool keeps spinning or failing and you want to know whether the endpoint is to blame.
- You have several candidate endpoints and want to pick one that works right now.
- You need `debug_traceTransaction` or historical state and want to check support first.

## Steps

1. Pick the **expected network** — used to compare against the `chainId` the endpoint returns.
2. Paste the **RPC endpoints**, one per line (up to 8).
3. Click **Run probe**. Endpoints are probed **one at a time**: running them concurrently
   only slows each other down and is more likely to trip the remote's rate limiting.

## Output

| Column | Meaning |
| --- | --- |
| Status | Reachable / Browser can't connect / Rate limited / Needs authorization / Bad response |
| chainId | The chain ID the endpoint actually reports; highlighted when it doesn't match |
| Block | `eth_blockNumber`, useful for spotting a lagging node |
| Latency | Median of several samples |
| Read capabilities | `eth_call` and historical (archive) state, as yes / no / unknown |

## Notes & gotchas

These determine how you should read the results:

- **"Can't connect" doesn't mean the node is down.** Browsers collapse CORS, DNS failures,
  network problems and non-existent endpoints into one indistinguishable error — JavaScript
  never sees the difference. So every possible cause is listed rather than one being asserted.
- **Latency is not an endpoint ranking.** It reflects only your network and this sampling
  window. From another region or at another time the ordering may reverse entirely.
- **One successful historical read does not prove full archive access.** That's why the
  probed block number is printed — the conclusion only holds for that block. To confirm
  deeper history, try again with an older block.
- **"Unknown" is not "no".** Rate limiting, an invalid sample and similar conditions all
  make the probe inconclusive, and that's reported as unknown. Treating unknown as "no"
  will make you discard endpoints that actually work.
- **URLs carrying an API key are flagged.** Don't put those in share links or unsanitized
  exports.

## About "Use in bulk tools"

That button writes **only** to the custom RPC shared by Sweep, bulk send by key, and the
balance checker. Other pages currently use the built-in public endpoints and don't expose a
custom RPC yet.

## Related tools

- [Transaction Tracer](./trace-view.md) — needs an endpoint supporting `debug_traceTransaction`
- [Balance Checker](../bulk/bulk-query-balance.md) — can use the custom RPC saved here
- [Security model](../security.md)

---

> Disclaimer: results reflect your network at the moment of probing and are not a
> recommendation or quality rating of any endpoint.
