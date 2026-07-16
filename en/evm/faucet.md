**English** · [简体中文](../../zh/evm/faucet.md) · [← Overview](../index.md)

# Faucets

> Testnet faucets grouped by network — copy a Chain ID, add the network to your
> wallet, and jump straight to a faucet.

## When to use it

- You need test coins to develop/test contracts and want the right faucet fast.
- You have a fresh wallet address and want SepoliaETH, tBNB, AVAX, etc.
- You want to add a testnet to your wallet without typing RPC / Chain ID by hand.

## Steps

1. Filter live with the search box by **network / currency / keyword** (e.g.
   `Sepolia`, `ETH`), or use the tabs **All / Ethereum testnets / L2 / sidechain /
   other**.
2. On a network card, **copy the Chain ID** or click **Add to wallet** to add it.
3. Click **Expand** on the card to see that network's faucet list.
4. Each faucet shows its host, a gating tag, and a note. Click **Claim ↗** to open
   the faucet in a new tab, or copy its URL.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Search box | live filter by network / currency / keyword |
| Tabs | All / Ethereum testnets / L2 / sidechain / other |
| Chain ID | each testnet's chain ID, one-click copy |
| Currency | the testnet's native coin (SepoliaETH / tBNB / AVAX / POL, …) |
| Gating tag | no login / login / connect wallet / PoW mining / mainnet balance |
| Claim | external link to a third-party faucet, or copy its URL |

## Notes & gotchas

- **Navigation only** — faucets are third-party; the actual rules, limits, and
  cooldowns live on their pages.
- **Gating varies** — some faucets need login / a connected wallet / PoW mining, or
  even a mainnet balance. Check the gating tag first.
- **Test coins have no value** — testnet tokens can't be used on mainnet and carry
  no real value; never trade them.
- **11 networks covered** — Sepolia, Hoodi, Polygon Amoy, Optimism / Arbitrum
  Sepolia, Aurora, BNB Chain Testnet, Avalanche Fuji, Gnosis Chiado, Harmony
  Testnet, Celo Alfajores. Missing a faucet? Open an issue / PR.

## Related tools

- [Generate Wallet](./generate-wallet.md) — create an address to receive coins
- [Vanity Address](./vanity.md) — addresses with a chosen prefix/suffix
- [Token Issuance](./token-issuance.md) — deploy and mint an ERC-20 on a testnet
- [Security model](../security.md)

---

> Disclaimer: faucets are third-party services; availability and rules are theirs.
> This tool is aggregation and navigation only.
