# Shardflux plugin for Codex

Give Codex a persistent cloud computer. With this plugin, Codex opens a [Shardflux](https://shardflux.dev) workspace
by key and runs commands, dev servers, builds, tests and a Chromium browser in it. The workspace keeps its files,
packages and running processes between tool calls and between sessions, suspends when idle, and wakes on the next
call. Forks copy a workspace, memory included, so Codex can try a risky change on a copy.

## Setup

1. Create a project API key at https://app.shardflux.dev under **API keys**, and export it in the shell profile that
   starts Codex: `export SHARDFLUX_API_KEY=sfk_...`
2. Add the marketplace and install the plugin:

   ```sh
   codex plugin marketplace add shardfluxdev/plugins
   codex plugin add shardflux@shardflux
   ```

Requirements: Node.js 24 or later.

## What the plugin runs and sends

- It starts `npx -y @shardflux/mcp@0.7.1` (the npm package [`@shardflux/mcp`](https://www.npmjs.com/package/@shardflux/mcp),
  Apache-2.0) as a local stdio MCP server, with your `SHARDFLUX_API_KEY`.
- That server sends each tool call to the Shardflux API (`https://api.shardflux.dev`) and to the workspace endpoints it
  returns (`*.shardflux.dev`). It sends nothing anywhere else and keeps no local copy of your workspace.
- Each tool call answers within 55 seconds, inside Codex's default 60-second tool timeout; a longer operation returns
  its `operation_id`, and `operation_wait` keeps waiting.

Tools and the `shardflux-workspaces` skill: see https://docs.shardflux.dev/reference/mcp. Privacy policy:
https://shardflux.dev/privacy · Terms: https://shardflux.dev/terms · Support:
https://github.com/shardfluxdev/community/issues

## License

Apache-2.0. See [LICENSE](./LICENSE).
