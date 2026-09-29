---
enabled: false
triggers:
  - provider: schedule
    event: cron_fired
    schedule:
      name: weekly-github-digest-github-weekly
      cron: "0 9 * * 1"
---
Choose a Slack destination by replacing {{SLACK_CHANNEL}} before saving. Summarize the past week of activity in the configured GitHub repositories: merged and open pull requests, notable issues, and pending reviews. Include source links and omit duplicate or routine bot activity. Send one concise digest to {{SLACK_CHANNEL}} using the connected Slack tools. Do not read Notion or assume a default channel. If the destination is not configured, do not post anywhere.
