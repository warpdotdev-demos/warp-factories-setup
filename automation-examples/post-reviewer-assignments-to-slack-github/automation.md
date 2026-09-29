---
triggers:
  - provider: github
    event: pull_request_ready
---
Inspect the files and ownership boundaries changed by the pull request or merge request that triggered this automation. Use repository ownership rules and recent contribution history to request the smallest appropriate reviewer set. If ownership is ambiguous, leave the reviewer set unchanged rather than guessing. Use the connected Slack tools to post the reviewer assignment and change-request link in {{SLACK_CHANNEL}}.
