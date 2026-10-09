---
name: factory-handoff
description: Preserves canonical Factory task ownership, cross-task notifications, and durable work handback. Use before task lookup, dependency notifications, Done-state closeout, or external work handback.
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
- `message_foreman`: coordinate an existing task's readiness, blocker, question,
  or delivery notification. It resumes communication with the existing owner; it
  does not hand work back or change the stage.
- `send_task`: new admitted ticket intake, or a real work handback after
  implementation/local iteration. For handback use the authoritative
  `factory_task_uid`, pushed branch/PR, and a precise note. Do not use it for
  routine status notifications or mint a new task for every event.
- `complete_task`: only the verified completion of the original owning task.
  Ending a run or Linear agent session is not task completion.

For intake/readiness, resolve the canonical task first. If it is outside the
current run tree, notify the existing owner and stop this routing run. Only a
confirmed not-found for an explicitly admitted unfinished issue may create intake through
`send_task(factory_uid=..., ticket_ref="linear:<issue UUID>", ticket_url=...,
title=..., note=...)`. The receiving conversation owns implementation.
Errors are not not-found. Do not create a new task for a completed issue.

Reuse the owning conversation, branch, and PR. Never start another writer while
implementation is active. Review-pending, human-paused, and terminal work is not
restarted automatically. Automatic readiness notifications clear only a
dependency pause after the owner checks ALL current prerequisites again.

## Done-state task closeout
The Done handler resolves the original task by the triggering issue and may
call `complete_task` with that original `factory_task_uid` after verification.
This is a closeout exception to intake's routing rule, not permission to code
under the event task. Never use the automation's own run ID to close another
ticket. An issue without a Factory task can still unblock admitted dependents.

## Durable hand-off and follow-ups
Push the assigned implementation and report created or adopted PRs with
`report_pr`. Record the criterion evidence, exact checks/results, head SHA,
current CI, and gaps in the owning conversation so Done closeout can inspect
them later. Attach the PR natively to the issue and current session.

For external/local work handback, use the existing task UID, pushed branch/PR,
and a compact note containing the request, changed behavior, verification, and
remaining work. Supply needed unsynced content explicitly; a cloud run cannot
read local-only files. Never send credentials or guess requester identities.

Answers, requested corrections, and CI failures resume the existing task and
PR. A finished conversation can resume; do not replace it just because its run
ended. Human review, merge, and Linear Done updates stay outside this factory.
