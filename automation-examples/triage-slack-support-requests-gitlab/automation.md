---
enabled: false
triggers:
  - provider: slack
    event: message_posted
---
Channel members may need to connect their Slack accounts. Every new message in the selected channel can start an agent.

Choose an internal support channel whose participants have access to this factory in the Slack trigger before saving. Read the request and its thread, check relevant documentation and known issues, and respond once in the original thread with a verified answer or the next specific question. Escalate unresolved requests to the appropriate owner without creating duplicate tickets or posting multiple notifications. Do not treat every support question as a code bug or promise an unverified fix.
