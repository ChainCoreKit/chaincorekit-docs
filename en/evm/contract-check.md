**English** · [简体中文](../../zh/evm/contract-check.md) · [← Overview](../index.md)

# Contract Inspector · EVM

> Enter an address to see whether it has code, whether it's a proxy, where the
> implementation lives, and whether it's delegated via EIP-7702. Read-only, no wallet.

## When to use it

- You have a contract address and want to know whether it's a proxy and where the real
  logic lives.
- You're about to call a contract in the ABI tool and aren't sure whether to use the
  proxy's or the implementation's ABI.
- You see an address that has code and want to know whether it's a traditional contract or
  an ordinary account delegated via EIP-7702.

## Steps

1. Pick the **network** and enter the **contract address**.
2. Click **Inspect**. The tool reads the runtime bytecode and probes four proxy slot
   families plus the EIP-7702 delegation marker.

## Output

| Item | Meaning |
| --- | --- |
| Runtime bytecode size | Zero means the address has no code |
| Proxy pattern | Which pattern matched, its target address and slot |
| EIP-1967 admin slot | The **proxy's administrator**, who can upgrade the implementation |
| EIP-7702 delegation | When present, the address is an EOA rather than a contract |

Coverage: EIP-1967 (implementation / beacon / admin), EIP-1822 (UUPS), the OpenZeppelin
legacy slot, and the EIP-7702 delegation marker.

## Notes & gotchas

- **"No known proxy pattern detected" is not "not a proxy".** This is the most important
  line on the page. A contract may keep its implementation in a custom slot — **USDC does
  exactly that: it is a proxy, yet all three EIP-1967 slots read zero** (FiatTokenProxy uses
  its own slot). So the tool only ever says "not detected"; it will never claim "this isn't
  a proxy" or "this can't be upgraded".
- **The admin slot is not the owner.** Admin is the proxy's administrator and can upgrade
  the implementation; the business contract's `owner()` is a separate thing, and the two can
  be entirely different addresses. Reading admin and concluding "this address controls
  everything" is wrong.
- **Having code no longer means "is a contract".** On chains supporting EIP-7702, an
  ordinary account can carry a `0xef0100 ‖ address` delegation. The tool identifies that
  case separately.
- **Only known patterns are probed.** Checking EIP-1967 alone would miss UUPS and the
  OpenZeppelin legacy slot, and a "not detected" that stems from a missing probe is even
  easier to misread — so all four are checked.
- **Source and ABI are not fetched.** That requires a block explorer API and is out of
  scope here.

## Related tools

- [ABI Interaction](./abi.md) — call the contract once you have the implementation address
- [Transaction Tracer](./trace-view.md) — see the full proxy call chain
- [RPC Diagnostics](./rpc-check.md) — check the endpoint first if reads fail

---

> Disclaimer: results reflect on-chain state at the moment of reading and are not an
> assessment of the contract's safety.
