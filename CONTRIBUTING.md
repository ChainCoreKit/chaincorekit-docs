# Contributing

Thanks for helping improve the ChainCore Kit documentation! This repo holds
**documentation only** — not the application source.

[简体中文见下 / Chinese below](#中文)

## Ways to contribute

- **Fix errors** — typos, broken links, outdated screenshots, inaccurate steps.
- **Improve clarity** — better explanations, examples, or Web3 context.
- **Translate** — keep the `en/` and `zh/` trees in sync (see below).

## Repository layout

```
en/            English docs        zh/            Chinese docs (mirror of en/)
  index.md       overview            index.md
  security.md    security model      security.md
  faq.md         FAQ                 faq.md
  glossary.md    glossary            glossary.md
  evm/  btc/  nft/  solana/  polkadot/  bulk/   one file per tool
```

Every tool page exists in **both** `en/` and `zh/` with the **same filename**
(kebab-case, matching the app's route id, e.g. `evm/abi.md`).

## Style rules

1. **Bilingual parity** — if you change a page in one language, update its
   counterpart. A translation-only PR that touches just one side is fine, but
   flag it as `translation`.
2. **Relative links only** between docs (e.g. `../security.md`), so links work
   on GitHub and in any future docs site.
3. **Follow the page template** — see any tool page. Sections:
   *What it's for → Steps → Inputs/Outputs → Notes & gotchas →
   Security (key/mnemonic tools only) → Related tools.*
4. **Neutral examples** — use public sample data (e.g. `vitalik.eth` =
   `0xd8dA…6045`); never label a sample as "my wallet".
5. **Keep technical terms in English**: ABI, ERC-20, Calldata, Wei/Gwei/Ether,
   SS58, PSBT, PDA, etc. Translate the explanation, not the term.
6. **English is meaning-first, not word-for-word** — use industry-standard
   wording (Sweep, Balance Checker, Transaction Tracer, Selector Lookup).
7. **No "open-source" claims about the product** — the application code is not
   published. Describe security as "local-first / keys never leave your device".

## Pull request checklist

- [ ] Both `en/` and `zh/` updated (or PR labelled `translation`).
- [ ] Only relative links between docs.
- [ ] Follows the page template and style rules.
- [ ] `CHANGELOG.md` updated for anything beyond a typo.

---

<a name="中文"></a>

# 参与贡献（中文）

感谢帮助改进 ChainCore Kit 文档！本仓库**仅含文档**，不含应用源代码。

## 贡献方式

- **纠错**：错别字、死链、过期截图、步骤不准确。
- **优化表达**：更好的解释、示例或 Web3 背景补充。
- **翻译**：保持 `en/` 与 `zh/` 两套目录同步。

## 目录结构

每个工具页在 `en/` 与 `zh/` 下**各有一份、文件名相同**（kebab-case，对齐应用 route id，如 `evm/abi.md`）。

## 风格约定

1. **双语对等**：改一侧就同步另一侧；纯翻译 PR 可只动一侧，但请标注 `translation`。
2. **文档互链只用相对路径**（如 `../security.md`）。
3. **遵循页面模板**：什么时候用 → 使用步骤 → 输入/输出 → 注意事项 → 安全提示（仅私钥类）→ 相关工具。
4. **示例用中立样本**（如 vitalik.eth = `0xd8dA…6045`），不要标成「我的钱包」。
5. **术语保留英文**：ABI、ERC-20、Calldata、Wei/Gwei/Ether、SS58、PSBT、PDA 等。
6. **英文意译而非直译**，遵循 Web3 行业术语习惯。
7. **不要把产品/应用代码描述为可公开获取源码**：应用代码未公开，安全卖点用「本地生成 / 私钥不出本机」。

## PR 检查清单

- [ ] `en/` 与 `zh/` 均已更新（或标注 `translation`）。
- [ ] 文档互链仅用相对路径。
- [ ] 符合页面模板与风格约定。
- [ ] 非错别字改动已更新 `CHANGELOG.md`。
