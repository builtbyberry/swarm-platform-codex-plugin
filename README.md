# Swarm — Codex plugin

The Codex plugin for [Swarm](https://swarmplatform.cloud), the shared context bus
for AI sessions. Installing it connects Codex to the hosted Swarm MCP server,
ships the Swarm skill, and adds hooks that teach the ritual: load what other
sessions already know at the start of a task, checkpoint your work at the end.

## Install

```bash
codex plugin marketplace add builtbyberry/swarm-codex
codex plugin install swarm
```

`codex plugin install swarm` registers the plugin for your user, so it is
available in every project. Codex opens Swarm in your browser to authorize on
install; if it needs a manual sign-in, run `codex mcp login swarmcloud`.

Prefer to pin the plugin to a specific channel? Download a personalized copy from
the [Connect page](https://swarmplatform.cloud/connect).

## What is inside

- `plugins/swarm/.mcp.json` — connects the hosted Swarm MCP server (browser
  OAuth; no token to copy).
- `plugins/swarm/skills/` — the Swarm skill plus the `swarm-load`,
  `swarm-checkpoint`, `swarm-onboard`, `swarm-curate`, `swarm-handoff`, and
  `swarm-dispatch` skills.
- `plugins/swarm/hooks/hooks.json` — reminders to load context at session start
  (and after a compaction) and to checkpoint when you finish.

## Generated — do not edit by hand

The marketplace under `plugins/swarm/` is generated from the canonical Swarm
sources via `php artisan swarm:publish-codex-marketplace`, so it never drifts
from the personalized download. Send fixes to the upstream Swarm project rather
than editing files here.

## License

Apache-2.0 (see `plugins/swarm/LICENSE`). The hosted Swarm service has its own
terms; "Swarm" is a trademark and the licence grants no rights to it.
