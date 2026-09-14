# Configuration

Config file: `~/.openaxies/config.json`

## Config options

```json
{
  "provider": "openaxies",
  "model": "llama-3.1-8b-instant",
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

## Fields

| Field | Type | Description |
|---|---|---|
| `provider` | string | Active provider (openaxies, groq, google, claude, deepseek, openai, mistral, xai, openrouter, ollama) |
| `model` | string | Active model ID |
| `apiKeys` | object | Named API keys per provider |
| `keyHealth` | object | Key health status (auto-managed) |
| `permissionMode` | string | ask, allow_all, or deny_all |
| `permissions` | object | Per-tool permission overrides |
| `thinking` | object | Thinking/reasoning config |

## Config UI

Press `Ctrl+P` to open the config panel:

- **Provider** — switch between providers
- **Model** — select model from list
- **API Keys** — add/remove named keys
- **Thinking** — configure reasoning options
- **Mode** — switch build/plan

Changes persist automatically to `~/.openaxies/config.json`.

## Thinking configuration

Different providers use different thinking parameters:

| Provider | Parameter | Options |
|---|---|---|
| Groq | `reasoning_effort` | low / medium / high |
| Gemini | `thinkingLevel` | minimal / low / medium / high |
| DeepSeek | `thinking` + `effort` | on/off + high/max |
| Claude | `effort` | low / medium / high / xhigh / max |
| OpenAI | `reasoning_effort` | low / medium / high |
| xAI | `thinking` toggle | on / off |

## Data storage

All data stored locally at `~/.openaxies/`:

```
~/.openaxies/
├── config.json          # Provider, model, keys, permissions
├── memory.db            # SQLite persistent memory
├── skills/              # Reusable workflow skills
├── sessions/            # Chat history
└── auth.json            # Auth tokens (if any)
```

## Environment variables

| Variable | Description |
|---|---|
| `OPENAXIES_GROQ_KEY` | Groq API key |
| `OPENAXIES_GOOGLE_KEY` | Google Gemini API key |
| `OPENAXIES_ANTHROPIC_KEY` | Claude API key |
| `OPENAXIES_DEEPSEEK_KEY` | DeepSeek API key |
| `OPENAXIES_OPENAI_KEY` | OpenAI API key |
| `OPENAXIES_MISTRAL_KEY` | Mistral API key |
| `OPENAXIES_XAI_KEY` | xAI API key |
| `OPENAXIES_OPENROUTER_KEY` | OpenRouter API key |
| `OPENAXIES_WEBSEARCH_KEY` | Web search API key (SerpAPI) |
