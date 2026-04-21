---
name: monthly-hygiene
description: Run the project-copilot monthly hygiene pass — Notion integrity check + file-system cleanup + Layer 1 size check
allowed-tools: [Read, Write, Edit, Bash, Skill]
argument-hint: (no arguments)
---

# Monthly Hygiene Pass

Load the `project-copilot` skill and run both hygiene procedures in order:

1. **File-system hygiene** — `references/filesystem-hygiene.md`. Inventories the project root, fixes misfiled files, archives superseded versions, queues backfills. ~20 min.
2. **Notion hygiene** — `references/notion-hygiene.md`. Integrity check across all 11 operational databases, cross-layer reconciliation with `project-context.md`, archive flags (never delete). ~25 min.
3. **Layer 1 size check** — if `project-context.md` exceeds `config.yaml → behavior.layer1_token_budget`, propose a targeted consolidation pass.

Both hygiene procedures present a consolidated action list **before** making any destructive change — the user must approve. Nothing is ever deleted without a backup zip.

Total time budget: ~45 minutes.

## Instructions

1. Use the Skill tool to load the `project-copilot` skill.
2. Run file-system hygiene first (Notion Files Index reconciliation depends on it).
3. Then run Notion hygiene.
4. Then do the Layer 1 size check.

Execute:
```
Load the project-copilot skill and run monthly hygiene (filesystem first, then notion, then layer-1 size check)
```
