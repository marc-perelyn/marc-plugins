---
description: Run the Personal OS evening shutdown — Chief of Staff §7.3, ≤5-min interaction
---

The user has invoked `/personal-os:evening-shutdown`. Run the **evening shutdown** per Chief of Staff §7.3.

This is the on-demand path. The cycle is constitutionally daily (§6.3 — "brief, pacing, shutdown"); the temporal anchor is "before the laptop closes," not a wall-clock fact, so Marc triggers it when he is actually closing the day.

Procedure:

1. Load the `chief-of-staff` skill at `marc-plugins/personal-os/skills/chief-of-staff/SKILL.md` if not already in context.
2. Load the `knowledge-steward` skill at `marc-plugins/personal-os/skills/knowledge-steward/SKILL.md`.
3. Read `/os/stage-0-constitution-and-architecture.md`, `/os/.os/config.yaml`, and `/os/.os/policy-library.yaml` (cache-eligible).
4. Run the §7.3 evening-shutdown procedure interactively against current state.

Shutdown contents per CoS §7.3, in order. Interaction, not a one-shot read — ask each question, collect Marc's answer, advance:

1. **Tomorrow prep done?** — meeting prep documents drafted; deep-work block defended. Pull tomorrow's calendar via CoS to anchor the question concretely.
2. **Open loops captured?** — anything from today that needs to land in KS (decisions, follow-ups, captures) before context is lost. Offer to route any uncaptured items through `KS.capture()` inline.
3. **Today's decisions written to Decision Log?** — `KS.search_decisions(date=today)`. Enumerate any material decisions surfaced in chat or notes today that are missing rows. Ask Marc to fill or skip; if fill, route through `KS.write_decision()` with the §6.4 protocol fields. If skip, the decision is by definition not material per §6.4 and that's fine.
4. **Drift fired today?** — name any drift signal that fired (deep-work block consumed by a meeting, planned outcome with no progress, unresolved calendar conflict). One line. Full pattern read happens at weekly. Stage 1 note: active pacing is documented-as-deferred in `policy-library.yaml`, so drift detection at shutdown is best-effort from observable signals, not from a pacing log.
5. **Laptop closes.** — your final line. Then you stop.

Mode discipline:

- In **Coach-mode** topics, do not press for closure. *"There's an open loop on [topic] but it's a Coach-mode item — leave it open, sleep on it."* is acceptable.
- In **degraded mode** (Constitution §3.6), shutdown reduces to a single line: *"Closing the laptop. Anything that cannot wait until you return?"* — do not enumerate.

Output:

- **Primary deliverable** — interactive in chat. ≤5-minute total interaction.
- **Durable copy** — write a shutdown note to `/os/episodic/{YYYY-MM-DD}/evening-shutdown.md` via `KS.write_note`. Include: tomorrow-prep status, open loops captured, decisions logged, drift named. If a same-day shutdown already exists (rare — Marc closes twice), suffix with `-{HH-MM}`.

Discipline (CoS §7.3):

- ≤5-min interaction. Over-running is the failure mode.
- Recommend, don't enumerate at length. One question, one answer, advance.
- "Laptop closes." is the final line. After it, stop. No coda, no encouragement.
