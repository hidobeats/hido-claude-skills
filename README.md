# HIDO Claude Kit

Production-tested toolkit for Claude Code — skills, agents, templates, and guides.

---

## What's Inside

### Skills

Ready-to-use skills that Claude Code activates automatically.

**auto-team** — Orchestrates parallel Agent Teams in isolated git worktrees. Handles preflight checks, plan, worktree setup, merge, rollback, and cleanup. Model selection per teammate.

**web-animations** — Modular animation reference with 70+ cataloged effects. Main SKILL.md (~80 lines) handles technique selection and performance rules. Detailed catalogs load on demand from `references/` — only what's needed enters context.

### Agents

Specialized domain experts that Claude delegates tasks to.

**security-auditor** — OWASP Top 10 compliance, XSS, SQL injection, auth bypass, exposed secrets. Outputs findings with severity levels and exact fixes.

**performance-reviewer** — PageSpeed 95+ targeting. Checks images, bundles, fonts, layout shift, code splitting. Estimates score impact per issue.

**database-designer** — Schema design, migrations, indexes, RLS policies. Follows UUID PKs, soft delete, money-as-cents, proper normalization.

**api-designer** — RESTful endpoint design, auth flows, Zod validation, error handling. Consistent response envelopes and pagination patterns.

**architect** — System design before code. Stack selection, folder structure, data models, API surface, risk assessment. Start here for new projects.

**refactor-expert** — Finds code smells, duplication, oversized files. Concrete before/after suggestions with specific triggers (300+ line files, 3+ repeated patterns).

### Templates

**CLAUDE.md** — Drop-in project configuration template. Architecture, rules, git conventions, performance targets, and explicit "Do NOT" section. Customize per project.

### Guides

**settings-explained** — Complete breakdown of every `settings.json` field with recommended values.

**mcp-setup-windows** — Step-by-step MCP installation on Windows. Covers the `cmd /c` requirement, common errors, and fixes.

**tips** — Non-obvious commands, keyboard shortcuts, prompting techniques, session management, and context optimization.

---

## Install

### Skills (copy to Claude Code skills directory)

```bash
# Global — available in all projects
cp -r skills/auto-team ~/.claude/skills/auto-team
cp -r skills/web-animations ~/.claude/skills/web-animations

# Project-level — current project only
cp -r skills/auto-team .claude/skills/auto-team
cp -r skills/web-animations .claude/skills/web-animations
```

### Agents (copy to Claude Code agents directory)

```bash
cp agents/*.md ~/.claude/agents/
```

### Templates (copy to project root)

```bash
cp templates/CLAUDE.md ./CLAUDE.md
# Edit the Context section for your project
```

---

## Structure

```
hido-claude-kit/
├── README.md
├── LICENSE
├── skills/
│   ├── auto-team/
│   │   └── SKILL.md
│   └── web-animations/
│       ├── SKILL.md
│       └── references/
│           ├── text-effects.md
│           ├── scroll-effects.md
│           ├── background-effects.md
│           ├── cursor-effects.md
│           ├── svg-effects.md
│           ├── micro-interactions.md
│           ├── easing-reference.md
│           └── code-patterns.md
├── agents/
│   ├── security-auditor.md
│   ├── performance-reviewer.md
│   ├── database-designer.md
│   ├── api-designer.md
│   ├── architect.md
│   └── refactor-expert.md
├── templates/
│   └── CLAUDE.md
└── guides/
    ├── settings-explained.md
    ├── mcp-setup-windows.md
    └── tips.md
```

---

## Requirements

| Component | Requirements |
|-----------|-------------|
| auto-team | Git, `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` |
| web-animations | React project (Framer Motion / GSAP optional) |
| agents | Claude Code with agent support |
| templates | Any project |
| guides | Any Claude Code setup |

---

## Contributing

Found a bug, have a better agent prompt, or want to add a guide? Open an issue or PR.

---

## License

MIT
