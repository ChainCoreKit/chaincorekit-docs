**English** · [简体中文](../../zh/solana/sol-idl.md) · [← Overview](../index.md)

# Program IDL · Solana

> Upload or paste an Anchor IDL and browse its instructions, accounts, types,
> events, and errors — no on-chain IDL required.

## When to use it

- You have an Anchor IDL and want a quick, structured view of its instructions,
  accounts, types, events, and error codes.
- The program has no IDL published on-chain, but you have the JSON file and want to
  read its structure offline.
- You want to review the IDL structure before encoding/decoding instructions.

## Steps

1. In the **Anchor IDL** card:
   - Paste the IDL JSON directly; or click **Choose IDL file** to upload a `.json`;
     or click **Load sample IDL**.
2. Once loaded, the **IDL contents** card lists, structurally: instructions,
   accounts, types, events, and errors.
3. Before loading it shows an empty-state prompt; it fills in on a successful load.

> Fetching an IDL from chain by Program ID needs read-only RPC and is **coming soon**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Anchor IDL | paste IDL JSON, upload a `.json` file, or load the sample |
| Program ID | entry point for on-chain IDL fetch (coming soon) |
| Output | structured list of instructions / accounts / types / events / errors |

## Notes & gotchas

- **Local parsing only**: it parses the JSON you provide — no network calls, no
  check for a matching on-chain program.
- **Match the IDL version**: different program versions have different IDLs; the
  wrong version shows stale instructions / fields.
- **On-chain fetch not yet available**: for now you can only paste or upload an IDL;
  Program ID fetch is coming soon.

## Related tools

- [Instruction Codec](./sol-instruction.md) — encode/decode instruction data with the same IDL
- [PDA / ATA](./sol-address.md) — compute the PDAs / ATAs a program uses
- [Compute / Fee / Rent](./sol-fee-rent.md) — estimate transaction fees
- [Security model](../security.md)

---

> Disclaimer: everything shown comes from the IDL you provide — confirm it matches
> the target program yourself.
