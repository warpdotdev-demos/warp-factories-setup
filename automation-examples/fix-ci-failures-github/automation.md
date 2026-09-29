---
triggers:
  - provider: github
    event: workflow_run_completed
    filter:
      conclusions: [failure]
---
For the failed completed workflow, locate its pull request and verify the run still corresponds to the current head and has not been superseded by a newer attempt. Act on PRs not already owned by this factory; leave factory-owned PRs to their existing tasks. Skip workflows triggered by this automation or by a previous fix to avoid loops. Read the failing logs, reproduce the failure, and change only code needed to fix it. Keep the work in this automation’s task and update the existing PR branch rather than opening another PR or sending duplicate notifications. Do not merge.
