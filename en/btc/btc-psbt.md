**English** · [简体中文](../../zh/btc/btc-psbt.md) · [← Overview](../index.md)

# PSBT Decode · BTC

> Parse a PSBT (BIP-174) locally to inspect inputs / outputs / fee and signing
> progress. Decode only — never signs.

## When to use it

- You received a PSBT to sign and want to see exactly which UTXOs it spends, where
  it sends, and the fee before signing.
- You're tracking how many signatures a PSBT has collected in a multisig or
  hardware-wallet flow.
- You want to verify a PSBT matches expectations to avoid mis-signing.

## Steps

1. Choose the network: **Mainnet** or **Testnet**.
2. Paste the PSBT — **Base64** (`cHNidP8…`) or **hex** (`70736274ff…`).
3. The decoded result shows automatically: inputs, outputs, fee, and signing
   progress.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Mainnet / Testnet |
| PSBT | Base64 (`cHNidP8…`) or hex (`70736274ff…`) |
| Output | input list, output list, fee, signing progress |

## Notes & gotchas

- **Decode only, never signs**: this tool never signs or broadcasts the PSBT.
- Pick the right network so address forms parse correctly — mainnet and testnet
  prefixes differ.
- Fee = total inputs − total outputs; a precise rate may be unavailable if fields
  are missing.
- The decode is for verification only — trust your own signing wallet's display as
  the final word.

## Related tools

- [UTXO Lookup](./btc-utxo.md) — view the UTXOs referenced by inputs
- [Address Format Convert](./btc-addr-convert.md) — verify output address forms
- [Generate BTC Wallet](./btc-wallet.md) — generate addresses locally
- [Security model](../security.md)

---

> Disclaimer: the decode is for reference — re-verify in a wallet you trust before
> signing.
