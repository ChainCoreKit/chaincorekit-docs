**English** · [简体中文](../../zh/evm/token-issuance.md) · [← Overview](../index.md)

# Token Issuance

> Create and deploy a standard mintable ERC-20 — preflight gas and balance, confirm,
> then sign. You can also import an existing contract to mint.

## When to use it

- You want to ship a standard ERC-20 quickly on a testnet / mainnet.
- You already deployed an ERC-20 and want to import it and keep minting.
- You want to see the estimated fee, network, and whether your balance is enough
  before deploying.

## Steps

### Deploy a new contract

1. **Connect a wallet** first (while disconnected the button shows "🔒 Connect
   wallet"; clicking it opens the connect flow).
2. On the **Deploy** tab, fill in **name / symbol / total supply / decimals** and
   pick a **network**.
3. Review the **deploy preflight**: contract type, initial supply, deploy network,
   your wallet's current network, estimated fee, and balance check.
4. Click **Deploy**, verify in the confirm dialog, then **Confirm & deploy**. A
   dialog shows pending → success / failure; on success, copy the contract address
   and tx hash and open the block explorer.

### Import an existing contract

1. Pick a **network** and enter the **token contract address** on the **Import** tab.
2. Click **Import** to interact as a standard ERC-20.

### Mint tokens

- After deploying or importing, in the **Mint** card fill **recipient** ("Use my
  address" available) and **amount**, review the estimated fee, and click **Mint**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Name / Symbol | token name and symbol (e.g. ChainCore Token / CCK) |
| Total supply | initial supply |
| Decimals | decimal places; usually 18, stablecoins like USDC/USDT use 6 |
| Network | Ethereum / Arbitrum One / Base / Polygon / Sepolia |
| Deploy preflight | contract type, supply, network, estimated fee, balance check |
| Contract info | after deploy/import: address, name, symbol, decimals, supply, network |
| Mint | recipient + amount, with estimated fee |
| Transaction history | type / tx hash / status |

## Notes & gotchas

- **Two-level gating** — a write needs (1) a connected wallet and (2) a deployed /
  imported contract; missing either disables the button.
- **Deploy / mint are real on-chain transactions** — they cost gas and are
  irreversible; verify network, supply, and account before confirming.
- **Native fee coin by network** — Ethereum / Arbitrum One / Base = ETH, Polygon =
  POL, Sepolia = SepoliaETH; the fee estimate follows the selected network.
- **Decimals change what an amount means** — with `decimals=18` the chain accounts in
  the smallest unit; don't read raw values as human-readable amounts.
- **Verify before importing** — confirm the address and network, and check whether
  the contract is verified on the explorer before any write.
- High-risk writes ask for a second confirmation — read the dialog carefully.

## Related tools

- [ABI Console](./abi.md) — call any contract visually
- [Faucets](./faucet.md) — fund your account before deploying
- [Unit Converter](./unit-convert.md) — Wei / Gwei / Ether
- [Transaction Tracer](./trace-view.md) — analyze deploy / mint transactions
- [Security model](../security.md)

---

> Disclaimer: write operations are real and irreversible — verify address, amount,
> and network before signing.
