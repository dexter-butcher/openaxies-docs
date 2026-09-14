# OpenAxies

An autonomous coding agent for your terminal. Understands codebases, writes files, runs commands, searches the web, and iterates on tasks through a chat interface.

**9 providers supported.** OpenAxies Z (free, no key needed), Groq, Google Gemini, Claude, DeepSeek, OpenAI, Mistral, xAI Grok, OpenRouter, Ollama.

## Quick Start

```bash
npm install -g openaxies
openaxies
```

Select **OpenAxies Z** as provider — zero setup, no API key required.

## Documentation

- [Installation](docs/install.md) — Install and first run
- [Providers](docs/providers.md) — All 9 providers and API key setup
- [Configuration](docs/configuration.md) — Config file, options, named keys
- [Tools](docs/tools.md) — 38 built-in tools reference
- [Modes](docs/modes.md) — Build, Plan, and Ask modes
- [CLI Reference](docs/cli-reference.md) — Commands, keybindings, slash commands
- [Security](docs/security.md) — Permissions, safety, data privacy
- [Troubleshooting](docs/troubleshooting.md) — Common issues and fixes

## Features

- **Streaming** — Tokens appear as they arrive, not buffered
- **Tool calling** — 38 tools: filesystem, search, execution, memory, skills, web search
- **Thinking models** — Reasoning display for Groq, Gemini, DeepSeek, Claude, OpenAI, xAI
- **Persistent memory** — SQLite-backed, survives restarts
- **Reusable skills** — Save and execute workflows
- **Permission system** — Ask, allow_all, deny_all for risky operations
- **Multi-key rotation** — Automatic fallback with cooldown on rate limits
- **Session management** — Save, load, browse chat history

## License

Proprietary. All rights reserved. See [LICENSE](./LICENSE).
