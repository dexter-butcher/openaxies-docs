# Troubleshooting

## "No API keys found"

Set an env var or press `Ctrl+P` → select provider → add a named key.

```bash
export OPENAXIES_GROQ_KEY=gsk_your_key_here
```

## "All keys exhausted"

All keys for a provider are failing. Check they're valid and have quota. Try a different provider.

## Terminal shows garbled output

Use a terminal with ANSI support:
- Windows Terminal
- VS Code terminal
- GNOME Terminal
- Termux (Android)

## Provider returns 401/403

API key is invalid or expired. Press `Ctrl+P` → manage keys → update the key.

## Provider returns 429

Rate limited. OpenAxies will automatically:
1. Rotate to next key
2. Wait for cooldown (30s)
3. Try fallback provider

## Provider returns 404

Model not found. The model ID may have changed. Press `Ctrl+P` → select a different model.

## "Request too large" (413)

Conversation is too long. OpenAxies will automatically compact history. If it persists, start a new chat with `/clear`.

## Streaming stops mid-response

Press `Esc` to cancel, then resend with `Ctrl+R`.

## Tools not appearing

Make sure you're in **build** mode, not **plan** or **ask**. Press `Tab` to switch.

## Thinking not showing

Not all models support thinking. Check the [Providers](providers.md) page for supported models.

## Memory not persisting

Check that `~/.openaxies/memory.db` exists and is writable.

## Skills not found

Skills are stored at `~/.openaxies/skills/`. Create one with the `create_skill` tool.

## Config not saving

Check that `~/.openaxies/config.json` is writable. Config saves automatically on every change.

## Ollama connection error

Make sure Ollama is running:

```bash
ollama serve
```

Then verify with:

```bash
curl http://localhost:11434/api/tags
```

## Web search not working

Set the web search API key:

```bash
export OPENAXIES_WEBSEARCH_KEY=your_serpapi_key
```

## Crashes on startup

Try clearing config:

```bash
rm ~/.openaxies/config.json
openaxies
```
