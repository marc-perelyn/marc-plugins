# Notion Hygiene Pass — Procedure

**Run:** First Monday of every month (same day as file-system hygiene).
**Duration:** ~25 minutes.
**Scope:** The project's Notion workspace (Layer 2). Does not touch Layer 1 or Layer 3 except to update pointers.

---

## Preconditions

1. SKILL, `config.yaml`, and `project-context.md` loaded.
2. Notion databases listed under `config.yaml → notion.databases` are reachable. If a database ID fails to resolve, stop and report — do not proceed with partial coverage.
3. Run file-system hygiene first (Files Index reconciliation depends on it).

---

## Step 1 — Database-by-database integrity check

Run the relevant sub-procedure for each of the eleven standard databases. Each sub-procedure collects issues into a consolidated action list (Step 2). Nothing is written back until Step 3.

### 1.1 Meetings

- Every row has a date, a title, at least one attendee, and a status.
- Every row older than 2 weeks has either a linked summary file (under `20 Meetings/Summaries/`) or an explicit "no summary required" flag.
- Meetings referenced from `project-context.md` Section 14 (Compressed Meeting History) exist as Notion rows.

### 1.2 Decisions

- Every row has: title, date, decision maker, rationale, status, foundational/operational tag.
- No two active decisions contradict each other — if you find one, flag it.
- Every decision tagged "Superseded" has a link to the superseding decision.
- Decisions older than 3 weeks marked as active but absorbed → re-tag as `Operational — absorbed`.

### 1.3 Tasks

- Every row has owner, due date (or explicit "no deadline"), priority, status.
- Tasks with status "To Do" or "In Progress" that are > 60 days old → flag for user review (stale).
- Tasks with no related entity (no link to Deliverable, Decision, Meeting, Risk) → flag for cleanup.
- "Done" tasks older than 90 days → archive (set `Archived = true`, not delete).
- No duplicate titles with identical owners.

### 1.4 Stakeholders

- Every row has name, role, organization, influence level, stance.
- Stakeholders who have not appeared in any Meetings, Tasks, or Decisions in the last 8 weeks → flag as `Dormant` (don't delete — history is valuable).
- No duplicate people (same email or same name + org).

### 1.5 Use Cases (or the project's equivalent unit-of-work DB)

- Every row has name, domain/category, status, sponsor.
- Use cases with no update in the last 6 weeks AND status not "Done/Rejected" → flag as stale.

### 1.6 Deliverables

- Every active deliverable has: owner, due date, status, audience, and a path to the current file version.
- Statuses align with file-system state (Notion says "Submitted" → file is in `30 Deliverables/`).
- Superseded versions are linked to their successor rather than left dangling.

### 1.7 Risks & Issues

- Every row has severity, likelihood, owner, mitigation.
- Open risks > 4 weeks with no mitigation activity → flag for review.
- Closed risks with a date → keep for audit; do not delete.

### 1.8 Market Intelligence

- Every row has source (URL or citation) and date.
- Entries > 6 months old with relevance "Low" → archive.
- Duplicate entries on the same topic → merge.

### 1.9 Open Questions

- Every row has owner and deadline.
- Any question answered but not closed → close it and migrate the answer to Key Information if it's a lasting fact.
- Open questions with no activity in 30 days → flag for user triage.

### 1.10 Key Information

- Every row has category, source, date.
- Facts that have been superseded by a later entry → mark superseded, link forward.

### 1.11 Files Index

- Cross-check completed during file-system hygiene. Here, confirm every Notion row's path still resolves on disk.
- Orphaned rows (file not found) → resolve (update path) or archive.

---

## Step 2 — Consolidate the action list

Collect every issue found in Step 1 into a single report. Format:

```
Notion hygiene proposals — YYYY-MM-DD

[Database]:
  - [Action]: [Entity] — [reason]
  - …

CONTRADICTIONS (human call required):
  - [Description]

STALE ITEMS (need user triage):
  - [Entity] — [last activity date]

PROPOSED AUTOMATED FIXES:
  - [N] rows with status auto-update (Operational migration, Superseded re-tag, Archive)
  - [N] rows with owner/due-date missing — cannot be fixed without user input

Proceed with automated fixes?
```

---

## Step 3 — Execute approved fixes

After the user approves, apply fixes in this order:

1. **Auto-tags:** Re-tag superseded decisions, migrate absorbed operational decisions, mark dormant stakeholders, archive old market intelligence.
2. **Close loops:** Close answered Open Questions (migrate content to Key Information where appropriate).
3. **Archive completions:** Move "Done" tasks > 90 days to archived.
4. **Update links:** Point superseded deliverables at their successors.
5. **Fix orphaned Files Index rows.**

Never delete a Notion row. Use archive flags. Deletion is reversible only by recreating from backup and Notion's recovery window is not guaranteed.

---

## Step 4 — Cross-layer reconciliation (5 min)

1. Every **active decision** in `project-context.md` Section 7 has a Notion Decisions row.
2. Every **active stakeholder** in `project-context.md` Section 5 has a Notion Stakeholders row.
3. Every **landmine** in Section 8 has a Notion Risks & Issues row.
4. Every **deliverable** in Section 9 has a Notion Deliverables row with matching status.
5. Every **compressed meeting** in Section 14 has a Notion Meetings row.

Mismatches → add the missing row, or correct the Layer 1 pointer.

---

## Step 5 — Update metadata

1. Add a one-liner to `project-context.md` Section 18 (Change Log). Example: *"2026-05-04 — Notion hygiene: 6 operational decisions migrated, 3 stakeholders marked dormant, 14 tasks archived."*
2. Update **Last updated** on `project-context.md`.

---

## Postconditions

- All 11 databases pass the integrity check, or flagged exceptions are on the user's triage list.
- Every row in every DB has its mandatory properties populated.
- Cross-layer pointers between Layer 1 and Layer 2 are consistent.
- No automated deletions took place — archive flags only.
- Change log updated.

---

## Output to the User

```
Notion hygiene complete — YYYY-MM-DD
- Databases scanned: 11
- Issues found: [N]
- Auto-fixes applied: [N]
- Items flagged for user triage: [N]
- Cross-layer mismatches resolved: [N]
```

Follow with the triage list if non-empty, so the user can action it in a subsequent session.

---

## Failure Modes to Avoid

- **Do not delete rows.** Archive only.
- **Do not auto-resolve contradictions.** Flag for user.
- **Do not silently change a decision's foundational/operational tag without preserving the original tag in a history note.**
- **Do not process all 11 DBs in one write burst.** Batch writes per DB and confirm each batch succeeded before moving to the next — partial failures mid-pass are hard to untangle.
