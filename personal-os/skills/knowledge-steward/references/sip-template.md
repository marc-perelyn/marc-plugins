# System Improvement Proposal — Template

*Use this template when authoring a SIP. Knowledge Steward writes SIPs to `/os/.os/sips/<YYYY-MM-DD>-<slug>.md` when a Pattern Engine threshold crosses, per Constitution §7.*

---

## SIP-{YYYY-MM-DD}-{slug}: {Short title}

**Authored by:** Knowledge Steward (Pattern Engine)
**Date:** {YYYY-MM-DD}
**Status:** Proposed | Modified-by-Marc | Accepted | Rejected | Withdrawn
**Surfacing cycle:** Weekly review of {YYYY-WNN}

---

### 1. Pattern observed

What recurred enough to trigger this proposal.

- **Event class:** {free-text label, e.g., "drafting LinkedIn posts in Marc voice", "calendar conflict between Liebherr workshops and family commitments", "comms with German clients requiring formal Siezen"}
- **Occurrences:** {N} in {window} *(default threshold: 5 in 4 weeks)*
- **Source records:** *(URLs of the captures, decisions, or notes that contributed to the count — never copy content; reference)*
  - {URL or `/os/episodic/<date>/<file>` path}
  - {URL or path}
  - {…}
- **Areas / projects involved:** {list}
- **Sensitivity of underlying records:** {standard | confidential | private — if mixed, list distribution}

---

### 2. Proposal type

Pick exactly one (per §7):

- [ ] Add a template — a draft type with the same structure
- [ ] Add a tag or field — metadata being inferred each time
- [ ] Add a workflow — a sequence of steps that recurs
- [ ] Add or adjust a Specialist — domain-expert work that would benefit from a defined role
- [ ] Adjust a constitution rule — tripwire, weight, or autonomy default needs to change
- [ ] Promote, retire, or reshape an area or project
- [ ] Propose a new System Agent — only when no combination of existing five + Specialists + workflows handles the recurring class

---

### 3. The proposal

What specifically is being added, changed, or removed.

**What:** {one sentence}

**Where it lives:** {file path / Notion page / DB schema location / Specialist domain folder}

**Concrete change:**

{prose or pseudo-spec — for templates, the template itself; for tags/fields, the column definition; for workflows, the step list; for Specialists, the five-element definition draft (Role / Expertise / Process / Output / Constraints); for constitutional changes, the exact diff against the current Constitution; for area/project changes, the new state}

**Blast radius:** {what other parts of the system this touches — agents that need to learn it, existing records that need migration, downstream Specialists}

**Reversibility:** {fully reversible | reversible with effort | irreversible — and why}

---

### 4. Counter-case

The strongest argument *against* accepting this proposal. Required even when the case feels obvious; SIPs without counter-cases are mirroring drift caught in proposal form.

{prose}

Specific things to consider:

- Does the proposal pre-bake a specific that should keep earning its place?
- Is the recurrence genuine or is it a one-week artifact that the Pattern Engine over-counted?
- Would accepting cause architectural sprawl (new Specialist, new workflow, new System Agent — each carries cost)?
- Does the proposal conflict with the simplicity commitment in Stage 0 §1?
- Is there a smaller change (tag instead of workflow; adjustment to existing template instead of a new one) that would cover the same recurrence?

---

### 5. Marc's decision frame

What Marc is being asked to decide. Three options always available:

- **Accept as proposed** — apply the change verbatim. Versioned and added to procedural memory or the relevant scope.
- **Accept with modifications** — Marc edits the proposal inline; the modified version is what's applied.
- **Reject** — proposal is logged as rejected and is **not re-proposed for at least one quarter**, even if the underlying pattern continues to recur.

What would change Marc's mind: {prose — for accept, what would push toward reject; for reject, what would make it acceptable later}

---

### 6. Decision (filled in by Marc at weekly review)

- **Decision:** Accept | Modified | Rejected | Deferred-to-quarterly
- **Date decided:** {YYYY-MM-DD}
- **Reasoning:** {Marc's one to three sentences}
- **Modifications (if any):** {inline edit or pointer to revised version}
- **Re-propose-after (if rejected):** {YYYY-MM-DD — default: today + 90 days}

---

### 7. Application (filled in by Knowledge Steward after acceptance)

- **Applied:** {YYYY-MM-DD}
- **Versioned changes:**
  - {file path or Notion page} — {what changed}
  - {…}
- **Migration of existing records:** {if any, summary; if none, "none"}
- **Communicated to agents:** {list of agents whose context or behaviour shifts as a result}
- **Links to Decision Log:** *(every accepted SIP creates a row in Decision Log with class=strategic, recommender=Knowledge Steward, decider=Marc)*

---

*End of SIP. The SIP itself is procedural memory; once applied, it becomes part of the audit trail at quarterly meta-review (Constitution §3.5 adversarial pass: "where has the system softened? Where has it converged on the Principal?").*
