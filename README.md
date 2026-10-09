# Factory setup prompts

Prompts for getting started and customizing Warp Factories to match your intended workflow. Send each prompt through the [factory web chat](https://platform.warp.dev/runs/new) or from any local coding agent using the [Factory MCP](https://docs.warp.dev/factories/factory-mcp/).
Each prompt is designed to assess and make recommendations requiring your approval before making changes.

## Suggested workflow

For each prompt replace the bracketed placeholders with your desired behavior.


1. **Assess underlying repo(s) agent readiness.** Send [AGENT_READINESS.md](AGENT_READINESS.md). The factory audits your repos in terms of agent docs, setup/test/verify commands, skills, and recommends helpful repository improvements.
2. **Address any underlying gaps with the underlying repos.** Choose which recommendations to implement, then make the changes yourself or approve the factory to make them.
3. **Customize the factory.** Warp Factories comes out of the box with a default workflow. To customize further, fill in and send [CUSTOMIZE_FACTORY.md](CUSTOMIZE_FACTORY.md) to the factory. Starting from the default configuration, the factory adjusts, adds, or removes agent steps (triage, planning, implementation, review, and completion) to match how your team works. It uses the integrations already connected to your factory.
4. **Run a few suitable tasks through the factory.** Send the factory a handful of real, suitabile tasks, such as straightforward bugs or small features adds.
5. **Review initial runs and refine.** Send [PILOT_TASK_REVIEW.md](PILOT_TASK_REVIEW.md) to the factory. The factory reviews its recent runs and recommends configuration improvements.

Repeat steps 3–5 as needed to get a solid baseline. Once the factory is matching your intended workflow [scorers](https://docs.warp.dev/factories/measure-and-improve/scorers/) can be set up to [continously improve the factory over time](https://docs.warp.dev/factories/measure-and-improve/self-improvement/).

## Examples

- [Factory examples](factory-examples/README.md): complete factory configurations, starting with a single-agent factory for well-specified Linear tickets.
- [Automation examples](automation-examples/README.md): individual triggers and prompts to add to an existing factory.
