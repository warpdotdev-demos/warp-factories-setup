# Example Ticket Factory

[All factory examples](../README.md) · [Setup guide](../../README.md)

A single agent factory to implement and verify linear tickets following this flow:
**read ticket → check blockers → implement -> verify → human PR hand-off**

This factory is meant for working on well specified tickets that already supplies requirements, diagnosis/reproduction when relevant, and acceptance criteria.

## Agent
**`implementer`:** reads the issue, checks readiness + blockers, implements the bug or feature, verifies it, and delivers one PR. Blocked work stops before coding.

## Automations
**`linear-intake`:** runs on Linear delegation or the `factory-implement` label.
**`check-blockers`:** runs only when an issue enters the configured `Done` state. It checks for newly unblocked issues and moves those to implementation.