**English** · [简体中文](../zh/index.md) · [← Repo home](../README.md)

# ChainCore Kit Documentation

ChainCore Kit is a browser-based, multi-chain developer toolkit spanning the
**EVM, Bitcoin, NFT, Solana, and Polkadot** ecosystems. Everything that touches
a private key or mnemonic — generation, wallet derivation, transaction signing —
runs locally in your browser. **Keys and mnemonics are never uploaded, stored,
or sent off your device.**

> Read the [security model](./security.md) before using any key-related tool.

## Getting started

1. Open the ChainCore Kit app, pick an ecosystem from the top nav (EVM / BTC /
   NFT / Solana / Polkadot / Batch), or find a tool via the sidebar or `⌘K`.
2. **Read-only tools** (converters, decoders, lookups) work without connecting a
   wallet.
3. **Write / signing tools** require a connected wallet. When disconnected, the
   button reads "Connect wallet to continue" and opens the connect dialog on click.
4. Keys and mnemonics in results are masked by default — click the eye icon to
   reveal, and only in a safe environment.

## Tool index

### EVM

| Tool | What it does |
| --- | --- |
| [Faucets](./evm/faucet.md) | Testnet faucet directory |
| [Generate Wallet](./evm/generate-wallet.md) | Generate EVM wallets locally; import mnemonic/key |
| [Vanity Address](./evm/vanity.md) | Addresses with a chosen prefix/suffix |
| [ABI Console](./evm/abi.md) | Import an ABI and call contracts visually |
| [Selector Lookup](./evm/query-selector.md) | 4byte selector ↔ function signature |
| [Unit Converter](./evm/unit-convert.md) | Wei / Gwei / Ether conversion |
| [Transaction Tracer](./evm/trace-view.md) | Inspect a transaction's flow, events and calls |
| [Address & ENS](./evm/address.md) | EIP-55 checksum, ENS resolution |
| [Event TopicID](./evm/topic-id.md) | Compute an event signature's TopicID |
| [Hash Tools](./evm/hash-tool.md) | keccak-256 and related hashing |
| [Calldata Codec](./evm/calldata.md) | Encode / decode transaction calldata |
| [ABI Codec](./evm/abi-codec.md) | Encode constructor args; decode event logs and revert errors |
| [Transaction Decoder](./evm/tx-decode.md) | Decode raw signed transactions and RLP, up to EIP-4844 / 7702 |
| [Signature Verifier](./evm/sig-verify.md) | Hash and verify EIP-191 messages and EIP-712 typed data |
| [RPC Diagnostics](./evm/rpc-check.md) | Check endpoint reachability, chainId, block height, latency and read capabilities |
| [Contract Inspector](./evm/contract-check.md) | Bytecode, proxy implementation, admin slot and EIP-7702 delegation |
| [Token Approvals](./evm/approvals.md) | Check and revoke allowances for the token / spender pairs you specify |
| [Address Prediction & Merkle](./evm/create2-merkle.md) | Predict CREATE / CREATE2 addresses and build airdrop Merkle trees |
| [Multi-chain Derivation](./evm/multichain-derive.md) | See EVM / BTC / Solana / Aptos / Sui / TON addresses from one mnemonic |
| [Batch Contract Read](./evm/batch-read.md) | Different read-only calls across many contracts, pinned to one block |
| [Token Issuance](./evm/token-issuance.md) | Deploy an ERC-20 token |

### Bitcoin

| Tool | What it does |
| --- | --- |
| [Generate Wallet](./btc/btc-wallet.md) | Generate a BTC wallet locally |
| [Address Format Convert](./btc/btc-addr-convert.md) | Legacy / SegWit / Taproot |
| [Balance Checker](./btc/btc-balance.md) | Batch-check BTC address balances |
| [UTXO Lookup](./btc/btc-utxo.md) | List an address's UTXOs |
| [PSBT Decode](./btc/btc-psbt.md) | Inspect a PSBT |

### NFT

| Tool | What it does |
| --- | --- |
| [NFT Preview](./nft/nft-preview.md) | Preview NFT metadata and media |
| [NFT Issuance](./nft/nft-issuance.md) | Deploy an NFT contract |

### Solana

| Tool | What it does |
| --- | --- |
| [Generate Wallet](./solana/sol-wallet.md) | Generate a Solana wallet locally |
| [PDA / ATA](./solana/sol-address.md) | Derive PDAs and associated token accounts |
| [Instruction Codec](./solana/sol-instruction.md) | Encode / decode instruction data |
| [Program IDL](./solana/sol-idl.md) | Browse an Anchor IDL |
| [Compute / Fee / Rent](./solana/sol-fee-rent.md) | Estimate compute units, fees, rent |
| [Token Inspector](./solana/sol-token-inspector.md) | Mint supply, decimals, authorities, Token-2022 extensions |

### Polkadot

| Tool | What it does |
| --- | --- |
| [Generate Wallet](./polkadot/dot-wallet.md) | Generate a Polkadot wallet locally |
| [SS58 Convert](./polkadot/dot-ss58.md) | Convert SS58 across chain prefixes |
| [DOT Units](./polkadot/dot-unit.md) | Planck / DOT conversion |
| [Hash / Storage Key](./polkadot/dot-hash-storage.md) | Compute storage keys |
| [SCALE Codec](./polkadot/dot-scale.md) | SCALE encode / decode |

### Batch

| Tool | What it does |
| --- | --- |
| [Disperse](./bulk/disperse.md) | One-to-many distribution via contract |
| [Per-wallet Send](./bulk/bulk-send.md) | Send from the connected wallet |
| [Multi-key Send](./bulk/bulk-send2.md) | Import multiple keys and batch-send |
| [Sweep](./bulk/bulk-collect.md) | Consolidate assets from many wallets |
| [Balance Checker](./bulk/bulk-query-balance.md) | Batch-check address balances |

## Related

- [Corbit endpoint CORS setup](./ai/corbit-cors.md)
- [Security model](./security.md)
- [FAQ](./faq.md)
- [Glossary](./glossary.md)

---

> Disclaimer: this documentation and the tools are provided "as is", without
> warranty. You are responsible for safeguarding your keys and for any
> transaction you sign. Always verify address, amount, and network. Losses are
> irreversible.
