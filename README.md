# Swarm — Codex plugin marketplace

The Codex CLI plugin marketplace for [Swarm](https://swarmplatform.cloud), the shared context bus. Installing the `swarm` plugin connects the hosted Swarm MCP server, ships the Swarm skill, and adds hooks that teach the load-at-start / checkpoint-at-end ritual.

## Install

This tree is a self-contained marketplace. In the Codex CLI, from this directory:

```bash
codex plugin marketplace add ./
codex plugin add swarm
```

On install, Codex opens Swarm in your browser to authorize — no token to copy. If the connection needs a manual sign-in, run `codex mcp login swarmcloud`. Codex will ask you to trust the plugin hooks on first run (`/hooks`).

Then run `$swarm-onboard` (or open `/skills`) to bind this project to a channel — the marketplace install has no channel baked in, so onboarding (or hand-adding a `<!-- swarm-channel: <key> -->` line to `AGENTS.md`) is what tells future sessions which one to use.

## Generated — do not edit

Every file here is rendered from the Swarm app's canonical connector by `swarm:publish-plugin`. Hand edits drift from canon and are pruned or flagged by the publisher's `--check` gate on the next publish; changes land only through a publisher PR.

## License

Apache-2.0 (see `plugins/swarm/LICENSE`) — fork and adapt the plugin freely. The hosted Swarm service it connects to is governed by its own terms; "Swarm" is a trademark and the licence grants no rights to it.
