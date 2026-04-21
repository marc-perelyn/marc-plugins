# marc-plugins

Marc Stiller's personal plugin marketplace for Claude Code and Cowork.

Sibling of `perelyn-plugins/` — same format, but this is the staging ground for plugins that are still personal-only or not yet ready for team-wide adoption. Once a plugin here proves itself across multiple users, it can be promoted to `perelyn-plugins/`.

## Installation

Add this marketplace to Claude Code:

```bash
claude plugins marketplace add /Users/marcstiller/Documents/ClaudeCowork/marc-plugins
```

Then install a plugin from it:

```bash
claude plugins install project-copilot@marc-plugins
```

In Cowork, the plugin is picked up automatically once the marketplace is registered.

## Plugins

### project-copilot

Operating model for running complex knowledge-work engagements (consulting projects, strategic initiatives, research programs) across sessions. Encodes the three-layer knowledge architecture, Notion brain schema, and weekly/monthly hygiene routines developed over the Liebherr AI Buy Strategy engagement.

See [`project-copilot/README.md`](./project-copilot/README.md).

## License

Personal tooling. Not licensed for external use.
