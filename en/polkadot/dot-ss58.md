**English** · [简体中文](../../zh/polkadot/dot-ss58.md) · [← Overview](../index.md)

# SS58 Convert

> SS58 address ↔ AccountId32 — re-encode and validate across network prefixes. The
> same AccountId32 under a different prefix is just a different textual form.

## When to use it

- You have a Polkadot address and want its Kusama or generic-Substrate rendering.
- You have an AccountId32 / public key (`0x` + 64 hex) and need the readable SS58
  address back.
- You want to check whether an SS58 address is valid (checksum correct).

> ⚠️ Changing the prefix only changes the address's textual form; the underlying
> AccountId32 is unchanged — **this does not mean funds can move across chains
> directly**.

## Steps

1. Paste an **SS58 address** (e.g. `5Grwva…`) or an **AccountId32 / public key**
   (`0x` + 64 hex) into the input.
2. Choose the **target SS58 prefix**:
   - **Polkadot (0)**
   - **Kusama (2)**
   - **Generic Substrate (42)**
   - **Custom**: choose this and enter a prefix integer (0–16383).
3. The result panel shows the SS58 address under the target prefix plus the
   underlying AccountId32.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Input | SS58 address, or AccountId32 / public key (`0x` + 64 hex) |
| Target SS58 prefix | Polkadot (0) / Kusama (2) / Generic Substrate (42) / custom |
| Custom prefix | prefix integer in range 0–16383 |
| Output | SS58 address under the target prefix and the underlying AccountId32 |

## Notes & gotchas

- **A prefix ≠ a different account**: Polkadot, Kusama, and Substrate addresses share
  one AccountId32; only the prefix makes the text differ.
- **Re-prefixing isn't bridging**: rendering an address with the Kusama prefix does
  not let Polkadot assets move to Kusama — cross-chain needs a bridge or XCM.
- **SS58 carries a checksum**: a single mistyped character usually fails validation;
  the tool validates before converting.
- **Prefix range 0–16383**: use an integer in that range for custom prefixes —
  Polkadot=0, Kusama=2, and generic Substrate=42 are the common ones.

## Related tools

- [Generate Wallet](./dot-wallet.md) — generate a Substrate wallet locally
- [Substrate Hash / Storage Key](./dot-hash-storage.md) — derive a storage key from an AccountId
- [DOT Units](./dot-unit.md) — Planck ↔ main unit
- [SCALE Codec](./dot-scale.md) — encode / decode by type expression
- [Security model](../security.md)

---

> Disclaimer: converting an address only changes its textual form — confirm the
> target chain and address before sending funds.
