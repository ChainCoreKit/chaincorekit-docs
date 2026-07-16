**English** · [简体中文](../../zh/btc/btc-addr-convert.md) · [← Overview](../index.md)

# Address Format Convert · BTC

> Enter an address or a compressed public key to derive its Legacy / Nested SegWit
> / Native SegWit / Taproot forms.

## When to use it

- You have one address and want to see its other-type forms (e.g. Native SegWit
  from a Legacy address).
- You have a compressed public key and want its address across each type.
- You want to confirm that different formats point to the same key.

## Steps

1. Choose the network: **Mainnet** or **Testnet**.
2. Enter an address (`1` / `3` / `bc1q` / `bc1p…`) or a compressed public key
   (`02` / `03…`, 66 hex).
3. The converted forms appear automatically.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Network | Mainnet / Testnet |
| Input | address (Legacy / Nested SegWit / Native SegWit / Taproot) or compressed pubkey (`02` / `03` + 64 hex = 66 total) |
| Output | Legacy / Nested SegWit / Native SegWit / Taproot address forms |

## Notes & gotchas

- **Different forms ≠ different funds**: they derive from the same key but are
  distinct on-chain addresses with separate balances.
- Only **compressed public keys** (starting `02` / `03`, 66 hex) are accepted as
  key input.
- Pick the right network — mainnet and testnet prefixes differ and don't transfer
  across networks.
- Conversion only maps forms; it doesn't touch private keys or fetch balances.

## Related tools

- [Generate BTC Wallet](./btc-wallet.md) — generate addresses of each type locally
- [Balance Checker](./btc-balance.md) — check balances across forms
- [UTXO Lookup](./btc-utxo.md) — view unspent outputs
- [Security model](../security.md)

---

> Disclaimer: the forms are independent on-chain addresses — receive to whichever
> the counterparty specifies.
