# File-System Hygiene Pass — Procedure

**Run:** First Monday of every month (or the weekday declared in `config.yaml → behavior.hygiene_weekday`).
**Duration:** ~20 minutes.
**Scope:** The project's folder structure on disk (Layer 3). Does not touch Layer 1 or Layer 2 except to update the Files Index.

---

## Preconditions

1. Confirm SKILL, config, and project-context are loaded.
2. Confirm the project root path from `config.yaml → paths.root`.
3. Nothing destructive happens before the user has approved the action list in Step 5.

---

## Step 1 — Inventory the root (2 min)

1. List all files/folders in the project root.
2. The only permitted items at root are:
   - `project-context.md`
   - `.copilot/`
   - The numbered top-level folders declared in `SKILL.md §7` (`00 Admin`, `10 Input`, `20 Meetings`, `30 Deliverables`, `40 Communication`, `50 Research`, `60 Working`, and any `70+` project-specific folders).
3. Any other file/folder at root → flag for relocation.

---

## Step 2 — Verify the standard subfolders exist (1 min)

For each top-level folder, confirm the canonical subfolders exist (see `SKILL.md §7`). If missing, create them empty. Never rename an existing folder without user approval.

---

## Step 3 — Scan for anomalies (5 min)

Walk the tree and collect candidates for action. Do not act yet — just list.

Categories to collect:

| Anomaly | Where to look | Action category |
|---------|--------------|-----------------|
| Files at root | Project root | Move |
| Files with no date prefix where one is expected | `20 Meetings/*`, `30 Deliverables/*`, `50 Research/Weekly Scans/*` | Rename |
| Superseded deliverable versions (`_v1`, `_v2`…) when a later `_vN` exists | `30 Deliverables/*`, `60 Working/*` | Archive to `60 Working/Archive/` |
| Daily Briefings older than 30 days | `00 Admin/Daily Briefings/` | Archive or delete per config |
| Duplicate filenames (same stem in multiple folders) | Anywhere | Investigate |
| Transcripts without matching summaries | `20 Meetings/Transcripts/` vs `20 Meetings/Summaries/` | Queue a summary creation task |
| Summaries without a Notion Meetings DB entry | `20 Meetings/Summaries/` vs Notion | Queue a Notion backfill |
| Files sitting in `60 Working/` root (not in a named subfolder) | `60 Working/` | Move into a subfolder or archive |
| Files explicitly rejected by the user in prior sessions | Anywhere | Flag for deletion |

---

## Step 4 — Cross-check Files Index (3 min)

1. For each file under `30 Deliverables/` and `10 Input/`, confirm it exists in the Notion **Files Index** database.
2. Add missing entries with the filename, path, type, description (one line), date added, and any related entity (stakeholder, meeting, deliverable).
3. Remove Files Index entries whose file no longer exists on disk — but only after confirming the file wasn't just moved. If moved, update the path.

---

## Step 5 — Present the action list (1 min)

Before doing anything destructive or structural, present the collected candidates to the user as a single action list:

```
File-system hygiene proposals — YYYY-MM-DD

MOVE ([N]):
  - [source] → [destination]
  - …

RENAME ([N]):
  - [old name] → [new name]
  - …

ARCHIVE ([N]):
  - [path] → 60 Working/Archive/
  - …

DELETE ([N]) (user rejected, confirmed obsolete):
  - [path]
  - …

BACKFILL ([N]):
  - Create summary for transcript: [path]
  - Create Notion Meetings entry for: [path]
  - Add Files Index entry for: [path]

Proceed?
```

Wait for explicit user approval. Partial approval is fine — execute only the approved subset.

---

## Step 6 — Execute approved actions (5 min)

1. **Moves and renames:** use `mv` via bash. Double-check destination paths exist.
2. **Archives:** move to `60 Working/Archive/` with original folder-of-origin preserved in the new filename if helpful (e.g. `deliv_YYYY-MM-DD_Report_v3.docx`).
3. **Deletions:** create a zip backup at `00 Admin/Backups/YYYY-MM-DD_pre-delete.zip` first, then delete. Never delete without a backup.
4. **Backfills:** file tasks in Notion Tasks DB for any summary/Notion-entry that needs to be created. Do not silently generate fake summaries.

---

## Step 7 — Update metadata (1 min)

1. Note the hygiene pass in Section 18 (Change Log) of `project-context.md` as a one-liner. Example: *"2026-05-04 — FS hygiene: 3 files moved, 2 archived, 1 backfill task queued."*
2. Update **Last updated** on `project-context.md`.

---

## Postconditions

- Project root contains only permitted items.
- All numbered top-level folders exist with canonical subfolders.
- No files flagged for move/rename/archive/delete remain unless the user declined.
- Backups exist for anything deleted.
- Notion Files Index is consistent with disk.
- Change log updated.

---

## Output to the User

```
File-system hygiene complete — YYYY-MM-DD
- Moved: [N]
- Renamed: [N]
- Archived: [N]
- Deleted (backup preserved): [N]
- Backfill tasks queued in Notion: [N]
- Backup archive: [path or "none"]
```

---

## Failure Modes to Avoid

- **Do not execute before user approval.** Step 5 is mandatory.
- **Do not delete without a backup zip.**
- **Do not rename a folder that other files reference.** Moving files in is fine; restructuring folders needs a separate conversation.
- **Do not silently generate a summary from a transcript.** Queue the task; let the user ask for the summary explicitly.
