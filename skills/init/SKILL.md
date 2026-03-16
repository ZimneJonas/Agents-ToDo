---
name: init
description: Initialize a project for AI agents — detect stack, generate AGENTS.md with architecture guide, and ensure .gitignore is complete. Triggers on "/init", "init project", "setup agents", "create agents.md".
---

# Project Init for AI Agents

Scan the project and produce a concise `AGENTS.md` that tells agents what they need to work effectively in this codebase.

## Triggers

- `/init`
- "init project", "setup agents", "create agents.md"

## Workflow

### Step 1: Scan the Project

Read `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod` and any config files present (eslint, prettier, biome, tailwind, tsconfig, svelte.config, vite.config, etc.). Check lock files to determine package manager and dev-tools. Build understanding.

### Step 2: Update .gitignore

Ensure relevant standard ignores are present for the detected stack. Always include `TODO.md`. Add only what's missing.

### Step 3: Identify Open Architecture Decisions

Before writing anything, flag decisions that are ambiguous or missing. Examples:

- No consistent naming convention found across files
- Mixed CSS approaches (some inline, some Tailwind, some modules)
- No test setup detected — should there be one?
- Multiple ways to do the same thing in the codebase
- No `.env.example` but environment-dependent code exists

For each open decision: **ask the user with a concrete recommendation.** Don't guess silently. Format as:

```
I found a few open decisions before I can write the style guide:

1. **CSS approach**: I see Tailwind classes and a `styles/` folder with global CSS. Should I treat Tailwind as the primary tool and CSS for globals/variables only? (Recommended)
2. **Component naming**: Some files are PascalCase, some kebab-case. Standardize to PascalCase for components? (Recommended)
```

Wait for answers before proceeding to Step 4.

Skip this step if the codebase is consistent and decisions are clear.

### Step 4: Generate AGENTS.md

If `AGENTS.md` already exists, read it first and update only what changed — preserve custom content.

Structure:

---

```markdown
# Agent Guide

## Stack

[Single line: framework · language · CSS · relevant adapter or mode]

## Key Commands

[Main file to check: Makefile / package.json. List build/check/test/format commands used every time. Include important notes like "Use `yarn` (not npm/pnpm)".]

## After Every Task

[Ordered checks to run before committing. Build must pass warning-free.]

## Project Structure

[Top-level directories, 3–6 lines. Only what's non-obvious.]

## Environment

[Only if .env.example or env-dependent code exists. List required variables or point to .env.example.]

## Testing

[Only if a test framework is detected. How to run, what to test, what's out of scope.]

## Style Guide

[Infer from existing code — naming conventions, component patterns, CSS approach, TS strictness, etc.
If no style can be inferred, use the answers from Step 3 or recommend a standard suited to the stack.
Prescriptive and brief — rules, not explanations.]

## Rules

- [Non-obvious constraints specific to this project]
```

---

**Writing principles:**

- Omit sections where you have nothing concrete to say
- Be prescriptive, not explanatory — state the rule, skip the rationale
- Prefer industry standards; surface deviations as decisions in Step 3
- This file is read before every task — keep it under 60 seconds to scan

### Step 5: Report

```
## Init complete

- **Stack**: [summary]
- **AGENTS.md**: Created / Updated
- **.gitignore**: Updated (added: X entries) / Already complete
```

## Rules

1. Infer answers - but ask questions with recommendations on architecture options
2. Read before writing — ensure deep understanding and purpose before editing.
3. Concise over complete — AGENTS.md should only point out what is important for every task, or where to look for more info.
