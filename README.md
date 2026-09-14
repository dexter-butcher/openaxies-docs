# OpenAxies

An autonomous coding agent for your terminal.

## Install

```bash
npm install -g openaxies
openaxies
```

Or run without installing:

```bash
npx openaxies
```

**Requirements:** Node.js >= 18

## Quick Start

```bash
openaxies
```

Select **OpenAxies Z** as provider — free, no API key needed.

Or use your own key:

```bash
export OPENAXIES_GROQ_KEY=gsk_your_key_here
openaxies
```

Press `Ctrl+P` to add API keys interactively.

## Providers

| Provider | Free? |
|---|---|
| OpenAxies Z | Yes |
| Groq | Yes |
| Google Gemini | Yes |
| Claude | No |
| DeepSeek | No |
| OpenAI | No |
| Mistral | No |
| xAI Grok | No |
| OpenRouter | No |
| Ollama | Yes (local) |

## Key Bindings

| Key | Action |
|---|---|
| `Enter` | Send message |
| `Ctrl+P` | Provider/model config |
| `Ctrl+R` | Resend last message |
| `Ctrl+L` | Clear conversation |
| `Tab` | Toggle mode (build/plan) |
| `Esc` | Cancel request |
| `/` | Command palette |

## Modes

- **build** — full tool access (read, write, execute, search)
- **plan** — read-only tools

## Safety

Risky operations prompt for permission:

- **ask** (default) — prompts before each action
- **allow_all** — auto-approves
- **deny_all** — blocks all

## License

Proprietary. All rights reserved. See [LICENSE](./LICENSE).
