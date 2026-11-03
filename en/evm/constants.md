**English** · [简体中文](../../zh/evm/constants.md) · [← Overview](../index.md)

# EVM Constants

> The fixed values you keep reaching for when writing contracts, building calldata or debugging: special addresses, well-known contracts, integer limits and common hashes. Every entry is one-click copyable.

## When to use it

- You need the zero address or a burn address as a parameter, or want to recognise them in logs.
- An unlimited approval needs `max uint256`; a Permit2 allowance cap needs `max uint160`.
- Scripts or tests need well-known addresses such as Multicall3, Permit2 or the ERC-4337 EntryPoint.
- You run into values like `0xc5d2…a470` or `0x56e8…b421` while debugging and want to know what they are.

## What's included

| Group | Entries |
| --- | --- |
| Special addresses | Zero address, common burn address `0x…dEaD` |
| Well-known contracts | Multicall3, Permit2 (Uniswap), CREATE2 deployer (Arachnid), ERC-4337 EntryPoint v0.7 / v0.6 |
| Integer limits | max uint256 (hex and decimal), max uint160 / uint128 / uint64, max / min int256 |
| Hashes & bytes | bytes32 zero, keccak256 of empty bytes, empty trie root |

Addresses are given in EIP-55 checksum form and can be pasted straight into a wallet or block explorer.

## Notes & gotchas

- **Same address on many chains ≠ deployed on every chain.** These contracts share an address on most EVM chains, but newer chains, private networks and some L2s may not have them yet. Confirm the address has contract code on the target chain's block explorer first.
- **EntryPoint has several versions** — v0.6 and v0.7 have incompatible interfaces; pick the one your smart account targets.
- **The burn address is a convention**: `0x…dEaD` has no known private key, but it isn't special at the protocol level; assets sent there can't be recovered.
- Using `max uint256` as an unlimited approval lets the spender move **all** of your balance in that token at any time. Make sure you trust the contract, and revoke it later with [Token Approvals](./approvals.md) if needed.

## Related tools

- [Timestamp Converter](./timestamp.md) — Unix timestamps to dates and back
- [Unit Converter](./unit-convert.md) — Wei / Gwei / ETH and token decimals
- [Hash Tools](./hash-tool.md) — keccak-256 of any input
- [Contract Inspector](./contract-check.md) — check whether an address has contract code
