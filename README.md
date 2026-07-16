<div align="center">

# ChainCore Kit — Documentation

**A local-first, multi-chain toolkit for Web3 developers.**
Generate wallets, decode calldata, call contracts, and run batch operations — with keys that never leave your machine.

English · [简体中文](./README.zh-CN.md)

</div>

---

> [!IMPORTANT]
> This repository contains **documentation only**. The ChainCore Kit application itself is proprietary and not published here. Nothing in this repo grants any license to the application's source code. See [LICENSE](./LICENSE).

## What is ChainCore Kit?

ChainCore Kit is a browser-based developer toolkit spanning **EVM, Bitcoin, NFT, Solana, and Polkadot** ecosystems. Sensitive operations — mnemonic and private-key generation, wallet derivation, transaction signing — run entirely in your browser. **Keys and mnemonics are never uploaded, stored, or sent off your device.**

These docs explain what each tool does, how to use it, and the Web3 concepts behind it.

## Documentation index

Full index: [English](./en/index.md) · [中文](./zh/index.md)

| Category | Tools |
| --- | --- |
| **EVM** | Faucets · Generate Wallet · Vanity Address · ABI Console · Selector Lookup · Unit Converter · Transaction Tracer · Address & ENS · Event TopicID · Hash Tools · Calldata Codec · Token Issuance |
| **Bitcoin** | Generate Wallet · Address Format Convert · Balance Checker · UTXO Lookup · PSBT Decode |
| **NFT** | Preview · Issuance |
| **Solana** | Generate Wallet · PDA / ATA · Instruction Codec · Program IDL · Compute / Fee / Rent |
| **Polkadot** | Generate Wallet · SS58 Convert · DOT Units · Hash / Storage Key · SCALE Codec |
| **Batch** | Disperse · Per-wallet Send · Multi-key Send · Sweep · Balance Checker |

## Quick links

- Getting started: [en/index.md](./en/index.md)
- Security model: [en/security.md](./en/security.md)
- FAQ: [en/faq.md](./en/faq.md)
- Glossary: [en/glossary.md](./en/glossary.md)

## Contributing

Documentation fixes and translations are welcome. Please read [CONTRIBUTING.md](./CONTRIBUTING.md) and our [Code of Conduct](./CODE_OF_CONDUCT.md) first.

## Security disclosure

Found a security issue in the docs (e.g. dangerous or misleading guidance)? See [SECURITY.md](./SECURITY.md). For issues in the application, use the in-app feedback channel.

## Disclaimer

ChainCore Kit and this documentation are provided **"as is", without warranty of any kind**. You are solely responsible for safeguarding your private keys and mnemonics, and for any transactions you sign and broadcast. Nothing here is financial, legal, or investment advice. Always verify addresses, amounts, and networks before signing. **Losses from lost keys or mistaken transactions are irreversible.**

## License

Prose and images are licensed under [CC BY 4.0](./LICENSE). Code snippets embedded in the docs are additionally available under the MIT License. This license covers the documentation only, **not** the ChainCore Kit application.
