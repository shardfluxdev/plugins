---
name: shardflux-workspaces
description: Run commands, servers, builds, tests and a browser in a persistent Shardflux cloud workspace instead of on this machine. Use when the user asks to run something in the cloud, in a sandbox, in their Shardflux workspace, or on a computer that keeps its state between sessions; when a task needs Linux, Python, Node.js, Chromium or a long-running process; or when work should be isolated from the local machine.
---

# Shardflux workspaces

A Shardflux workspace is a persistent Linux computer in the cloud: files, installed packages and running processes stay
as they are between tool calls and between sessions. The `shardflux` MCP server in this plugin exposes it as tools.
Every workspace tool takes a `workspace_key`; the same key always reaches the same workspace.

## Workflow

1. **Pick one key per project and reuse it.** Use a stable, readable key such as `<project>` or `<user>/<project>`.
   Reusing the key brings back the same files and processes; a new key is a new computer.
2. **Open it.** Call `workspace_open` with `workspace_key` (the default template is `python-node-browser`: Ubuntu with
   Python, Node.js and Chromium). The first call creates the workspace; later calls reconnect or resume it and never
   reset it.
3. **Work in it.**
   - `exec` runs a shell command (`bash -lc`) and returns its output. Pass an absolute `cwd`; the home directory is
     `/home/user`.
   - For a dev server, a watcher or a job longer than a minute, run `exec` with `background: true`, then follow it
     with `exec_read` (by `session_id` and the offsets it returns) and stop it with `exec_cancel`.
   - `read_file`, `write_file`, `edit_file` (exact `old_text` → `new_text` edits), `list_files` and `search_files`
     work on the workspace's files. Prefer `edit_file` for changes to existing files.
   - `browser_screenshot` and `browser_content` load a URL in the workspace's Chromium and return an image or the
     page's text.
   - `git_clone`, `git_status` and `git_commit` work with repositories in the workspace.
   - `terminal_open`, `terminal_send` and `terminal_read` drive an interactive program, such as a REPL or an installer
     that asks questions; `terminal_close` ends it.
   - `list_processes` and `signal_process` inspect and stop processes.
4. **Branch risky work.** `workspace_fork` copies the workspace, memory and running processes included, to a new key.
   Try the change there and keep whichever copy works.
5. **Suspend when done.** Call `workspace_suspend` with `after_seconds: 0` when you finish a task: the workspace is
   suspended as soon as it is idle, with its memory and processes saved. Any later tool call on the key wakes it
   automatically; there is no separate resume step.

## Good practice

- Tell the user which `workspace_key` you used, so they can come back to it.
- Use `workspace_status` to see a workspace's state and recent operations, and `workspace_list` to find existing keys.
- A tool result with `code: timeout` and an `operation_id` means the operation is still running: call
  `operation_wait` with that id instead of starting it again.
- `usage_summary` shows the organization's usage and allowances in the current billing period.
- If something behaves unexpectedly, `send_feedback` sends a note straight to the Shardflux team.

Reference: https://docs.shardflux.dev/reference/mcp
