# ADR-003: Freeze FitID and garment-spec versions at order time

**Status:** Accepted

## Context

Both a customer's FitID and a garment specification can change after checkout. If an order references mutable "current" state, the original recommendation becomes impossible to reproduce reliably.

## Decision

Persist immutable references to the FitID snapshot and garment-spec version used for the order.

## Consequences

Positive:
- deterministic post-order analysis
- reliable fit-feedback attribution
- clear separation between profile evolution and historical transactions
- safer debugging of recommendation outcomes

Trade-offs:
- version storage and retention requirements
- migrations must preserve old representations
- downstream systems need version-aware contracts
