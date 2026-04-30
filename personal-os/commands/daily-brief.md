---
description: Run the Personal OS daily brief — Chief of Staff §7.1, ≤2-min read
---

The user has invoked `/personal-os:daily-brief`. Run the **daily brief** per Chief of Staff §7.1.

This is the on-demand path. The cycle is constitutionally daily (§6.3) but Marc triggers it when he sits down at the desk rather than from a fixed-time scheduler. Treat invocation time as the brief time.

Procedure:

1. Load the `chief-of-staff` skill at `marc-plugins/personal-os/skills/chief-of-staff/SKILL.md` if not already in context.
2. Load the `knowledge-steward` skill at `marc-plugins/personal-os/skills/knowledge-steward/SKILL.md`.
3. Read `/os/stage-0-constitution-and-architecture.md`, `/os/.os/config.yaml`, and `/os/.os/policy-library.yaml` (cache-eligible).
4. Run the §7.1 daily brief procedure against current state.

Brief contents per CoS §7.1, in order, omit any line that is empty:

1. **Today's commitments** — calendar items, deep-work blocks named explicitly. Source: Outlook (CoS owns calendar reads).
2. **Tripwire status** — any tripwire close to firing or already fired. One line each. Source: `KS.get_tripwire_state()`.
3. **Decisions awaiting Marc** — `KS.get_open_decisions()`, grouped by area, most-blocking first.
4. **Decisions due for review today** — `KS.get_decisions_for_review(by=today)`, with original decision date.
5. **Override patterns from yesterday** — if any, one line. Full review at weekly.
6. **One forcing-function note** — if a deadline is approaching that the current week's plan does not adequately serve, name it. Else omit.

What the brief does NOT contain (CoS §7.1):

- Brand-new tasks not already in the operating plan.
- Re-summaries of meetings Marc was in.
- Encouragement, motivation, "have a great day" filler.
- Anything Marc could read for himself in 30 seconds in Outlook.

If degraded mode is active (Constitution §3.6 — Marc on leave / sick / off-grid), reduce to what is unmissable: hard tripwires only.

Output:

- **Primary deliverable** — surface the brief inline in chat. ≤2-minute read.
- **Durable copy** — write to `/os/episodic/{YYYY-MM-DD}/daily-brief.md` via `KS.write_note`. If a same-day brief already exists, suffix the filename with `-{HH-MM}` rather than overwriting (on-demand invocations can recur within a day if Marc returns to the desk later).

Discipline (CoS §7.1):

- ≤2-min read. Over-reporting is the failure mode.
- Recommend, don't enumerate.
- No mirroring. No filler.
- Do not surface SIPs in the daily brief unless the underlying pattern is itself a tripwire (CoS §9).
