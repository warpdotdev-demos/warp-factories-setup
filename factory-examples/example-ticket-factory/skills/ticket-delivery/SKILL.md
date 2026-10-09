---
name: ticket-delivery
description: Implements well-specified Linear tickets with dependency deferral, verification, and human PR hand-off. Use for intake, implementation, dependency readiness checks, or explicitly requested task closeout.
---
# Ticket delivery

One agent handles both paths: read ticket → check blockers → implement and
verify → human PR review. Bug fixes use regression coverage; features use
acceptance coverage. No worker dispatch, triage, specs, ticket decomposition,
autonomous code review, automatic merge, or polling.
Read `factory-handoff` for ownership/coordination, `linear` before tracker or
session operations, and `github` before branch/PR operations. Resolve paths
from the available skill catalog. The workflow below does not replace those
surface mechanics.

## Scope and Linear
- Work only in **Customer Team / Customer Project**, in repositories declared
  in `factory.yaml`. These are setup placeholders, not discovery hints.
- Explicit intake means `factory-implement` or a human delegation through a Linear
  agent session. A dependency event is not authorization to adopt a ticket.
  For label-only intake, removing `factory-implement` withdraws admission. A recorded
  human delegation remains valid until explicitly withdrawn; a previous label
  alone is not such a delegation.
- `A blocks B` makes A a prerequisite of B, not the reverse. `related`,
  `duplicate`, and parent/child relations alone do not establish execution
  order. Also honor explicit prerequisites in ticket text/latest decisions;
  report disagreement with native relations rather than silently choosing.
- Read parent requirements and explicit parent prerequisites that apply to
  the child. Do not wait for the parent itself to be Done: that would deadlock
  a parent whose completion depends on its children.
- A parent/container with multiple implementation children is context, not
  one giant implementation request. Accept its specified leaf tickets, or ask
  which existing ticket to work on. Do not generate another backlog.
- The implementer uses the team's started/review states as work proceeds.
  A human or existing integration sets Done after merge; never set it at PR
  hand-off or change it from a Done-event handler. Preserve human fields.
- Record pause reason, blocker/readiness facts, task/PR references, and gaps
  durably through structured data/native links. Use a concise updatable issue
  comment only for facts without a native representation, under `linear`;
  live progress and final responses stay in the current agent session.

## Canonical task ownership
Follow `factory-handoff`: resolve the exact ticket/task, notify its existing
owner for cross-task events, and implement only inside the owning task. Use
`message_foreman` for status/questions, `send_task` for intake, actual handback,
or an eligible existing-task dependency wakeup.
Reuse conversation/branch/PR; never restart active, review-pending, or terminal
work automatically. Distinguish dependency pauses from human, clarification,
and verification pauses; only dependency pauses can wake automatically.

These are prompt-level duplicate-avoidance rules using the Factory's canonical
ticket/task identity, not a distributed lock. Do not claim exactly-once dispatch.

## Readiness gate
Apply before coding and again before delivery; explicit bug blockers
are respected too.

- A ticket must remain in scope, unfinished, explicitly admitted, and sufficiently
  specified to implement its acceptance criteria. Honour withdrawal of intake
  or a human pause; do not use stale approval from an earlier run.
- Every explicit prerequisite must be satisfied. One completed blocker does
  not release a ticket with another unresolved blocker.
- For code prerequisites, require a completed Linear state, fetch required PRs,
  and verify they are merged into the ticket's intended repository/base and
  their change is in the current base used for implementation. Completed
  Linear status alone is insufficient; open, draft, review-approved, or
  closed-unmerged PRs do not count.
- A prerequisite already satisfied without a PR needs concrete evidence in
  the target base and an explicit recorded completion decision. For non-code
  prerequisites, require a completed state and the ticket's stated evidence.
- Check all required deliveries recorded on the prerequisite, not simply the
  first attached PR; ignore PRs merely cited as context. Incomplete or unclear
  delivery evidence pauses the dependent.
- Cancelled prerequisites, deleted/inaccessible issues, failed relation reads,
  reopened blockers, and uncertain merge/base evidence do not count as ready.
  Ask for the precise missing fact or a recorded human waiver. Never waive or
  remove dependencies yourself. Report a discovered self-dependency or cycle;
  do not attempt to resolve it by coding through it.
- When blocked, preserve the pickup label and finish with `success: false` and
  `Deferred: waiting on dependencies`, naming blocker IDs/states or verification
  gaps. Do not implement or call `complete_task`. The marker must describe a
  real dependency pause, not a clarification, review, or unrelated failure.
  When ready, fetch the latest base; do not implement against an unmerged dependency
  branch. Independent ready tickets can proceed; blocked ones cannot.

## Implementation and verification
- Use the ticket as the contract and the repository's existing conventions.
  Ask only about material missing decisions. Do not create PRODUCT/TECH specs.
- Use one branch/PR per ticket; if the requested delivery genuinely requires
  more, ask the human for direction rather than inventing a multi-PR plan.
- Add meaningful regression/acceptance tests. Run the documented relevant
  tests, formatting/linting, typecheck, and build. Discover actual commands
  from repository guidance; do not assume a framework or package manager.
- Distinguish passed, failed, pending, and not run. Infrastructure failures are
  verification gaps, not passes. Do not loop waiting for CI or provision
  production resources to get a green result.
- For UI changes requiring visual validation, build successfully before using
  computer use. Capture relevant evidence through its media policy fields,
  and attach evidence to the PR; never commit media or scratch artifacts.
- Report each acceptance criterion's evidence, commands/results, PR head SHA,
  CI status, and unresolved gaps. A change in code requires affected checks
  again. Verification is behavioral evidence, not a second code-review stage.

## PR hand-off
- The implementer is authorized to commit/push only the assigned implementation.
  Follow `github` for identity, base/head, draft/promotion, labels, attribution,
  template/artifact blocks, PR reporting, and requested-feedback mechanics.
- Record criterion evidence, checks, head SHA, and CI/gaps under `factory-handoff`.
  Attach the PR to the issue/current session under `linear`, update review
  status, and give the human the PR/evidence. Keep failed/unverified work draft.
- The requester/team reviews separately and decides whether to merge.

## Explicit task closeout
The Done automation only wakes existing dependency-deferred tasks. It never
closes the triggering issue's Factory task. Closeout requires an explicit human
request; ending an execution or setting Linear Done is not Factory completion.

1. Reread the requested issue and require a completed workflow state. Resolve
   its original task and required PRs, verifying actual merges, repository/base,
   and evidence for the delivered revision. Never complete referenced issues
   or a parent/container from a child's merge.
2. Require the ticket's acceptance criteria and required checks to be satisfied.
   A merge alone does not replace missing verification. Missing ownership,
   failed checks, or an externally changed/unverified head needs human input.
3. Call `complete_task` with the **original** `factory_task_uid` only when
   delivery is verified. Do not rewrite Linear's state. Already-complete is a
   no-op; never complete a cancelled task. Report uncertain/failed closeout,
   leaving it pending for explicit human follow-up.

## Dependency wakeups
Follow the main agent's dependency readiness scan. Only an existing idle task
whose latest actual agent outcome explicitly deferred on dependencies can wake.
Require the pickup label and ALL current prerequisites to be ready; skip active,
terminal, review-pending, human-gated, missing, or unverifiable tasks.
Use `send_task` with the existing task UID, never new-intake arguments.
The owner rechecks mutable state before coding. Removed relations, missed
events, and reopened work require explicit recheck; there is no polling fallback.
