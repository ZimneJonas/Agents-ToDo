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
| `/init` | Scans your project and generates `AGENTS.md` — an architecture guide for AI agents |
| `/task` | Adds a new task to `TODO.md` with an auto-generated ID |
| `/next` | Picks the next task to work on |
| `/submit` | Marks a task ready for review and commits |
| `/review` | Diffs current branch, code-reviews changes, and produces a test checklist |

## Workflow

**1. Initialize** — run `/init` once. Agent scans your stack and writes `AGENTS.md` so agents know how to work in your codebase.

**2. Add tasks** — describe what needs doing:
```
/task fix the login redirect bug
/task add dark mode
```
Agent infers the type and priority and appends it to `TODO.md`.

**3. Pick a task** — run `/next`. Agent shows the highest-priority work and marks it `IN PROGRESS`.

**4. Submit** — when done, run `/submit`. Agent runs checks, marks the task ready for review, and commits.

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

### ~~TASK-2~~: Dark mode (✅ DONE)
```

**Types**: `TASK` · `BUG` · `FEATURE` · `INQUIRY`
**Priorities**: `P0` (critical) · `P1` · `P2` (default) · `P3` (backlog)
IDs are sequential across all types.

## License

MIT
