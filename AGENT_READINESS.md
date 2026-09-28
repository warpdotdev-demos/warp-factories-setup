Assess how agent ready the repos in this factory are and how easy it is for a coding agent to understand and work in each. Recommend repository improvements for a human to review. Do not make any changes until a human has confirmed what recommendations to implement.

Scope
- Assess the repos available to this factory.
- Keep typical work in mind: small bug fixes, feature changes, and maintenance.

For each repository, identify its purpose, major components, and where an agent would begin a typical task. Read relevant source code, and compare to agent/human documentation, commands, scripts, tests, and CI. For monorepos, sample representative subprojects. Keep recommendations scoped to each repository.

Assess these dimensions:

1. Orientation and instructions. Look for `AGENTS.md` (including nested files), `CLAUDE.md`, other agent instructions, README, CONTRIBUTING, architecture/domain docs. Are they discoverable by the intended agents, accurate, scoped to the right directories, and free of contradictions? Do they explain where to work, how to build and check changes, and what done means? Do not require both `AGENTS.md` and `CLAUDE.md` just to check boxes.
2. Reproducible environment. Inspect pinned runtimes, package managers and lockfiles, setup scripts, containers, private dependencies, required services, seed data, and platform requirements. From the repository alone, could a newcomer infer how to set up a fresh run? Flag undocumented prerequisites.
3. Verification and feedback loops. Identify documented local build, test, lint, type, and relevant e2e commands. Inspect a few representative tests for the behavior an agent is likely to change. A test directory alone is not proof of useful coverage. Read CI files to see which checks are configured and when they trigger.
4. Skills. Look for repository skills (`.agents/skills/` and `.claude/skills/`), rules, hooks, and pre-commit checks. Are they in the right location, discoverable, relevant to the work, current/accurate, scoped appropriately, and consistent with the other repository guidance?

Using evidence from repository files, assess each dimension as **good**, **needs improvement**, **none**, or **unknown**. Cite a relevant file path and short reason for each assessment. Use **unknown** when repository evidence is insufficient.

Report back with:
- A brief summary of strengths and the most important repository-level gaps.
- One concise section per repository with areas inspected and ratings with file evidence.
- A prioritized list of small, concrete repository recommended improvements. For each, name the gap, the file or location to change, and why it helps.

Avoid generic advice and recommending every possible change. Favor a small number of high-leverage fixes grounded in the actual repositories.
Do not use any sub agents, do all of this in the main foreman conversation.
