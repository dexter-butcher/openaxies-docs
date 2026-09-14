# Providers

OpenAxies supports 9 AI providers. OpenAxies Z is free and requires no setup.

## Provider List

| Provider | Env Variable | Free? | Models |
|---|---|---|---|
| **OpenAxies Z** | none needed | Yes | Hosted models via backend |
| **Groq** | `OPENAXIES_GROQ_KEY` | Yes | GPT-OSS 120B/20B, Qwen3 32B, Llama 3.3 70B |
| **Google Gemini** | `OPENAXIES_GOOGLE_KEY` | Yes | Gemini 3.5 Flash, 2.5 Flash, 2.5 Pro |
| **Claude** | `OPENAXIES_ANTHROPIC_KEY` | No | Sonnet 4.6, Opus 4.8, Haiku 4.5 |
| **DeepSeek** | `OPENAXIES_DEEPSEEK_KEY` | No | V4 Flash, V4 Pro |
| **OpenAI** | `OPENAXIES_OPENAI_KEY` | No | GPT-4o, o3, o4-mini |
| **Mistral** | `OPENAXIES_MISTRAL_KEY` | No | Mistral Large, Codestral |
| **xAI Grok** | `OPENAXIES_XAI_KEY` | No | Grok 4.3 |
| **OpenRouter** | `OPENAXIES_OPENROUTER_KEY` | No | 300+ models |
| **Ollama** | none needed | Yes (local) | Any local model |

## Setting API keys

### Environment variable

```bash
export OPENAXIES_GROQ_KEY=gsk_your_key_here
```

### Named keys (interactive)

Press `Ctrl+P` → select provider → "Add API Key" → enter a name and key.

Keys are stored in `~/.openaxies/config.json` with names — never displayed as raw values.

### Multiple keys per provider

Add multiple named keys for automatic rotation:

```json
{
  "apiKeys": {
    "groq": [
      { "name": "Work Key", "key": "gsk_..." },
      { "name": "Backup", "key": "gsk_..." }
    ]
  }
}
```

## Smart routing

When a request fails, OpenAxies automatically:

| Error | Action |
|---|---|
| **413** (request too large) | Compact conversation history, retry |
| **404** (model not found) | Try fallback model, then fallback provider |
| **429** (rate limited) | Rotate to next key, then fallback provider |
| **401/403** (auth error) | Skip key, try next |
| **Model cooldown** | Failed models get 30s cooldown |

## Fallback chains

Each provider has a fallback chain:

- Groq → Gemini → DeepSeek → OpenAI
- Claude → OpenAI → Groq
- DeepSeek → Groq → Gemini

## Key health

Key health is tracked automatically:
- **healthy** — working normally
- **cooling** — rate limited, cooling down (30s)
- **failures** — consecutive failures count

Health status visible in `Ctrl+P` config UI.

## OpenRouter

OpenRouter provides 300+ models through a single API key. Three selection modes:

- **Auto Route** — OpenRouter picks the best model
- **Curated Models** — pick from curated list
- **Custom Model ID** — type any OpenRouter model ID

## Ollama

Ollama runs locally with no API key needed. Start Ollama first:

```bash
ollama serve
```

Then select Ollama in OpenAxies config. Supports any model you've pulled.
