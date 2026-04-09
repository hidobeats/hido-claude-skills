---
name: auto-team
description: Auto-spawn Agent Teams in git worktrees for parallel tasks. Handles preflight, plan, worktree setup, merge, rollback, and cleanup. Trigger for 3+ independent subtasks.
---

# Auto Team — Agent Teams with Worktree Automation

## When to Activate

Use Agent Teams with worktrees when ALL of these are true:
- Task has **3 or more independent parts** that can run in parallel
- Parts touch **different files/modules** (not the same file)
- Task would take **>30 minutes** sequentially

Do NOT use when:
- Task is simple (single file edit, bug fix, small feature)
- Parts depend on each other sequentially
- User explicitly asks for single-session work
- Repository has uncommitted changes (stash or commit first)

---

## Example

**User:** "Build a dashboard with auth, charts, and API endpoints"

**Plan:**
1. `feature/auth` → login/register pages, JWT middleware
2. `feature/charts` → recharts components, data visualization
3. `feature/api` → REST endpoints, database queries

**Worktrees:** `../dashboard-auth`, `../dashboard-charts`, `../dashboard-api`

**Result:** Three teammates work in parallel, merge into `feature/integration-dashboard`, user reviews and merges to main.

---

## Workflow

### Phase 0: Preflight Check (NEVER skip)

Before anything, verify the environment is ready:

```bash
# 1. Verify git repo
git rev-parse --git-dir

# 2. Check for uncommitted changes
git status --porcelain
# If dirty → ask user to commit or stash before proceeding

# 3. Verify Agent Teams enabled
# Check CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1

# 4. Check no conflicting worktrees
git worktree list

# 5. Record current branch for safety
git branch --show-current
# Store as ORIGINAL_BRANCH for rollback
```

If any check fails — stop and inform user what needs to be fixed.

### Phase 1: Plan (ALWAYS do this first)

1. Analyze the task
2. Break into independent parts (3-4 max for cost efficiency)
3. Assign model per teammate based on complexity
4. Present the plan to user for approval:

```
I'll split this into [N] parallel tasks:

1. [task] → branch: feature/[name] (Opus — complex logic)
2. [task] → branch: feature/[name] (Sonnet — implementation)
3. [task] → branch: feature/[name] (Sonnet — tests)

Integration branch: feature/integration-[project-name]
Estimated token usage: ~[N]x single session

Proceed?
```

5. Wait for user confirmation before proceeding

### Phase 2: Setup Integration Branch and Worktrees

```bash
# Create integration branch (NEVER merge directly to main/master)
git checkout -b feature/integration-[project-name]

# Create worktrees from integration branch
git worktree add ../[project]-[task1] feature/[task1]
git worktree add ../[project]-[task2] feature/[task2]
git worktree add ../[project]-[task3] feature/[task3]
```

Naming convention:
- Integration branch: `feature/integration-[project-name]`
- Worktree folder: `../[project-name]-[short-task-name]`
- Task branch: `feature/[short-task-name]`

### Phase 3: Spawn Agent Team

```
Create a team:
- Teammate 1 (Opus): work in ../[project]-[task1] on [description]
- Teammate 2 (Sonnet): work in ../[project]-[task2] on [description]
- Teammate 3 (Sonnet): work in ../[project]-[task3] on [description]

Rules for all teammates:
- Commit frequently with clear messages
- Run tests/build before final commit
- Do not modify files outside your scope
- Do not touch package.json unless explicitly told
- Signal completion when done
```

### Phase 4: Auto-Merge (after all teammates complete)

```bash
# Return to main working directory
cd [original-project-dir]

# Ensure we're on integration branch
git checkout feature/integration-[project-name]

# Merge each branch one by one
git merge feature/[task1] --no-edit
# Verify build: npm run build or npm test
# If fails → rollback this merge, report to user

git merge feature/[task2] --no-edit
# Verify build again

git merge feature/[task3] --no-edit
# Final verification: npm run build && npm test
```

### Phase 5: Cleanup (ALWAYS do this)

```bash
# Remove worktrees
git worktree remove ../[project]-[task1]
git worktree remove ../[project]-[task2]
git worktree remove ../[project]-[task3]

# Delete merged branches
git branch -d feature/[task1]
git branch -d feature/[task2]
git branch -d feature/[task3]

# Prune any stale worktree references
git worktree prune
```

### Phase 6: Report

After cleanup, report to user:

```
✅ Team completed. Summary:

Integration branch: feature/integration-[project-name]

- [task1] (Opus): [what was done, files changed]
- [task2] (Sonnet): [what was done, files changed]
- [task3] (Sonnet): [what was done, files changed]

Build: ✅ pass
Tests: ✅ pass (N/N)
Branches merged and cleaned up.

→ Ready to merge into main when you approve.
```

---

## Safety Rules

- **NEVER** merge directly into `main` or `master`
- Always create `feature/integration-*` branch first
- Merge teammates into integration branch
- User decides when to merge integration → main
- Record `ORIGINAL_BRANCH` at start for emergency rollback

---

## Error Handling

| Problem | Action |
|---------|--------|
| Uncommitted changes at start | Stop. Ask user to commit or stash. |
| Agent Teams not enabled | Stop. Tell user to set `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` |
| Worktree creation fails | Branch may exist. `git branch -D` if stale, or pick different name. |
| Merge conflict (1-2 files) | Attempt auto-resolution. |
| Merge conflict (3+ files) | `git merge --abort`. Stop and ask user. |
| Build fails after merge | `git revert -m 1 HEAD`. Report which merge broke it. |
| All merges fail | `git merge --abort` and `git checkout ORIGINAL_BRANCH`. Report. |
| Test failure after merge | Report which merge broke tests, offer to revert. |
| Teammate idle >5 min | Reassign task or complete from lead session. |
| Folder manually deleted | Run `git worktree prune` to clean stale refs. |

### Emergency Rollback

If everything goes wrong:

```bash
# Abort any in-progress merge
git merge --abort

# Return to original branch
git checkout [ORIGINAL_BRANCH]

# Remove all worktrees
git worktree remove ../[project]-[task1] --force
git worktree remove ../[project]-[task2] --force
git worktree remove ../[project]-[task3] --force

# Delete integration and task branches
git branch -D feature/integration-[project-name]
git branch -D feature/[task1]
git branch -D feature/[task2]
git branch -D feature/[task3]

# Clean up
git worktree prune
```

---

## Model Selection per Teammate

| Task Type | Model | Why |
|-----------|-------|-----|
| Architecture, API design, complex logic | Opus | Needs deep reasoning |
| Component implementation, features | Sonnet | Good balance speed/quality |
| Tests, linting, formatting | Sonnet or Haiku | Straightforward tasks |
| Documentation, README | Sonnet | Clear writing |

Specify in spawn prompt: "Use Sonnet for this teammate"

---

## Token Optimization

- Keep teammate prompts short and focused — one clear task per teammate
- Limit team to **3-4 teammates max** for cost efficiency
- 3 teammates ≈ 3-4x tokens of a single session
- Compact lead session after spawning teammates
- Use Sonnet/Haiku for simple teammates to reduce cost
- Do NOT use Agent Teams for tasks a single session handles in <30 min
