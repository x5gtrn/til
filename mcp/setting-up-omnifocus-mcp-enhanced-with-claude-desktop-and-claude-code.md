---
title: Setting Up omnifocus-mcp-enhanced with Claude Desktop and Claude Code
layout: post
date: 2026-04-07T09:06+09:00
category: mcp
tags:
  - claude
  - mcp
  - omnifocus
  - self-managenent
in: TIL
---

# Setting Up omnifocus-mcp-enhanced with Claude Desktop and Claude Code

## Overview

This guide documents the process of integrating [omnifocus-mcp-enhanced](https://github.com/search?q=omnifocus-mcp-enhanced) with both **Claude Desktop** and **Claude Code** on macOS, including the pitfalls encountered along the way.

---

## Prerequisites

- macOS with [Homebrew](https://brew.sh/) installed
- Node.js installed via Homebrew (`/opt/homebrew/bin/node`)
- Claude Desktop installed
- Claude Code installed (`npm install -g @anthropic-ai/claude-code`)
- OmniFocus installed

---

## Step 1: Install omnifocus-mcp-enhanced

```bash
npm install -g omnifocus-mcp-enhanced
```

Global npm packages installed via Homebrew's Node.js are placed at:

```
/opt/homebrew/lib/node_modules/<package-name>/
```

To verify the installation:

```bash
ls /opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/
```

---

## Step 2: Find the Correct Entry Point

This is where things get tricky. There are a few common mistakes to avoid.

### ❌ Mistake 1: Using the `.ts` source file directly

```
/opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/src/server.ts
```

TypeScript files cannot be executed directly by `node`. Always use the **compiled JavaScript** in the `dist/` directory.

### ❌ Mistake 2: Assuming `dist/index.js` exists

```
Error: Cannot find module '.../dist/index.js'
```

The entry point filename varies by package. Always check the actual contents:

```bash
ls /opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/dist/
cat /opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/package.json | grep -E '"main"|"bin"' -A 3
```

For `omnifocus-mcp-enhanced`, the correct entry point is:

```
/opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/dist/server.js
```

### ❌ Mistake 3: Using the system `node` instead of Homebrew's `node`

Claude Desktop launches processes in a minimal environment where the system PATH may not include Homebrew's binaries. Using just `"command": "node"` can resolve to an older system Node.js that doesn't support ES Modules, causing:

```
SyntaxError: Cannot use import statement outside a module
```

Always use the **full path** to Homebrew's Node.js:

```bash
which node
# → /opt/homebrew/bin/node

/opt/homebrew/bin/node --version
# → v25.9.0
```

---

## Step 3a: Configure Claude Desktop

The configuration file is located at:

```
~/Library/Application Support/Claude/claude_desktop_config.json
```

> **Note:** The `Library` folder is hidden in Finder. Use Terminal or navigate via **Claude Desktop → Settings → Developer → Edit Config**.

Create or update the file with the following content:

```json
{
  "mcpServers": {
    "omnifocus": {
      "command": "/opt/homebrew/bin/node",
      "args": ["/opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/dist/server.js"]
    }
  }
}
```

You can apply this via Terminal in one shot:

```bash
cat > ~/Library/Application\ Support/Claude/claude_desktop_config.json << 'EOF'
{
  "mcpServers": {
    "omnifocus": {
      "command": "/opt/homebrew/bin/node",
      "args": ["/opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/dist/server.js"]
    }
  }
}
EOF
```

After saving, **fully quit and restart Claude Desktop**. Then verify the connection via the **"+" button → Connectors** in the chat interface.

---

## Step 3b: Configure Claude Code

Claude Code provides a CLI command for registering MCP servers:

```bash
claude mcp add omnifocus /opt/homebrew/bin/node /opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/dist/server.js
```

This saves the configuration to `~/.claude.json` (user scope, applied globally across all projects).

To verify:

```bash
claude mcp list
claude mcp get omnifocus
```

### Scope Options

|Flag|Scope|Config file|
|---|---|---|
|`-s user` (default)|All projects for this user|`~/.claude.json`|
|`-s project`|Current project only|`.mcp.json` in project root|

---

## Troubleshooting

### "Could not attach" in Claude Desktop

Check the MCP server log:

```bash
cat ~/Library/Logs/Claude/mcp-server-omnifocus.log
```

Common causes:

|Symptom|Cause|Fix|
|---|---|---|
|`Cannot find module`|Wrong file path|Check `dist/` contents with `ls`|
|`Cannot use import statement`|Old Node.js version|Use full path `/opt/homebrew/bin/node`|
|`Could not attach`|Server crashes on startup|Run the command manually in Terminal to see the error|

### Manual test before configuring Claude

Always test the server manually before adding it to Claude's config:

```bash
/opt/homebrew/bin/node /opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/dist/server.js
```

If it runs without errors (or waits for input), Claude should be able to connect to it.

---

## Summary

|What|Value|
|---|---|
|Package install path|`/opt/homebrew/lib/node_modules/omnifocus-mcp-enhanced/`|
|Correct entry point|`dist/server.js` (not `src/server.ts`, not `dist/index.js`)|
|Node.js to use|`/opt/homebrew/bin/node` (full path, not `node`)|
|Claude Desktop config|`~/Library/Application Support/Claude/claude_desktop_config.json`|
|Claude Code command|`claude mcp add omnifocus <command> <args>`|

---

## Key Takeaways

1. **Always use the compiled `dist/` file**, not the TypeScript source.
2. **Check the actual filename** in `dist/` — don't assume it's `index.js`.
3. **Use the full path to Node.js** in Claude Desktop config to avoid PATH-related issues.
4. **Test manually in Terminal first** before debugging inside Claude.
5. Claude Desktop and Claude Code use **separate configuration mechanisms** — you need to set up both independently.