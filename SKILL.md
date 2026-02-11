---
name: playwright-mcp-skill
description: >
  Use Playwright MCP for browser automation in AI coding agents.
  Use when setting up Playwright MCP, installing the Chrome extension,
  configuring MCP servers, taking browser screenshots,
  or troubleshooting browser automation issues.
metadata:
  author: Leeor Nahum
  version: "1.0"
---

# Playwright MCP

Playwright MCP is an MCP server that provides browser automation via structured accessibility snapshots -- no vision models or screenshots needed. It works on any website without site-side changes.

## Extension Mode

To use your real Chrome browser (with existing logins, cookies, sessions), run Playwright MCP in `--extension` mode with the Playwright MCP Bridge Chrome extension installed. This avoids re-authentication. See [references/SETUP.md](references/SETUP.md) for first-time installation.

## Configuration

Use `--output-dir` to redirect session logs, traces, console recordings, and auto-named screenshots to a temp folder instead of the project root.

**Windows** (`cmd /c` expands `%TEMP%`):

```json
{
  "command": "cmd",
  "args": ["/c", "npx @playwright/mcp@latest --extension --output-dir %TEMP%/playwright-mcp"],
  "env": { "PLAYWRIGHT_MCP_EXTENSION_TOKEN": "<token>" }
}
```

**macOS / Linux** (`sh -c` expands `/tmp`):

```json
{
  "command": "sh",
  "args": ["-c", "npx @playwright/mcp@latest --extension --output-dir /tmp/playwright-mcp"],
  "env": { "PLAYWRIGHT_MCP_EXTENSION_TOKEN": "<token>" }
}
```

## Screenshots

When calling `browser_take_screenshot`, do not pass a custom `filename`. Auto-generated names (`page-{timestamp}.png`) correctly route to `--output-dir`. Custom filenames bypass `--output-dir` and save to the workspace root.

## Troubleshooting

- **`.playwright-mcp/` folder in project** -- config is missing `--output-dir`; add it and delete the folder
- **"No MCP clients are currently connected"** -- restart your editor, verify `mcp.json` is saved
- **Connection popup every time** -- ensure `PLAYWRIGHT_MCP_EXTENSION_TOKEN` is set in the `env` block
- **"Process with MCP failed to execute tool"** -- Chrome must be open with the extension loaded (not disabled)
- **Token changed** -- tokens regenerate on extension reinstall; update the config with the new value
