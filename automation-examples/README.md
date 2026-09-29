# Automation examples

Each file contains a trigger and the complete agent instructions from the corresponding catalog template. Copy the directory for the variant matching your Factory's code forge to `automations/` under a file-backed Factory.

## Incidents and triage

- [Triage new GitHub issues](triage-new-github-issues-github/automation.md)
- [Triage Slack bug reports — GitHub](triage-slack-bug-reports-github/automation.md) / [GitLab](triage-slack-bug-reports-gitlab/automation.md)
- [Triage Slack support requests — GitHub](triage-slack-support-requests-github/automation.md) / [GitLab](triage-slack-support-requests-gitlab/automation.md)
- [Send a weekly GitHub digest](weekly-github-digest-github/automation.md)
- [Review the weekly Linear backlog — GitHub](weekly-linear-backlog-cleanup-github/automation.md) / [GitLab](weekly-linear-backlog-cleanup-gitlab/automation.md)
- [Check new Linear issues for duplicates — GitHub](linear-duplicate-checker-github/automation.md) / [GitLab](linear-duplicate-checker-gitlab/automation.md)

## Implementation

- [Autofix new GitHub issues](autofix-new-github-issues-github/automation.md)
- [Autofix new Linear issues — GitHub](autofix-new-linear-issues-github/automation.md) / [GitLab](autofix-new-linear-issues-gitlab/automation.md)
- [Autofix new Jira issues — GitHub](autofix-new-jira-issues-github/automation.md) / [GitLab](autofix-new-jira-issues-gitlab/automation.md)
- [Autofix PR review comments](autofix-pr-review-comments-github/automation.md)
- [Fix CI failures](fix-ci-failures-github/automation.md)
- [Fix CI issues after merge](autofix-flaky-tests-github/automation.md)
- [Draft a weekly changelog — GitHub](weekly-changelog-github/automation.md) / [GitLab](weekly-changelog-gitlab/automation.md)

## Code review

- [Auto-review pull requests](auto-review-pull-requests-github/automation.md) / [merge requests](auto-review-pull-requests-gitlab/automation.md)
- [Assign PR reviewers](assign-pr-reviewers-github/automation.md) / [MR reviewers](assign-pr-reviewers-gitlab/automation.md)
- [Post reviewer assignments to Slack — GitHub](post-reviewer-assignments-to-slack-github/automation.md) / [GitLab](post-reviewer-assignments-to-slack-gitlab/automation.md)
- [Follow up on stale Factory PR reviews](stale-factory-pr-reviews-github/automation.md)

## Security and monitoring

- [Find vulnerabilities — GitHub](find-vulnerabilities-github/automation.md) / [GitLab](find-vulnerabilities-gitlab/automation.md)
- [Audit dependencies — GitHub](audit-dependencies-github/automation.md) / [GitLab](audit-dependencies-gitlab/automation.md)
- [Report vulnerabilities to Slack — GitHub](report-vulnerabilities-to-slack-github/automation.md) / [GitLab](report-vulnerabilities-to-slack-gitlab/automation.md)

Connect the corresponding GitHub or GitLab integration before adding code-forge triggers. Linear, Jira, and Slack examples require their respective integrations as well. The Slack prompts containing `{{SLACK_CHANNEL}}` need a channel ID before enabling. Every weekly example runs on Mondays at **09:00 UTC**, adjust its cron expression for your preferred schedule.

The Slack bug-report and support-request examples are **disabled** because an unfiltered `message_posted` trigger could run on every channel message. Set a `filter.channels` list to the intended channel names (or `filter.channel_ids` to connected Slack channel IDs), then set `enabled: true`. The weekly GitHub digest is also disabled until `{{SLACK_CHANNEL}}` is replaced.
