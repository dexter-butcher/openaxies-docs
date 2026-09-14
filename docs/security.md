# Security

## Permission system

Risky operations prompt for permission before execution.

### Permission modes

| Mode | Behavior |
|---|---|
| **ask** (default) | Prompts before each risky action |
| **allow_all** | Auto-approves all actions |
| **deny_all** | Blocks all risky actions |

### Setting permission mode

Via config UI (`Ctrl+P`) or config file:

```json
{ "permissionMode": "ask" }
```

### Per-tool permissions

Override permissions for specific tools:

```json
{
  "permissions": {
    "bash": "allow_all",
    "write_file": "ask",
    "delete": "deny_all"
  }
}
```

## Risky operations

These tools require permission by default:
- `bash` — shell command execution
- `write_file` — file creation/modification
- `edit_file` — file editing
- `delete` — file deletion
- `move_file` — file moving
- `replace_in_file` — regex replacement

## Data privacy

### What OpenAxies stores locally

- `~/.openaxies/config.json` — provider, model, key names (not values), permissions
- `~/.openaxies/memory.db` — persistent memory (SQLite)
- `~/.openaxies/skills/` — reusable workflow skills
- `~/.openaxies/sessions/` — chat history

### What never leaves your machine

- Raw API keys (never displayed or transmitted by OpenAxies)
- File contents (only sent to your chosen provider for inference)
- Chat history (stored locally only)
- Memory contents (stored locally only)

### OpenAxies Z (hosted tier)

When using OpenAxies Z:
- Messages are routed through the backend for inference only
- No message content is stored long-term
- API keys live on the server, never exposed to the CLI

### BYO keys (your own provider)

When using your own API keys:
- All API calls go directly to the provider
- No data passes through OpenAxies servers
- Provider's privacy policy applies

## Anti-loop rules

The agent will not:
- Repeat failed tool calls without diagnosis
- Repeatedly search the same query
- Repeatedly read the same large file
- Call multiple equivalent tools without reason

## Destructive operations

Before destructive actions (mass delete, overwrite), the agent will:
1. Determine if the action is actually required
2. Preserve relevant work when possible
3. Ask for confirmation when required by tool policy
