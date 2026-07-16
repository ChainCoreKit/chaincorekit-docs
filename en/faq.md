**English** · [简体中文](../zh/faq.md) · [← Overview](./index.md)

# FAQ

## Are my private keys uploaded?

No. Mnemonic/key generation, derivation, and signing all happen locally in your
browser — nothing is uploaded, stored, or sent off your device. See the
[security model](./security.md).

## Can I recover a generated key after closing the page?

No. Keys/mnemonics from a session live only in memory and disappear on refresh or
close. Export or write them down before leaving.

## Which tools need a connected wallet?

Read-only tools (unit conversion, calldata decoding, address conversion, balance
checks) need no connection. Write and signing tools (contract writes, transfers,
deployments, sweeps) require a wallet; when disconnected they read "Connect wallet
to continue".

## What's the difference between "same mnemonic" and "independent mnemonics"?

- **Same mnemonic (HD)**: one BIP39 mnemonic derives many addresses via BIP44;
  backing up that single phrase restores all of them.
- **Independent mnemonics**: each wallet gets its own unrelated mnemonic and must
  be backed up separately.

See [Generate Wallet](./evm/generate-wallet.md).

## Why distinguish Wei / Gwei / Ether?

They're units of the same value: 1 Ether = 10⁹ Gwei = 10¹⁸ Wei. Contracts express
amounts in the smallest unit (Wei), gas prices are usually in Gwei, and values are
converted to Ether only for display. See [Unit Converter](./evm/unit-convert.md)
and the [glossary](./glossary.md).

## Which networks are supported?

On the EVM side: Ethereum, Arbitrum, Base, Optimism, BNB Chain, Polygon,
Avalanche, and the Sepolia testnet, among others — plus dedicated Bitcoin, Solana,
and Polkadot tools. Block-explorer links map automatically per network.

## A transaction failed — now what?

Results distinguish success from failure and show the revert reason on failure.
Common causes: insufficient gas or balance, invalid parameters, or a missing
`approve`. Fix and retry.

## Is the documentation or the code public?

**This documentation repository** is openly licensed (CC BY 4.0 + MIT for code
snippets). The **ChainCore Kit application itself is proprietary; its source code
is not published.**

## How do I report issues or contribute?

For documentation issues, open an issue in this repo (see [SECURITY.md](../SECURITY.md)
/ [CONTRIBUTING.md](../CONTRIBUTING.md)). For the application itself, use the in-app
feedback channel.

---

> Disclaimer: nothing here is financial or investment advice. Verify address,
> amount, and network before signing.
