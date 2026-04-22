# Claude / AI Prompts & Scripts

A personal reference repo for Claude Code prompts, MCP setups, and utility scripts used in AI-assisted trading workflows.

---

## MCP Setups

Step-by-step guides to install and configure MCP servers with Claude Code.

| File | Description |
|------|-------------|
| [TradingView-MCP-Setup.md](MCP%20Setups/TradingView-MCP-Setup.md) | Install and configure the TradingView MCP server — connects Claude Code to a live TradingView Desktop chart via CDP |

---

## Prompts

Skill prompts and agent definitions for Claude Code workflows.

| File | Description |
|------|-------------|
| [pine-develop.md](Prompts/pine-develop.md) | Full Pine Script development loop — write, compile, fix errors, iterate |
| [chart-analysis.md](Prompts/chart-analysis.md) | Technical analysis workflow — set symbol/timeframe, add indicators, annotate, screenshot |
| [strategy-report.md](Prompts/strategy-report.md) | Generate a backtest performance report — metrics, trade analysis, equity curve, recommendations |
| [performance-analyst.md](Prompts/performance-analyst.md) | Agent prompt for in-depth trading strategy performance analysis |

---

## Scripts

Utility scripts for interacting with TradingView via CDP.

| File | Description |
|------|-------------|
| [pine_pull.js](scripts/pine_pull.js) | Pull current Pine Script source from TradingView editor → saves to `current.pine` |
| [pine_push.js](scripts/pine_push.js) | Push local `current.pine` to TradingView editor and compile |

---

## Setup Requirements

- [Claude Code](https://claude.ai/code) CLI installed
- [TradingView Desktop](https://www.tradingview.com/desktop/) installed
- Node.js 18+
