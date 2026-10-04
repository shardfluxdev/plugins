# Shardflux plugins

Persistent cloud workspaces for AI agents. These plugins give Claude Code and Codex the
[Shardflux](https://shardflux.dev) MCP server and a skill for working in a workspace: a Linux computer in the cloud that
keeps its files, packages and running processes between sessions, suspends when idle and wakes on the next call.

## Claude Code

```text
/plugin marketplace add shardfluxdev/plugins
/plugin install shardflux@shardflux
```

Then run `/mcp`, select **plugin:shardflux:shardflux** and **Authenticate**: sign in to Shardflux and choose a project.
No API key to copy. Details: [plugins/shardflux](./plugins/shardflux).

## Codex

```sh
codex plugin marketplace add shardfluxdev/plugins
codex plugin add shardflux@shardflux
codex mcp login shardflux
```

Details: [codex/shardflux](./codex/shardflux).

## Other MCP clients

Add the hosted server `https://mcp.shardflux.dev/mcp` to any client with remote MCP and OAuth (Claude, ChatGPT,
Cursor, VS Code). Setup for each, and the local server `npx -y @shardflux/mcp`: https://docs.shardflux.dev/reference/mcp

Support: https://github.com/shardfluxdev/community/issues · License: Apache-2.0
