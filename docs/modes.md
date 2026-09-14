# Modes

OpenAxies has three operating modes.

## Build mode (default)

Full tool access. The agent can:
- Read, write, edit, delete files
- Execute shell commands
- Search the web
- Save memories and skills
- Create and manage todos

```json
{ "mode": "build" }
```

## Plan mode

Read-only. The agent can:
- Inspect files and directories
- Search codebases
- Analyze and reason
- Build a plan

The agent MUST NOT:
- Write or edit files
- Delete files
- Execute commands
- Modify memory or skills

```json
{ "mode": "plan" }
```

Use plan mode when you want the agent to analyze without making changes.

## Ask mode

No tools. The agent can only:
- Answer questions
- Have conversations
- Provide explanations

No file operations, no search, no execution.

## Switching modes

- Press `Tab` to toggle between build and plan
- Use `/mode` command to switch explicitly
- Change in config UI (`Ctrl+P`)

## When to use each mode

| Mode | Use when |
|---|---|
| **build** | Default. You want the agent to work autonomously |
| **plan** | You want analysis without changes (code review, architecture) |
| **ask** | You want conversation only (explanations, brainstorming) |
