# [Project Short Name] — Project Context

> **This is Layer 1** of the project-copilot three-layer architecture. It stores **what is true right now**, **why key decisions were made that way**, and **how to navigate this project**. It does not store "what happened" — that belongs in Notion (Layer 2) and the file system (Layer 3).
>
> **Core test for every item below:** *"If this changed tomorrow, would it change how I behave, whom I approach, or what I say?"* If yes → here. If it is fact, history, or status → Notion or file system.
>
> **Size budget:** ≤ 20K tokens (~500 lines). If this file grows past that, a pruning pass is overdue.

---

**Last updated:** YYYY-MM-DD
**Update cadence:** Daily (Section 12 only) · Weekly pruning (Friday) · Monthly hygiene (first Monday)
**Operating model:** `project-copilot` skill (SKILL.md)
**Config:** `.copilot/config.yaml`

---

## 1. Project Identity

- **Formal name:** [Full Project Name]
- **Client:** [Client Org]
- **User's role:** [e.g. Senior AI Project Lead]
- **Mission (one sentence):** [What this project exists to achieve]
- **Start → target end:** YYYY-MM-DD → YYYY-MM-DD
- **Current phase / week:** [e.g. Discovery, W3]

---

## 2. Mandate & Scope

### In scope

- [Bullet — what the project commits to delivering]
- [Bullet]

### Out of scope

- [Bullet — what the project explicitly does NOT cover]
- [Bullet]

### Non-negotiables

- [Conditions that would break the engagement if violated]

---

## 3. Objectives & Success Criteria

| # | Objective | Success criterion | Owner | Status |
|---|-----------|-------------------|-------|--------|
| 1 | [What] | [How we know it's done] | [Name] | [🟢/🟡/🔴] |
| 2 |  |  |  |  |

*Status legend:* 🟢 on track · 🟡 at risk · 🔴 blocked · ⚪ not started

---

## 4. Operating Approach

The project-specific method, framework, or playbook being used. Keep it tight — link out to deeper docs rather than reproducing them.

- **Method / framework:** [Name + one-line description]
- **Cadence:** [Weekly steering meeting, daily standup, etc.]
- **Artifacts produced:** [Top-level list — full inventory lives in Notion Deliverables DB]

---

## 5. Stakeholder Map (Active Only)

Only people who currently influence day-to-day decisions. Historical contacts and full profiles live in Notion Stakeholders DB.

| Name | Role | Org / Division | Influence | Stance | Notes |
|------|------|----------------|-----------|--------|-------|
| [Name] | [Title] | [Unit] | High/Med/Low | Supportive/Neutral/Skeptical/Blocker | [One-liner] |

→ **Full roster + history:** Notion Stakeholders DB

---

## 6. Political & Cultural Rules of Engagement

Short imperatives that change how the user should act. No prose. No history.

- [e.g. "Always brief the CFO before the CIO on financial figures."]
- [e.g. "Use German in all steering committee material."]
- [e.g. "Never copy legal on rough drafts."]

---

## 7. Active Decisions (Foundational)

Decisions that still shape current behavior. Foundational only. Operational decisions older than ~3 weeks migrate to Notion.

| # | Decision | Date | Rationale | Still active because… |
|---|----------|------|-----------|-----------------------|
| D1 | [What was decided] | YYYY-MM-DD | [Why] | [What would change if we abandoned it] |

→ **Full decision log (including superseded + operational):** Notion Decisions DB

*Aim for ≤ 15–20 entries here. If more, migrate the oldest operational ones.*

---

## 8. Open Landmines & Watch Items

Risks, sensitivities, or unresolved questions that could disrupt progress if ignored. RAID log lives in Notion — this section only lists what's hot right now.

- ⚠️ [Short name] — [one-line why it matters, who owns it]
- ⚠️ [Short name] — …

→ **Full RAID log:** Notion Risks & Issues DB

---

## 9. Deliverables (High-Level View)

One-line pointer per active deliverable. Full spec, version history, audience in Notion.

| Deliverable | Type | Status | Due | Path |
|-------------|------|--------|-----|------|
| [Name] | Report / Deck / Memo | Planned / In progress / Review / Submitted | YYYY-MM-DD | `30 Deliverables/…` |

→ **Full inventory:** Notion Deliverables DB

---

## 10. Project Taxonomy & Domain Vocabulary

Only terms the copilot must handle specifically. External glossaries should be linked, not pasted.

- **[Term]** — [one-line definition]
- **[Term]** — …

---

## 11. Communication & Tooling Conventions

- **Client language:** [de/en/…]
- **Internal language:** [de/en/…]
- **CI:** [Apply / Not applicable — see `.copilot/config.yaml`]
- **Primary channels:** [Email, Slack, Teams, …]
- **Where meetings live:** [Outlook / Google / …]
- **File naming:** `YYYY-MM-DD_DescriptiveTitle_vX.ext`

---

## 12. Current Focus (Updated Daily — ≤10 lines)

**Week:** [e.g. W6 · 2026-04-20]

- **This week's top goal:** [One sentence]
- **Hot items:** [2-4 bullets]
- **Landmines active this week:** [0-2 bullets]
- **Next decision point:** [What + when]

*This block is refreshed daily by the scheduled daily-briefing task. Nothing else in this file should change day-to-day.*

---

## 13. Recent Meetings (Rolling ≤ 2 Weeks)

Fresh entries get detailed bullets. Entries older than 2 weeks get compressed to one-liners at the next weekly pruning pass.

**M[N] — YYYY-MM-DD — [Meeting title]**
Attendees: [list]
Outcome: [one sentence]
Pattern-breaking intelligence (if any — most meetings have none):
- [What changed about who's on the radar, what we say, or how we behave]
Summary: `20 Meetings/Summaries/YYYY-MM-DD_….md`
Notion: [link]

---

## 14. Compressed Meeting History

One line per meeting older than 2 weeks. Promote an insight up into Sections 5/6/7 first if it should keep influencing behavior, then compress.

- M[N-k] YYYY-MM-DD · [Title] → [one-sentence outcome]. Summary: [path]. Notion: [link]

---

## 15. Pointers (Layer 2 & Layer 3)

- **Notion workspace:** [link]
- **Key databases:** [links or IDs — or defer to `.copilot/config.yaml`]
- **Project root on disk:** [absolute path]
- **Deliverables folder:** `30 Deliverables/`
- **Working folder:** `60 Working/`
- **Meeting transcripts:** `20 Meetings/Transcripts/`

---

## 16. Environment & Constraints

Environmental factors (budget, contract, access) that constrain how work is done. Keep to changes-of-state, not standing facts.

- **Contract window:** [dates]
- **Access constraints:** [e.g. no VPN from outside EU]
- **Known unavailability:** [e.g. client out YYYY-MM-DD → YYYY-MM-DD]

---

## 17. Session Start Checklist (For the Copilot)

When you load this file at the start of a session:

1. Read it in full.
2. Load `.copilot/config.yaml`.
3. Check **Last updated** above — if > 5 days old, ask the user what changed.
4. Confirm readiness in one sentence.
5. Wait for the task.

Do not summarize everything you read unless asked. Do not modify Layer 1 unless explicitly instructed.

---

## 18. Change Log for This File (Not a Journal)

One line per structural change to project-context.md itself. Not for project events.

- YYYY-MM-DD — Initial creation from template.

---

*End of project-context.md. Any content beyond this point is out of bounds and should be migrated to Notion or the file system.*
