---
name: submit
description: Mark tasks ready for review in TODO.md and run checks. Triggers on "/submit", "ready for review", "submit task", "ship it".
---

# Submit for Review

## Triggers

- `/submit`
- "ready for review", "submit task", "ship it"

## Workflow

### Step 1: Determine What's Done

Check TODO.md for IN PROGRESS tasks. Cross-reference with conversation context to confirm what's complete. Ask only if genuinely unclear.

### Step 2: Run Checks

Check AGENTS.md for lint/build commands and run them. Skip if already run and passed this session.

### Step 3: Update TODO.md

Mark completed tasks as `👀 Review` in all occurrences (roadmap table, section header).

### Step 4: Suggest a Commit Message

Use only what the user actually changed. Conventional commit format, one line:

```
docs: add credits to README
fix: login redirect bug
```

Only suggest the message — never run git commands.
Don't include everything, just the abstract commit idea.

## Rules

- Only suggest a commit for what was actually done — don't invent scope
- Mark all completed tasks
