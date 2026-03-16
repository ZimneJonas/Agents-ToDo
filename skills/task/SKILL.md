---
name: task
description: Create a new task in TODO.md with auto-generated sequential IDs. Triggers on "/task", "add task", "new task", "create task", "track this".
---

# Task Creator

## Triggers

- `/master-plan:task`
- "add task", "new task", "create task", "track this", "log a bug"

## Workflow

### Step 1: Find or Create TODO.md

Search: `docs/TODO.md` → `TODO.md`. If not found, create `docs/TODO.md` with sections: Roadmap table · Active Work · Completed.

### Step 2: Generate ID

Scan all `(TASK|BUG|FEATURE|ROAD|IDEA|ISSUE|INQUIRY)-(\d+)` occurrences. IDs are sequential across all types — next ID = highest found + 1.

Output `Using task number: [ID]` before anything else.

### Step 3: Infer Type and Priority

From the user's message and context — don't ask unless genuinely ambiguous.

**Type**: "bug/broken/crash/error" → BUG · "investigate/understand/why" → INQUIRY · "major feature/new system" → FEATURE · otherwise → TASK

**Priority**: "critical/blocker/urgent" → P0 · "important/soon" → P1 · "low/someday/backlog" → P3 · otherwise → P2

### Step 4: Add to TODO.md

Add a row to the roadmap table and a `###` section with status PLANNED, priority, date, inferred first steps.

### Step 5: Confirm

Output: ID · title · priority · status. Suggest `/master-plan:next` to start it.

## Rules

- Never reuse IDs — always scan first
- IDs are global across all types
- Infer, don't ask — only prompt if truly unclear
