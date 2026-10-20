**English** · [简体中文](../../zh/evm/token-issuance.md) · [← Overview](../index.md)

# Token Issuance

> Deploy a standard ERC-20 whose source you can read and verify on Sourcify. Gas, balance and owner privileges are checked before you sign; you can also import an existing contract and mint.

## When to use it

- You want to launch a standard ERC-20 on a testnet or mainnet quickly.
- You need a token contract whose **source can be checked on a block explorer / Sourcify**, so holders and partners can confirm there's no backdoor.
- You already deployed an ERC-20 and want to import it and keep minting.

## Steps

### Deploy a new contract

1. **Connect a wallet** first (while disconnected the button shows "🔒 Connect
   wallet"; clicking it opens the connect flow). The deploy network **follows the
   chain your wallet is on** — switch networks in your wallet.
2. On the **Deploy** tab, fill in **name / symbol / total supply**, and optionally a
   **max supply** (leave empty for no cap).
3. Review the **deploy preflight**: contract type, **owner privileges**, initial
   supply, deploy network, estimated fee, and balance check.
4. To see exactly what gets deployed, click **View contract source**: the full
   contract and its build settings (OpenZeppelin version, solc version, optimizer
   runs, EVM version) are shown.
5. Click **Deploy**, verify in the confirm dialog, then **Confirm & deploy**. The
   dialog shows pending → success / failure.
6. After a successful deploy, click **Verify source on Sourcify**; the result
   arrives within seconds to a minute, then **View on Sourcify**. The contract
   info card has the same button, so you can verify any time after closing the dialog.

### Import an existing contract

1. On the **Import** tab, enter the **token contract address** and click **Import**
   to interact as a standard ERC-20.

### Mint tokens

- After deploying or importing, in the **Mint** card fill **recipient** ("Use my
  address" available) and **amount**, check the echoed parameters, and click **Mint**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Name / Symbol | token name and symbol (e.g. ChainCore Token / CCK); symbol is 1–12 letters or digits |
| Total supply | in **whole tokens**, all minted to the deploying wallet |
| Max supply (optional) | in whole tokens; empty = no cap. Can't be lower than the total supply and **can't be changed after deployment** |
| Decimals | always 18 for contracts deployed here (read-only) |
| Deploy preflight | contract type, owner privileges, supply, network, estimated fee, balance check |
| Contract info | address, name, symbol, decimals, total supply, max supply, network |
| Mint | recipient + amount; the echo also shows the converted base-unit value |
| Transaction history | type / tx hash / status |

## Owner privileges (read before deploying)

- **The deploying wallet becomes owner**; only the owner can mint.
- **Without a max supply, the owner can mint without limit.** With a cap, total
  minting can never exceed it (burned tokens free up room to be minted again).
- Any holder can burn their own tokens.
- The owner can transfer or renounce ownership; **after renouncing, minting is
  disabled forever**.

All of this is stated in the preflight's "Owner privileges" row and can be checked
line by line in the source.

## Notes & gotchas

- **Two-level gating** — a write needs (1) a connected wallet and (2) a deployed /
  imported contract; missing either disables the button.
- **Switching networks before you sign is blocked** — if you change chains in your
  wallet after confirming but before signing, nothing is sent and the page asks
  you to switch back. The same address can be a completely different contract on
  another chain.
- **Deploy / mint are real on-chain transactions** — they cost gas and are
  irreversible; verify network, supply, and account before confirming.
- **Minting needs the token's decimals first** — imported tokens may use 6, 8, etc.
  If decimals can't be read, the Mint button is disabled with a **Retry** option:
  minting with the wrong decimals mints a completely different amount, irreversibly.
- **Verifying sends the source to Sourcify**, a public source-verification service;
  the result is visible to everyone. Etherscan is verified separately: click
  **Download Standard JSON** and submit it on Etherscan's "Verify & Publish" page
  as *Standard JSON Input*.
- **Contracts from the previous template can't be verified** — the earlier template
  had no published source. Those contracts can still be imported and minted, but
  not verified on Sourcify.
- **Deploy failures come in three kinds** with different fixes; the result dialog
  says which:
  - **Rejected in the wallet** — nothing was sent and no gas was spent; adjust and retry;
  - **Send failed** (insufficient balance, RPC error, …) — also never reached the
    chain; fix the stated cause;
  - **Deploy reverted · constructor failed** — the transaction **was mined and gas
    was spent**, but there is no code at that address; fix the parameters and redeploy.
- **Native coin by network** — Ethereum / Arbitrum One / Base / Optimism = ETH,
  BNB Chain = BNB, Polygon = POL, Avalanche = AVAX, Sepolia = SepoliaETH.

## Related tools

- [ABI Console](./abi.md) — call any contract visually
- [Faucets](./faucet.md) — fund your account before deploying
- [Unit Converter](./unit-convert.md) — Wei / Gwei / Ether
- [Transaction Tracer](./trace-view.md) — analyze deploy / mint transactions
- [Security model](../security.md)

---

> Disclaimer: write operations are real and irreversible — verify address, amount,
> and network before signing.
