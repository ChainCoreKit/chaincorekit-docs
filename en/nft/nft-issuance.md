**English** · [简体中文](../../zh/nft/nft-issuance.md) · [← Overview](../index.md)

# NFT Issuance

> Deploy a standard ERC-721 contract, set a Base URI, and mint NFTs to a chosen
> address.

## When to use it

- Launch a standard ERC-721 collection quickly, deploying a contract without
  writing Solidity.
- Set a Base URI or keep minting on an ERC-721 contract you've already deployed.
- Validate the issuance flow on a testnet (deploy → set URI → mint → preview)
  before going to mainnet.

## Steps

1. Connect your wallet (top right). While disconnected, write actions show
   **"🔒 Connect wallet to continue"** — clicking opens the connect dialog.
2. In the **Contract** card, pick a mode:
   - **Deploy new contract**: enter **Name** and **Symbol**, choose the
     **network** (Ethereum / Polygon / Arbitrum One / Base / Sepolia). The
     **pre-flight** panel shows contract type, deploy network, wallet's current
     network, estimated fee, and whether the balance is sufficient. Click
     **Deploy** to open the confirmation dialog; after verifying, **confirm and
     deploy** — the dialog shows pending → success (contract address + tx hash)
     or failure (reason).
   - **Import existing contract**: choose the network, enter the **contract
     address**, and click **Import**.
3. After deploy or import, the **Contract info** card shows the address, name,
   symbol, standard, network, and minted count, with copy-address and explorer
   links.
4. **Set Base URI**: enter `ipfs://…/` or `https://…/metadata/`, review the
   estimated fee, and click **Set**.
5. **Mint NFT**: enter the **recipient address** (or click "use my address"),
   optionally enter a **Token URI** (blank falls back to Base URI concatenation),
   review the estimated fee, and click **Mint NFT**.
6. The **Transaction history** card logs each deploy / mint by type, tx hash,
   Token ID, and status.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Name / Symbol | the ERC-721 Name / Symbol |
| Network | Ethereum / Polygon / Arbitrum One / Base / Sepolia |
| Contract address (import) | `0x…`, an already-deployed ERC-721 |
| Base Token URI | `ipfs://…/` or `https://…/metadata/` |
| Recipient | `0x…`, the address receiving the NFT |
| Token URI (optional) | metadata URI for one token; blank uses Base URI |
| Output | contract address, tx hash, Token ID, tx status |

## Notes & gotchas

- **Two-level gating**: writes require ① a connected wallet and ② a deployed or
  imported contract; when unmet, the card shows an empty-state guide, not fake
  data.
- **Network consistency**: before deploy / mint, confirm the "deploy network"
  matches the "wallet's current network" to avoid the wrong chain.
- **tokenURI concatenation depends on the contract**: commonly Base URI + tokenId
  or Base URI + tokenId.json — make sure metadata is uploaded to that path.
- **Verify imported contracts**: check on the block explorer whether the contract
  is verified before writing; be cautious if the ABI source isn't trusted.
- **Native coins differ per chain**: Ethereum/Arbitrum/Base = ETH, Polygon = POL,
  Sepolia = SepoliaETH; gas is charged in the chain's native coin.
- **Fees are estimates**: pre-flight and confirmation fees are estimates; the
  wallet's final signing figure is authoritative.

## Security

- Deploy and mint are **real, irreversible** on-chain writes — verify the network,
  name/symbol, recipient, and fee before signing.
- High-risk actions (e.g. transferring contract ownership) warrant extra care and
  a second confirmation.
- Before a large mint, run the full flow on a testnet (Sepolia) first.

## Related tools

- [NFT Preview](./nft-preview.md) — preview media and metadata after minting
- [ABI Console](../evm/abi.md) — call contracts visually
- [Security model](../security.md)

---

> Disclaimer: deploy and mint are real, irreversible on-chain transactions —
> verify the network, address, and fee before signing.
