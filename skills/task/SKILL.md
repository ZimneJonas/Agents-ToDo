---
name: task
description: Create a new task in TODO.md with auto-generated sequential IDs. Triggers on "/task", "add task", "new task", "create task", "track this".
---

# Task Creator

## Triggers

- `/task`
- "add task", "new task", "create task", "track this", "log a bug"

## Workflow

### Step 1: Find or Create TODO.md

Search: `docs/TODO.md` / `TODO.md`. If not found, create `TODO.md` with sections: Roadmap table · Active Work · Completed.

### Step 2: Generate ID

Scan all `(TASK|BUG|FEATURE|ROAD|IDEA|ISSUE|INQUIRY)-(\d+)` occurrences. IDs are sequential across all types — next ID = highest found + 1.
IDs are sequential across ALL types. If TASK-42 and BUG-43 exist, the next ID is 44 regardless of type.

Output `Using task number: [ID]` before anything else.

### Step 3: Infer Type and Priority

From the user's message and context — ask if ambiguous.

**Type**: "bug/broken/crash/error" → BUG
- "investigate/understand/why" → INQUIRY
- "major feature/new system" → FEATURE
- otherwise → TASK

**Priority**:
- "critical/blocker/urgent" → P0
- "important/soon" → P1
- "low/someday/backlog" → P3
- otherwise/default → P2

### Step 4: Add to TODO.md

#### 4a. Add to Roadmap Table (if one exists)

Look for a markdown table with task IDs. Insert a new row:

```markdown
| **[TYPE]-[ID]** | **[Title]** | **[Priority]** | PLANNED | - |
```

#### 4b. Add Detailed Section

Add a new `###` section at the appropriate place (typically at the end of the active work area, before completed tasks):

```markdown
### [TYPE]-[ID]: [Title] (PLANNED)
**Priority**: [Priority]
**Status**: PLANNED (YYYY-MM-DD)

[Description based on context]
```

### Step 5: Confirm

Output: ID · title · priority · status. Suggest `/next` to start it.

## Rules

- Never reuse IDs — always scan first
- IDs are global across all types
- Infer, don't ask — only prompt if truly unclear
- Add enough information to have a clear starting point for this task, if necessary by asking questions. This can also just be topics to further explore as INQUIRY.
