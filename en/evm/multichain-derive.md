**English** · [简体中文](../../zh/evm/multichain-derive.md) · [← Overview](../index.md)

# Multi-chain Derivation · Cross-ecosystem

> Take one BIP39 mnemonic and see what it derives to across EVM, Bitcoin, Solana, Aptos,
> Sui and TON. All computed locally.

## When to use it

- You want to confirm which address a mnemonic corresponds to on another chain.
- Addresses don't match after switching wallets and you suspect a derivation-path difference.
- You want to understand why the same mnemonic yields a completely different address on TON.

## Steps

1. Paste a mnemonic (or click "Generate one"). The input is masked by default.
2. (Optional) Enter a BIP39 passphrase and adjust the address index.
3. The table lists each ecosystem's **derivation path** and address.

## The rules do not carry across ecosystems

That's the reason this page exists. The same mnemonic is handled quite differently:

| Ecosystem | Path / rule | Watch out for |
| --- | --- | --- |
| EVM | `m/44'/60'/0'/0/i` | Standard BIP32/44 |
| Bitcoin | `m/84'/0'/0'/0/i` (Native SegWit) | The prefix changes with address type |
| Solana | `m/44'/501'/i'/0'` | ed25519 — **hardened derivation only** |
| Aptos | `m/44'/637'/i'/0'/0'` | Address = `sha3_256(pubkey ‖ 0x00)`; scheme byte goes **after** |
| Sui | `m/44'/784'/i'/0'/0'` | Address = `blake2b256(0x00 ‖ pubkey)`; scheme byte goes **before** |
| TON | **Not BIP39** | See below |

- **ed25519 chains permit hardened derivation only.** Solana, Aptos and Sui are all ed25519,
  and SLIP-0010 rules out non-hardened derivation. Plain BIP32 yields the wrong key.
- **Aptos and Sui put the scheme byte on opposite sides** — one after the public key, one
  before. Swap them and you get a perfectly well-formed address that simply doesn't exist.
- **TON does not use BIP39 at all.** It runs PBKDF2 (100 000 rounds) with the salt
  `TON default seed` rather than a BIP39 seed. The trap is that **TON happens to use the same
  2048-word list**, so generic BIP39 tools accept a TON mnemonic, compute a completely wrong
  private key, and **raise no error whatsoever**. The reverse holds too: a valid BIP39
  mnemonic is usually not a valid TON mnemonic. This tool reports both validations separately.

## About TON addresses

This tool shows the **TON public key only, not an address**. A TON address is
`workchain:hash(StateInit)`, and StateInit contains the **wallet contract code** — the same
key yields different addresses under v3R2 / v4R2 / v5. Inventing one address would be
misleading.

## Notes & gotchas

- When an address doesn't match, **compare the paths first** before doubting the mnemonic —
  it's almost always a path convention difference (Solana under Phantom and Ledger, for example).
- A passphrase changes the result on every chain **except TON**, which has its own separate
  password mechanism.
- Mnemonics and private keys stay in browser memory only: never uploaded, stored, or written
  to localStorage.

## Related tools

- [Generate EVM Wallet](./generate-wallet.md)
- [Generate BTC Wallet](../btc/btc-wallet.md)
- [Generate Solana Wallet](../solana/sol-wallet.md)
- [Security model](../security.md)

---

> Disclaimer: derivation is computed locally; verify with a small amount before importing into
> a live wallet.
