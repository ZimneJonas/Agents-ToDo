---
name: next
description: Pick the next task to work on. Reads TODO.md, scores by priority and status, presents selection. Triggers on "/next", "what should I work on", "next task", "what's next".
---

# What's Next?

## Triggers

- `/master-plan:next`
- "what should I work on", "next task", "what's next"

## Arguments

`bugs` · `progress` · `planned` · `review` · `active` · `all`

## Workflow

### Step 1: Read TODO.md

Search: `docs/TODO.md` → `TODO.md`. If not found, tell the user to run `/master-plan:task` first.

Check git status — if uncommitted changes exist, mention it briefly.

### Step 2: Parse Tasks

Read the file and extract tasks from `###` headers matching this pattern:

```
### [optional ~~]TASK-123[optional ~~]: Title (STATUS)
```

Regex: `^###\s+(~~)?((TASK|BUG|FEATURE|ROAD|IDEA|ISSUE|INQUIRY)-\d+)(~~)?:\s*(.+?)\s*\(([^)]+)\)`

Use `AskUserQuestion` to show top tasks — this is inherently interactive. Unless user already specified task.
Piroitize:

- IN PROGRESS tasks first with a note if any exist.
- based on session context flow
- based on priorty

### Step 3: Start

After selection, Show the selected task's full detail from TODO.md. Mark it IN PROGRESS (all occurrences).

## Rules

- P0 always first
- If one IN PROGRESS task exists and no argument given, suggest continuing it rather than picking something new
- Update all occurrences when changing status (table, header, bullets)
