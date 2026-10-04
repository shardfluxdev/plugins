# Shardflux plugins

Persistent cloud workspaces for AI agents. These plugins give Claude Code, Cowork and Codex the
[Shardflux](https://shardflux.dev) MCP server and a skill for working in a workspace: a Linux computer in the cloud that
keeps its files, packages and running processes between sessions, suspends when idle and wakes on the next call.

## Claude Code

```text
/plugin marketplace add shardfluxdev/plugins
/plugin install shardflux@shardflux
```

Claude Code asks for your Shardflux API key (create one at https://app.shardflux.dev under **API keys**) and keeps it
in your system's secure credential store. Details: [plugins/shardflux](./plugins/shardflux).

## Codex

```sh
export SHARDFLUX_API_KEY=sfk_...
codex plugin marketplace add shardfluxdev/plugins
codex plugin add shardflux@shardflux
```

Details: [codex/shardflux](./codex/shardflux).

## Other MCP clients

Run the server directly: `SHARDFLUX_API_KEY=sfk_... npx -y @shardflux/mcp`. Setup for Cursor, Claude Desktop and
others: https://docs.shardflux.dev/reference/mcp

Support: https://github.com/shardfluxdev/community/issues · License: Apache-2.0
