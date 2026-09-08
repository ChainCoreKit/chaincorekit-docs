**English** · [简体中文](../../zh/ai/corbit.md) · [← Docs home](../index.md)

# Corbit AI assistant

> The built-in AI assistant. It runs on **your own** OpenAI-compatible endpoint and API key, straight from the browser.

## When to use it

- A piece of calldata, an error, or an ABI field doesn't make sense and you want to ask right there.
- You want the current tool explained without leaving the page to search.
- You already have a key from OpenAI / DeepSeek / Moonshot / Alibaba Bailian and don't want yet another account.

Corbit ships **no model and no quota of its own** — it's a client, and usage bills to your key.

## Setup

1. Open Corbit from the floating button, then open its settings.
2. Enter the **API endpoint**. A bare domain works — `/v1` is appended automatically. Endpoints with unusual paths (Azure, for example) need the full URL.
3. Enter your **API key**.
4. Fetch the model list and pick one, or type a model name directly.

| Provider | Example endpoint |
| --- | --- |
| OpenAI | `https://api.openai.com/v1` |
| DeepSeek | `https://api.deepseek.com/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| Alibaba Bailian | `https://dashscope.aliyuncs.com/compatible-mode/v1` |

## Where your key lives

- **Only in your own browser** (localStorage). Never uploaded, never synced.
- Requests go **straight from your browser to the endpoint you configured** — no server of this project is involved.
- Switching devices means entering it again. That's deliberate: keys are not synced across devices.

> This applies to Corbit only. Wallet, mnemonic and private-key tools compute entirely locally, network or not.

## One exception: the secure relay

Some endpoints don't permit cross-origin browser calls, and **only the endpoint itself can lift that restriction** — no amount of frontend code gets around it. When Corbit hits one, it automatically retries through a secure relay; usually all you notice is a normal reply plus a "Via secure relay" line under the input box.

Your key passes through that relay for that request only — not stored, not logged. **Don't skip past that line**: the product promise is "your key stays between your browser and your endpoint", and while relaying that isn't fully true, so you're told.

Major providers (OpenAI, DeepSeek, Moonshot, Bailian) all support direct connections and never trigger the relay.

See [endpoint CORS setup](./corbit-cors.md) for details.

## Notes

- **It will get things wrong.** Verify addresses, amounts and networks yourself before any on-chain action — never sign straight from an AI answer.
- **Never paste a private key or mnemonic into it.** That would send them to your endpoint (and possibly the relay) along with the conversation. There is never a reason to do this.
- Conversations are not persisted; refreshing the page clears them.

## Related

- [Endpoint CORS setup](./corbit-cors.md) — read this when an endpoint won't connect
- [Security model](../security.md) — the data boundaries across the site

---

> Disclaimer: AI output is for reference only and is not operational advice. Verifying and signing transactions remains your responsibility.
