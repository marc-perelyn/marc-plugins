# personal-os

Marc Stiller's **Personal Operating System** — a small, durable arrangement of agents, workflows, and shared memory whose job is to make the Principal successful in his role at Perelyn and in his personal life, in that integrated order. Not a productivity tool. A small team, built from a fixed roster of System Agents, a library of Specialist roles, a shared memory, and a constitution.

This plugin is **code**. The running OS's state — Constitution, decision log, episodic memory, Pattern Engine observations, authored SIPs — lives separately under `/Users/marcstiller/Documents/ClaudeCowork/projects/os/` and in the user's Notion workspace. The plugin reads `projects/os/.os/config.yaml` to find both.

## Architecture (Stage 0 v0.2)

Two design commitments are non-negotiable:

- **Simplicity.** A small fixed set of primitives. Specifics (templates, tags, fields, libraries) are *content* that lives inside the primitives, not new architecture.
- **Pattern-driven evolution.** Specifics earn their place through demonstrated use, not preemptive design. The Pattern Engine (Constitution §7) proposes additions when patterns recur; the Principal accepts or rejects.

Read the full Constitution at `projects/os/stage-0-constitution-and-architecture.md` and the design context at `projects/os/stage-0-handoff-brief.md` before working on this plugin.

## The Five System Agents (fixed roster)

Per Constitution §5.1. Stage 1 activates the first two; the rest activate in later stages on evidence.

| Agent | Role | Stage activated |
|---|---|---|
| **Chief of Staff** | Orchestrator. Owns calendar/time state. Routes work between Specialists, agents, and humans. Enforces the autonomy ladder. Selects model tier per task. Runs daily/weekly/monthly/quarterly cycles. | Stage 1 |
| **Knowledge Steward** | Owns the three memory scopes and three types. Performs hygiene. Maintains the entity graph and the decision log. Provides indexed/scoped memory access. Hosts the Pattern Engine. | Stage 1 |
| **Challenger** | Owns the anti-mirror commitment. Standing rights to surface. Runs override review and quarterly adversarial review. | Stage 4 |
| **Comms** | Voice and format substrate. Adapts content into target voice and format. Handles redaction at the gate. | Stage 4 |
| **Researcher** | On-demand. Investigates novel topics, pulls external knowledge, runs synthetic-expert reviews. | Stage 4 |

System Agents are **fixed at five**. Domain expertise lives in **Specialists** — role configurations defined in domain procedural memory, instantiated by Chief of Staff when relevant work arises. Specialists are written into Personal Affairs domain memory in Stage 2 and beyond.

## The Three Memory Scopes (per Constitution §4)

| Scope | Holds | Read by | Written by |
|---|---|---|---|
| **Global** | Constitution, entity graph, decision log, area & project indexes, calendar/time state, voice/brand standards | Every agent | System processes only |
| **Domain** *(Stage 2+)* | Area-specific procedures, KPIs, stakeholder context, Specialist role definitions | Agents tagged to that area | Same |
| **Local** *(Stage 3+ under new architecture; Stage 1 still uses project-copilot)* | Project Layer-1, project-scoped decisions and entities | Agents in scope | Same |

**Two non-negotiable rules:** one identity per entity, one source of truth per fact.

## Stage Plan

Per Constitution §9. Each stage produces a working system before the next begins.

