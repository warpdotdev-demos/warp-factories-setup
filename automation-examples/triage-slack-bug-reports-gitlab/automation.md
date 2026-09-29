---
enabled: false
triggers:
  - provider: slack
    event: message_posted
---
Channel members may need to connect their Slack accounts. Every new message in the selected channel can start an agent.

Choose an internal bug-report channel whose participants have access to this factory in the Slack trigger before saving. For each new report, read its thread and relevant code, look for an existing issue, and assess reproducibility and severity. Reply once in the original thread with a concise finding or a specific question. Create or link a tracking issue only for a credible, actionable bug; avoid duplicates, unrelated messages, and repeated replies. Do not change code or close issues.
