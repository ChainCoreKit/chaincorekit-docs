**English** · [简体中文](../../zh/evm/vanity.md) · [← Overview](../index.md)

# Vanity Address · EVM

> Brute-force an EVM address with a chosen prefix/suffix locally in your browser —
> keys never leave your device.

## When to use it

- You want a memorable, recognizable address (e.g. starting `dead`, ending `beef`).
- You need an address with a specific marker for branding / a contract.
- You want to generate it locally without handing keys to any online service.

## Steps

1. Enter the hex characters you want in **Prefix** (after `0x`) and/or **Suffix**
   (end of the address) — either one is enough.
2. (Optional) Check **Case-sensitive (EIP-55 checksum)**: on = exact case match
   (harder); off = ignore case (faster hits).
3. The UI shows a difficulty estimate for your rule. Click **Start** to begin the
   local search.
4. Watch progress and speed in the **Progress / results** card; on a hit it shows
   the address and its private key. Click **Stop** anytime.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Prefix | leading chars after `0x`, hex (0-9 a-f), optional |
| Suffix | trailing chars of the address, hex, optional |
| Case-sensitive | on: exact EIP-55 case; off: ignore case |
| Difficulty | estimated effort for the rule |
| Output | matched address + private key, plus search progress / rate |

## Notes & gotchas

- **Difficulty grows exponentially** — each extra prefix/suffix char multiplies
  expected tries by ~16; case-sensitivity doubles it per letter position. Long
  patterns can take a very long time.
- **Hex only** — addresses use 0-9 and a-f; `g`, `z`, etc. can't be targeted.
- **Fully local** — addresses are generated in the browser, no network solve; speed
  depends on your machine.
- **Not persisted** — the key shows once; leaving/refreshing loses it. Copy or write
  it down immediately on a hit.

## Security

- **Keys are generated 100% locally and never leave your device** — no upload, no
  storage.
- Review and save a matched key only in a **safe environment**; anyone with the key
  fully controls the address.
- Sensitive data is never written to localStorage and is cleared from memory on
  close.

## Related tools

- [Generate Wallet](./generate-wallet.md) — bulk-generate / import EVM wallets
- [Address & ENS](./address.md) — checksum, EIP-55, ENS resolution
- [Faucets](./faucet.md) — get test coins for a new address
- [Security model](../security.md)

---

> Disclaimer: lost keys cannot be recovered — always back up offline. This tool
> assumes no liability for asset loss.
