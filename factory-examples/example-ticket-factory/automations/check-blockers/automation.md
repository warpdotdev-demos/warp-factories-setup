---
agent: implementer
triggers:
  - provider: linear
    event: issue_state_changed
    filter:
      teams: [Customer Team]
      states: [Done]
---
Handle this as a Done-state dependency check, not implementation intake.

1. Refresh the triggering issue; stop if it is no longer completed.
2. Apply `ticket-delivery` completion rules to its original Factory task, if
   one exists. An untracked, human-owned prerequisite can still unblock work.
3. Find its dependents, including inherited parent prerequisites. Apply the
   shared scope, admission, and readiness rules to ALL their blockers, then
   resume newly ready work in its own conversation using `factory-handoff`.
4. Do not implement the completed issue or its dependents inside this event's
   task, or change the completed issue's state.
