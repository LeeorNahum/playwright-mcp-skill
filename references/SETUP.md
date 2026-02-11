# Playwright MCP Setup

First-time installation guide for Playwright MCP in extension mode (using your real Chrome browser).

## Prerequisites

- Chrome, Edge, or Chromium browser
- Node.js 18+

## 1. Install the Chrome Extension

1. Go to [github.com/microsoft/playwright-mcp/releases](https://github.com/microsoft/playwright-mcp/releases)
2. Download the Chrome extension `.zip` from the latest release assets
3. Unzip to a permanent folder (e.g. `C:\Tools\playwright-mcp-extension\` or `~/tools/playwright-mcp-extension/`)
4. In Chrome, navigate to `chrome://extensions/`
5. Enable **Developer mode** (top right toggle)
6. Click **Load unpacked** and select the unzipped folder
7. The Playwright MCP Bridge icon appears in the toolbar

## 2. Get the Extension Token

1. Click the Playwright MCP Bridge extension icon in Chrome
2. Copy the `PLAYWRIGHT_MCP_EXTENSION_TOKEN` value
3. Keep this token -- it enables auto-approved connections (without it, you must manually approve each connection in Chrome)

Tokens regenerate if you reinstall the extension. Update your config if this happens.

## 3. Configure Your Editor

### Cursor

Add to `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (project-level):

**Windows:**

```json
{
  "mcpServers": {
    "playwright": {
      "command": "cmd",
      "args": ["/c", "npx @playwright/mcp@latest --extension --output-dir %TEMP%/playwright-mcp"],
      "env": {
        "PLAYWRIGHT_MCP_EXTENSION_TOKEN": "<your-token>"
      }
    }
  }
}
```

**macOS / Linux:**

```json
{
  "mcpServers": {
    "playwright": {
      "command": "sh",
      "args": ["-c", "npx @playwright/mcp@latest --extension --output-dir /tmp/playwright-mcp"],
      "env": {
        "PLAYWRIGHT_MCP_EXTENSION_TOKEN": "<your-token>"
      }
    }
  }
}
```

### Claude Code

```bash
claude mcp add playwright \
  --env PLAYWRIGHT_MCP_EXTENSION_TOKEN=<your-token> \
  -- npx @playwright/mcp@latest --extension --output-dir /tmp/playwright-mcp
```

### VS Code (GitHub Copilot)

```bash
code --add-mcp '{"name":"playwright","command":"npx","args":["@playwright/mcp@latest","--extension","--output-dir","/tmp/playwright-mcp"],"env":{"PLAYWRIGHT_MCP_EXTENSION_TOKEN":"<your-token>"}}'
```

### Standard JSON Config (Most MCP Clients)

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest", "--extension", "--output-dir", "/tmp/playwright-mcp"],
      "env": {
        "PLAYWRIGHT_MCP_EXTENSION_TOKEN": "<your-token>"
      }
    }
  }
}
```

On Windows, wrap with `cmd /c` and use `%TEMP%/playwright-mcp` to let the OS expand the temp path. On macOS/Linux, wrap with `sh -c` and use `/tmp/playwright-mcp`.

## 4. Verify

1. Open your editor's MCP settings and confirm `playwright` appears as a connected server
2. Ensure Chrome is open with the extension installed
3. Ask the agent to navigate to a website -- on first use, a tab picker appears in Chrome to select which tab the AI connects to
