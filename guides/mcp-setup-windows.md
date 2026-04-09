# MCP Setup on Windows

Step-by-step guide for installing and configuring MCP servers on Windows with Claude Code.

## Important: Windows Requires `cmd /c`

On Windows, `npx` must be wrapped with `cmd /c`. Without it, MCP servers will show as **failed**.

## Recommended MCP Servers

### Context7 — Live Library Documentation

```bash
claude mcp add --scope user context7 -- cmd /c npx -y @upstash/context7-mcp@latest
```

What it does: Fetches up-to-date docs for any library (React, Next.js, Tailwind, etc.) directly into Claude's context. No more outdated API suggestions.

Free API key (optional, higher rate limits): [context7.com/dashboard](https://context7.com/dashboard)

### Magic (21st.dev) — UI Components

```bash
claude mcp add --scope user magic -- cmd /c npx -y @21st-dev/magic@latest
```

Requires API key from [21st.dev](https://21st.dev). Add via env:

```bash
claude mcp add --scope user --env API_KEY=your_key magic -- cmd /c npx -y @21st-dev/magic@latest
```

### Playwright — Browser Automation

```bash
claude mcp add --scope user playwright -- cmd /c npx -y @playwright/mcp@latest
```

What it does: Claude can open browsers, click buttons, fill forms, take screenshots, test your site.

## Common Issues

### "Windows requires 'cmd /c' wrapper to execute npx"

Your MCP was installed without `cmd /c`. Fix:

```bash
claude mcp remove <name>
claude mcp add --scope user <name> -- cmd /c npx -y <package>
```

### MCP shows "failed" but works in regular terminal

Check if `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` is set in your settings.json env. This can block MCP connections in some cases.

Also try: close Claude Code completely, reopen, run `/mcp`.

### `claude mcp add` converts `cmd /c` to `C:/`

Known Windows bug. Fix by editing `~/.claude.json` directly. Change the args array to:

```json
"args": ["/c", "npx", "-y", "@upstash/context7-mcp@latest"]
```

Note: the command should be `"command": "cmd"` and `/c` goes as the first arg.

## Managing MCP Servers

```bash
claude mcp list              # Show all servers
claude mcp get context7      # Details for specific server
claude mcp remove context7   # Remove server
/mcp                         # Check status inside Claude Code
```

## Scopes

| Scope | Location | Available in |
|-------|----------|-------------|
| `--scope user` | `~/.claude.json` | All projects |
| `--scope project` | `.mcp.json` in project root | Current project only |

Use `--scope user` for servers you want everywhere. Use project scope for project-specific databases or APIs.

## How Many MCP Servers?

**3-5 maximum.** Each server adds tools to context. More than 5 = slower startup, more token usage, diminishing returns.
