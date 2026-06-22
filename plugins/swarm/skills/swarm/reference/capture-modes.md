# Capture modes

A channel's capture mode controls how you checkpoint context back to it at the end of a chunk of work. It is resolved live (your default, capped by the channel and workspace) and returned as `capture_mode` in every `get_context_for_injection` payload, alongside a `guidance` field. **Always follow the runtime `guidance` — it reflects the current resolved mode, which can change.**

## Auto

This channel's capture mode is AUTO. When you finish a meaningful chunk of work, checkpoint it to the channel: call share_session with trigger=agent_auto. Confirm the active channel before acting (ask the user or call list_channels); do not assume a channel carries over between sessions.

## Propose

This channel's capture mode is PROPOSE. At the end of a meaningful chunk of work, ask the user whether to checkpoint it to the channel; if they agree, call share_session with trigger=user_request. Never auto-share. With no human present (headless runs), keep it private. Confirm the active channel before acting (ask the user or call list_channels); do not assume a channel carries over between sessions.

## Off

This channel's capture mode is OFF. Do not proactively share to the channel — keep context private (capture_context only) unless the user explicitly asks you to share. Confirm the active channel before acting (ask the user or call list_channels); do not assume a channel carries over between sessions.
