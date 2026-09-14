---
name: obsidian-mcp
description: >-
  Antigravity skill that configures and runs the Obsidian MCP (mcpvault) for the Secondbrain vault.
  It installs required tools, writes the required mcpvault configuration files, and provides a convenient command
  to start the MCP server.
---

# Obsidian MCP Skill

This skill automates the setup of the **Obsidian + MCP** integration for your Secondbrain vault.

## What it does
- Checks that **Node.js**, **npm** and **mcpvault** are installed.
- Installs `@bitbonsai/mcpvault` globally if missing.
- Writes the three required configuration files (`~/.claude/settings.json`, `<workspace>/.claude/settings.local.json`, `<workspace>/.mcp.json`).
- Provides a `run_mcpvault` command to start the server as a background daemon.

## Usage
In the Antigravity CLI (`agy`) you can run:
```bash
agy skill run obsidian-mcp --setup   # Perform the full setup
agy skill run obsidian-mcp --start   # Start the mcpvault daemon (if not already running)
```
The `--setup` flag will perform all checks and write the config files. The `--start` flag simply launches the daemon.

## Configuration file contents (generated automatically)
```json
{
  "mcpServers": {
    "obsidian": {
      "command": "C:\\Users\\carloschen\\AppData\\Roaming\\npm\\mcpvault.cmd",
      "args": ["G:\\我的雲端硬碟\\Secondbrain"]
    }
  }
}
```
The paths are escaped for JSON compatibility.

## Commands provided by the skill
- `obsidian-mcp.setup()` – Runs the full environment check and writes the config files.
- `obsidian-mcp.start()` – Starts `mcpvault "G:\我的雲端硬碟\Secondbrain"` as a daemon.

These commands can be invoked from the Antigravity REPL or via slash commands.

## Dependencies
- Windows OS
- PowerShell 5+ (built‑in)
- Internet connection (for npm install)

## Notes
- The `mcpvault` daemon will keep running until you stop it with `agy task kill <task-id>`.
- If you change the vault location, re‑run `obsidian-mcp.setup()` to update the configuration files.
