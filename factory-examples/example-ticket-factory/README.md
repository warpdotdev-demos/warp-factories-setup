# Example Ticket Factory

[All factory examples](../README.md) · [Setup guide](../../README.md)

One agent implements and verifies well-specified Linear tickets.
**Read → check blockers → implement → verify → human PR hand-off.**

## Agents
- **`implementer`:** implements tickets; unresolved dependencies end the run as deferred, without completing the task.

## Automations
- **`linear-intake`:** starts on delegation or the `factory-implement` label.
- **`check-blockers`:** on Done, scans labeled issues and wakes only existing idle tasks explicitly deferred on dependencies.

## Required setup
Replace or confirm these values everywhere listed:

| Value | Set or confirm | Files |
| --- | --- | --- |
| `customer-org` / `customer-repo` | Your GitHub owner/repository | [Factory](factory.yaml) |
| `Customer Team` | Your Linear team name | [Intake](automations/linear-intake/automation.md), [blockers](automations/check-blockers/automation.md), [scope skill](skills/ticket-delivery/SKILL.md) |
| `Customer Project` | Your Linear project name | [Intake](automations/linear-intake/automation.md), [scope skill](skills/ticket-delivery/SKILL.md) |
| `Done` | The team's completed state name | [Blockers](automations/check-blockers/automation.md) |
| `factory-implement` | Pickup label; required for automatic dependency wakeups | [Intake](automations/linear-intake/automation.md), [agent](agents/implementer/agent.md), [scope skill](skills/ticket-delivery/SKILL.md) |

Connect GitHub and Linear with repository/issue access.

## Optional customization
Change the name, alias, or model in [factory.yaml](factory.yaml), or the [default runner](runners/default.yaml).
If changing the alias, align `factory:<alias>` in the [GitHub skill](skills/github/SKILL.md); currently `factory:example-tickets`.
For cross-team blockers, add prerequisite teams and completed states to the [blocker filter](automations/check-blockers/automation.md).

## Before enabling
Follow the [validation steps](../README.md#use-an-example) before enabling this factory.
A human or existing integration must set Done **after merge**. There is no polling fallback.
Done scans do not close Factory tasks; closeout is explicitly requested.
