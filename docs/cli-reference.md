# CLI Reference

## Commands

| Command | Description |
|---|---|
| `openaxies` | Start the TUI |
| `npx openaxies` | Run without installing |

## Keybindings

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

## Slash commands

Type `/` to open the command palette:

| Command | Description |
|---|---|
| `/help` | Show commands |
| `/model` | Choose model + effort |
| `/mode` | Switch build / plan / ask |
| `/think` | Toggle thinking |
| `/effort` | Set reasoning: low / mid / high |
| `/tier` | Switch hosted / byo |
| `/usage` | Show quota |
| `/clear` | Clear chat |
| `/export` | Export transcript |
| `/history` | List saved chats |
| `/load` | Load a saved chat |
| `/permissions` | Show permission rules |
| `/setup` | Re-run setup |
| `/quit` | Exit |

## Status bar

```
› _
build · ollama · streaming
```

Shows: mode, provider, status (streaming/idle).

## Thinking display

When thinking is enabled:

```
── reasoning ──
I'll analyze the codebase structure first...
```

## Tool display

```
● read_file src/app.js
⎿  435 lines

● bash npm test
⎿  all tests passed
```

## Error display

```
✗ Permission denied
  You denied the operation.
```
