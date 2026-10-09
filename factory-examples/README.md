# Factory examples

[Setup guide](../README.md) · [Automation examples](../automation-examples/README.md)

Complete factory templates. Each example has its own workflow and setup checklist.

## Available factories

- [Example Ticket Factory](example-ticket-factory/README.md): one agent implements
  and verifies Linear tickets, with dependency-aware intake.

## Use an example

1. Copy an example directory, follow its setup checklist, and connect its integrations.
2. Register the directory containing `factory.yaml` as the Factory root.
3. Ask Warp Agent: “Validate the factory definition at `<factory-root>` using the `factory-files` skill.” See [validation instructions](https://docs.warp.dev/factories/factory-as-code/#validate-with-a-coding-agent).
4. For a registered GitHub-backed factory, review the [`warp/factory-config` PR check](https://docs.warp.dev/factories/factory-as-code/#pull-request-checks) for proposed resource changes and access errors before merging.

## Add an example

Add a complete factory directory and link its README above. Keep that README short:
**Agents**, **Automations**, **Required setup** (values and files),
**Optional customization**, and **Before enabling**.
