# Ownership and Routing as Stateful Workflows

Enterprise ownership logic becomes fragile when it is treated as a collection of unrelated triggers. A safer mental model is a state machine with explicit inputs, eligibility rules, transitions, and side effects.

## Inputs

Typical inputs can include:

- customer/account segment
- geography
- sales motion
- current owner
- queue capacity
- record status
- opportunity context
- integration source

## State-machine view

```text
UNASSIGNED
   ↓ eligibility
QUEUED
   ↓ assignment
OWNED
   ↓ reassignment condition
REVIEW
   ↓ approved transition
OWNED
```

The exact states differ by business process, but the architectural benefits are consistent:

- transition rules become testable
- invalid jumps can be rejected
- side effects can be idempotent
- ownership history can be audited
- routing failures become observable

## Integration boundary

Ownership changes often trigger downstream behavior. The local update should therefore be separated from external side effects through an event/outbox boundary rather than assuming every consumer succeeds synchronously.

This note is based on real enterprise workflow architecture experience and uses generic public-safe concepts rather than employer-specific routing logic.