---
description: Capture a one-liner into the Personal OS — Knowledge Steward classifies and routes
---

The user has invoked `/personal-os:capture` followed by capture text (the arguments to this command). Treat the arguments as the capture input.

This is the deterministic capture entry point per Constitution §6.1 — sub-10-second, voice-memo-or-one-line-chat. Forms are forbidden.

Procedure:

1. Load the `knowledge-steward` skill at `marc-plugins/personal-os/skills/knowledge-steward/SKILL.md` if not already in context. Read it in full.
2. Read `/os/.os/config.yaml` and `/os/stage-0-constitution-and-architecture.md` (cache-eligible).
3. Pass the capture text to Knowledge Steward's `capture(input, source=chat)` operation per its §4. KS classifies (task / promise / fact / observation / event / decision / reference) and routes with smart defaults.
4. Confirm the classification and routing in **one line**. Example: *"Captured as a fact about Liebherr; updated entity row. Correct?"* — not a structured response.
5. If Marc corrects with one line, re-classify and re-route. Otherwise the capture is committed.

Discipline:

- Sub-10-second commitment applies. The confirmation must be one line, not a paragraph.
- If the capture is *material* (decision class ∈ strategic / investment / medical / legal / scope change / personnel), KS routes through Chief of Staff to run the §6.4 decision protocol. Surface this to Marc in the one-line confirmation.
- If the capture is sensitive (Coach-mode-engaging topic), KS pauses and asks consent before logging.
- The Pattern Engine observes every capture — that's part of `KS.capture()`, not a separate step.

If no arguments are passed, prompt Marc with: *"What do you want to capture?"* — one line, then capture his next utterance through the same path.
