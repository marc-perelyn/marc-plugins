---
name: monthly-hygiene
description: Run the project-copilot monthly hygiene pass — file-system cleanup + Notion integrity check + Layer 1 size & structure check (with consolidation if drift is detected)
allowed-tools: [Read, Write, Edit, Bash, Skill]
argument-hint: (no arguments)
---

# Monthly Hygiene Pass

Load the `project-copilot` skill and run all three hygiene procedures in order:

1. **File-system hygiene** — `references/filesystem-hygiene.md`. Inventories the project root, fixes misfiled files, archives superseded versions, queues backfills. ~20 min.
2. **Notion hygiene** — `references/notion-hygiene.md`. Integrity check across all 12 operational databases, cross-layer reconciliation with `project-context.md`, archive flags (never delete). ~25 min.
3. **Layer 1 size & structure check.** Measure `project-context.md` against `config.yaml → behavior.layer1_token_budget`. Run the same diagnostic checklist as weekly-pruning Step 0 (parallel stakeholder lists, Current Focus over budget, header journaling, etc.). If the file is over budget OR any structural drift flag fires, run the **Layer 1 consolidation pass** (`references/layer1-consolidation.md`) — it presents a section-by-section move list, gets user approval, then executes. ~30–45 min if consolidation runs; ~5 min if not.

All three procedures present a consolidated action list **before** making any destructive change — the user must approve. Nothing is ever deleted without a backup.

Total time budget: ~45 min if Layer 1 is healthy; ~75 min if consolidation runs.

## Instructions

1. Use the Skill tool to load the `project-copilot` skill.
2. Run file-system hygiene first (Notion Files Index reconciliation depends on it).
3. Then run Notion hygiene.
4. Then run the Layer 1 size & structure check. If drift is detected, dispatch to `references/layer1-consolidation.md`.

Execute:
```
Load the project-copilot skill and run monthly hygiene (filesystem → notion → layer-1 size+structure check; consolidate if drift detected)
```
