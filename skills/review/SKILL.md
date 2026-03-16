---
name: review
description: Code-review the current branch before merging. Diffs against target (feat > dev or dev > main), reviews changes, and produces a test checklist. Triggers on "/review", "review this", "review my changes", "ready to merge?".
---

# Code Review

Review the current branch's changes before merging: diff against target, assess the code, and produce a testing checklist.

## Triggers

- `/review`
- "review this", "review my changes", "ready to merge?"

## Workflow

### Step 1: Determine Merge Direction

Check the current branch name and git history to determine the target branch:

- `feat/*` or `feature/*` → target is `dev` or `develop`
- `dev` or `develop` → target is `main` or `master`
- If unclear → ask the user which branch to diff against

Run:
```
git log --oneline <target>..<current>
```

List the commits that will be merged. If none, tell the user and stop.

### Step 2: Diff the Branches

```
git diff <target>...<current>
```

Read the full diff. Group changes by file/concern for the review.

### Step 3: Check Against AGENTS.md

Read `AGENTS.md` (if it exists). Verify the changes align with the project's style guide, architecture decisions, and rules. Flag any deviations as findings in the code review below.

### Step 4: Code Review

Assess the changes across these dimensions — only flag what's actually relevant:

- **Correctness** — logic errors, edge cases, off-by-ones
- **Security** — injections, exposed secrets, auth bypasses, unvalidated input
- **Breaking changes** — API shape changes, removed exports, schema changes
- **Side effects** — unintended changes outside the task scope
- **Code quality** — readability, duplication, overly complex logic

Format findings as:

```
### 🔴 Must fix
- [file:line] issue description

### 🟡 Should fix
- [file:line] issue description

### 🟢 Looks good
- [what was done well]
```

Skip sections that have nothing to report.

### Step 5: Testing Checklist

Based on what changed, produce a concrete checklist of things to verify before merging:

```
## How to test

- [ ] [specific thing to click/run/check]
- [ ] [edge case to verify]
- [ ] [regression to confirm still works]
```

Be specific — reference actual UI, endpoints, or behaviors changed.

### Step 6: Update TODO.md

Read TODO.md and find all tasks currently in `👀 Review` status — these are all the tasks covered by this branch review, list them for context.

If the diff touches areas related to tasks that are NOT in `👀 Review`, flag them and ask the user to either run `/submit` on those tasks or confirm they should be included in this review.

After the testing checklist is presented, ask: "Should I mark all reviewed tasks as done and move them to Completed?"

- If yes: for each task, remove it from `## Active Work` and add it under `## Completed` with strikethrough title and status `✅ Done` — e.g. `### ~~TASK-XXX~~: Title (✅ Done)`

The branch is then ready to merge.

## Rules

- Never approve changes with 🔴 findings — require fixes first
- Be specific: reference file names and line numbers
- Keep the testing checklist actionable, not generic
- If the diff is empty, say so and stop
