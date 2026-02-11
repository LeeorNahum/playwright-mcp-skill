---
name: playwright-mcp-skill
description: >
  Use Playwright MCP for browser automation in AI coding agents.
  Use when setting up Playwright MCP, installing the browser extension,
  configuring MCP servers, taking browser screenshots,
  or troubleshooting browser automation issues.
metadata:
  author: Leeor Nahum
  version: "1.0"
---

# Playwright MCP

Playwright MCP is an MCP server for browser automation using structured accessibility snapshots. It works on any website without site-side changes and supports Chromium, Firefox, and WebKit.

For first-time installation and editor-specific configuration, see [references/SETUP.md](references/SETUP.md).

## Screenshots

When calling `browser_take_screenshot`, omit the `filename` parameter. Auto-generated names (`page-{timestamp}.png`) route to `--output-dir` correctly. Custom filenames bypass `--output-dir` and save to the workspace root (known upstream issue).

## Troubleshooting

- **`.playwright-mcp/` folder in project** -- config is missing `--output-dir`; add it per [references/SETUP.md](references/SETUP.md) and delete the folder
- **Connection popup every time** -- ensure `PLAYWRIGHT_MCP_EXTENSION_TOKEN` is set in the `env` block
- **"No MCP clients are currently connected"** -- restart the editor, verify MCP config is saved
- **"Process with MCP failed to execute tool"** -- the browser must be open with the extension loaded
- **Token changed** -- tokens regenerate on extension reinstall; update the config with the new value
