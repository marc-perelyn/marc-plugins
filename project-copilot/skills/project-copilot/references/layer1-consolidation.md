# Layer 1 Consolidation Pass — Procedure

**When to run:**
- As part of monthly hygiene if the Layer 1 size + structure check (final step of `/monthly-hygiene`) flags drift.
- On demand when the user says "consolidate Layer 1" or "run consolidation" — escape hatch for mid-month drift.
- Never as part of weekly pruning — weekly Step 0 only *detects* drift; consolidation lives here.

**Duration:** ~30–45 min per pass, depending on which sections need work. Not a single linear procedure — a menu of section-level moves selected based on diagnostic flags.

**Scope:** `project-context.md` (Layer 1) only. Restructures sections, migrates content to Notion or `.copilot/` reference files, never touches Layer 3 directly.

---

## Preconditions

1. SKILL, `config.yaml`, and `project-context.md` loaded.
2. Snapshot `project-context.md` to `.copilot/backups/YYYY-MM-DD_pre-consolidation.md` before any edit. This is a heavier change than weekly pruning — the backup is non-negotiable.
3. Confirm Notion Stakeholders / Tasks / Risks / Open Questions / Deliverables / Key Information / Files Index are reachable (most consolidation moves push content into one of these).
4. The user has approved the consolidation. Consolidation always pauses for explicit approval — it is restructure, not maintenance.

---

## Step 1 — Diagnostic re-check (3 min)

Run the same six checks as weekly pruning Step 0, plus:

- **Section-level token budget:** measure token count per section (rough char-count / 4 is fine). Any section ≥30% of total Layer 1 budget is a candidate for consolidation.
- **Reference material in Layer 1:** scan for tables / lists that are reference data (frameworks inventory, folder trees, lookup tables) rather than behavior-shaping content. These are candidates for migration to `config.yaml` (if structured) or `.copilot/[name].md` (if narrative).
- **§-level duplication with SKILL/config:** sections that document HOW the copilot operates (architecture, update protocols, session-start instructions) duplicate the SKILL and should collapse to pointers.

Compile a flag list with section pointer + proposed move for each. Present to user.

---

## Step 2 — User approval of move list (2 min)

Present the consolidation plan in this format:

```
Layer 1 consolidation proposals — YYYY-MM-DD
Current size: [X tokens] (budget: [Y]). Target after pass: [Z].

Section-level moves:
  §[N] [Title]
    Issue: [diagnostic flag]
    Move: [where the content goes — Notion DB / config.yaml key / .copilot/ file / collapse to pointer]
    Estimated savings: [tokens]
    Risk: [low / moderate / high — what depends on this content elsewhere]

Migrations to Notion (require Notion connector):
  - [N] stakeholders to Stakeholders DB
  - [N] tasks to Tasks DB
  - [N] risks to Risks DB
  - …

Files to create in .copilot/:
  - [path] — [purpose]

Total estimated savings: [tokens] (~[%] reduction).
Proceed with all? Or pick a subset?
```

Wait for explicit approval. Partial approval is fine — execute only the approved subset. If Notion is unreachable, defer Notion-dependent moves to a follow-up session via a handoff file in `.copilot/handoffs/`.

---

## Step 3 — Section-level moves (menu, run only what was approved)

Each move below is independent. Execute in the order listed (low-risk first). Re-measure size after each section to confirm progress.

### 3a. Collapse architecture / update-protocol sections to SKILL pointers (low risk)

**Trigger:** sections that document the copilot's operating model (Three-Layer Architecture, Update Protocol, Session Start Instructions, "Sensitive Information" notes that duplicate `config.yaml political.rules` or `behavior.reveal_ai`).

