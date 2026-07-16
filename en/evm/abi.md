**English** · [简体中文](../../zh/evm/abi.md) · [← Overview](../index.md)

# ABI Console

> Import an ABI to auto-generate a function list and call contracts visually.
> Manage multiple contracts, grouped by Read / Write.

## When to use it

- You want Etherscan-style "Contract" interaction — calling read/write functions
  without writing code.
- You have a contract ABI (yours or a third party's) and need to test it quickly.
- You need to manage several contracts and switch between them.

## Steps

1. Click **Add contract** on the left and fill in:
   - **Contract name** (e.g. USDC, MyToken).
   - **Network**: current connected network / Ethereum / Arbitrum One / Base, etc.
     (drives the explorer link and the call network).
   - **Contract address** (`0x…`, validated live against EIP-55).
   - **ABI source**: paste ABI / upload an ABI file ("fetch from explorer" and
     "common ABIs" are coming soon).
2. The contract appears in the left list; select it to show the functions panel.
3. Switch the group tabs **All / Read / Write** (each with a count), or use the
   **filter** box to search by function name.
4. Expand a function and fill in parameters:
   - **Read**: enter params and call to see the return value.
   - **Write**: requires a connected wallet; goes through
     preview → gas estimate → confirm → sign → pending → result.
   - For amount params, use the **Wei / Gwei / Ether** switch to help input.
5. The top bar lets you **View ABI**, open the **block explorer**, **edit** the
   contract, or **share / delete** from the `···` menu.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Contract name | a label for the list only |
| Network | drives explorer URL and call network |
| Contract address | `0x` + 40 hex, live EIP-55 check |
| ABI source | paste ABI JSON array / upload file |
| Unit switch | Wei / Gwei / Ether, aids amount inputs only |
| Function group | All / Read (view) / Write |

## Notes & gotchas

- **Read vs Write**: `view`/`pure` are Read (free, no signing); `nonpayable`/
  `payable` are Write (require signing, on-chain).
- **payable functions** need an extra ETH value — mind the unit (Wei/Gwei/Ether).
- **Amount precision**: uint256 amounts are scaled by the token's `decimals`
  (USDC=6, most ERC-20=18). Don't read a raw Wei value as human-readable.
- **Type aliases**: `uint` = `uint256`, `int` = `int256`, `byte` = `bytes1`;
  `bytes/bytes32` need `0x`-prefixed hex.
- **Unverified contracts**: if the ABI source isn't trustworthy, be cautious —
  don't blindly trust a third-party ABI.
- High-risk writes (`transferOwnership`, `selfdestruct`, `upgrade`) warrant extra
  care and usually a second confirmation.

## Related tools

- [Calldata Codec](./calldata.md) — encode/decode call data manually
- [Selector Lookup](./query-selector.md) — selector ↔ function signature
- [Event TopicID](./topic-id.md) — compute an event's TopicID
- [Unit Converter](./unit-convert.md) — Wei / Gwei / Ether
- [Security model](../security.md)

---

> Disclaimer: write operations are real and irreversible — verify address, amount,
> and network before signing.
