# Made-to-Measure Order Orchestration

Chanamill's made-to-measure flow crosses software and physical operations. That makes workflow state more important than a typical cart-to-shipping pipeline.

## Order boundary

An order should freeze:
- FitID version
- garment-spec version
- selected configuration
- pricing decision

## Operational flow

```text
order accepted
    ↓
FitID/spec snapshot locked
    ↓
payment authorized
    ↓
production job created
    ↓
manufacturing assignment
    ↓
quality-control result
    ↓
freight / fulfillment
    ↓
delivery
    ↓
fit feedback
```

## Why explicit orchestration

Physical work introduces irreversible or costly steps. A timeout after production has started is fundamentally different from a retryable API read. The orchestrator therefore needs to distinguish:

- retryable technical failure
- business rejection
- physical work already completed
- compensation still possible
- manual review required

## Required properties

- durable state
- idempotent external commands
- explicit transition history
- versioned order inputs
- human-review escape hatch
- post-delivery feedback event

This note describes the system boundary behind Chanamill's measurement-to-production loop without exposing manufacturing partners or private implementation details.