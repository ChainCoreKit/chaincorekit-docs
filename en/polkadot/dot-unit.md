**English** · [简体中文](../../zh/polkadot/dot-unit.md) · [← Overview](../index.md)

# DOT Units

> Convert precisely between Planck and main units like DOT / KSM / PAS, with a
> custom-decimals option. Works fully offline.

## When to use it

- On-chain amounts are quoted in the smallest unit (Planck); you need to read them
  back as human-readable DOT / KSM.
- You have a DOT figure and want the exact Planck value to drop into an extrinsic.
- You're dealing with Kusama, Paseo, or another Substrate chain whose decimals
  differ and need to switch per chain.

## Steps

1. Enter the amount in the **value** box (e.g. `1.5` or `15000000000`).
2. Pick the **chain / decimals**:
   - **Polkadot · DOT** (decimals 10)
   - **Kusama · KSM** (decimals 12)
   - **Paseo · PAS** (decimals 10)
   - **Custom decimals**: choose this and enter the target chain's decimals.
3. Use the toggle to say whether your input is **in the main unit** or **in Planck**.
4. The result panel shows the converted value automatically — no button needed.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Value | amount to convert — decimal (main unit) or integer (Planck) |
| Chain / decimals | DOT (10) / KSM (12) / PAS (10) / custom |
| Custom decimals | the target chain's decimal places (when "custom" is selected) |
| Input mode | `main unit` / `Planck` |
| Output | the matching main-unit and Planck values |

## Notes & gotchas

- **Planck is the smallest unit**: 1 DOT = 10,000,000,000 Planck (10 decimals),
  while KSM uses 12 — don't reuse the same multiplier across chains.
- **Decimals vary by chain**: before switching to a non-default chain, confirm its
  real decimals; a wrong custom value shifts everything by orders of magnitude.
- **Planck must be an integer**: main-unit fractions finer than `decimals` can't be
  represented as whole Planck, so watch for precision truncation.
- **Reading symbol / decimals from chain metadata needs a read-only RPC** — that's
  coming soon; conversion currently uses built-in constants.

## Related tools

- [SS58 Convert](./dot-ss58.md) — SS58 ↔ AccountId32
- [Substrate Hash / Storage Key](./dot-hash-storage.md) — Blake2 / XXHash and storage keys
- [SCALE Codec](./dot-scale.md) — encode / decode by type expression
- [Generate Wallet](./dot-wallet.md) — generate a Substrate wallet locally
- [Security model](../security.md)

---

> Disclaimer: conversions are for reference only — re-check the amount and unit
> before submitting a transaction.
