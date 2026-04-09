# settings.json Explained

Complete breakdown of Claude Code's `~/.claude/settings.json`. Every field, what it does, and recommended values.

## Location

```
Windows:  C:\Users\<name>\.claude\settings.json
macOS:    ~/.claude/settings.json
Linux:    ~/.claude/settings.json
```

## Environment Variables

```json
"env": {
  "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1",
  "ENABLE_TOOL_SEARCH": "1"
}
```

| Variable | What it does |
|----------|-------------|
| `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` | Enables parallel agent teams with git worktrees |
| `ENABLE_TOOL_SEARCH` | Auto-discovers MCP tools without loading all at startup |
| `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` | Blocks telemetry, auto-updates, version checks |

## Permissions

```json
"permissions": {
  "allow": ["Bash(git *)", "Edit(*)", "Read(*)", "Write(*)"],
  "deny": ["Bash(rm -rf *)", "Read(.env*)"],
  "defaultMode": "dontAsk"
}
```

**defaultMode options:**
- `"dontAsk"` — full autonomy, never asks permission
- `"allowEdits"` — auto-approves edits, asks for bash commands
- `"askEveryTime"` — asks before every action

**Deny rules** override allow rules. If something is in both lists, deny wins.

**Common deny patterns:**
- `Read(.env*)` — prevent reading environment files with secrets
- `Read(**/*.pem)` — prevent reading SSL certificates
- `Bash(rm -rf *)` — prevent recursive deletion
- `Bash(git push *)` — prevent pushing (force branch workflow)
- `Bash(sudo *)` — prevent privilege escalation

## Effort Level

```json
"effortLevel": "high"
```

- `"low"` — fast, minimal thinking
- `"medium"` — balanced (recommended for saving rate limits)
- `"high"` — deep thinking on every task (formerly "max")

Use `ultrathink` in your prompt for maximum depth on a specific task without changing the global setting.

## Auto Compact

```json
"autoCompact": true,
"autoCompactThreshold": 75
```

Default threshold is 95%. Setting 75% means Claude compresses context earlier, preserving quality for longer sessions. Recommended range: 70-80%.

## Plugins

```json
"enabledPlugins": {
  "superpowers@claude-plugins-official": true,
  "frontend-design@claude-plugins-official": true
}
```

Anthropic auto-installs official plugins. You can enable/disable them here. Don't add more than 5-7 plugins — each one adds 500-2000 tokens to every session.

## Hooks

```json
"hooks": {
  "PreToolUse": [{ "matcher": "Bash", "hooks": [{ "type": "command", "command": "..." }] }],
  "PostToolUse": [{ "matcher": "Write(*)", "hooks": [{ "type": "command", "command": "..." }] }],
  "PreCommit": [{ "hooks": [{ "type": "command", "command": "npm run lint" }] }],
  "Notification": [{ "hooks": [{ "type": "command", "command": "..." }] }]
}
```

**Events:** PreToolUse, PostToolUse, PreCommit, PostCompact, Notification, Stop

**`blocking: true`** — if the hook fails (exit code 1), the action is blocked.

**Important:** Hook structure requires nested `hooks` array with `type: "command"`. Flat format does NOT work.

## Attribution

```json
"attribution": {
  "commit": "Co-Authored-By: Claude <noreply@anthropic.com>",
  "pr": "🤖 Generated with Claude Code"
}
```

Added to every git commit and PR description automatically.

## Other Settings

| Setting | Value | What it does |
|---------|-------|-------------|
| `autoMemoryEnabled` | `true` | Claude remembers patterns across sessions |
| `autoUpdatesChannel` | `"latest"` | Update channel: latest, stable, beta |
| `telemetryDisabled` | `true` | Disable usage analytics |
| `skipDangerousModePermissionPrompt` | `true` | Skip warning when using `--dangerously-skip-permissions` |

## What NOT to put in settings.json

- **MCP servers** — use `claude mcp add --scope user` instead
- **Project-specific rules** — put in project's `.claude/settings.json`
- **CLAUDE.md content** — keep in project root as CLAUDE.md file
