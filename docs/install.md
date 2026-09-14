# Installation

## Requirements

- Node.js >= 18
- A terminal with ANSI color support (Windows Terminal, VS Code terminal, GNOME Terminal, Termux)

## Install from npm

```bash
npm install -g openaxies
```

## Run without installing

```bash
npx openaxies
```

## First run

```bash
openaxies
```

On first run, OpenAxies will:
1. Create config directory at `~/.openaxies/`
2. Initialize SQLite memory database at `~/.openaxies/memory.db`
3. Create skills directory at `~/.openaxies/skills/`
4. Show the splash screen with provider selection

## Quick setup

1. Select a provider (OpenAxies Z is free, no key needed)
2. Press `Enter` to start chatting
3. Type your request and press `Enter`

## Android / Termux

```bash
pkg install nodejs
npm install -g openaxies
node $(which openaxies)
```

Note: On Android, `chmod +x` may not work on FUSE storage. Run as `node bin/xenos` instead.

## Update

```bash
npm install -g openaxies@latest
```

## Uninstall

```bash
npm uninstall -g openaxies
```

Config and memory are stored at `~/.openaxies/` — delete manually if needed.
