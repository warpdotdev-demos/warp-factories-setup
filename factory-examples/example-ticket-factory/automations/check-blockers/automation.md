---
enabled: true
agent: implementer
triggers:
  - provider: linear
    event: issue_state_changed
    filter:
      teams: [Customer Team]
      states: [Done]
---
Run your dependency readiness scan. Wake eligible previously deferred tasks
using `send_task` with their existing `factory_task_uid`.
Do not implement the triggering issue again, create replacement tasks, or close tasks.
