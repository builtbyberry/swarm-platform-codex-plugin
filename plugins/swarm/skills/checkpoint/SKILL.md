---
name: swarm-checkpoint
description: Checkpoint the current session back to its Swarm channel. Use ONLY when the user explicitly asks to checkpoint, share, or save their work to Swarm — never invoke automatically, because sharing is gated on the channel's capture mode and the user's intent.
allow_implicit_invocation: false
---

# Checkpoint to Swarm

Checkpoint the current session to its Swarm channel, following the `guidance` field returned by `get_context_for_injection`:

- **Auto** — call `share_session` with `trigger=agent_auto`.
- **Propose** — ask the user first; if they agree, call `share_session` with `trigger=user_request`.
- **Off** — keep it private; do not share unless the user explicitly asks.
