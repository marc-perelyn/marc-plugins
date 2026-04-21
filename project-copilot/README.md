# project-copilot

A Claude plugin that provides the operating model for running complex knowledge-work engagements (consulting projects, strategic initiatives, research programs, product builds) across many sessions without losing context.

## Overview

This plugin does **not** store project data. It defines **how** to work — the division of labor between the context file, Notion, and the file system; the session lifecycle; how to classify incoming information; when to prune. Each project brings its own:

- `project-context.md` at the project root (the "map")
- `.copilot/config.yaml` (project-specific IDs, stakeholders, taxonomy, language, CI, governance rules)
- A Notion workspace with the standardized 12 databases

Once those are in place, any session that loads the skill gets the full operating model and project-specific context automatically.

## The Three-Layer Architecture

| Layer | What | Role |
|---|---|---|
| **Layer 1** | `project-context.md` at project root | Session restoration & permanent intelligence. The "map." ≤20K tokens. |
| **Layer 2** | Notion workspace with 12 databases | Structured operational tracking. The "detail." |
| **Layer 3** | File system | Artifacts, documents, deliverables. The "output." |

Layer 1 stores what's true right now and why decisions were made that way. Layer 2 stores the historical record and operational detail. Layer 3 stores artifacts, referenced from Layers 1 and 2 via path pointers.

## Commands

- `/project-copilot:start-session` — Run the session-start ritual (load skill, read config, read project-context.md, check handoffs).
- `/project-copilot:new-project` — Bootstrap a new project with the skill's folder structure, config template, and Notion schema.
- `/project-copilot:weekly-pruning` — Run the end-of-week pruning pass: migrate old decisions, compress meeting entries, reconcile Current Focus.
- `/project-copilot:monthly-hygiene` — Run the monthly pass: Notion hygiene + file-system hygiene + Layer 1 size check.

## Skill Invocation

The skill also triggers automatically on phrases like:

- "start [project name] session"
- "project copilot"
- "load project context"
- Or when a project folder contains a `.copilot/config.yaml`

## Installation

This plugin lives in the `marc-plugins` marketplace.

```bash
claude plugins marketplace add /Users/marcstiller/Documents/ClaudeCowork/marc-plugins
claude plugins install project-copilot@marc-plugins
```

## Bootstrapping a New Project

1. Create the project folder.
2. Run `/project-copilot:new-project` — the skill will scaffold `.copilot/config.yaml` from the template, create `project-context.md` from the template, lay down the default folder structure (`00 Admin/`, `10 Input/`, `20 Meetings/`, etc.), and guide you through creating the 12 Notion databases.
3. Fill in project-specific details in `.copilot/config.yaml` (Notion IDs, stakeholders, CI, language, etc.).
4. Use `/project-copilot:start-session` to open your next session.

## Using an Existing Project

Projects that already have `.copilot/config.yaml` + `project-context.md` at the root (e.g., Liebherr AI Buy Strategy) continue to work unchanged. The skill reads whatever config and context the current project supplies.

## Structure

```
project-copilot/
├── .claude-plugin/plugin.json        # manifest
├── README.md                          # this file
├── commands/                          # slash commands
│   ├── start-session.md
│   ├── new-project.md
│   ├── weekly-pruning.md
│   └── monthly-hygiene.md
└── skills/project-copilot/
    ├── SKILL.md                        # the operating model (project-agnostic)
    └── references/
        ├── config.template.yaml        # per-project config template
        ├── project-context.template.md # Layer 1 template
        ├── weekly-pruning.md           # weekly hygiene procedure
        ├── notion-hygiene.md           # monthly Notion pass
        ├── filesystem-hygiene.md       # monthly file-system pass
        └── new-project-setup.md        # project bootstrap procedure
```

## Authoring Notes

- SKILL.md is the single source of truth for operating principles.
- `references/*.template.*` files are copied into a new project during bootstrap.
- `references/*-hygiene.md` and `references/weekly-pruning.md` are procedures the skill reads on demand — they do not get copied into projects.
