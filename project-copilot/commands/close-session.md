---
name: close-session
description: Run the project-copilot session-close ritual — diff Layer 1, surface open loops, file handoffs, emit summary
allowed-tools: [Read, Write, Edit, Bash, Skill]
argument-hint: (no arguments)
---

# Close Project Copilot Session

Load the `project-copilot` skill and execute `references/close-session.md`.

The procedure:

1. **Bail check** — if the session was conversational-only (no Layer 1 edits, no Notion writes, no files created), exit cleanly. No ritual needed.
2. **Layer 1 diff** — diff `project-context.md` against the most recent pre-session backup. Flag staleness (header, §19b dates, missing change-log entry).
3. **Open-loop scan** — walk the session transcript for decisions / tasks / risks / meetings / stakeholders / open questions / implied handoffs that should be in Notion or `.copilot/handoffs/`.
4. **Handoff closure** — list pending handoffs, propose moving resolved ones to `_done/`.
5. **Present action list** — single ≤15-line approval block to the user. Partial approval is fine.
6. **Execute approved actions** — Notion writes, handoff file moves, small Layer 1 fixes (header refresh, change-log entry).

Total: ≤3 min for routine sessions; ≤10 min when material changes need filing.

The procedure never edits anything destructively without Step 5 approval. It never re-journals the session into `project-context.md`.

## Instructions

1. Use the Skill tool to load the `project-copilot` skill.
2. The skill takes over and executes `references/close-session.md`.

Execute:
```
Load the project-copilot skill and run the close-session procedure
```
