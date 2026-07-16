**English** · [简体中文](../zh/glossary.md) · [← Overview](./index.md)

# Glossary

Grouped by topic. Terms stay in their standard form; explanations are in English.

## General / EVM

- **ABI** (Application Binary Interface): a contract's interface description
  (functions, events, parameter types) used to encode calls and decode returns.
- **Calldata**: the hex content of a transaction's `data` field = 4-byte function
  selector + ABI-encoded arguments.
- **Selector**: the first 4 bytes of the keccak-256 hash of a function signature,
  e.g. `transfer(address,uint256)` → `0xa9059cbb`.
- **TopicID / Event Topic**: the keccak-256 hash (32 bytes) of an event signature,
  used for log filtering.
- **keccak-256**: the hash used across Ethereum — function selectors, event
  TopicIDs, EIP-55 checksums.
- **EIP-55**: mixed-case address checksum that catches address typos.
- **ENS**: Ethereum Name Service — resolves names like `vitalik.eth` to addresses.
- **Wei / Gwei / Ether**: units of ETH. 1 Ether = 10⁹ Gwei = 10¹⁸ Wei; gas prices
  are usually in Gwei.
- **Gas**: the compute a transaction consumes; fee = gas used × gas price.
- **ERC-20 / ERC-721**: standard interfaces for fungible tokens / NFTs.
- **decimals**: a token's precision, e.g. USDC=6, most ERC-20=18; convert amounts
  accordingly when displaying.
- **payable / nonpayable / view / pure**: function mutability. `payable` can
  receive ETH with the call; `view`/`pure` are read-only.
- **approve / allowance**: the ERC-20 approval mechanism letting an address move
  your tokens up to a limit.

## Wallets / derivation

- **BIP39**: mnemonic standard (12/15/18/21/24 words).
- **BIP44**: HD wallet path standard; EVM commonly uses
  `m/44'/60'/account'/0/index`.
- **HD Wallet**: hierarchical-deterministic wallet — many addresses from one
  seed/mnemonic.

## Bitcoin

- **UTXO**: Unspent Transaction Output — Bitcoin's accounting model.
- **PSBT** (Partially Signed Bitcoin Transaction): a format for multi-party signing.
- **Legacy / SegWit / Taproot**: BTC address types (`1...` / `bc1q...` / `bc1p...`).

## Solana

- **PDA** (Program Derived Address): a program-owned address with no private key.
- **ATA** (Associated Token Account): a wallet's account for holding a given token.
- **IDL** (Interface Definition Language): an Anchor program's interface, like an
  EVM ABI.
- **Rent**: fee for the on-chain storage a Solana account occupies.
- **Compute Units**: the compute-budget unit for a Solana transaction.

## Polkadot

- **SS58**: the Polkadot/Substrate address encoding; the prefix distinguishes chains.
- **Planck / DOT**: units of DOT — 1 DOT = 10¹⁰ Planck.
- **SCALE**: Substrate's compact encoding format.
- **Storage Key**: the key of an on-chain storage item, hashed from module and item
  names.

---

[← Back to overview](./index.md)
