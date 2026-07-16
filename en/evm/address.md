**English** · [简体中文](../../zh/evm/address.md) · [← Overview](../index.md)

# Address & ENS

> Generate EIP-55 checksummed addresses locally (keccak-256) and resolve ENS names
> both ways.

## When to use it

- You have a lowercase address and want the EIP-55 checksummed (mixed-case) form.
- You want to verify an address's checksum and format.
- You want to resolve an ENS name to an address, or an address back to a name.

## Steps

### Address format conversion

1. Paste a `0x` + 40 hex address (sample: vitalik.eth = `0xd8dA…6045`).
2. It outputs the **EIP-55 checksum** and **all-lowercase** forms live — click copy.

### ENS smart resolution

1. Enter an **ENS name or address**; the tool detects the type automatically.
2. A `.eth` name → forward-resolves to an address; an address → reverse-resolves to a
   name. Results are copyable.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Address | `0x` + 40 hex, validated live |
| EIP-55 checksum | canonical mixed-case address via keccak-256 |
| Lowercase | the all-lowercase form |
| ENS input | `.eth` name or `0x` address (auto-detected) |
| Result | name → address (forward) / address → name (reverse) |

## Notes & gotchas

- **EIP-55 encodes the checksum in letter case** — changing any letter's case breaks
  validation, so don't alter case when copying.
- **Checksum is computed locally with keccak-256** — no network, no upload.
- **ENS resolution uses a local dictionary** — only sample names (e.g. `vitalik.eth`,
  `nick.eth`); it does not reflect live on-chain resolution.
- Addresses are hex (0-9, a-f); invalid characters error immediately.

## Related tools

- [Vanity Address](./vanity.md) — addresses with a chosen prefix/suffix
- [Hash Tools](./hash-tool.md) — keccak-256 and other hashes / encodings
- [Generate Wallet](./generate-wallet.md) — bulk-generate / import EVM wallets
- [Security model](../security.md)

---

> Disclaimer: ENS resolution here uses a local dictionary — for live results consult
> a block explorer / the ENS app.
