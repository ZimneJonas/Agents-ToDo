---
name: done
description: Mark tasks complete in TODO.md, run checks if needed, and commit. Triggers on "/done", "mark done", "task complete", "finish task", "ship it".
---

# Task Completion Workflow

Finalize a completed task: verify tests pass, commit changes, update MASTER_PLAN.md, and push.

## Triggers

- `/master-plan:done`
- "mark done", "task complete", "finish task", "ship it"

## Workflow

### Step 1: Determine What's Done

Check TODO.md for IN PROGRESS tasks. Cross-reference with conversation context (or git diff) to determine which tasks are actually complete.

If multiple tasks appear finished based on context, mark all of them. Only ask for confirmation if it's genuinely unclear.

### Step 2: Run Checks (if not already done this session)

Check AGENTS.md or package.json for the project's lint/format/build commands. If they haven't been run yet in this conversation, run them now. Fix any errors before proceeding.

Skip if checks were already run and passed.

### Step 3: Mark Review in TODO.md

Update all occurrences of the task (roadmap table, section header, bullet points):

```markdown
### ~~TASK-XXX~~: Title ( Review)
```

### Step 4: Explain

Tell the user what changed and how to verify it's working, if not obvious.

## Rules

- Never skip checks if they haven't run this session
- Mark all completed tasks
