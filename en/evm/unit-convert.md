**English** · [简体中文](../../zh/evm/unit-convert.md) · [← Overview](../index.md)

# Unit Converter

> Type any Ether unit and the rest convert live; a separate arbitrary-precision field handles ERC-20 tokens. Every field is one-click copyable.

## When to use it

- Convert amounts or gas prices between Wei / Gwei / Ether.
- Check what a raw uint256 Wei value from a contract is in ETH.
- Convert to finer-grained units (Kwei, Szabo, Finney, Kether, …).
- **You have a token amount rather than ETH** — e.g. USDC's raw `1000000`, and you want to know how many USDC that is.

## Steps

1. Enter a value in any of the **common** fields (Ether / Gwei / Wei).
2. The other units convert **live** — click the copy button by each field.
3. Expand **more units** for Kwei · Mwei · Szabo · Finney · Kether · Mether ·
   Gether · Tether.
4. Use the **quick chips** (1 ETH / 0.1 ETH / 1 Gwei / 100 Gwei) to prefill, or the
   top-right button to **reset to 1 ETH**.

### Converting ERC-20 token amounts

The eleven units above are all **ether-family**, while most on-chain amounts are not
ether. In the **arbitrary precision** section:

1. Enter the token's **decimals** (look them up with the
   [Token Inspector](./token-inspector.md) if you don't know them). Quick chips cover
   USDC / USDT (6), WBTC (8) and DAI / WETH (18).
2. Put the raw uint256 in the **Wei** field, or a human-readable figure in the
   arbitrary-precision field — the two convert live in both directions.

Changing the precision **does not clear** what you've entered: Wei is the single
source of truth, so a new precision is just a different reading and every other
field stays consistent.

## Inputs / outputs

| Unit | Magnitude vs Ether |
| --- | --- |
| Wei | 10⁻¹⁸ (smallest unit) |
| Kwei | 10⁻¹⁵ |
| Mwei | 10⁻¹² |
| Gwei | 10⁻⁹ (common for gas) |
| Szabo | 10⁻⁶ |
| Finney | 10⁻³ |
| Ether | 1 |
| Kether / Mether / Gether / Tether | 10³ / 10⁶ / 10⁹ / 10¹² |

## Notes & gotchas

- **1 ETH = 10¹⁸ Wei**; gas prices are usually quoted in Gwei.
- **Wei is an integer unit** — anything below 1 Wei is meaningless and rounds.
- **Don't read raw Wei as human-readable** — uint256 amounts in a contract are
  usually in the smallest unit; scale before displaying.
- This converts **native Ether units**; ERC-20 tokens have their own `decimals`
  (e.g. USDC=6) — don't mix the two.

## Related tools

- [ABI Console](./abi.md) — the unit switch helps amount inputs when calling
- [Calldata Codec](./calldata.md) — encode / decode call params
- [Address & ENS](./address.md) — validate and resolve addresses
- [Security model](../security.md)

---

> Disclaimer: conversions are for reference — verify the actual amount and unit
> before signing.
