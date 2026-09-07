**English** · [简体中文](../../zh/evm/create2-merkle.md) · [← Overview](../index.md)

# Address Prediction & Merkle · EVM

> Compute a contract address before deploying, and build a Merkle root and proofs for an
> airdrop allowlist with an explicitly chosen leaf encoding. All computed locally.

## When to use it

- You want to know where a contract will land before deploying it (to pre-fund it, or to
  hard-code it elsewhere).
- You're doing a same-address deployment across chains with a CREATE2 factory and need to
  confirm the salt and initCode.
- You're running an airdrop and need a Merkle root for the contract plus a proof per address.

## Contract address prediction

### CREATE

The address depends only on the **deployer and that account's nonce** — never on the
contract's contents. So you can predict your next deployment address, but any transaction in
between changes the nonce and therefore the address.

### CREATE2

The address depends on the **factory, the salt and the initCode hash**, and not on any nonce.
That's exactly how same-address deployment across chains works: match all three and the
address matches.

> **initCode is not runtime bytecode.** This is the most common mistake: initCode is the
> constructor bytecode plus encoded constructor arguments, whereas runtime bytecode is what
> ends up stored on chain after deployment. Pass the wrong one and the address will never match.

> Being able to compute the address doesn't mean deployment will succeed on that chain — the
> factory has to exist, and the salt must not already be used.

## Salt miner

To get a contract address with a chosen prefix or suffix (say `0x0000…`), enter the factory
address and initCode here, give the hex pattern you want, and the browser tries salts locally.

**A salt is nothing like a vanity wallet.** Vanity search looks for a private key — finding one
means holding the assets. A salt is a public deployment parameter: anyone with the same factory
and initCode can recompute the exact same result. Mining a nice-looking salt involves no secret
at all, which is why the search starts from 0 and needs no secure randomness.

**Difficulty: each extra hex character multiplies the expected attempts by 16.**

| Total pattern length | Expected attempts |
| --- | --- |
| 4 chars | ~65 thousand |
| 5 chars | ~1.05 million |
| 6 chars | ~16.8 million |
| 8 chars | ~4.3 billion |

4–5 characters are practical in a browser, 6 takes a while, and beyond that you want a GPU tool.
The page shows the expected attempt count and the live rate up front so you can decide whether
it's worth the wait.

You can **stop** at any point, and leaving the page stops the search automatically (otherwise it
would keep burning CPU in the background) — you'll need to restart when you come back.

## Merkle allowlist

### The leaf encoding must be chosen explicitly

This is the most important point on the page. Two conventions are in common use, and **the
same data yields completely different roots** under them:

| Scheme | Leaf hash | Seen in |
| --- | --- | --- |
| **OpenZeppelin StandardMerkleTree** | `keccak(keccak(abi.encode(values)))` — **double hashing** | The usage paired with OZ's `MerkleProof` |
| **merkletreejs (encodePacked)** | `keccak(abi.encodePacked(values))` — **single hashing** | Older tutorials and sample code |

Most online Merkle tools **never tell you which one they use**, so the root you compute
silently fails to match the one your contract verifies against — while both look perfectly
normal. That's why the choice is mandatory here and shown alongside the result.

The "sort leaves" and "sort pairs" switches change the root as well; they have to match your
contract's implementation.

### Export

The exported CSV **carries the construction settings** (encoding, column types, both sort
switches, root), because root and proofs alone are not enough for anyone else to reproduce
the same tree.

## Notes & gotchas

- **A wrong root means the airdrop contract rejects everyone** — and a wrong root looks
  exactly like a correct one. Verify with a couple of addresses on a testnet before going live.
- **Column types must match the contract's `abi.encode` order**; one column more or fewer
  yields a different root.
- This tool only produces the root and proofs — it **does not create a claim contract**.
  Eligibility proof and actual distribution are two separate things.

## Related tools

- [Contract Inspector](./contract-check.md) — confirm the address and implementation after deploying
- [ABI Codec](./abi-codec.md) — encode constructor arguments
- [Hash Tool](./hash-tool.md) — keccak-256

---

> Disclaimer: predicted addresses and Merkle output are computed locally; verify before
> sending anything on chain.
