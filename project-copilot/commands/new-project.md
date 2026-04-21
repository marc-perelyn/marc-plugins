---
name: new-project
description: Bootstrap a new knowledge-work project with the project-copilot skill (folder tree, config, project-context.md, Notion schema)
allowed-tools: [Read, Write, Edit, Bash, Skill]
argument-hint: (no arguments — the skill will interview the user for project details)
---

# New Project Bootstrap

Load the `project-copilot` skill and run its `references/new-project-setup.md` procedure.

The skill will:

1. Interview the user for project identity (name, client, role, mission, dates, root path, Notion workspace, languages, timezone, CI, special folders, political rules).
2. Create the folder tree at the project root per SKILL.md §7.
3. Generate `.copilot/config.yaml` from the template.
4. Create the 12 standard Notion databases and link them via relations.
5. Generate `project-context.md` from the template with identity and scope pre-filled.
6. Set up the scheduled daily briefing.
7. Optionally seed initial data (existing documents, known stakeholders, known decisions).
8. Validate the setup end to end.

This command is idempotent only up to Step 3 — if a Notion workspace already has databases for this project, surface that to the user before creating more.

## Instructions

1. Use the Skill tool to load the `project-copilot` skill.
2. The skill then executes `references/new-project-setup.md` step by step.

Execute:
```
Load the project-copilot skill and run the new-project-setup procedure
```
