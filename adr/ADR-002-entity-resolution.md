# ADR-002: Separate candidate generation from entity scoring

**Status:** Accepted

## Context

Comparing every record with every other record is O(n²) and becomes impractical quickly. At the same time, aggressive blocking can reduce recall if it is intertwined with final match logic.

## Decision

Split entity resolution into two explicit stages:

1. candidate generation / blocking to reduce the comparison set
2. feature scoring and decision logic to determine whether a candidate pair matches

## Consequences

Positive:
- candidate-reduction efficiency can be measured independently
- scoring stays explainable
- blocking strategies can evolve without rewriting match logic
- recall and precision can be tuned separately

Trade-offs:
- more pipeline stages to operate
- poor blocking choices can still hide true matches
- evaluation requires labeled or synthetic validation data
