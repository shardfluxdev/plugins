# Shardflux plugin for Codex

Give Codex a persistent cloud computer. With this plugin, Codex opens a [Shardflux](https://shardflux.dev) workspace
by key and runs commands, dev servers, builds, tests and a Chromium browser in it. The workspace keeps its files,
packages and running processes between tool calls and between sessions, suspends when idle, and wakes on the next
call. Forks copy a workspace, memory included, so Codex can try a risky change on a copy.

## Setup

```sh
codex plugin marketplace add shardfluxdev/plugins
codex plugin add shardflux@shardflux
codex mcp login shardflux
```

`codex mcp login` opens Shardflux in your browser: sign in, choose the project Codex works in, and select **Connect**.
No API key to copy and nothing to install on your machine.

## What the plugin connects to

- Shardflux's hosted MCP server, `https://mcp.shardflux.dev/mcp` (MCP Streamable HTTP, OAuth). Each tool call goes
  there and runs in your workspace in the cloud.
- The connection is a project API key named `<client> (MCP connector)`, listed on the project's **API keys** page at
  https://app.shardflux.dev. Revoke it there to disconnect Codex.
- Tool calls get 150 seconds (`tool_timeout_sec`), above the server's 120-second per-call deadline; a longer operation
  returns its `operation_id`, and `operation_wait` keeps waiting.

Tools and the `shardflux-workspaces` skill: see https://docs.shardflux.dev/reference/mcp. Privacy policy:
https://shardflux.dev/privacy · Terms: https://shardflux.dev/terms · Support:
https://github.com/shardfluxdev/community/issues

## License

Apache-2.0. See [LICENSE](./LICENSE).
