Review the initial factories tasks and tell us what to improve in terms of factory configuration. Recommend factory improvements for a human to review. Do not make any changes until a human has confirmed what recommendations to implement.

Scope
- Time window: [default: all runs that worked on a ticket]
- What we care about most: [for example, PR quality, setup failures, review time, unnecessary questions]

How to review
- Find historical tasks in scope
- For each task, trace what happened from intake to where it stopped, investigate run conversations, integrations (first parties/MCPs, PRs, CI. Don't rely on final summaries alone.
- Compare what happened with the configured workflow: routing, stages, approval gates, and integrations. Note where the factory skipped a step, asked when it didn't need to, or got stuck without asking. Also look for any contradictions that may need to be resolved in the agent prompts/skills.
- Focus on blockers and inefficiencies you find across runs, we want to identify real systematic issues not single run specific nits.
- Name each problem's likely source: the repository (docs, setup, tests, skills) or factory configuration (workflow, prompts, skills, automations, integrations, runners).

Report back with
- The tasks reviewed, each with a link, outcome, and one-line summary.
- What worked well.
- The most important problems, each with examples and its likely source.
- A short, prioritized list of changes. For each: the evidence, the smallest change that fixes it and where to make it
- Anything you couldn't verify.
