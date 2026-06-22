---
name: swarm-context-bus
description: Use when working in a project connected to Swarm, a shared context bus over MCP. At the start of a task, load shared context with get_context_for_injection; at meaningful checkpoints, share back per the channel's capture mode. Triggers whenever the Swarm MCP tools (get_context_for_injection, capture_context, share_session, list_channels) are available.
---

# Swarm: shared context bus

Swarm is a shared context bus. RITUAL: at the START of a task, call get_context_for_injection for the relevant channel to load what other sessions already know; at the END of a meaningful chunk, checkpoint per that channel's capture_mode (returned in the injection payload and its `guidance` field) — Auto: share_session with trigger=agent_auto; Propose: ask the user, then share_session with trigger=user_request; Off: keep it private. Always confirm the active channel (ask the user or call list_channels); never assume a channel carries over between sessions. Use capture_context for private working notes, and promote_context_to_record only after explicit user intent. At the end of a meaningful chunk, also do a curation check: offer to record durable, reusable knowledge the channel does not already hold — the offer follows capture mode (skip on Off, or when no human is present), but creating the record always needs explicit user intent, even in Auto.


## The loop

1. **Start of a task** — call `get_context_for_injection` for the active channel to load what other sessions already know. Its payload includes the channel's current `capture_mode` and a `guidance` field telling you exactly what to do at the end.
2. **While working** — keep private working notes with `capture_context`. These stay yours; they are not visible to the channel until you share or promote them.
3. **End of a meaningful chunk** — checkpoint per the channel's capture mode. Follow the `guidance` field from the injection payload; see `reference/capture-modes.md` for what each mode means.
4. **Curation check** — before you finish, offer to record any durable, reusable knowledge the channel does not already hold. Never create records on your own; that needs explicit user intent. What qualifies, and when to skip the offer, is in `reference/curation.md`.

## Rules that matter

- **Always confirm the active channel** before acting (ask the user or call `list_channels`). Never assume a channel carries over between sessions.
- **Trust the runtime `guidance`** field over anything written here — capture mode is resolved live and can change.
- **`promote_context_to_record` only on explicit user intent** — turning context into durable, channel-visible canon is a curation act, not something to do automatically.

## Beyond the loop

**Curation** — turn working context into durable canon on explicit user intent: `promote_context_to_record` (from a captured session) or `create_record` (authored directly), `create_relationship` to link records, and `supersede_record` to mark one record as replaced by another.

**Handoffs** — transfer curated context to another actor with a handoff bundle: `create_handoff_bundle` (a narrative plus a priority-ordered reading path of records), `inspect_handoff_bundle` to review it, and `acknowledge_handoff_bundle` — which only the recipient may call.

**Dispatch** — an operator can hand a scoped task to a local agent (you) and get back a provisional proposal. You pick up an outbound handoff bundle with `inspect_handoff_bundle`, follow the exact steps in its `open_questions`, report progress with `report_dispatch_progress`, capture and promote your finding as provisional, then return a proposal bundle to the operator. Findings always land provisional — confirming them is the operator's call.

The full tool catalog is in `reference/tools.md`. Capture-mode behavior is in `reference/capture-modes.md`. Curation, handoffs, and running a dispatch as a worker are in `reference/curation.md`, `reference/handoff.md`, and `reference/dispatch.md`.

Connect a tool to Swarm at `https://swarmplatform.cloud/mcp/swarm` (browser OAuth on first use; no token to copy).

Licensed under Apache-2.0. The hosted Swarm service has its own terms; "Swarm" is a trademark.