**Move:** replace each section with a 1–3 line pointer to the relevant SKILL section. Keep only project-specific content (e.g. the project's scheduled tasks table, project-specific navigation pointers).

**Save:** typically ~80–120 lines / 1.5–2K tokens.

### 3b. Move folder structure tree to `.copilot/folder-structure.md` (low risk)

**Trigger:** the Folder Structure section is a >50-line ASCII tree.

**Move:** create `.copilot/folder-structure.md` with the full tree + key file locations + filing rules. Replace the Layer 1 section with a one-line pointer + last-verified date.

**Save:** ~80 lines / 1.2K tokens.

### 3c. Move framework inventory to `config.yaml` (low risk)

**Trigger:** a "Key Frameworks" table with reference rows (framework name + role description) that doesn't change between sessions.

**Move:** convert to YAML under `liebherr_context.key_frameworks` (or equivalent project-specific key). Keep behavior-shaping prose (e.g. mapping rules, baseline maturity) inline in Layer 1.

**Save:** ~15–25 lines / 400–600 tokens.

### 3d. Compress meeting archive index to one-liners (low risk)

**Trigger:** archive index is a wide multi-column table with multi-phrase takeaway cells.

**Move:** convert to bullet list using the SKILL template format: `**M[N]** YYYY-MM-DD · [Title] → [outcome]. · [path]`. Drop file-path columns, inline the path.

**Save:** ~5–10 lines / 300–500 tokens (modest, but improves scannability).

### 3e. Tighten political/approach profiles (moderate risk)

**Trigger:** stakeholder profiles in the political-intelligence section contain factual sentences (role, history, team composition) instead of approach rules only.

**Move:** for each profile, keep only sentences that answer "what do I do differently because of this?" Drop the rest — descriptive facts live in Notion Stakeholders.

**Save:** typically 30–50% per profile section / 600–1500 tokens.

**Verification:** spot-check that the daily briefing and session-start can still answer "how should I approach X?" using the tightened profile.

### 3f. Merge parallel stakeholder lists (moderate risk, Notion-dependent)

**Trigger:** Layer 1 has two parallel stakeholder lists (e.g. an operational "Stakeholder Map" and a political "Quick Reference" table) covering the same people.

**Preconditions specific to this move:** Notion Stakeholders DB has a current entry for every person in both lists, with org / role / engagement / political note populated. If gaps exist, audit first and create missing entries / fix duplicates / refresh stale notes before merging.

**Move:** collapse to one canonical list with Name · Org · Engagement · single political note (≤25 rows). All operational detail is in Notion. Intern team and similar sub-lists also collapse.

**Save:** 60–80 lines / ~2K tokens.

**Verification:** the daily briefing pulls per-person data from Notion (not from Layer 1) and the cross-section navigation pointers in §20 still resolve correctly.

### 3g. Rebuild Current Focus block (moderate risk, Notion-dependent)

**Trigger:** Current Focus / operational-status section runs ≥30 lines and contains delta blocks, second-tier carry-forward, open-name parking lots, or other operational accumulators.

**Preconditions:** Notion Tasks / Risks / Open Questions / Deliverables / Key Information are reachable.

**Move:**
1. Save the current Current Focus content to `.copilot/operational-status_YYYY-MM-DD.md` as a snapshot.
2. Migrate items into Notion DBs:
   - Action items → Tasks
   - Active risks → Risks
   - Open names / unresolved items → Open Questions
   - Shipped artifacts → Deliverables
   - Background facts (research projects, mapping references) → Key Information
3. Replace the Layer 1 section with a tight Current Focus block (≤15 lines): vacation/availability banner if relevant, top goal this week, active landmines, hard milestones in next 2–4 weeks, next decision point, pointer to the snapshot.

**Save:** ~60–80 lines / ~2K tokens.

**Verification:** daily briefing still surfaces the right priorities (it now reads from Notion, not the deleted delta blocks).

### 3h. De-journal "Last updated" header (low risk)

**Trigger:** header at the top of `project-context.md` contains nested prior-value paragraphs ("Last updated: X — prior value: Y — prior value: Z…").

**Move:** rewrite the header as one paragraph describing the current state. If change history needs to persist, create a separate "Recent change log" section directly below the header with one bullet per dated change (newest first).

**Save:** ~20–40 lines / 600–1000 tokens depending on how much journaling accumulated.

---

## Step 4 — Update metadata (2 min)

1. Update the **Last updated** line at the top of `project-context.md` (one paragraph; describe the consolidation). If a Recent change log exists, prepend a new entry there.
2. Add a one-liner to the change log noting which moves ran and how much was saved.
3. Re-measure file size and report against `behavior.layer1_token_budget`.

---

## Step 5 — Verification (3 min)

Smoke tests after consolidation:

1. Read the file end-to-end. Section structure must be intact (every `## N. Title` heading still parses). Section numbering may have changed if sections collapsed; if so, update internal cross-references.
2. Confirm every removed item has a target home: Notion entry, `config.yaml` key, or `.copilot/[file].md`. No orphaned content.
3. Spot-test the copilot's behavior: ask 2–3 questions that previously got rich answers ("how should I approach [stakeholder]?", "what's hot this week?", "why was [decision] made?"). Confirm answer quality is unchanged because content moved, not vanished.
4. Confirm the daily briefing scheduled task still resolves its data sources. If §-numbers it references changed, update the task or its config.

---

## Postconditions

- `project-context.md` parses cleanly and is under the token budget (or has a documented reason it can't go further without losing behavior-shaping content).
- Backup exists at `.copilot/backups/YYYY-MM-DD_pre-consolidation.md`.
- Every removed item has a documented target home (Notion / config / `.copilot/`).
- "Last updated" header is one paragraph; change log (if present) holds the journaling.
- Smoke tests pass.

---

## Output to the User

```
Layer 1 consolidation complete — YYYY-MM-DD
- Pre-size: [X tokens] · Post-size: [Y tokens] · Reduction: [Z%]
- Section moves executed: [count] of [proposed]
- Notion entries created: [count]
- .copilot/ files created: [list]
- Smoke tests: [pass / N flagged]
- Backup: [path]
```

If smoke tests flagged anything, list the items inline so the user can investigate.

---

## Failure Modes to Avoid

- **Do not run without explicit user approval of the move list.** Consolidation is restructure, not maintenance.
- **Do not skip the backup.** This is the most reversible-only-from-backup operation in the skill.
- **Do not execute Notion-dependent moves (3f, 3g) without verifying Notion is current.** Audit first; if gaps, defer those moves and create a handoff file.
- **Do not delete content without confirming its new home exists.** Every removed paragraph must be either obsolete or filed elsewhere.
- **Do not consolidate sections the user is actively editing.** If a section was touched in the last 48 hours, ask before restructuring it — the user may have unmerged context the SKILL rules don't see.
- **Do not change section numbering silently.** If §13 disappears and §14 becomes the new §13, surface this; cross-references in scheduled tasks or external docs may break.
