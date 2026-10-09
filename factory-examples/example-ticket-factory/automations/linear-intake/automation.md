---
enabled: true
agent: implementer
triggers:
  - provider: linear
    event: agent_session_created
    filter:
      teams: [Customer Team]
  - provider: linear
    event: issue_labeled
    filter:
      teams: [Customer Team]
      projects: [Customer Project]
      labels: [factory-implement]
---
Process the triggering Linear issue using your normal ticket-implementation workflow.
