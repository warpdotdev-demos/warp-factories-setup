---
triggers:
  - provider: schedule
    event: cron_fired
    schedule:
      name: weekly-changelog-gitlab-weekly
      cron: "0 9 * * 1"
---
Review changes merged into the configured repositories during the last seven days, deduplicate related change requests, and draft a concise customer-facing changelog with links and attribution. Use repository release-note conventions when present. Do not publish a release or merge a draft without human review; if no customer-visible changes exist, report that instead of inventing entries.
