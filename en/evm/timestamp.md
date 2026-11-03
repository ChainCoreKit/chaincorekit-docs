**English** · [简体中文](../../zh/evm/timestamp.md) · [← Overview](../index.md)

# Timestamp Converter

> Convert Unix timestamps to dates and back: paste a timestamp to get UTC / ISO 8601 / local time, or pick a date to get its timestamp. Seconds and milliseconds are detected automatically.

## When to use it

- You see a `block.timestamp`, a `deadline`, a lock-up expiry or a vesting schedule in a contract and want to know which date and time it is.
- You're building transaction parameters (a swap `deadline`, a permit expiry) and need the seconds timestamp for a given date.
- You have a 13-digit number and aren't sure whether it's seconds or milliseconds.

## How to use

### Timestamp → date

1. Enter a value in the **Timestamp** field (thousands separators and underscores are fine).
2. A hint under the field tells you whether it was read as **seconds** or **milliseconds**.
3. The result shows UTC, ISO 8601, local time and the seconds / milliseconds timestamps — every row is one-click copyable.

**Use current time** in the card header fills both sides with the current moment.

### Date → timestamp

1. Pick a date and time under **Date and time** (interpreted in your device's time zone).
2. You get the seconds and milliseconds timestamps plus the matching UTC time.

## Input / output

| Digits | Read as | Typical source |
| --- | --- | --- |
| ≤ 11 | Seconds | On-chain `block.timestamp`, contract parameters, most backend APIs |
| ≥ 12 | Milliseconds | JavaScript `Date.now()`, some front-end analytics |

## Notes & gotchas

- **On-chain time is always in seconds.** Passing a milliseconds value into a contract won't revert — it just lands tens of thousands of years in the future, e.g. a `deadline` that never expires.
- **Reading seconds as milliseconds** lands in January 1970, again without any error. The "read as seconds / milliseconds" hint under the field is there to catch both.
- **Date → timestamp** uses your **local time zone**; when you need a UTC boundary, check the UTC row of the result.
- Only plain decimal numbers are accepted; a `0x` hex value is flagged as invalid — convert it to decimal first.

## Related tools

- [Unit Converter](./unit-convert.md) — Wei / Gwei / ETH and token decimals
- [EVM Constants](./constants.md) — zero address, uint256 limits and other fixed values
- [Transaction Tracer](./trace-view.md) — see when a transaction's block was produced
