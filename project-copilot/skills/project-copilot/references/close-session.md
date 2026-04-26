# Session-Close Pass — Procedure

**Run:** At end of an interactive session, when the user says "close session", "end session", "wrap up", or invokes `/close-session`.
**Duration:** ≤3 min for routine sessions; ≤10 min when material changes need filing.
**Scope:** Detect what this session changed, surface open loops, prompt for filing decisions. Never destructive without approval. Never re-journal the session into Layer 1.

---

## Preconditions

1. Confirm SKILL, `config.yaml`, and `project-context.md` are loaded (this is a session-end ritual, so they should already be in context).
2. Identify the most recent pre-session snapshot of `project-context.md` — the most recent file in `.copilot/backups/` whose timestamp predates this session.

---

## Step 0 — Bail check (10 sec)

If the session was conversational-only (no Layer 1 edits, no Notion writes, no files created/modified, no decisions logged), bail:

```
Session was conversational. No close ritual needed. ✓
```

Detection signal: no edits to `project-context.md` since session start AND no entries appear to have been written to Notion this session AND no new files in the project's `60 Working/` or `30 Deliverables/` folders. If unsure, run the steps below — they're cheap.

---

## Step 1 — Layer 1 diff (1 min)

1. Diff `project-context.md` against the most recent pre-session backup. If no backup is recent enough (e.g. fresh project), diff against `git` HEAD if the project is in git, or report "no baseline available".
2. From the diff, surface:
   - Sections touched (e.g. §17.6, §19b).
   - "Last updated" header — was it refreshed to reflect today's work? If not, **flag**.
   - Change-log section — does today's date have an entry? If not, **flag**.
   - §19b Current Focus / current-week block — does it still reference yesterday's work as "today" or carry stale dates? If yes, **flag**.

Do not edit. Just report.

---

## Step 2 — Open-loop scan (1 min)

Walk the conversation transcript (or recent context) looking for items that were *introduced* this session but may not have been *filed*. Categories:

| Signal | Should be in | Flag if missing |
|---|---|---|
| A decision was made or proposed | Notion Decisions DB | Yes |
| A new task / next-step was committed to | Notion Tasks DB | Yes |
| A risk / blocker was identified | Notion Risks & Issues | Yes |
| A meeting was discussed / referenced | Notion Meetings + (if recent) `20 Meetings/Summaries/` | Yes |
| A new stakeholder was mentioned | Notion Stakeholders | Yes (if substantive) |
| An open question was raised but not resolved | Notion Open Questions | Yes |
| A handoff for next session was implied ("next time, push X") | `.copilot/handoffs/YYYY-MM-DD_<slug>.md` | Yes |
| A file was created or substantially modified | Notion Files Index (if 30 Deliverables/ or 10 Input/) | Best-effort |

For each flag, propose a specific filing target. Do not auto-create — wait for approval in Step 4.

---

## Step 3 — Handoff closure (30 sec)

1. List `.copilot/handoffs/*.md` (excluding `_done/`).
2. For each, ask: was this resolved during the session?
3. For resolved handoffs, propose moving to `.copilot/handoffs/_done/`.

Do not move yet — include in the Step 4 approval block.

---

## Step 4 — Present action list + summary (30 sec)

Single block to the user. Keep it ≤15 lines. Format:

```
Session close — YYYY-MM-DD HH:MM

WHAT LANDED
- [section / artifact / Notion entry] — [one-line description]

PENDING IN NOTION ([N])
- [DB] [proposed page title] — [one-line context] · CREATE?

HANDOFFS
- New: [path] for [reason]
- Resolve: [path] → _done/

LAYER 1 STALENESS
- "Last updated" header: [stale / current]
- §19b Current Focus dates: [stale / current]
- Change-log entry for today: [present / missing]

PROPOSED FIXES — apply?
- [list of small edits the user might want, e.g. "rewrite Last updated to reflect today"]
```

Wait for explicit approval. Partial approval is fine — execute only the approved subset.

---

## Step 5 — Execute approved actions (1–5 min)

1. Notion writes (decisions, tasks, risks, etc.) — batch by DB; use `notion-create-pages`.
2. Handoff file moves to `_done/`.
3. Small Layer 1 fixes (header rewrite, change-log entry, §19b date refresh) — these are routine maintenance, not restructure.
4. Backup creation if Layer 1 changed materially and no backup since session start.

Never run any of Step 5 without Step 4 approval.

---

## Postconditions

- Every material decision, task, risk, open question, meeting, and handoff introduced this session has a documented home (Notion or `.copilot/handoffs/`).
- `project-context.md` is internally consistent (header reflects current state; no stale "today" references).
- A session summary was emitted to the user.
- Backup exists for any substantial Layer 1 change.

---

## Output to the User (final)

```
Session closed — YYYY-MM-DD
- Notion entries created: [N]
- Handoffs filed: [N] new · [N] resolved
- Layer 1 fixes applied: [N]
- Open follow-ups for next session: [list, ≤3 lines]
```

If no material activity, just `Session closed — no action needed. ✓`

---

## Failure Modes to Avoid

- **Do not re-journal the session into `project-context.md`.** The change-log entry is a single dated line, not a narrative. Detail belongs in Notion.
- **Do not auto-execute without Step 4 approval.** Same pattern as weekly-pruning + monthly-hygiene.
- **Do not run on non-interactive sessions** (scheduled tasks, daily briefings). Refuse and report.
- **Do not invent open loops.** If the conversation didn't actually produce a decision/risk/task, don't manufacture one to fill the report.
- **Do not duplicate weekly-pruning work.** This procedure is event-driven (per session); weekly Step 0 is calendar-driven (Friday). They're complementary, not redundant.
