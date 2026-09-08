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

## ERC-165 interface probing

After the check runs, the page also probes which standard interfaces the contract supports (ERC-721, ERC-1155, ERC-2981, …).

Detection follows **the procedure EIP-165 defines for itself**: `supportsInterface(0x01ffc9a7)` must return true **and** `supportsInterface(0xffffffff)` must return false. The second step is not optional — a contract that returns true for any input would pass the first step alone and be reported as supporting every interface, making every subsequent probe a lie. Such contracts are reported here as not implementing ERC-165.

The three outcomes mean different things:

| Outcome | Meaning |
| --- | --- |
| Implements ERC-165 | Passed both steps; the interfaces listed below are trustworthy |
| Does not implement ERC-165 | Confirmed non-conforming. **This says nothing about the contract being sound** — it simply has no self-describing interface mechanism |
| Could not probe | The call failed or returned a non-standard value. **It does not mean no interfaces are supported**, only that this route can't tell |

The known-interface list is limited, so "implements ERC-165 but matched nothing" is a normal result too.

## Interface ID calculator

Below the check is a purely local calculator: enter function signatures (one per line) and get the interface ID. No address, no RPC.

Two rules that are easy to get wrong:

- **It's the XOR of every function selector**, not a hash of the concatenation. Get it wrong and you still get a well-formed `bytes4` — it just returns `false` from `supportsInterface`, with nothing to hint that your own math was off.
- **Functions only, never events, and inherited functions are not included.** The `ERC721Metadata` ID comes from just the three functions it adds — `name()` / `symbol()` / `tokenURI(uint256)` — not the nine it inherits from `ERC721`.

A malformed signature is reported with its **line number**. A result of `0x00000000` prompts you to check for duplicates, since XOR cancels repeated entries out.

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
