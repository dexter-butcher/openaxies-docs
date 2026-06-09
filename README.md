# OpenAxies

An autonomous coding agent that runs in your terminal. Understands codebases, writes files, runs commands, searches the web, and iterates on tasks through a chat interface — using your own API keys, on your machine.

**8 providers supported:** Groq, Google Gemini, Claude (Anthropic), DeepSeek, OpenAI, Mistral, xAI Grok, OpenRouter.

## Installation

```bash
npm install -g openaxies
openaxies
```

Or run without installing:

```bash
npx openaxies
```

**Requirements:** Node.js >= 18, a terminal with ANSI color support.

## Quick Start

### 1. Set an API key

Export an env var for at least one provider:

```bash
# Groq (fast, free tier available)
export OPENAXIES_GROQ_KEY=gsk_your_key_here

# Or Google Gemini (free tier available)
export OPENAXIES_GOOGLE_KEY=your_gemini_key_here
```

Or use the config UI (`Ctrl+P`) to add named API keys interactively — keys are stored by name in `~/.openaxies/config.json`, never displayed as raw values.

### 2. Run

```bash
openaxies
```

Press **Enter** to start chatting. Try "explore this project" or "fix the bug in src/main.js".

## Providers

All 8 providers. Keys are loaded from environment variables (`OPENAXIES_*`) or from named entries in `~/.openaxies/config.json`. When both exist, user keys are tried first, then global env var keys as fallback.

| Provider | Env Variable | Key Required |
|---|---|---|
| **Groq** | `OPENAXIES_GROQ_KEY` | Free tier |
| **Google Gemini** | `OPENAXIES_GOOGLE_KEY` | Free tier |
| **Claude (Anthropic)** | `OPENAXIES_ANTHROPIC_KEY` | Paid |
| **DeepSeek** | `OPENAXIES_DEEPSEEK_KEY` | Paid |
| **OpenAI** | `OPENAXIES_OPENAI_KEY` | Paid |
| **Mistral** | `OPENAXIES_MISTRAL_KEY` | Paid |
| **xAI Grok** | `OPENAXIES_XAI_KEY` | Paid |
| **OpenRouter** | `OPENAXIES_OPENROUTER_KEY` | Paid |

Global fallback keys (`OPENAXIES_GROQ_KEY`, `OPENAXIES_GOOGLE_KEY`) are creator-provided by default. All other providers require you to add your own key.

Multiple keys per provider are supported — round-robin'd with automatic cooldown on rate limits (429) and auth errors (401/403). Transient errors (timeout, 500) do NOT trigger cooldown.

## Named API Keys

Keys are stored with user-defined names in `~/.openaxies/config.json`:

```json
{
  "apiKeys": {
    "groq": [
      { "name": "Work Key", "key": "gsk_...", "addedAt": 1717000000000 },
      { "name": "Backup", "key": "gsk_...", "addedAt": 1717000000001 }
    ]
  }
}
```

The config UI shows key names with health status (healthy/cooling/failures) — **never the raw key value**.

## Smart Routing

When a request fails, OpenAxies automatically recovers:

| Error | Action |
|---|---|
| **413** (request too large) | Compact conversation history, retry |
| **404** (model not found) | Try fallback model, then fallback provider |
| **429** (rate limited) | Rotate to next key, then fallback provider |
| **Model cooldown** | Failed models get 30s cooldown before retry |

Fallback chains per provider (e.g. Groq → Google → DeepSeek → OpenAI).

## Thinking Models

Models with reasoning/thinking show a "Thinking" config screen on selection:

| Provider | Model | Type | Options |
|---|---|---|---|
| **Groq** | GPT-OSS 120B/20B | `reasoning_effort` | low / medium / high |
| **Groq** | Qwen3 32B | `reasoning_effort` | none / default |
| **Gemini** | 2.5 Flash/Pro | `thinkingBudget` | tokens (0=off, -1=dynamic) |
| **Gemini** | 3.5 Flash | `thinkingLevel` | minimal / low / medium / high |
| **DeepSeek** | V4 Flash | `thinking` toggle | enabled / disabled |
| **DeepSeek** | V4 Pro | `toggle + effort` | disabled / high / max |
| **Claude** | Sonnet 4.6 / Opus 4.8 | `effort` | low / medium / high / xhigh / max |
| **Claude** | Haiku 4.5 | `budget_tokens` | 1K / 4K / 8K / 16K / 32K |
| **OpenAI** | o3 / o4-mini | `reasoning_effort` | low / medium / high |
| **xAI Grok** | Grok 4.3 | toggle | enabled / disabled |

## OpenRouter

OpenRouter provides 300+ models through a single API. Three selection modes:

- **Auto Route** — OpenRouter picks the best model for your task
- **Curated Models** — pick from a curated list (GPT-4o, Claude Sonnet 4.6, DeepSeek V4 Pro, Gemini 2.5 Pro, etc.)
- **Custom Model ID** — type any OpenRouter model ID (e.g. `nousresearch/hermes-4`)

## Key Bindings

| Key | Action |
|---|---|
| `Enter` | Send message |
| `Ctrl+P` | Open provider/model config |
| `Ctrl+R` | Resend last message |
| `Ctrl+L` | Clear conversation |
| `Ctrl+Z` | Rollback last checkpoint |
| `Tab` | Toggle mode (build/plan) |
| `Esc` | Cancel running request |
| `↑/↓` | Scroll chat history |
| `PgUp/PgDn` | Scroll faster |
| `/` | Command palette |

## Modes

- **build** (default) — full tool access (read, write, execute, search)
- **plan** — read-only tools (no writes or execution)

## Safety

Risky operations (bash, write_file, edit_file, etc.) prompt for permission:

- **`ask`** (default) — prompts before each risky action
- **`allow_all`** — automatically approves all actions
- **`deny_all`** — blocks all risky actions

Set via config UI or `~/.openaxies/config.json`:
```json
{ "permissionMode": "ask" }
```

## Configuration File

`~/.openaxies/config.json`:

```json
{
  "provider": "groq",
  "model": "llama-3.3-70b-versatile",
  "apiKeys": {},
  "keyHealth": {},
  "permissionMode": "ask",
  "permissions": {},
  "thinking": {
    "effort": "medium",
    "budget": 0,
    "level": "medium",
    "toggle": "disabled"
  }
}
```

## Data & Privacy

- All API calls go directly to your chosen provider's API
- No data is sent to third-party proxies
- Configuration and key names stored locally in `~/.openaxies/`
- Raw API keys are **never** displayed in the UI or logs

## Troubleshooting

**"No API keys found":**
Set an env var from the Providers table above, or press `Ctrl+P` → select provider → add a named key.

**"All keys exhausted":**
All your keys for a provider are failing. Check they're valid and have quota. Try a different provider.

**Terminal shows garbled output:**
Use a terminal with ANSI support (Windows Terminal, VS Code terminal, GNOME Terminal, etc.).

## License

MIT
