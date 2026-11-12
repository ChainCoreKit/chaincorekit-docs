**English** · [简体中文](../../zh/evm/rpc-check.md) · [← Overview](../index.md)

# RPC Diagnostics · EVM

> Probe any EVM RPC endpoint from your current network: can it connect, which chain is it on,
> how far behind is it, and which read capabilities does it support. Run several rounds to see
> how stable it is.

## When to use it

- A tool keeps spinning or failing and you want to know whether the endpoint is to blame.
- You have several candidate endpoints and want to pick one that works right now.
- You need `debug_traceTransaction` or historical state and want to check support first.
- An endpoint is flaky and you want several rounds to see intermittent failures, rate limiting
  and latency swings.

## Steps

1. Paste the **RPC endpoints**, one per line — only `http://` or `https://` URLs are accepted.
   Below the box you'll see how many endpoints were detected, how many duplicates were folded
   (each is probed once) and how many fall past the limit of 8 (not probed). Lines that aren't
   http(s) URLs are flagged by line number and must be fixed or removed before you can run.
   There's no network to pick: each endpoint reports its own chain ID, so endpoints on
   different chains can be probed together.
2. Choose the number of **probe rounds** (1 / 3 / 5 / 10). Each round probes every endpoint in
   turn, with a 3-second pause between rounds.
3. Click **Run probe**. Endpoints are probed **one at a time**: running them concurrently
   only slows each other down and is more likely to trip the remote's rate limiting.
4. Click **Stop probing** to end early: the endpoint being probed finishes and every result so far is
   kept. Stopping during the pause between rounds ends the run immediately. Afterwards a note
   next to the button says which round it stopped in and how much was completed.

## Output

| Column | Meaning |
| --- | --- |
| Status | Reachable / Browser can't connect / Rate limited / Needs authorization / Bad response; failures explain the cause and what to try next |
| chainId | The chain ID the endpoint actually reports, with the chain name for known chains, e.g. `8453 · Base` |
| Block | `eth_blockNumber`; when several endpoints share a chain, shows how many blocks each trails the highest |
| Latency | Median of several samples |
| Read capabilities | `eth_call` and historical (archive) state, as yes / no / unknown |

### Multi-round summary

With more than one round, a **per-endpoint summary** comes first, one row per endpoint:

| Column | Meaning |
| --- | --- |
| Success / probed | Successful rounds / rounds probed so far — green when all succeed, orange when some fail, red when all fail. When some rounds fail, the endpoint cell shows which round failed last and why |
| chainId | As above |
| Latest block | Block height from the endpoint's last successful round. When several endpoints share a chain, shows how many blocks each trails the highest; different chains are never compared |
| Latency (median) | Median across successful rounds, with the min – max range below; failed rounds are excluded |
| Read capabilities | From the latest successful round; flagged when rounds disagree |

The raw per-round results are collapsed by default — click **Show per-round results** to expand
them and filter by round. A failure cause that repeats for the same endpoint is written out once,
then shown as "Same cause as round N".

On phones and other narrow screens, both tables switch to one card per endpoint so every result
is visible without scrolling sideways.

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
