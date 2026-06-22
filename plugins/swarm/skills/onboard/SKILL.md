---
name: swarm-onboard
description: Set up a new project on Swarm — create its channel and seed it with intelligence records. Use when connecting a repository to Swarm for the first time, or when the user asks to onboard, initialize, or set up a project on Swarm.
---

# Onboard a project to Swarm

Onboarding has a single canonical source: the **`onboard-project` MCP prompt**. Invoke that prompt and follow it end to end — do not restate or shortcut its steps here, so onboarding never drifts from the server.

The prompt walks the full ritual: call `list_channels` first (and stop if a channel for this project already exists), distill the repository into atomic typed records, pick the target workspace if the user belongs to more than one, then call `onboard_project` to create the channel and seed it.

After onboarding, treat the channel as the project's shared memory: load it at the start of each task with `get_context_for_injection`, and checkpoint at the end per the channel's capture mode.
