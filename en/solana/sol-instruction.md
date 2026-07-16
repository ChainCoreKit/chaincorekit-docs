**English** · [简体中文](../../zh/solana/sol-instruction.md) · [← Overview](../index.md)

# Instruction Codec · Solana

> Encode / decode instruction data from an Anchor IDL (discriminator + Borsh args).

## When to use it

- You want to build an Anchor instruction's data by hand and check that the args
  serialize correctly.
- You have a hex / base58 blob of instruction data and want to know which
  instruction it maps to and what its args are.
- You're debugging a transaction and need to verify the discriminator and Borsh
  encoding.

## Steps

1. Paste an IDL JSON into the **Anchor IDL** card, or click **Load sample IDL**.
2. In the **Codec** card pick a mode:

   ### Encode
   - Pick an instruction from the **Instruction** dropdown.
   - Fill in each **argument** (Borsh type) and the relevant **accounts** as prompted.
   - Click **Encode to instruction data**; the result shows the encoded bytes.

   ### Decode
   - Paste `0x…` hex or base58 into the **Instruction Data** box.
   - Click **Decode** to match the discriminator against the IDL and recover the args.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Anchor IDL | Anchor IDL JSON (paste or load sample) |
| Mode | `Encode` / `Decode` |
| Instruction | picked from the IDL's instruction list in encode mode |
| Arguments | filled per the Borsh types the instruction defines |
| Instruction Data | decode-mode input, `0x…` hex or base58 |
| Output | encoded instruction data; or the decoded instruction name and args |

## Notes & gotchas

- **Discriminator prefix**: Anchor instruction data begins with an 8-byte
  discriminator, followed by the Borsh args; decoding relies on matching the IDL
  definition.
- **IDL must match the program**: a wrong-version IDL means the discriminator won't
  match or args come out misaligned.
- **hex or base58**: decode input is read as hex when it starts with `0x`, otherwise
  as base58 — don't mix them.
- **Complex types**: nested structs / enums serialize per the IDL definition; enter
  args in types that match the definition.

## Related tools

- [Program IDL](./sol-idl.md) — browse the IDL structurally before coding
- [PDA / ATA](./sol-address.md) — compute the PDAs / ATAs an instruction uses
- [Compute / Fee / Rent](./sol-fee-rent.md) — estimate transaction fees
- [Security model](../security.md)

---

> Disclaimer: results depend on whether the IDL you provide matches the target
> program — verify it yourself.
