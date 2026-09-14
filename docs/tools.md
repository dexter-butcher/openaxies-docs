# Tools

OpenAxies has 38 built-in tools organized into 6 categories.

## Filesystem (14 tools)

| Tool | Description |
|---|---|
| `read_file` | Read a file from the filesystem |
| `write_file` | Write content to a file (creates directories) |
| `edit_file` | Replace exact text in a file |
| `delete` | Delete a file or empty directory |
| `mkdir` | Create a directory and parents |
| `move_file` | Move or rename a file |
| `copy_file` | Copy a file |
| `list_dir` | List directory contents with sizes |
| `file_info` | Get file metadata |
| `head_file` | Read first N lines (default 20) |
| `tail_file` | Read last N lines (default 20) |
| `append_file` | Append content to a file |
| `replace_in_file` | Regex replace all occurrences |
| `diff_files` | Compare two files line by line |

## Search (4 tools)

| Tool | Description |
|---|---|
| `grep` | Search file contents with regex |
| `glob` | Find files by glob pattern |
| `search_files` | Regex + glob combo search |
| `search_workspace` | Combined grep + glob |

## Execution (4 tools)

| Tool | Description |
|---|---|
| `bash` | Execute a shell command |
| `run_command` | Alias for bash |
| `build` | Run project build command |
| `test` | Run project test command |

## User Interaction (2 tools)

| Tool | Description |
|---|---|
| `ask_question` | Ask the user a question |
| `confirm` | Confirm a destructive action |

## Memory (5 tools)

| Tool | Description |
|---|---|
| `save_memory` | Store a key-value pair |
| `recall_memory` | Retrieve by key |
| `update_memory` | Update existing memory |
| `search_memory` | Search all memories |
| `delete_memory` | Remove by key |

## Skills (4 tools)

| Tool | Description |
|---|---|
| `create_skill` | Create a reusable workflow |
| `update_skill` | Update skill definition |
| `execute_skill` | Run a saved skill |
| `search_skills` | Find relevant skills |

## Other (5 tools)

| Tool | Description |
|---|---|
| `web_search` | Search the web for current information |
| `read_multiple_files` | Read several files at once |
| `todo_add` | Add a task to the todo list |
| `todo_done` | Mark a todo as complete |

## Tool selection policy

OpenAxies uses minimum effective tools. The hierarchy:

```
DISCOVERY → search_workspace, grep, glob
    ↓
TARGETED INSPECTION → file_info, head_file, read_file
    ↓
MODIFICATION → edit_file, write_file, move_file
    ↓
EXECUTION → build, test, bash
    ↓
VERIFICATION → read_file, diff_files, test
```

Prefer narrower tools over broader ones. Don't use `bash` when `read_file` works.

## Tool deduplication

Equivalent tools — pick one:

- `bash` ≈ `run_command`
- `grep` ≈ `search_files` ≈ `search_workspace`
- `read_file` ≈ `head_file` ≈ `tail_file`

Don't call multiple equivalent tools for the same thing.
