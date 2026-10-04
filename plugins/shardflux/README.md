# Shardflux plugin for Claude

Give Claude a persistent cloud computer. With this plugin, Claude opens a [Shardflux](https://shardflux.dev) workspace
by key and runs commands, dev servers, builds, tests and a Chromium browser in it. The workspace keeps its files,
packages and running processes between tool calls and between sessions, suspends when idle, and wakes on the next
call. Forks copy a workspace, memory included, so Claude can try a risky change on a copy.

## What you get

- **The `shardflux` MCP server**: workspace tools (`exec` with background commands, `read_file`, `write_file`,
  `edit_file`, `list_files`, `search_files`, `git_clone`, `git_status`, `git_commit`, terminal tools,
  `browser_screenshot`, `browser_content`, `list_processes`, `signal_process`) and management tools
  (`workspace_open`, `workspace_list`, `workspace_status`, `workspace_suspend`, `workspace_fork`, `operation_wait`,
  `usage_summary`, `send_feedback` and more).
  Full reference: https://docs.shardflux.dev/reference/mcp
- **The `shardflux-workspaces` skill**: the workflow Claude follows: one stable key per project, background
  commands for servers, forks for risky changes, suspend when done.

## Setup

1. Create a project API key at https://app.shardflux.dev under **API keys**.
2. Install the plugin. Claude Code asks for the key and stores it in your system's secure credential store.
3. Ask Claude to do something in a workspace, for example: *"Clone my repo into a Shardflux workspace called
   `my-app`, install it and run the tests."*

Requirements: Node.js 24 or later on the machine that runs Claude Code or Cowork.

## What the plugin runs and sends

- It starts `npx -y @shardflux/mcp@0.7.1` (the npm package [`@shardflux/mcp`](https://www.npmjs.com/package/@shardflux/mcp),
  Apache-2.0) as a local stdio MCP server.
- That server sends each tool call, authenticated with your API key, to the Shardflux API (`https://api.shardflux.dev`)
  and to the workspace endpoints it returns (`*.shardflux.dev`). It sends nothing anywhere else and keeps no local
  copy of your workspace.
- Commands, files and browsing happen inside your workspace in the cloud, not on your machine.

Privacy policy: https://shardflux.dev/privacy · Terms: https://shardflux.dev/terms · Support:
https://github.com/shardfluxdev/community/issues

## License

Apache-2.0. See [LICENSE](./LICENSE).
