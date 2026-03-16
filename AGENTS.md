# Agent Guide

## Stack

Claude Code skills plugin · Markdown only · no build tools

## Project Structure

```
skills/          # One directory per skill, each with a SKILL.md
templates/       # Reusable file templates (e.g. TODO.md)
.claude-plugin/  # Plugin metadata (plugin.json, marketplace.json)
```

## Style Guide

- Each skill lives in `skills/<name>/SKILL.md` with YAML frontmatter (`name`, `description`)
- Skill docs use `##` for top-level sections, `###` for workflow steps

## Rules

- `templates/TODO.md` is commit as a template.
- `AGENTS.md` is the reference for `/review` to check style/architecture alignment
- No build, lint, or test commands — this is a pure Markdown project