- **Stage 0** — Constitution and architecture. Approved 2026-04-30 at v0.2.
- **Stage 1** — *(this plugin's current scope)* Skeleton in production: Chief of Staff and Knowledge Steward; global memory layer in Notion; capture path; daily/weekly/monthly cycles; Pattern Engine observation begins.
- **Stage 2** — Personal Affairs domain memory and first Specialists (Health, Finances).
- **Stage 3** — `project-copilot` rewritten under the new architecture. Until then, `project-copilot` continues to run for active projects (Liebherr, etc.) as a sibling plugin.
- **Stage 4** — Challenger, then Comms, then Researcher activated as load justifies.
- **Stage 5** — Additional domains, Specialists, and per-project agents on evidence.

## Installation

This plugin lives in the `marc-plugins` marketplace.

```bash
claude plugins marketplace add /Users/marcstiller/Documents/ClaudeCowork/marc-plugins
claude plugins install personal-os@marc-plugins
```

In Cowork, the plugin is picked up automatically once the marketplace is registered.

## Slash commands

Explicit entry points. Shipped as of 2026-04-30.

| Command | Purpose | Anchored to |
|---|---|---|
| `/personal-os:capture <text>` | Sub-10-second capture; KS classifies (task / promise / fact / observation / event / decision / reference) and routes with smart defaults; surfaces tripwire firings on capture per KS §4.1; surfaces override candidates per KS §5.1. | Constitution §6.1 |
| `/personal-os:daily-brief` | On-demand morning brief per CoS §7.1. ≤2-min read. Today's commitments, tripwire status, open decisions, decisions-due-for-review-today, yesterday's overrides, optional forcing-function note. | Constitution §6.2 / §6.3, CoS §7.1 |
| `/personal-os:evening-shutdown` | On-demand evening close-out per CoS §7.3. ≤5-min interaction. Tomorrow prep / open loops / decisions logged / drift / "Laptop closes." | Constitution §6.2 / §6.3, CoS §7.3 |

Cycles still on cron (calendar-pinned non-negotiables, not slash commands):

- **Weekly review** — Fri 17:00 (Marc's confirmed time); scheduled task `personal-os-weekly-review`. Per CoS §7.4.
- **Monthly hygiene + Quarterly meta-review** — first Mon 09:00, smart-routed by date; scheduled task `personal-os-monthly-quarterly-hygiene`. Per CoS §7.5 / §7.6.

The daily brief and evening shutdown are deliberately **on-demand** rather than cron-scheduled — Cowork scheduled tasks fire only when the Mac is awake and Claude Desktop is open, and these cycles' temporal anchors ("when I sit down" / "before I close the laptop") are not wall-clock facts. Active pacing is in scope per Constitution §6.3 + CoS §13 but **deferred** in `policy-library.yaml` until daily-brief data exists to pace against.

## Skill auto-invocation

Skills also trigger automatically on phrases that match their declared description (see each skill's frontmatter). Common entry points beyond the slash commands above:

- *"Remember that…", "log this"* — Knowledge Steward classifies and routes (same as `/capture`).
- *"What do I know about…", "show me decisions on…", "what's open"* — Knowledge Steward retrieval.
- *"What should I focus on", "what's drifting", "where do I stand"* — Chief of Staff orchestration.
- *"Is this material", "should I escalate this"* — Chief of Staff §6.4 decision protocol orchestration.
- *"Coach mode", "Challenger mode"* — mode switches (Constitution §3.4).

## State (lives outside this plugin)

The plugin reads but does not write to:

- `projects/os/.os/config.yaml` — Notion DB IDs, sensitivity vocabulary, priority axes, autonomy ladder values.
- `projects/os/stage-0-constitution-and-architecture.md` — the Constitution (file copy; Notion is the other authoritative copy).
- `projects/os/stage-0-handoff-brief.md` — Stage 0 design context.
- `projects/os/episodic/` — episodic memory, written by Knowledge Steward at runtime.
- `projects/os/.os/pattern-events/` — Pattern Engine observation buffer.
- `projects/os/.os/sips/` — authored System Improvement Proposals.

Plus the four global Notion databases referenced in `config.yaml`: Areas, Entities, Projects, Decision Log.

## Structure

```
personal-os/
├── .claude-plugin/plugin.json          # plugin manifest
├── README.md                            # this file
├── skills/
│   ├── knowledge-steward/
│   │   ├── SKILL.md                     # memory ownership + Pattern Engine
│   │   │                                #   §4 capture classification
│   │   │                                #   §4.1 tripwire evaluation on capture
│   │   │                                #   §5 decision log discipline
│   │   │                                #   §5.1 override detection on capture
│   │   │                                #   §7 hierarchical compression + hygiene
│   │   │                                #   §8 Pattern Engine
│   │   └── references/
│   │       └── sip-template.md          # System Improvement Proposal template
│   └── chief-of-staff/
│       ├── SKILL.md                     # orchestration + autonomy ladder + cycles
│       │                                #   §7.1 daily brief
│       │                                #   §7.3 evening shutdown
│       │                                #   §7.4 weekly review
│       │                                #   §7.5 monthly hygiene
│       │                                #   §7.6 quarterly meta-review
│       │                                #   §9 routing rules
│       │                                #   §9.1 tripwire_fired receiver procedure
│       └── references/                  # (filled as patterns warrant)
└── commands/
    ├── capture.md                       # /personal-os:capture
    ├── daily-brief.md                   # /personal-os:daily-brief
    └── evening-shutdown.md              # /personal-os:evening-shutdown
```

New commands earn their place from observed need per the Constitution's pattern-driven-evolution rule, not from pre-baking. Stage 4 will likely add commands as Comms / Researcher / Challenger ship.

## Authoring Notes

- The Constitution is the single source of truth for operating principles. Skills implement it; they do not amend it.
- Constitutional amendments happen at the quarterly meta-cycle, deliberately and visibly.
- New System Agents only via Pattern Engine proposal at quarterly review (Constitution §7), and only when no combination of the existing five plus Specialists plus workflows handles the recurring class.
- New Specialists are *content* — written into domain procedural memory under the relevant area, not added to this plugin's `skills/` folder. (Possible exception: skills closely tied to a single global Specialist may be packaged here once the pattern is clear; defer until needed.)

## License

Personal tooling. Not licensed for external use.
