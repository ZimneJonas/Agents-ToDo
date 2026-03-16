---
name: next
description: Pick the next task to work on. Reads TODO.md, scores by priority and status, presents selection. Triggers on "/next", "what should I work on", "next task", "what's next".
---

# What's Next?

## Triggers

- `/next`
- "what should I work on", "next task", "what's next"

## Arguments

`bugs` · `progress` · `planned` · `review` · `active` · `all`

## Workflow

### Step 1: Read TODO.md

Search: `docs/TODO.md` → `TODO.md`. If not found, tell the user to run `/task` first.

Check git status — if uncommitted changes exist, recommend the user commit them first before picking a new task (suggest running `/submit`).

### Step 2: Parse Tasks

Read the file and extract tasks from `###` headers matching this pattern:

```
### [optional ~~]TASK-123[optional ~~]: Title (STATUS)
```

Regex: `^###\s+(~~)?((TASK|BUG|FEATURE|ROAD|IDEA|ISSUE|INQUIRY)-\d+)(~~)?:\s*(.+?)\s*\(([^)]+)\)`

Use `AskUserQuestion` to show top tasks — this is inherently interactive. Unless user already specified task.
Prioritize:

- IN PROGRESS tasks first with a note if any exist.
- based on session context flow
- based on priority

### Step 3: Start

After selection, Show the selected task's full detail from TODO.md. Mark it IN PROGRESS (all occurrences).

When the task is done, recommend to run `/submit`.

## Rules

- If one IN PROGRESS task exists and no argument given, suggest continuing it rather than picking something new
- Update all occurrences when changing status (table, header, bullets)
