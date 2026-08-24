# ADR-001: Prefer explicit orchestration for multi-step order workflows

**Status:** Accepted

## Context

Order processing crosses inventory, payment, and fulfillment boundaries. Each subsystem can fail independently and cannot participate in one atomic database transaction.

## Decision

Use an explicit saga coordinator for workflows that require ordered steps, compensation, and a clear terminal state.

## Consequences

Positive:
- workflow state is inspectable
- compensation is centralized
- operational debugging is simpler
- business sequencing is explicit

Trade-offs:
- coordinator owns additional state
- service contracts must remain narrow
- orchestration can become over-centralized if unrelated workflows are added indiscriminately

## Rejected alternative

Pure event choreography was rejected for the core order path because control flow and compensation would become distributed across too many consumers.