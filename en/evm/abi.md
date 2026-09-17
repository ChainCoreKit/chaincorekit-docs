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

## Export / import the contract list

Switch machines, switch browsers, or clear site data and that left-hand list is
gone — you'd have to re-enter every contract by hand. You can carry the whole
list instead.

Below **Add contract** there is a `Contracts · N` row with a `···` menu:

| Menu item | What it does |
| --- | --- |
| Import list | Pick a `.json` file, or paste the list straight in |
| Export all · N | Save every contract into one JSON file |
| Export current contract | Export only the contract selected on the left |

The exported file is plain JSON and `abi` is an array (not a string), so scripts
and other tooling can consume it directly:

```json
{
  "format": "chaincorekit-abi-contracts",
  "version": 1,
  "exportedAt": "2026-09-16T08:30:00.000Z",
  "count": 1,
  "contracts": [
    {
      "name": "USDC",
      "network": "Ethereum",
      "address": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
      "abi": [{ "type": "function", "name": "balanceOf", "stateMutability": "view", "inputs": [], "outputs": [] }]
    }
  ]
}
```

Importing **previews first, writes second**: every entry is labelled with what
will happen to it, and each one can be ticked or unticked.

| Label | Meaning |
| --- | --- |
| New | Not in your list yet — it will be added |
| Will skip / Will overwrite | You already have this contract (**same address on the same network**); which one depends on the policy below |
| Invalid | It can't come in, and the row says why: invalid contract address / network missing / ABI is not a JSON array / duplicate within the list |

For **Existing contracts** pick **Skip** (default) or **Overwrite**. When the
import finishes you're told how many were imported, overwritten, skipped and
invalid.

## Inputs / outputs

| Field | Meaning / format |
| --- | --- |
| Contract name | a label for the list only |
| Network | drives explorer URL and call network |
| Contract address | `0x` + 40 hex, live EIP-55 check |
| ABI source | paste ABI JSON array / upload file |
| Unit switch | Wei / Gwei / Ether, aids amount inputs only |
| Function group | All / Read (view) / Write |
| Contract list file | JSON with name / network / address / ABI; both an exported file and a bare array are accepted |

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
- **Overloaded functions** (e.g. ERC-721's two `safeTransferFrom`, 3-arg and
  4-arg) each get their own card. Expanding, filling and sending one never
  affects the other — the transaction is encoded for the overload whose card you
  opened.
- **An exported list holds only contract names, networks, addresses and ABIs** —
  all public information, no private keys, mnemonics or credentials. It still
  reveals which contracts and chains you work with, so think before sharing it.
- **Overwriting can't be undone**: the local entry's name and ABI are replaced by
  the ones in the list. Export a copy first if you're unsure.
- The contract list lives in your own browser and is **never synced to a server**
  — which is why moving devices needs export / import, and why clearing site data
  clears the list too.
- High-risk writes get an inline warning when expanded and an extra tick-box
  before sending: `transferOwnership`, `renounceOwnership`, `selfdestruct`,
  `upgrade`, and **`setApprovalForAll`** — the last one hands over every token in
  an NFT collection in a single call, after which the operator can move them at
  any time without you seeing another confirmation.

## Related tools

- [Calldata Codec](./calldata.md) — encode/decode call data manually
- [Signature Lookup](./signature-lookup.md) — both the selector and the TopicID are slices of the keccak-256 hash
- [Unit Converter](./unit-convert.md) — Wei / Gwei / Ether
- [Security model](../security.md)

---

> Disclaimer: write operations are real and irreversible — verify address, amount,
> and network before signing.
