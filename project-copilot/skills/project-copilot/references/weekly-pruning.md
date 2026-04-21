# Weekly Pruning Pass — Procedure

**Run:** Every Friday afternoon (or the weekday declared in `config.yaml → behavior.pruning_weekday`).
**Duration:** ~15 minutes.
**Scope:** Only `project-context.md` (Layer 1) and its pointers into Notion. Do not touch the file system or run Notion DB-wide cleanup here — those belong to monthly hygiene.

---

## Preconditions

1. Confirm the session has loaded `SKILL.md`, the project's `config.yaml`, and `project-context.md`.
2. Snapshot `project-context.md` to `.copilot/backups/YYYY-MM-DD_weekly-pre-prune.md` before any edit.
3. Check current token size of Layer 1. If > `behavior.layer1_token_budget`, flag this to the user and suggest a heavier consolidation pass rather than a normal prune.

---

## Step 1 — Promote durable insights (5 min)

For every meeting entry in **Section 13 (Recent Meetings)** older than 2 weeks:

1. Ask: does this entry contain pattern-breaking intelligence that should change how the user behaves, whom they approach, or what they say?
2. If yes, promote it up to the correct section:
   - New or shifted stakeholder dynamic → **Section 5 (Stakeholder Map)**
   - Cultural / political rule learned → **Section 6 (Rules of Engagement)**
   - Decision made or confirmed → **Section 7 (Active Decisions)** + mirror to Notion Decisions DB
   - New risk → **Section 8 (Landmines)** + Notion Risks & Issues
3. If no, the entry is ready for compression (Step 2).

Never delete a meeting entry without first performing this promotion check.

---

## Step 2 — Compress old meetings (3 min)

For every meeting in **Section 13** older than 2 weeks that has passed Step 1:

1. Collapse the entry to a single one-liner in **Section 14 (Compressed Meeting History)** using this format:
   ```
   M[N] YYYY-MM-DD · [Title] → [one-sentence outcome]. Summary: [path]. Notion: [link]
   ```
2. Delete the long-form entry from Section 13.
3. Verify the Notion Meetings DB entry for this meeting still exists and is linked correctly. Fix if missing.

---

## Step 3 — Age decisions (3 min)

For every entry in **Section 7 (Active Decisions)**:

1. Apply the decision-aging test: *"If a new session tomorrow never read this decision, would the user make a worse choice?"*
2. If no (decision has been absorbed into practice and is now obvious background), migrate it:
   - Ensure a matching entry exists in Notion Decisions DB with status `Operational — absorbed` and the original rationale preserved.
   - Remove the entry from Section 7.
3. If yes, keep in Section 7. Optionally add a dated one-line note if something meaningful has changed about why it still matters.

Target state after Step 3: **≤ 15–20 active decisions in Section 7.**

---

## Step 4 — Reconcile Section 12 (Current Focus) (2 min)

1. Read Section 12.
2. Replace "this week's top goal" with next week's top goal (or mark "carry over" if unchanged).
3. Remove hot items that have been resolved.
4. Add any landmines that became visible this week.
5. Update the "Next decision point" line.

This section is also updated daily by the scheduled task, but the Friday pass resets it to the week ahead.

---

## Step 5 — Check for duplication (1 min)

1. Ctrl-F for stakeholder names that appear in more than one section — ensure each person is only canonically listed in Section 5 (name + one-liner elsewhere is fine; full profile is not).
2. Ctrl-F for duplicate decision titles between Section 7 and the compressed history — remove from Section 7 if they have been superseded.
3. Ensure no full meeting summaries have leaked back into Layer 1. Only pointers belong.

---

## Step 6 — Update metadata (1 min)

1. Update the **Last updated** line at the top of `project-context.md`.
2. Add a one-line entry to **Section 18 (Change Log)** summarizing what changed (e.g. *"2026-04-24 — Weekly prune: compressed M11-M13, migrated D07 and D11 to Notion, promoted stakeholder shift from M14 to Section 5."*).
3. Re-measure file size. If still > `layer1_token_budget`, surface the number to the user and propose a targeted consolidation.

---

## Postconditions

- `project-context.md` still parses (section headings intact, lists valid).
- Backup exists at `.copilot/backups/YYYY-MM-DD_weekly-pre-prune.md`.
- Notion mirror is consistent — every decision/meeting/risk promoted or migrated has a live Notion entry.
- Change log has one new dated line.

---

## Output to the User

One short block summarizing the prune:

```
Weekly pruning complete — YYYY-MM-DD
- Meetings compressed: [N]
- Decisions migrated to Notion: [N]
- New promotions into Sections 5/6/7: [N]
- Layer 1 size: [X tokens / Y lines] (budget: [Z])
- Backup: [path]
```

Do not report anything else unless the user asks. Do not re-summarize the project.

---

## Failure Modes to Avoid

- **Do not delete meeting entries before promotion.** You lose intelligence permanently.
- **Do not migrate foundational decisions to Notion.** Only operational/absorbed ones.
- **Do not let the prune turn into a restructure.** If the file needs a restructure, stop and ask the user.
- **Do not skip the backup.** Every prune creates a restorable snapshot.
