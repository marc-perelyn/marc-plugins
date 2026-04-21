---
name: weekly-pruning
description: Run the project-copilot weekly pruning pass on project-context.md (promote durable insights, compress old meetings, age decisions, reset Current Focus)
allowed-tools: [Read, Write, Edit, Bash, Skill]
argument-hint: (no arguments)
---

# Weekly Pruning Pass

Load the `project-copilot` skill and execute `references/weekly-pruning.md`.

Scope: Layer 1 only (`project-context.md`) and its Notion pointers. Does not touch the file system. Target duration: ~15 minutes.

Steps the skill runs:

1. Back up `project-context.md` to `.copilot/backups/`.
2. Promote durable insights from Recent Meetings (Section 13) into Sections 5/6/7/8 as appropriate.
3. Compress meeting entries older than 2 weeks into one-liners in Section 14.
4. Age decisions: migrate absorbed operational decisions from Section 7 to Notion.
5. Reconcile Section 12 (Current Focus) for the week ahead.
6. Check for duplication across sections.
7. Update "Last updated" and add a one-line Section 18 change-log entry.
8. Report the prune results.

Never delete meeting entries before promoting durable insights. Never migrate foundational decisions.

## Instructions

1. Use the Skill tool to load the `project-copilot` skill.
2. The skill then executes `references/weekly-pruning.md`.

Execute:
```
Load the project-copilot skill and run the weekly-pruning procedure
```
