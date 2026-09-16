**English** · [简体中文](../../zh/evm/token-inspector.md) · [← Docs home](../index.md)

# Token Inspector

> Read the name / symbol / decimals / total supply an ERC-20 contract reports about itself, and flag the fields that fail to decode or fall outside the spec.

## When to use it

- You have an unfamiliar token address and want to see what it actually is **before** approving or transferring.
- You have a raw uint256 balance and need to know what to divide it by.
- You suspect a token is impersonating a well-known one (the name looks identical but the contract isn't).
- You want to confirm whether an address holds a contract **on this particular chain**.

## Steps

1. Pick a **network**. The same address doesn't necessarily hold a contract on every chain — the wrong network shows "no contract code".
2. (Optional) Enter a **custom RPC**. Public nodes rate-limit aggressively; use your own endpoint for repeated lookups.
3. Paste the **contract address** and click **Inspect**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Which chain to read from |
| Custom RPC (optional) | Blank uses a public node |
| Contract address | `0x` + 40 hex characters, EIP-55 checked as you type |
| Name / Symbol | The contract's `name()` / `symbol()` |
| Decimals | The contract's `decimals()` — the divisor for every amount |
| Total supply | Shown both converted and as the **raw base-unit value** |
| owner() | Displayed when the method exists; means the contract has a privileged account |
| Code size | Length of the contract bytecode |

## Why these fields need checking

**Token metadata comes from the contract itself, so none of it is trustworthy by default.** A contract can return anything:

- **Decimals out of range**: ERC-20 defines `decimals` as `uint8`, but a contract may return any
  number. When that happens this page **does not show a converted figure** — a number derived from
  the wrong precision looks perfectly normal while being off by orders of magnitude, which is more
  dangerous than showing nothing. Rely on the raw base-unit value.
- **Invisible characters in the name**: zero-width characters and bidirectional overrides let two
  visually identical names belong to different contracts — a common way to impersonate a known
  token. These are flagged explicitly.
- **bytes32-style names**: MKR, SAI and other early tokens declare `name` as `bytes32` rather than
  `string`. That's a historical quirk, not a risk, so it is shown as a note rather than a warning.
- **Missing methods**: plenty of tokens have no `owner()`, and some have no `decimals()` at all.
  That isn't a lookup failure — it is reported honestly as "the contract has no such method".

## Notes & gotchas

- **This page does not score safety.** The same field means opposite things in different projects:
  an owner is necessary for an upgradeable stablecoin and a risk for a token claiming
  decentralisation. The tool reports what the contract says; judge it alongside the project context.
- **An NFT's totalSupply is a different unit**: it counts items rather than value, and NFTs have no
  decimals. ERC-721 / ERC-1155 interfaces are detected and called out.
- **No contract code has three possible causes**: a regular wallet address, a contract that isn't
  deployed yet, or the wrong network. The third is the one most often mistaken for a typo.
- **Name and symbol are not identity.** Anyone can deploy a contract calling itself `USDC`.
  The only identity is the **contract address** — check it against the project's official channels.

## Related tools

- [Approvals](./approvals.md) — review and revoke existing token allowances
- [Unit Converter](./unit-convert.md) — Wei / Gwei / Ether conversion
- [Contract Check](./contract-check.md) — bytecode and basic contract info
- [Security model](../security.md)
