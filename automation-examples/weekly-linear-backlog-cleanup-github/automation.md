---
triggers:
  - provider: schedule
    event: cron_fired
    schedule:
      name: weekly-linear-backlog-cleanup-github-weekly
      cron: "0 9 * * 1"
---
Review open Linear issues in the selected teams each week. Identify stale work, plausible duplicates, and items needing an owner or clarification; report a concise linked shortlist for human review. Do not auto-close, change state, archive, or delete issues. Skip unchanged items already flagged in a prior report rather than repeating notifications.
