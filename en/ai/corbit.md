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

- **In memory by default**: closing or reloading the page means entering it again.
- Only if you tick "Remember key" is it saved to this browser's local storage (in plain text). It isn't synced to other devices; clear it any time with "Clear key" in settings.
- The key is only sent with each request to the endpoint you configured, for authentication (and through the secure relay when that is in use — see the next section). It goes nowhere else.
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
- **Chat history is kept locally in this browser** (the latest 50 messages), so it survives a reload, and it isn't synced to other devices. Use "Clear chat history" in settings to delete it. Note: **each time you ask, the earlier conversation is sent along as context to the model endpoint you configured** (and through the secure relay when that is in use). Messages that look like keys or mnemonics are not saved (see below), but they are still sent with the request they were typed in — so don't paste them.
- **Ticking "Remember key" stores it in plain text in this browser**: browser extensions that can read this site's storage, or anyone else using the computer, could get it. Only tick it on a personal device, and clear it in settings when you're done.
- **Messages containing keys or mnemonics are not saved to chat history**: besides EVM keys and mnemonics, this covers BTC WIF keys, extended private keys (xprv and friends), Solana secret keys and keypair arrays, and Polkadot seeds. Such a message simply won't be there after a reload.
- **Images in replies are shown as text**: they're never loaded, so a link to an external image can't carry your conversation out.

## Related

- [Endpoint CORS setup](./corbit-cors.md) — read this when an endpoint won't connect
- [Security model](../security.md) — the data boundaries across the site

---

> Disclaimer: AI output is for reference only and is not operational advice. Verifying and signing transactions remains your responsibility.
