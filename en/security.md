**English** · [简体中文](../zh/security.md) · [← Overview](./index.md)

# Security model

ChainCore Kit is **local-first**: every operation involving a private key or
mnemonic happens inside your browser.

## Keys never leave your device

- Mnemonic/key generation, wallet derivation, and transaction signing all run in
  your browser's **local memory**.
- This sensitive data is **never uploaded, stored, or sent off your device**, and
  is never written to localStorage.
- After you close or refresh the page, keys/mnemonics generated in that session
  are gone from memory and cannot be recovered — so export or write them down
  first.

## Results are masked by default

- Keys/mnemonics in results are masked; click the eye icon to reveal.
- View and save them only in a **safe environment** (no shoulder-surfing, screen
  recording, or remote sessions).
- QR codes are generated for **addresses only** and are safe for receiving test
  coins. **Never** generate a QR code of a private key.

## Risk of exporting files with keys

- Exporting a "table with private keys" writes a **plaintext** file of keys and
  mnemonics.
- Anyone who obtains that file gains **full control** of those wallets.
- Do it only in a safe environment, store it carefully, and delete it promptly.

## Safe flow for write operations

Write operations (transfers, contract write functions, deployments) follow a
fixed flow — no step is skipped:

**Preview params → estimate gas → user confirm → wallet signs → pending → result**

- When no wallet is connected, write buttons read "Connect wallet to continue"
  and never fire silently.
- High-risk actions (`transferOwnership`, `selfdestruct`, upgrades) require an
  extra confirmation.
- Before signing, verify the three essentials: **address, amount, network**.

## Vanity addresses: the 2022 Profanity incident

If your vanity address (for example one starting with `0x0000…`) was generated with the `profanity` tool **before September 2022**, treat it as **compromised and move the funds now**.

- That tool seeded its random number generator with only 32 bits, collapsing the effective private-key space from 2²⁵⁶ to roughly 2³².
- The consequence is that **the private key can be recovered from the public address**. The flaw was exploited at scale in September 2022 and several vanity addresses were drained.
- What matters is **which tool generated it and when** — not how the address looks. The same prefix produced by a sound generator carries no such weakness.

ChainCore Kit's vanity search and wallet generation always draw a full 256 bits of entropy from the browser's cryptographically secure random source (`crypto.getRandomValues`), with no truncation. In environments where that source is unavailable, generation is refused outright rather than falling back to weak randomness.

## Recommendations

- Rehearse on a **testnet** (e.g. Sepolia) before mainnet.
- Validate the flow with a small amount before any large operation.
- Be cautious with contract ABIs from unknown or unverified sources.
- For collision-generated addresses (e.g. vanity), safety depends on the tool and
  environment that produced them — generate locally and store offline (see the
  Profanity incident above).

## Related

- [FAQ](./faq.md)
- [Glossary](./glossary.md)

---

> Disclaimer: provided "as is", without warranty or investment advice. Losses
> from lost keys or mistaken transactions are irreversible; you bear the risk.
