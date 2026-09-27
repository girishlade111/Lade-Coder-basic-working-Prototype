# Lade Coder — Basic Working Prototype

> A **single-file AI website builder** (Lovable/Bolt-style) in pure HTML/CSS/JS. Describe the website you want in plain language, pick a model, and watch it generate a live, previewable page in seconds — then iterate with follow-up chat prompts, undo changes, and download the result as a `.zip`.

This is the **basic working prototype** of Lade Coder (later evolved into `Lade-Coder-Working-Prototype` and the LadeStack no-code builder family). No build step, no dependencies to install — the entire app is one `index.html` that you can open in a browser.

Live demo: https://girishlade111.github.io/Lade-Coder-basic-working-Prototype/

## Features

- **Prompt → website** — type a description ("portfolio site for a photographer") and the app streams back a complete HTML page
- **3 model options**:
  - `Qwen3-Coder` via OpenRouter (streaming) — recommended
  - `Kimi-72B` via OpenRouter (non-streaming)
  - `DialoGPT-medium` via Hugging Face Inference API
- **Live preview + code view** — toggle tabs show the rendered site (sandboxed iframe) or the raw HTML
- **Follow-up chat** — keep refining: "make the navbar sticky", "add dark mode" — the current code is sent as context and the full updated page is regenerated
- **Undo** — history stack with a restore button to roll back to any earlier version
- **Download as .zip** — one-click export of the generated `index.html` (via JSZip)
- Neon glassmorphism UI (Tailwind CDN + Lucide icons)

## How It Works

1. Open the app, choose a model, describe your site, hit **Generate ✨**
2. The model is prompted to return *only* a complete ```` ```html ```` block
3. The app extracts the code, renders it in a sandboxed `<iframe>`, and shows the source in the code tab
4. Use the chat panel to iterate; every generation is pushed onto the history stack
5. Download your final page as `lade-coder.zip`

## Quick Start

No build tools required:

```bash
# Option 1: just open it
open index.html          # or double-click the file

# Option 2: serve it (avoids some file:// quirks)
npx serve .
# → http://localhost:3000
```

Then enter your **own** API key where prompted in the code (see "API keys" below) — or edit the `OPEN_KEY` / `HF_KEY` constants at the top of the `<script>` block.

## Project Structure

```
index.html    # the whole app: UI, chat panel, preview iframe,
              # streaming OpenRouter client, HF inference client,
              # code-history stack, zip export
```

## API Keys

The prototype calls the OpenRouter and Hugging Face APIs directly from the browser, so keys are entered client-side:

- **OpenRouter** (`OPEN_KEY` in `index.html`) — the committed value is redacted; get a free key at https://openrouter.ai/keys and use the `:free` models (`qwen/qwen3-coder:free`, `moonshotai/kimi-dev-72b:free`)
- **Hugging Face** (`HF_KEY` in `index.html`) — used for the DialoGPT option; replace with your own token from https://huggingface.co/settings/tokens, or revoke/rotate it if it's yours and public

## Security Note

This is a *prototype* — API keys are visible to anyone who views the page source. For a production version, proxy API calls through your own backend (e.g. the `Lade-Coder-Working-Prototype` successor) and never ship secret keys in client-side code.

## Deployment

Fully static — deploy by hosting `index.html`:

- **GitHub Pages** — live at https://girishlade111.github.io/Lade-Coder-basic-working-Prototype/ (the `gh-pages` branch contains exactly this repo's root)
- **Any static host** (Cloudflare Pages, Netlify, Vercel) — upload the single file

---

Built by Girish Lade — https://ladestack.in
