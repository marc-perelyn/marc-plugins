# New Project Setup — Procedure

**Run:** Once, when bootstrapping a new project with `project-copilot`.
**Duration:** ~30–45 minutes for the interactive parts; creating Notion databases may take longer depending on user preferences.
**Scope:** Creates the folder structure, config file, project-context.md, Notion workspace skeleton, and scheduled daily briefing task for a brand-new project.

---

## Preconditions

1. The user has a project in mind with at minimum: a project name, a client (if applicable), a role, and a rough mission.
2. The user has decided where on disk the project root should live.
3. The user has access to a Notion workspace where the project's brain will live.
4. The `project-copilot` skill is installed and reachable.

---

## Step 1 — Interview the user (5 min)

Use a single structured intake, not rapid-fire questions. Ask for:

1. **Project short name** (used everywhere — keep it snappy, 2-4 words).
2. **Formal name** (used in client-facing artifacts).
3. **Client organization** (if external) or "Internal".
4. **User's role** on this project.
5. **Mission** — one sentence on what the project exists to achieve.
6. **Start date** and **target end date** (ok to approximate).
7. **Project root path on disk** — absolute path.
8. **Notion workspace/page** — where the brain should live.
9. **Client language** and **internal language** (default en/en).
10. **Timezone** (default: user's system).
11. **Calendar source** (Outlook / Google / iCal / none).
12. **Any CI constraints** (templates, brand assets) — yes/no; details can come later.
13. **Any project-specific folders** beyond the default 00-60 structure — free text.
14. **Any known political rules** up front — free text, can stay empty.

Record the answers. They become the initial values in `config.yaml`.

---

## Step 2 — Create the folder structure (2 min)

At the project root, create:

```
[Project Root]/
├── .copilot/
│   ├── backups/
│   └── config.yaml              # populated in Step 3
├── 00 Admin/
│   ├── Contracts/
│   ├── Daily Briefings/
│   └── Backups/
├── 10 Input/
├── 20 Meetings/
│   ├── Transcripts/
│   ├── Summaries/
│   └── Guides/
├── 30 Deliverables/
├── 40 Communication/
├── 50 Research/
│   └── Weekly Scans/
├── 60 Working/
│   ├── Meeting Prep/
│   └── Archive/
└── [70+ project-specific folders as declared]
```

Create any additional 70+ folders the user declared in Step 1.

---

## Step 3 — Generate `config.yaml` (3 min)

1. Copy `references/config.template.yaml` (from this plugin) to `.copilot/config.yaml` in the project root.
2. Fill in every field from the Step 1 interview.
3. Leave Notion database IDs blank for now — they will be populated after Step 4.
4. Commit to disk. Show the user the populated config for a quick sanity check before moving on.

---

## Step 4 — Create the Notion workspace skeleton (10 min)

Create the eleven standard databases under the project's Notion root page. Use the property names listed in `SKILL.md §6` exactly.

| # | Database | Required properties |
|---|---|---|
| 1 | Meetings | Date, Title, Type, Attendees (relation → Stakeholders), Decisions (relation → Decisions), Tasks (relation → Tasks), Summary, Transcript file ref, Status |
| 2 | Decisions | Title, Status, Date, Decision maker (relation → Stakeholders), Rationale, Impact, Foundational/Operational, Meeting (relation → Meetings), Tasks (relation → Tasks) |
| 3 | Tasks | Title, Owner, Due date, Priority, Status, Category, Related to (relation), Notes |
| 4 | Stakeholders | Name, Role, Organization, Division, Email, Influence level, Stance, Communication preference, Notes, Meetings (relation) |
| 5 | Use Cases (or renamed unit-of-work) | Name, Domain, Status, Business impact, Feasibility, Sponsor (relation → Stakeholders), Notes |
| 6 | Deliverables | Name, Type, Status, Due date, Audience, File reference, Version, Tasks (relation) |
| 7 | Risks & Issues | Title, Type, Severity, Likelihood, Owner, Mitigation, Status, Date identified |
| 8 | Market Intelligence | Title, Technology/Vendor, Category, Relevance, Date, Source, Summary |
| 9 | Open Questions | Question, Context, Owner, Deadline, Status, Resolution |
| 10 | Key Information | Title, Category, Content, Source, Date, Related to |
| 11 | Files Index | Filename, Location, Type, Description, Date added, Related to, Last updated |

**Relation setup:** create the databases first with scalar properties, then add relations in a second pass. Notion relations need both databases to exist.

**Rename rules:** If the user wants a different label for the "Use Cases" DB, create the DB with the new name and also set `config.yaml → notion.unit_of_work_label` to match.

Once all databases exist, copy their IDs (or URLs) back into `config.yaml → notion.databases`.

---

## Step 5 — Generate `project-context.md` (5 min)

1. Copy `references/project-context.template.md` (from this plugin) to `[Project Root]/project-context.md`.
2. Fill in:
   - Section 1 (Project Identity) from Step 1 answers.
   - Section 2 (Scope) — ask the user for initial in/out-of-scope bullets.
   - Section 3 (Objectives) — ask for 3-7 initial objectives.
   - Section 6 (Rules of Engagement) — paste the political rules from Step 1.
   - Section 10 (Taxonomy) — leave empty if the user hasn't surfaced terms yet; populate later.
   - Section 11 (Communication & Tooling) — derive from config.
   - Section 12 (Current Focus) — one line for "Week 1 kickoff".
   - **Last updated** line and an initial Section 18 change-log entry.
3. Leave Sections 5, 7, 8, 9, 13, 14 empty with their headings intact. They fill up naturally as the project progresses.

---

## Step 6 — Install scheduled daily briefing (2 min)

1. Create a scheduled task (via the `schedule` skill if installed, or note it manually for the user to set up) that runs daily at `config.yaml → daily_briefing.time`.
2. The task's job is to refresh `project-context.md` **Section 12 only**, per the rules in `SKILL.md §8`.
3. Do **not** install any scheduled task that updates other sections of Layer 1.

---

## Step 7 — Seed initial data (5–10 min, optional)

If the user already has starting materials for this project:

1. For each existing document → place in the correct folder, rename per the `YYYY-MM-DD_DescriptiveTitle_vX.ext` convention, add a row to the Files Index DB.
2. For any known stakeholders → add them to Stakeholders DB and mirror the active ones into `project-context.md` Section 5.
3. For any known decisions → record them in Decisions DB (foundational or operational) and mirror foundational ones into Section 7.
4. For any known risks → Risks & Issues DB, landmines into Section 8.

---

## Step 8 — Validate setup (3 min)

Run a quick end-to-end check:

1. Load the skill, config, and project-context.md as if starting a fresh session.
2. Confirm every referenced Notion database resolves.
3. Confirm every path in `config.yaml` exists on disk.
4. Confirm `.copilot/backups/` exists and is writable.
5. Confirm `project-context.md` size is well under the token budget (should be for a new project).
6. Post a one-paragraph "I am ready to work on [Project]" confirmation to the user, listing what was created.

---

## Postconditions

- Project folder tree exists per `SKILL.md §7`.
- `.copilot/config.yaml` is fully populated.
- `project-context.md` exists at the project root with filled-in identity and placeholder sections.
- 11 Notion databases exist with the standard schema, linked via relations.
- Scheduled daily briefing is configured (or documented for manual setup).
- Any seed documents are filed correctly and indexed in Notion.

---

## Output to the User

```
New project bootstrap complete — [Project Short Name]

Created:
- Folder tree: [path]
- Config: .copilot/config.yaml
- Context file: project-context.md
- Notion databases: 11 (linked)
- Scheduled daily briefing: [time]

Next step: tell me when your first meeting or first deliverable is — I'll start populating intelligence from there.
```

---

## Failure Modes to Avoid

- **Do not proceed if the user cannot give a mission in one sentence.** Stop, iterate on the mission. Everything else depends on it.
- **Do not create the Notion databases in parallel with the folder tree** — if Notion creation fails, you don't want an orphan folder tree advertising a workspace that doesn't exist.
- **Do not skip Step 8.** A silent misconfiguration here breaks every future session.
- **Do not copy Liebherr-specific (or any other project's) content into the new context file.** Templates only. All project specifics come from Step 1.
