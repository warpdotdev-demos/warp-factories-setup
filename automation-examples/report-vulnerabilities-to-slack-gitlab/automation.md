---
triggers:
  - provider: gitlab
    event: merge_request
    filter:
      actions: [open]
---
Review the pull request or merge request that triggered this automation for exploitable security vulnerabilities. Validate findings against the changed code and relevant surrounding code. Submit actionable review comments for confirmed findings, then use the connected Slack tools to post a concise alert with the change-request link, impact, evidence, and remediation in {{SLACK_CHANNEL}}. Do not report speculative findings. If there is no validated vulnerability, leave the change request unchanged and do not post to Slack.
