---
name: submit
description: Mark tasks ready for review in TODO.md and run checks. Triggers on "/submit", "ready for review", "submit task", "ship it".
---

# Submit for Review

Mark a finished task as ready for review: run checks and update TODO.md.

## Triggers

- `/submit`
- "ready for review", "submit task", "ship it"

## Workflow

### Step 1: Determine What's Done

Check TODO.md for IN PROGRESS tasks. Cross-reference with conversation context (or git diff) to determine which tasks are actually complete.

If multiple tasks appear finished based on context, mark all of them. Ask for confirmation if it's genuinely unclear.

### Step 2: Run Checks (if not already done this session)

Check AGENTS.md to verfy aproach to changes.
Verify with project's lint/format/build commands. If they haven't been run yet in this conversation, run them now. Fix any errors before proceeding.

Skip if checks were already run and passed.

### Step 3: Mark Ready for Review in TODO.md

Update all occurrences of the task (roadmap table, section header, bullet points):

```markdown
### TASK-XXX: Title (👀 Review)
```

### Step 4: Recommend a Commit Message

Summarize the changes and suggest a commit message for the user to run. Use conventional commit format:

```
fix: button not reloading
refactor: helper auth logic
style: align form inputs
```

### Step 5: Handoff

Run `/next` to pick the next task. When ready to merg-review the branch, run `/review`.

## Rules

- Never skip checks if they haven't run this session
- Mark all completed tasks
- Never run git commands — only suggest the commit message
