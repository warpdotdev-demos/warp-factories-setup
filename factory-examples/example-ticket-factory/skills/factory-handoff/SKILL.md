---
name: factory-handoff
description: Preserves canonical Factory task ownership, existing-task dependency wakeups, and durable work handback. Use before task lookup, dependency scans, or external work handback.
---
# Factory handoff

One implementer conversation owns each ticket from intake through PR hand-off.
It implements directly; there is no worker dispatch or agent-to-agent pipeline.

## Tools and credentials
- Discover the connected Factory MCP and read its current tool descriptions
  and schemas before first use. When available, read
  `skill://warp/factory-mcp/SKILL.md`; if the resource cannot be read, use the
  live server instructions and descriptions. Never invent a tool or argument.
- Use MCP for Factory operations. Missing authentication/access is a reported
  blocker, not a reason to call a raw API or create a competing task.
- Use this run's `WARP_FACTORY_ID` to scope lookups. Use runtime-provided run
  IDs, integration connections, and credentials as-is. Never copy a demo ID,
  print a token, replace git identity, or pass secrets in a brief.
- Factory integrations provide the issue and agent-session MCPs when connected
  and enabled. Do not mask them with custom entries using their reserved names.
  Agent/automation `mcpServers` and `secrets` overrides replace inherited values;
  omit them unless an intentional complete override is required.

## Choose the correct handoff
- `get_task`: read the canonical task by exact issue/PR reference, scoped to
  this factory. Inspect stage, runs, and outputs before acting.
- `message_foreman`: status updates, questions, or blocker coordination with
  an existing owner. It does not hand work back or change the stage; eligible
  dependency wakeups use `send_task` below.
- `send_task`: new admitted ticket intake, or a real work handback after
  implementation/local iteration. For handback use the authoritative
  `factory_task_uid`, pushed branch/PR, and a precise note. Do not use it for
  routine status notifications or mint a new task for every event.
- Dependency wakeups are a specific `send_task` handback: after the readiness
  scan proves eligibility, send the existing task UID and the agent's wakeup
  note. Never pass new-ticket fields or create a task when scan lookup fails.
- `complete_task`: only the verified completion of the original owning task.
  Ending a run or Linear agent session is not task completion.

For normal intake, resolve the canonical task first. If it is outside the
current run tree, notify the existing owner and stop this routing run. Only a
confirmed not-found for an explicitly admitted unfinished issue may create intake through
`send_task(factory_uid=..., ticket_ref="linear:<issue UUID>", ticket_url=...,
title=..., note=...)`. The receiving conversation owns implementation.
Errors are not not-found. Do not create a new task for a completed issue.
This new-intake path is NOT available to a dependency scan; no existing task
means no automatic wakeup. Use `get_conversation` to establish the latest real
stop reason, and current task/run data to prove idle state; uncertainty means skip.

Reuse the owning conversation, branch, and PR. Never start another writer while
implementation is active. Review-pending, human-paused, and terminal work is not
restarted automatically. Automatic readiness notifications clear only a
dependency pause after the owner checks ALL current prerequisites again.

## Done scans and task closeout
The Done handler scans labeled unfinished issues and wakes only existing idle
dependency-deferred tasks. It neither implements nor closes tasks. An issue
with no Factory task is skipped, not adopted.
Only an explicit human closeout request may call `complete_task` after the
`ticket-delivery` completion checks, using the original task UID. Never complete
a dependency-deferred task or substitute an event run's ID.

## Durable hand-off and follow-ups
Push the assigned implementation and report created or adopted PRs with
`report_pr`. Record the criterion evidence, exact checks/results, head SHA,
current CI, and gaps in the owning conversation for human review and later
explicit closeout. Attach the PR natively to the issue and current session.

For external/local work handback, use the existing task UID, pushed branch/PR,
and a compact note containing the request, changed behavior, verification, and
remaining work. Supply needed unsynced content explicitly; a cloud run cannot
read local-only files. Never send credentials or guess requester identities.

Answers, requested corrections, and CI failures resume the existing task and
PR. A finished conversation can resume; do not replace it just because its run
ended. Human review, merge, and Linear Done updates stay outside this factory.
