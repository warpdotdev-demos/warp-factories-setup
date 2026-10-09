# Factory examples

[Setup guide](../README.md) · [Automation examples](../automation-examples/README.md)

Complete file-based factory configurations you can use as starting points.
Each example has its own README describing its workflow and a `factory.yaml`
with the agents, automations, runners, and skills it needs.

## Available factories

- [Example Ticket Factory](example-ticket-factory/README.md): one agent implements
  and verifies well-specified Linear bugs and features. Intake uses delegation
  or the `factory-implement` label; a Done-state automation checks for newly
  unblocked work. Human review and merge remain outside the factory.

## Use an example

1. Read the example's README and the [setup guide](../README.md) to choose a
   workflow that fits your team.
2. Copy the complete example directory into your factory configuration
   repository. Replace the repository, Linear team/project, and workflow-state
   placeholders, and connect its required integrations.
3. Register the directory containing that example's `factory.yaml` as the
   Factory root, not this catalog directory or the repository root.
4. Validate the complete tree with the current Factory file validator and
   inspect the apply plan before enabling it. Structural validation does not
   check live credentials, provider names, or runtime availability.

Examples are templates, not preconfigured live factories. For this ticket
example, a human or the existing GitHub–Linear integration moves tickets to
Done after merge; there is no scheduled sweep or GitHub lifecycle automation.

## Add an example

Add a sibling directory with a complete factory tree and its own README,
then link that README under **Available factories**. Keep the detailed
workflow in the example's README rather than duplicating it in this catalog.
