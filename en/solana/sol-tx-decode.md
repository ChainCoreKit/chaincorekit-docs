**English** · [简体中文](../../zh/solana/sol-tx-decode.md) · [← Docs home](../index.md)

# Transaction Decoder · Solana

> Paste a serialized transaction and decode its version, signatures, account roles, instructions and lookup table references — locally.

## When to use it

- A wallet is asking you to sign something and you want to see which accounts it touches and which programs it calls first.
- You're debugging a transaction you built and need to check account ordering and the `signer` / `writable` flags.
- You have a base64 blob and want to know whether it's legacy or v0, and which lookup tables it references.

## Steps

1. Paste the transaction. **base64**, **base58** and **0x hex** all work.
2. Results appear as you type — **decoded entirely in your browser, never sent to a server**.
3. If it's a v0 transaction referencing address lookup tables, the page tells you how many accounts are still unresolved; pick a network and hit "Fetch lookup tables" to fill them in.

## What you get

| Section | Contents |
| --- | --- |
| Overview | Version (Legacy / v0), signatures, message header, `recentBlockhash` |
| Accounts | Public key, role (signer / writable / readonly), source (in message / lookup table) |
| Instructions | Program address and known program name, account indexes, raw data |
| Address lookup tables | Table address and the writable / readonly indexes it supplies |

## Gotchas

- **A v0 transaction is not fully decodable without fetching its lookup tables.** The message stores only the table address and a set of indexes; the actual account keys live in that on-chain table. Looking only at the static accounts leaves you believing you've seen every participant — when the account that actually matters may be precisely the one in the table. So when accounts are unresolved the page says so prominently rather than leaving a blank for you to interpret.
- **Account ordering is defined by the protocol**: static accounts → writable entries from each table → readonly entries from each table. Instructions reference accounts by **index**, so a wrong order points at a different account. Re-check the indexes after fetching the tables.
- **All-zero signatures are placeholders, not signatures.** They show up when an unsigned message is pasted as a transaction, and the page labels them "Placeholder (all zeros — not signed yet)".
- **Instruction arguments are never guessed.** Common SPL Token instructions are named; every other program needs its IDL to decode arguments, so anything unrecognized is shown as raw bytes. To decode Anchor program instructions, pair this with [Instruction Codec](./sol-instruction.md) and [Program IDL](./sol-idl.md).

## Related tools

- [Instruction Codec](./sol-instruction.md) — encode / decode a single instruction's data
- [Program IDL](./sol-idl.md) — browse an Anchor IDL
- [Token Inspector](./sol-token-inspector.md) — mint supply, authorities and extensions

---

> Disclaimer: decoding reflects the transaction data itself. A successful decode does not mean the transaction is safe for you to sign.
