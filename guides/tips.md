# Claude Code Tips & Tricks

Non-obvious features, shortcuts, and workflows that make Claude Code significantly faster.

## Commands You Probably Don't Know

| Command | What it does |
|---------|-------------|
| `/clear` | Fresh session. Use after every completed task |
| `/compact` | Compress context manually. Add focus: `/compact focus on auth changes` |
| `/cost` | Token usage for current session |
| `/stats` | Detailed statistics. `Ctrl+S` inside for screenshot |
| `/memory` | View what Claude remembers about you |
| `/plan` | Planning mode — Claude thinks but doesn't act until approved |
| `/plan fix the auth bug` | Jump straight into planning with description |
| `/loop 30m check CI status` | Recurring task, runs every 30 min for up to 3 days |
| `/schedule "run tests" --cron "0 9 * * *"` | Runs on Anthropic's servers, even when your PC is off |
| `/teleport` | Transfer session between terminal, phone, and web |
| `/remote-control` | Connect to running session from another device |
| `/voice` | Dictate instead of type |
| `/batch` | Parallel processing across many files |
| `/effort` | Change thinking depth mid-session |

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Shift+Tab` | Switch permission mode (ask → auto-edit → auto) |
| `Shift+Enter` | Multi-line input (run `/terminal-setup` first) |
| `Ctrl+C` | Stop current generation |
| `Esc Esc` | Undo last file change |
| `Ctrl+S` in `/stats` | Screenshot statistics |

## Prompting Tips

**`ultrathink`** — write this word in your prompt for maximum thinking depth on that specific task. No need to change global effort level.

**Interview approach** — instead of explaining everything:
```
Ask me questions to understand the requirements. Use AskUserQuestion tool.
```

**Cross-model review:**
```
Review this plan as a staff engineer. Find weaknesses.
```

**Be specific about output:**
```
Bad:  "make a login page"
Good: "create a login page with email/password, Zod validation,
       loading state, error messages, redirect to /dashboard on success.
       Use shadcn/ui components. Mobile-first."
```

## Session Management

- **One task = one session.** `/clear` after each completed task.
- **Commit before `/clear`.** Context is lost after clear.
- **`/compact` every 30-40 minutes** in long sessions. Or rely on `autoCompact: true`.
- **Start with context:** begin each session by telling Claude what you're working on.

## Git Workflow

```
1. git checkout -b feature/description
2. Claude writes code
3. git add . && git commit -m "feat: description"
4. git push origin feature/description
5. /clear
6. Repeat
```

Never work on main directly. Branches are cheap, broken main is expensive.

## File Organization

- Keep files under 300 lines — Claude works faster with smaller files
- 800 lines = mandatory split into modules
- Extract reusable components early
- Group by feature, not by type (all auth files together, not all components together)

## Context Window Optimization

- Don't install more than 5-7 plugins — each eats 500-2000 tokens at session start
- Don't install more than 5 MCP servers — same reason
- Write focused CLAUDE.md — specific rules, not generic advice
- Use `/compact` with focus instructions to preserve important context

## The `_claude.json` File

Located at `~/` (home directory). This is Claude Code's internal cache — statistics, feature flags, OAuth data, project metrics. **Never edit or delete it.** It's not your settings file.

Your actual settings: `~/.claude/settings.json`

## Files That Matter

| File | Location | Purpose |
|------|----------|---------|
| `settings.json` | `~/.claude/settings.json` | Global settings (permissions, plugins, hooks) |
| `CLAUDE.md` | Project root | Project-specific instructions |
| `.claude/settings.json` | Project root | Project-specific settings |
| `_claude.json` | `~/` | Internal cache (don't touch) |
| `.claude.json` | `~/` | MCP server configs |
| `.mcp.json` | Project root | Project-level MCP configs |
