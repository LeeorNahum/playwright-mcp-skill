---
name: playwright-mcp-skill
description: >
  Use Playwright MCP for browser automation in AI coding agents.
  Use when setting up Playwright MCP, installing the browser extension,
  configuring MCP servers, taking browser screenshots,
  or troubleshooting browser automation issues.
metadata:
  author: Leeor Nahum
  version: "1.1"
---

# Playwright MCP

Playwright MCP is an MCP server for browser automation using structured accessibility snapshots. It works on any website without site-side changes and supports Chromium, Firefox, and WebKit.

## First-Time Setup

Setting up Playwright MCP requires manual steps that the user must perform (installing a browser extension, retrieving a token, editing config files). If Playwright MCP is not yet configured, guide the user through the steps in [references/SETUP.md](references/SETUP.md). If it is already installed but missing the `--output-dir` flag, update the config per the same reference.

## Screenshots

When calling `browser_take_screenshot`, omit the `filename` parameter. Auto-generated names (`page-{timestamp}.png`) route to `--output-dir` correctly. Custom filenames bypass `--output-dir` and save to the workspace root.

## Troubleshooting

- **"Extension connection timeout"** -- the MCP server cannot reach the browser extension. Common causes:
  1. **Version mismatch**: the server and extension versions must match. Check the extension version at `chrome://extensions/` and either update the extension or pin the server to the same version in the config (e.g. `@playwright/mcp@0.0.64`).
  2. **Browser not open**: the browser with the extension must be running.
  3. **Service worker asleep**: click "service worker" under Inspect views on the extension details page to wake it, then restart the MCP server in your editor.
  4. **Stale MCP server process**: restart the MCP server in your editor settings (toggle off then on).
- **`.playwright-mcp/` folder in project** -- config is missing `--output-dir`; update per [references/SETUP.md](references/SETUP.md) and delete the folder
- **Connection popup every time** -- ensure `PLAYWRIGHT_MCP_EXTENSION_TOKEN` is set in the `env` block
- **"No MCP clients are currently connected"** -- restart the editor, verify MCP config is saved
- **"Process with MCP failed to execute tool"** -- the browser must be open with the extension loaded
- **Token changed** -- tokens regenerate on extension reinstall; update the config with the new value
