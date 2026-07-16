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

## Recommendations

- Rehearse on a **testnet** (e.g. Sepolia) before mainnet.
- Validate the flow with a small amount before any large operation.
- Be cautious with contract ABIs from unknown or unverified sources.
- For collision-generated addresses (e.g. vanity), key safety depends on the
  generation environment — generate locally and store offline.

## Related

- [FAQ](./faq.md)
- [Glossary](./glossary.md)

---

> Disclaimer: provided "as is", without warranty or investment advice. Losses
> from lost keys or mistaken transactions are irreversible; you bear the risk.
