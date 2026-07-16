# Security Policy

This repository holds **documentation only**. There are two kinds of security
concerns, handled differently.

## 1. Security issues in the documentation

If a doc page gives **dangerous or misleading guidance** — for example, telling
users to paste a private key somewhere unsafe, generate a QR code of a secret,
or trust an unverified contract — please report it:

- Open a GitHub issue using the **Documentation issue** template, **or**
- If you consider it sensitive, contact the maintainer privately via GitHub.

We treat "docs that could cause users to lose funds" as high priority.

## 2. Security issues in the ChainCore Kit application

The application source is **not** in this repository. For vulnerabilities in
the app itself (e.g. a page leaking a key, a bad signing flow), please use the
**in-app feedback channel** rather than a public issue here, so the report is
not disclosed before a fix is available.

## Please do NOT

- Post real private keys, mnemonics, or seed phrases in issues or PRs.
- Include real funds' transaction data that could deanonymize a user.

Use neutral, public sample data (e.g. `vitalik.eth` = `0xd8dA…6045`) in any
example.

## Golden rules for users (reminder)

- Keys and mnemonics should **never leave your device**. No legitimate tool
  asks you to upload them.
- Always verify **address, amount, and network** before signing.
- Lost keys and mistaken transactions are **irreversible**.
