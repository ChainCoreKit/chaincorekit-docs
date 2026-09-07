**English** · [简体中文](../../zh/solana/sol-token-inspector.md) · [← Docs home](../index.md)

# Token Inspector · Solana

> Read a mint account: supply, decimals, mint and freeze authority, and Token-2022 extension fields.

## When to use it

- You have a token address and want to know whether **more can still be minted** and whether **holders can be frozen**.
- You hit a Token-2022 token and want to see which extensions it carries (transfer fee, permanent delegate, transfer hook, …).
- You need exact supply and decimals for reconciliation, not a rounded figure from some frontend.

## Steps

1. Pick the network (Mainnet Beta / Devnet / Testnet). The public mainnet endpoint is rate-limited — put your own endpoint in "Custom RPC" for frequent queries.
2. Enter the **mint address** (base58).
3. Hit **Inspect**.

## What you get

| Field | Meaning |
| --- | --- |
| Supply | Scaled by decimals, with the raw base-unit amount alongside — the raw value is the on-chain fact |
| Decimals | decimals |
| Mint authority | An address = it can still mint; **Revoked (None) = no more tokens can ever be minted** |
| Freeze authority | An address = it can freeze any holder's account; revoked = it cannot |
| Extensions | Token-2022 only. Recognized extensions are decoded into fields; unrecognized ones are shown as raw bytes |

## Gotchas

- **"Revoked" and "couldn't read it" are different answers.** A `None` authority is a definite, positive conclusion (no more minting / no freezing), and the page states it in green rather than leaving a blank for you to interpret.
- **Don't paste a token account (ATA) as the mint.** Both are owned by a Token Program, but an ATA holds one owner's balance. Decoding an ATA with the mint layout reads its first 32 bytes — the mint address — as the "mint authority", a wrong value that looks perfectly legitimate. This tool classifies the account first and tells you when you've pasted an ATA or a multisig.
- **No safety score.** The same field means opposite things per project: a retained mint authority is required for a stablecoin and a red flag for a token claiming fixed supply. The tool reports the facts and leaves the judgement to you.
- **Unrecognized extensions are labelled as such.** Token-2022 keeps adding extension types; anything this tool doesn't know is marked unrecognized and shown as raw bytes, never mapped onto a similar-looking known extension. **Unrecognized does not mean problematic.**

## Related tools

- [Address / PDA / ATA](./sol-address.md) — derive an ATA from mint + owner
- [Program IDL](./sol-idl.md) — browse an Anchor IDL
- [Compute / Fee / Rent](./sol-fee-rent.md) — fee and rent estimates

---

> Disclaimer: this page reports account fields only. It is not investment or security advice.
