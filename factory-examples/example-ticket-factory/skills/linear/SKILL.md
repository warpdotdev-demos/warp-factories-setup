---
name: linear
description: Uses Linear issue and agent-session MCPs for durable tracking and requester communication. Use before reading or updating a Linear issue or communicating in its agent session.
---
# Linear

## Separate tracker data from live communication
- Discover the current tools and schemas. Use `linear` for issue descriptions,
  comments, states, labels, relations, parents, projects, and native attachments.
  Use `linear_agent_session` only for the current request's live communication.
- Factory dispatch injects these managed integration MCPs when Linear is
  declared, connected, and enabled. Do not hardcode provider URLs or API keys.
  If required issue tools are unavailable, report the access blocker; never
  treat unreadable relations as no blockers or bypass access with a CLI/API.
- The owning implementer communicates with the requester and owns tracker
  writes/session updates. Event-routing runs notify that owner without posting
  into another request's session.
- Use the `session_id` from the current request/follow-up for every session
  call. Never reuse an old session ID or assume a tool defaults to this session.
  Background events without a current session perform durable tracker work
  or notify the owner; they do not manufacture a session or post into an old one.

## Read and update
Fetch current description, latest comments, labels, state, assignee, team,
project, parent, relations in both directions, and attachments. Page through
results. Respect the configured team/project and explicit intake.

Discover valid workflow states per team; status tracks progress, labels route
work. Read before writes, preserve unrelated fields/labels, and combine changed
fields into one issue update where supported. Resolve identities from supplied
platform identifiers; do not guess from display names.

Report an adopted issue once per run with `report_external_reference`,
`reference_type: linear_issue`, its HTTPS URL, and title. Reporting failures are
disclosed, not retried in a loop or treated as permission to duplicate intake.

## Session and durable artifacts
- The implementer uses `post_thought` for short progress, `post_action` for meaningful
  actions/results, and `add_external_urls` for PRs and durable artifacts.
  `update_plan`, if useful, is a session progress list, not a spec: send the
  complete list with `pending`, `inProgress`, and `completed` statuses.
- Use structured fields and native links for durable issue data. Do not post
  routine acknowledgements, progress, final summaries, or PR-link comments.
- A concise issue comment is allowed only when explicitly requested or when
  a durable fact cannot be represented by fields/native links. A dependency
  pause record can use one updatable factory-owned comment under that rule;
  it must not become a second copy of the session transcript.
- Attach a delivered PR natively to the issue and to the current agent session.
  Use a comment only as a last resort for a required durable link when no
  native operation exists.
- Do not retry an ambiguous session/mutation failure without checking whether
  it already succeeded. Report failures accurately; no success claim on error.
- The implementer calls `finish_task` once for the final response when the run is
  handed off or blocked, including PR/evidence and gaps. This ends the session,
  not the Factory ticket. Do not call session tools afterward in that run.
  Without the session MCP, use `finish_task` and tracker data; do not replace
  missing live communication with routine issue comments.
