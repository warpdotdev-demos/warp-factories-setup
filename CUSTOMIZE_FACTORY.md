We have the default Warp Factories configuration, now help us customize this factory's workflow based on our preferences below. Change factory configuration only, not application code. Inspect the current configuration, then recommend changes for a human to review. Do not make changes until a human confirms which to implement.

Interactive work (tasks a person sends into factory). Adjust, add and remove agent steps.

1. Triage: Reproduce bugs before fixing? [always / only when asked / no] Can the factory create tickets? [yes / no] Update tickets? [yes / no]
2. Planning: What happens before coding? [nothing straight to implementation / short plan recorded in the ticket / spec in the repo, etc.] Approval step? [human / no approval needed]
3. Implementation: Open PRs as [draft / ready for review] Must pass before opening a PR: [e.g. tests and lint, look at AGENTS.md] When to use video verification? [always UI related / only when requested]
4. Review: Existing PR review tool? [tool / none] Should the factory review its own PRs? [yes / no]
5. Completion: After merge, the ticket should [move to Done / stay as is]

When you make changes, update every part of the config (agents, prompts, skills, automations) to match this workflow, and remove references to anything stale.

Before finishing, run the configuration checks and trace a bug and a feature from intake to completion. Report back with the resulting workflow, what changed, and any setup left for humans.
