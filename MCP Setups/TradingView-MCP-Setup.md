# TradingView MCP — Setup Guide

Step-by-step guide to install and configure the TradingView MCP server with Claude Code.

Source repo: https://github.com/tradesdontlie/tradingview-mcp

---

## Step 1: Clone and Install

```bash
git clone https://github.com/tradesdontlie/tradingview-mcp.git ~/tradingview-mcp
cd ~/tradingview-mcp
npm install
```

If you prefer a different install path, replace `~/tradingview-mcp` accordingly.

---

## Step 2: Add to Claude Code MCP Config

The config file is at `~/.claude/.mcp.json` (global) or `.mcp.json` (project-level).

```json
{
  "mcpServers": {
    "tradingview": {
      "command": "node",
      "args": ["<INSTALL_PATH>/src/server.js"]
    }
  }
}
```

Replace `<INSTALL_PATH>` with the actual cloned path (e.g., `/Users/username/tradingview-mcp`).

If the config already has other MCP servers, **merge** the `tradingview` entry — do not overwrite.

---

## Step 3: Launch TradingView Desktop with CDP

TradingView Desktop must run with Chrome DevTools Protocol enabled on port 9222.

**Auto-launch (recommended):** After the MCP connects, use the `tv_launch` tool — it auto-detects on Mac, Windows, and Linux.

**Manual launch by platform:**

**Mac:**
```bash
/Applications/TradingView.app/Contents/MacOS/TradingView --remote-debugging-port=9222
```

**Windows:**
```bash
%LOCALAPPDATA%\TradingView\TradingView.exe --remote-debugging-port=9222
```

**Linux:**
```bash
/opt/TradingView/tradingview --remote-debugging-port=9222
```

---

## Step 4: Restart Claude Code

The MCP server only loads at Claude Code startup.

1. Exit Claude Code (`Ctrl+C`)
2. Relaunch Claude Code
3. The `tradingview` MCP server connects automatically

---

## Step 5: Verify Connection

Run the `tv_health_check` tool. Expected response:

```json
{
  "success": true,
  "cdp_connected": true,
  "chart_symbol": "...",
  "api_available": true
}
```

If `cdp_connected: false` — TradingView is not running with `--remote-debugging-port=9222`.

---

## Step 6: Install CLI (Optional)

To use the `tv` command globally from any terminal:

```bash
cd ~/tradingview-mcp
npm link
```

Commands available: `tv status`, `tv quote`, `tv pine compile`, etc.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| `cdp_connected: false` | Launch TradingView with `--remote-debugging-port=9222` |
| `ECONNREFUSED` | TradingView isn't running or port 9222 is blocked |
| MCP not showing in Claude Code | Check `~/.claude/.mcp.json` syntax, restart Claude Code |
| `tv` command not found | Run `npm link` from the project directory |
| Tools return stale data | TradingView may still be loading — wait a few seconds |
| Pine Editor tools fail | Open Pine Editor first: `ui_open_panel pine-editor open` |

---

## Key Files in the MCP Repo

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Decision tree for which tool to use (auto-loaded by Claude Code) |
| `README.md` | Full tool reference (78 MCP tools, 30 CLI commands) |
| `SETUP_GUIDE.md` | Original setup guide |
| `scripts/pine_pull.js` | Pull Pine Script source from TradingView editor |
| `scripts/pine_push.js` | Push Pine Script to TradingView editor and compile |
| `scripts/launch_tv_debug_mac.sh` | Launch TradingView on Mac with CDP |
