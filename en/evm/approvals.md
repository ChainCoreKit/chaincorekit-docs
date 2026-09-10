**English** · [简体中文](../../zh/evm/approvals.md) · [← Overview](../index.md)

# Token Approvals · EVM

> Check the current allowance for the token / spender pairs you specify, and revoke them in
> place.

## When to use it

- You're done with a DApp and want to take back the approval you gave it.
- After a batch disperse or sweep, you want to confirm whether an allowance is still open.
- You want to know exactly how much an address has approved for a token — and whether it's
  unlimited.

## Steps

1. Pick the **network**.
2. Enter the **owner address** (leave empty to use the connected wallet).
3. Enter one **token address + spender address** pair per line, separated by a space or
   comma; up to 20 lines. Any line that can't be parsed (a missing address, one mistyped
   character) is listed below the box with **its line number and the original text** — it is
   never skipped silently, or you would assume everything you pasted had been checked.
4. Click **Check approvals**. Token type is detected: ERC-721 / ERC-1155 use
   `isApprovedForAll`, everything else reads the ERC-20 `allowance`.
5. If you are the owner and your wallet is on the matching network, active approvals get a
   **Revoke** button.

## Output

| Case | Shown as |
| --- | --- |
| ERC-20 with an allowance | The value scaled by `decimals` |
| ERC-20 unlimited | `∞ · unlimited` (in red) |
| ERC-721 / ERC-1155 approved for all | `Approved for all (setApprovalForAll)` (in red) |
| Token decimals unreadable | The unconverted integer (a smallest-unit count) — **not a human-readable amount** |
| Read failed | Explicitly marked as failed — never shown as 0 |

## Handoff from Disperse

After approving a token on the Disperse page, a "Review or revoke this approval" link appears there; following it pre-fills the token and the spender (the Disperse contract). Approvals granted for a dispersal are easy to forget about afterwards, which is exactly what this path is for.

If the parameters are malformed they are **ignored entirely — never partially applied**. A half-filled form reads as "already correct" and invites you to check the wrong spender.

## Notes & gotchas

- **This tool does not discover approvals.** The most important point: plain RPC has no
  method to list every approval for an address; full discovery requires scanning historical
  `Approval` events or an indexing service. So **finding nothing here only means the pairs
  you entered have no approval** — it does not mean the address has no other approvals, and
  it certainly does not mean it is safe. The tool will never show a "no risk found" verdict.
- **Unlimited is judged by magnitude.** Projects write "unlimited" in different ways
  (`type(uint256).max`, `2^255`, a `uint96` ceiling, …), so exact-equality checks miss most
  of them. Anything above `2^255` is shown as `∞` — better to flag a huge-but-finite
  allowance as unlimited than to print a truly unlimited one as a long number that looks
  bounded.
- **Permit2 adds a second layer.** Once a token is approved to Permit2, the actual spending
  permission lives inside Permit2, and revoking the ERC-20 approval here **does not clear
  it**. That has to be done through the corresponding protocol's own interface.
- **Only the owner can revoke.** Any address can be queried, but revoking requires the
  owner's own wallet signature. No revoke button appears when you query someone else.
- **ERC-20 and ERC-721 share the same `Approval` topic0**, so the event alone can't tell
  them apart — the type is probed via `supportsInterface`. ERC-1155 answers "no" to the
  ERC-721 probe, so it is asked about separately; otherwise it would be treated as an
  ERC-20, queried for an allowance, and left showing nothing but "read failed" — even though
  an ERC-1155 `setApprovalForAll` hands over the whole collection exactly like ERC-721 does.
- **Revoking targets the chain the approval lives on, not whatever you later pick in the
  network dropdown.** Check on Ethereum, then switch the dropdown to Base: the table still
  shows the Ethereum results (changing the dropdown does not re-query), and a wallet on Base
  gets a "Switch network" button rather than a green light — the same address is often an
  entirely different contract on another chain, so the revocation has to land where the
  approval actually exists.
- **After a successful revoke the row's allowance is re-read.** Sending a transaction and the
  approval actually being gone are two different things: a revert, or revoking the wrong
  spender, makes the first true and the second false. The row is re-queried on the spot, so
  you see the new on-chain value rather than just a "Revoked" badge. The transaction hash is
  shown, can be copied, and links straight to the block explorer.
- **A token's self-reported precision is ignored when it isn't credible.** `decimals` is
  whatever the contract claims, and this tool exists to inspect suspicious tokens; absurd
  values are treated as "decimals unreadable" and the raw integer is shown instead of being
  used for conversion.

## The revoke flow

Revoking is a write operation and follows the project's standard sequence: **parameter
preview → wallet signature → confirmation → result**. When no wallet is connected the button
reads "Connect wallet to revoke" (clicking opens the connect modal); when the wallet is on
the wrong network it reads "Switch network". No transaction is ever sent before you confirm.

## Related tools

- [Disperse](../bulk/disperse.md) — check approvals after a batch distribution
- [Sweep](../bulk/bulk-collect.md) — likewise
- [Contract Inspector](./contract-check.md) — find out what the spender contract actually is
- [Security model](../security.md)

---

> Disclaimer: results cover only the pairs you explicitly specified and are not a complete
> assessment of that address's approval exposure.
