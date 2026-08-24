# Engineering Architecture Notes

A public notebook for system-design decisions, integration patterns, reliability trade-offs, and architecture write-ups.

This repository is intentionally code-light. The goal is to document **how I reason about systems**: boundaries, contracts, failure modes, observability, consistency, and operational trade-offs.

## Topics

- API and integration architecture
- idempotency and retries
- event-driven workflows
- entity resolution and data quality
- distributed transaction patterns
- observability and failure isolation
- commerce domain boundaries
- architecture decision records (ADRs)

## Notes

- [Idempotency in distributed workflows](notes/idempotency.md)
- [Saga orchestration vs choreography](notes/saga-orchestration.md)
- [Entity-resolution design trade-offs](notes/entity-resolution.md)

## ADRs

- [ADR-001: Prefer explicit orchestration for multi-step order workflows](adr/ADR-001-order-orchestration.md)
- [ADR-002: Separate candidate generation from entity scoring](adr/ADR-002-entity-resolution.md)

The examples are original reference material and do not contain employer or client implementation details.