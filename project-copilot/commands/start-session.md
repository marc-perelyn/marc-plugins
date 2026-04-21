---
name: start-session
description: Run the project-copilot session-start ritual for the current project
allowed-tools: [Read, Skill]
argument-hint: (no arguments)
---

# Start Project Copilot Session

Load the `project-copilot` skill and execute its Section 13 session-start sequence:

1. Read SKILL.md in full.
2. Read the project's `.copilot/config.yaml`.
3. Read the project's `project-context.md` at the project root.
4. Check the project's handoffs folder (default: `.copilot/handoffs/` or `00 Admin/project-copilot-skill/handoffs/`) for any pending `*.md` files not in `_done/`.
5. Check the "Last updated" line on `project-context.md` — flag if older than 5 days.
6. Confirm readiness in one short sentence. If a handoff exists, name it and ask whether to proceed.
7. Wait for the user's task.

Do not summarize everything you read. The point of this command is to restore operating state quietly.

## Instructions

1. Use the Skill tool to load the `project-copilot` skill.
2. The skill takes over and executes §13.

Execute:
```
Load the project-copilot skill
```
