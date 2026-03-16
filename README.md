# Agents-ToDo

AI-native task management for Agent Code. Track tasks in a `TODO.md` file — pick, save, and review — all through Agent Code skills.

## Install

```
/plugin marketplace add ZimneJonas/Agents-ToDo
/plugin install Agents-ToDo
```

## Skills

| Command | What it does |
|---|---|
| `/init` | Scan project → generate `AGENTS.md` and `TODO.md` |
| `/task` | Capture a task, bug, or idea into `TODO.md` |
| `/next` | Pick the highest-priority task and start it |
| `/submit` | Run checks, mark done, suggest commit |
| `/review` | Branch diff → code review → test checklist |


## Workflow

**Setup** — run `/init` once. Scans your stack, writes `AGENTS.md` (architecture guide for agents), and creates `TODO.md`.

**Brain-dump** — capture anything without losing focus on what you're doing:
```
/task fix the login redirect bug
/task add dark mode
```

**Pick up work** — run `/next`. Scores tasks by priority and marks the chosen one `IN PROGRESS`.

**Wrap up** — run `/submit` when done. Runs checks, marks the task `👀 Review`, and suggests a commit message.

**Before merging** — run `/review`. Diffs the branch against its target, reviews the code, and produces a test checklist. Marks all reviewed tasks `✅ Done`.


## TODO.md structure

```markdown
## Roadmap

| ID | Title | Priority | Status | Dependencies |
|----|-------|----------|--------|--------------|
| **BUG-1** | Fix login redirect | P0 | IN PROGRESS | - |

## Active Work

### BUG-1: Fix login redirect (IN PROGRESS)
**Priority**: P0
**Status**: IN PROGRESS (2026-03-16)

Description of the task...

## Completed

### ~~TASK-2~~: Dark mode (✅ Done)
```

**Types**: `TASK` · `BUG` · `FEATURE` · `INQUIRY`
**Priorities**: `P0` (critical) · `P1` · `P2` (default) · `P3` (backlog)
IDs are sequential across all types.

## Credits

Inspired by [endlessblink/master-plan](https://github.com/endlessblink/master-plan).

## License

MIT
