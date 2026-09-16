**English** · [简体中文](../../zh/polkadot/dot-balance.md) · [← Docs home](../index.md)

# Polkadot Balance

> Look up a Polkadot / Kusama account by SS58 address, with transferable, frozen and reserved listed separately.

## When to use it

- Find out how much an account **can actually move right now**, not just its on-chain total.
- Check the transferable balance before a transfer — staking, governance votes and vesting all lock part of it.
- Get an account's current nonce (for constructing offline transactions).
- Query your own node instead of relying on a third-party explorer.

## Steps

1. Pick a **network** (Polkadot / Kusama / Westend testnet).
2. (Optional) Enter a **custom RPC**. An https endpoint is enough — this tool speaks HTTP
   JSON-RPC and needs no WebSocket.
3. Paste an **SS58 address** and click **Look up**.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Polkadot / Kusama / Westend |
| Custom RPC (optional) | https JSON-RPC endpoint; blank uses a public node |
| Account address | SS58 format, checksum validated as you type |
| Transferable | `free − max(frozen − reserved, 0)` — **this is what can actually move** |
| Free | The unreserved balance, part of which may still be frozen |
| Reserved | Deposits locked by on-chain features (identity, proxies, multisig) |
| Frozen | Amounts locked by staking, voting or vesting |
| Total | free + reserved |
| Nonce | Number of transactions this account has sent |

## Notes & gotchas

- **Transferable ≠ free.** This is the single most important thing on the page. Staking,
  governance voting and vesting all freeze part of `free`, so reading `free` as "what I have"
  overstates it — you find out when the transfer fails. That's why transferable comes first.
- **A different SS58 prefix doesn't affect the lookup.** The same AccountId is valid on every
  Substrate chain; only the address formatting differs. Looking up a Polkadot balance with a
  Kusama-formatted address is perfectly reasonable — the page notes it rather than blocking you.
- **"No such account on chain" is not a lookup failure.** It means the address has never received
  funds, or its balance fell below the **existential deposit** and was reaped (a Substrate-specific
  mechanism: accounts below the threshold are deleted to reclaim storage).
- **What "frozen" means depends on the runtime version**: newer runtimes use it for staking /
  voting / vesting locks, while older ones put `miscFrozen` in that slot. The byte layouts are
  identical so it can't be told apart locally — Polkadot and Kusama both run the newer form today.
- **This is a read-only lookup.** No wallet connection, no private key.

## Related tools

- [SS58 Converter](./dot-ss58.md) — SS58 ↔ AccountId32
- [Polkadot Wallet Generator](./dot-wallet.md) — generate Substrate wallets locally
- [DOT Unit Converter](./dot-unit.md) — Planck ↔ main unit
- [Substrate Hash / Storage Key](./dot-hash-storage.md) — derive storage keys from an AccountId
- [Security model](../security.md)
