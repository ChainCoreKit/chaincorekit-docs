**English** · [简体中文](../../zh/nft/nft-preview.md) · [← Overview](../index.md)

# NFT Preview

> Enter a contract address and Token ID to preview an NFT's media and metadata —
> no wallet required.

## When to use it

- Quickly check a Token ID's image and traits before minting or buying.
- Render an `ipfs://` link through a gateway when metadata is hosted on IPFS.
- After deploying a contract and setting a Base URI, verify that `tokenURI`
  points to the right metadata.

## Steps

1. Choose the **network**: Ethereum / Polygon / Arbitrum One / Base.
2. Choose the **IPFS gateway**: ipfs.io / Pinata / dweb.link (used to load
   `ipfs://` resources).
3. Enter the **contract address** (`0x…`, validated live against EIP-55).
4. Enter the **Token ID** (e.g. 3749).
5. Click **Preview** to read `tokenURI` on-chain and render the media and
   metadata, or click **Sample** to load an example set.
6. The result card shows a standard badge (ERC-721); you can **view the raw
   metadata JSON** in a dialog and **copy the JSON**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Ethereum / Polygon / Arbitrum One / Base |
| IPFS gateway | ipfs.io / Pinata / dweb.link, loads `ipfs://` resources |
| Contract address | `0x` + 40 hex, live EIP-55 check |
| Token ID | the NFT's integer ID |
| Output | NFT media, metadata fields, raw JSON (copyable) |

## Notes & gotchas

- **Read-only tool**: preview sends no transaction and needs no wallet — safe and
  side-effect free.
- **ERC-721 is supported** for metadata preview; ERC-1155 is coming soon.
- **Gateway differences**: if one IPFS gateway is slow or times out, switch to
  another and retry.
- **Missing metadata**: if the contract has no `tokenURI` or the path is empty,
  the media won't render — check the Base URI and where metadata was uploaded.
- **Match the network**: the contract address must match the selected network,
  otherwise the token can't be read.

## Related tools

- [NFT Issuance](./nft-issuance.md) — deploy ERC-721, set Base URI, and mint
- [ABI Console](../evm/abi.md) — call contracts visually
- [Security model](../security.md)

---

> Disclaimer: preview is read-only; media and metadata are third-party hosted, and
> what's shown reflects on-chain data.
