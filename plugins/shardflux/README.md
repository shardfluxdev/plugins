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

1. Install the plugin:

   ```text
   /plugin marketplace add shardfluxdev/plugins
   /plugin install shardflux@shardflux
   ```

2. Run `/mcp`, select **plugin:shardflux:shardflux** and **Authenticate**. Sign in to Shardflux in the browser, choose
   the project Claude works in, and select **Connect**.
3. Ask Claude to do something in a workspace, for example: *"Clone my repo into a Shardflux workspace called
   `my-app`, install it and run the tests."*

No API key to copy and nothing to install on your machine.

## What the plugin connects to

- Shardflux's hosted MCP server, `https://mcp.shardflux.dev/mcp` (MCP Streamable HTTP, OAuth). Each tool call goes
  there and runs in your workspace in the cloud: commands, files and browsing happen there, not on your machine.
- The connection is a project API key named `<client> (MCP connector)`, listed on the project's **API keys** page at
  https://app.shardflux.dev. Revoke it there to disconnect Claude.

Privacy policy: https://shardflux.dev/privacy · Terms: https://shardflux.dev/terms · Support:
https://github.com/shardfluxdev/community/issues

## License

Apache-2.0. See [LICENSE](./LICENSE).
