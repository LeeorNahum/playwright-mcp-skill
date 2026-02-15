# Playwright MCP Setup

First-time installation guide for Playwright MCP in extension mode (using your real browser with existing logins and sessions).

## Prerequisites

- Chrome, Edge, or Chromium-based browser
- Node.js 18+

## 1. Install the Browser Extension

1. Go to [github.com/microsoft/playwright-mcp/releases](https://github.com/microsoft/playwright-mcp/releases)
2. Download the browser extension `.zip` from the latest release assets
3. Unzip to a permanent folder (do not delete -- the browser references it directly)
4. In your browser, navigate to `chrome://extensions/` (or equivalent)
5. Enable **Developer mode**
6. Click **Load unpacked** and select the unzipped folder

## 2. Get the Extension Token

1. Click the Playwright MCP Bridge extension icon in the browser toolbar
2. Copy the `PLAYWRIGHT_MCP_EXTENSION_TOKEN` value
3. Keep this token -- it auto-approves connections so you don't manually approve each one

Tokens regenerate if you reinstall the extension. Update your config if this happens.

## 3. MCP Server Configuration

The JSON config is the same across editors. The only differences are the file path and whether to use a shell wrapper for OS variable expansion.

The server and extension versions must match. Using `@latest` is fine as long as the extension is also up to date. If you hit connection timeouts, check for a version mismatch.

### Config (JSON)

**Windows** (use `cmd /c` to expand `%TEMP%`):

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

**macOS / Linux** (use `sh -c` to expand `/tmp`):

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

The `--output-dir` flag redirects session logs, traces, console recordings, and auto-named screenshots to a temp folder instead of creating a `.playwright-mcp/` directory in your project.

### Config (TOML -- Codex only)

```toml
[mcp_servers.playwright]
command = "npx"
args = ["@playwright/mcp@latest", "--extension", "--output-dir", "/tmp/playwright-mcp"]

[mcp_servers.playwright.env]
PLAYWRIGHT_MCP_EXTENSION_TOKEN = "<your-token>"
```

### Where to Place the Config

| Editor | Global config | Project config |
|--------|--------------|----------------|
| Cursor | `~/.cursor/mcp.json` | `.cursor/mcp.json` |
| Claude Code | `~/.claude.json` | `.claude/mcp.json` |
| Claude Desktop | `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Win) | -- |
| VS Code | User MCP settings or `code --add-mcp '{...}'` | `.vscode/mcp.json` |
| Codex | `~/.codex/config.toml` | -- |

### CLI Shortcuts

**Claude Code:**
```bash
claude mcp add playwright \
  --env PLAYWRIGHT_MCP_EXTENSION_TOKEN=<your-token> \
  -- npx @playwright/mcp@latest --extension --output-dir /tmp/playwright-mcp
```

**VS Code:**
```bash
code --add-mcp '{"name":"playwright","command":"npx","args":["@playwright/mcp@latest","--extension","--output-dir","/tmp/playwright-mcp"],"env":{"PLAYWRIGHT_MCP_EXTENSION_TOKEN":"<your-token>"}}'
```

## 4. Verify

1. Open editor MCP settings and confirm `playwright` appears as a connected server
2. Ensure the browser is open with the extension installed
3. Ask the agent to navigate to a website -- on first use, a tab picker appears in the browser to select which tab the AI connects to
