Help us customize this factory for our pilot. First inspect the entire current factory configuration: its factory definition and format, foreman workflow, agent prompts, skills, automations, integrations, and runners. Understand how these pieces currently depend on one another before making changes. Preserve anything we have not asked to change. Do not modify our application code as part of this request.

Our scope
- Repositories and teams: [repos and teams]
- Work we want the factory to handle: [bugs, features, maintenance, design, PRs, etc.]
- Where requests arrive: [factory chat, Slack, Linear/Jira, GitHub, etc.]
- Where work is tracked: [tracker and project; when a ticket is or is not required]
- Engineering conventions: [test/build commands, coding guidance, PR template, branching rules]

Our desired workflow

1. Triage: [What should be investigated? When should the factory create or update a ticket? Should triage reproduce bugs, leave reproduction for implementation, or do it only when requested?]

2. Planning, specs, and design: [Keep the spec agent, replace it with a planning agent, add a design agent, or skip these stages. When should each run, what should it produce, and who approves the result?] Store plans and specs [in the repository / on the ticket or PR / in the conversation / elsewhere].

3. Implementation: [When may coding start? What tests, builds, and other checks are required? Should the factory open a draft or ready-for-review PR?]

4. Review: [What should the factory review itself? What does our existing PR review tool already handle? How should findings be addressed without duplicate comments or conflicting decisions?]

5. Completion: [Who approves and merges? What should happen to the ticket and factory task after merge?]

Automations

Keep only the automations we want during the pilot; delete the others. For each one we keep, propose a sensible trigger, scope, permitted actions, and human escalation point before enabling it.

- Bug intake & remediation: [where bugs arrive; triage only or proceed to a fix PR]
- Security remediation: [alert source; assess only or propose a patch]
- CI/CD remediation: [which failed checks or PRs; diagnose only or update the PR]
- Observability & incident triage: [alert or incident source; evidence to gather; when to hand off to a human]
- Ticket triage & enrichment: [which projects; duplicate checks, missing details, labels, priority, ownership]
- Other: [describe]

Prevent duplicate work on the same alert, ticket, incident, or PR. Keep our existing monitoring, CI, security, and incident tools as the source of truth.

Tools and environment
- MCPs and integrations needed: [service → which agents need it → purpose → read-only or write access]
- Existing tools or bots to work alongside: [tools and their responsibilities]
- Computer use: [only when explicitly requested / for UI bugs / for UI verification / never]. Apply this rule consistently wherever it matters, including triage, implementation, review, and their skills.
- Runners: [which repos or tasks need Linux, macOS, iOS simulators, or other environments]
- Access restrictions: [permissions and credential requirements]. Do not ask us to paste secrets into chat.

Human gates and boundaries
- Stop for approval before: [planning or design decisions, starting implementation, publishing a PR, dependency changes, deployment, etc.]
- May proceed without approval for: [investigation, ticket enrichment, routine fixes, tests, etc.]
- Never do: [merge, deploy, dismiss security alerts, close incidents, etc.]
- Direct questions and escalations to: [person, team, or channel]

Consistency is a requirement, not a final cleanup step. Make each workflow change end-to-end across every affected part of the factory. The foreman's routing, individual agent responsibilities and outputs, prompt instructions, skills, automation triggers, integrations, runner assignments, and default factory settings must describe the same workflow. Do not leave an old instruction in one place that contradicts a new instruction elsewhere.

In particular, check that:
- Every workflow stage has an owner, a clear input and output, and a defined next step or human gate.
- Agents and the foreman agree on who may create tickets, write specs or plans, use tools, post reviews, open PRs, and communicate with the user.
- Skills and shared guidance do not reintroduce removed behavior or point to tools the agent cannot access.
- Automations route to agents that exist and are equipped to handle their triggers.
- Runners and integrations required by an agent are actually available or are reported as setup gaps.
- Existing PRs, CI failures, review feedback, and answers to earlier questions can re-enter the workflow without starting duplicate work.
- There are no stale references to renamed or removed agents, artifacts, gates, or workflow stages.

Ask concise questions when a decision is genuinely blocking or would materially change access, cost, or approval authority. Otherwise choose the simplest least-privileged interpretation and state your assumptions. Make changes reviewable; do not silently enable destructive or production-facing automation.

Before calling the customization complete, validate the configuration using the available checks and walk through at least three scenarios: a new bug, a new feature, and work arriving at a later stage such as an existing PR or failed CI check. Trace each scenario from trigger through handoffs, human gates, and completion. Fix inconsistencies you find rather than merely listing them.

When finished, show us the resulting workflow, the configuration changes made, validation results, and anything we still need to set up. Flag any behavior you could not verify.
