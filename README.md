# Engineering Architecture Notes

A public notebook of architecture decisions and systems patterns drawn from the **actual problem domains I work in**: enterprise CRM/data systems, API/integration architecture, workflow orchestration, and Chanamill's measurement-to-manufacturing personalization loop.

The notes are written from experience but use public-safe abstractions. They contain no employer/client source code, private schemas, credentials, or Chanamill protected algorithms.

## Enterprise systems track

My enterprise work has involved Salesforce/Apex/LWC, MuleSoft/REST integrations, large-volume CRM data, onboarding and ownership workflows, opportunity/sales processes, routing, and deduplication/entity resolution across millions of records.

Notes in this track:

- [CRM entity resolution at multi-million-record scale](notes/entity-resolution.md)
- [Idempotency across API and workflow boundaries](notes/idempotency.md)
- [Designing downstream-safe merge operations](notes/downstream-safe-merge.md)
- [Ownership and routing as state machines](notes/ownership-routing.md)
- [Salesforce + MuleSoft integration boundaries](notes/salesforce-mulesoft-integration.md)

## Chanamill systems track

Chanamill combines software with physical-world constraints: measurements, fit preferences, garment specifications, visualization, made-to-measure production, creator commerce, fulfillment, and delivered-fit feedback.

Notes in this track:

- [FitID as a versioned identity model](notes/fitid-versioning.md)
- [Measurement provenance and capture confidence](notes/measurement-provenance.md)
- [Separating fit, style and behavior signals](notes/fit-vs-preference.md)
- [3D visualization as a versioned boundary](notes/3d-visualization-boundary.md)
- [Made-to-measure order orchestration](notes/mtm-orchestration.md)
- [Made-to-measure manufacturing and fulfillment](notes/manufacturing-fulfillment.md)
- [Creator commerce as an attribution layer](notes/creator-commerce.md)
- [Physical-world feedback loops](notes/closed-loop-systems.md)

## One architecture, two contexts

The same engineering principles appear repeatedly across enterprise software and Chanamill:

```text
Enterprise CRM                          Chanamill
--------------                          ---------
Lead / Contact identity        <->      FitID identity
Data provenance                <->      Measurement provenance
Ownership / routing            <->      Product / creator routing
API integration                <->      Capture / render / production boundaries
Workflow state                 <->      MTM manufacturing state
Downstream side effects        <->      Physical production side effects
Operational feedback           <->      Delivered-fit feedback
```

The domain changes; the systems problem does not. In both cases the architecture has to preserve context, make irreversible decisions reproducible, tolerate retries and partial failure, and keep enough provenance to explain what happened later.

## Architecture decision records

- [ADR-001: Prefer explicit orchestration for multi-step order workflows](adr/ADR-001-order-orchestration.md)
- [ADR-002: Separate candidate generation from entity scoring](adr/ADR-002-entity-resolution.md)
- [ADR-003: Freeze FitID and garment-spec versions at order time](adr/ADR-003-fitid-snapshots.md)
- [ADR-004: Preserve merge provenance before destructive consolidation](adr/ADR-004-merge-lineage.md)

## Engineering principles

- preserve business context before mutating data
- treat integrations as independently failing systems
- make state transitions explicit
- make retries idempotent
- version decisions that must be reproduced later
- separate raw observations from derived state
- keep explanations and provenance available for operational review
- use reconciliation before repeating physical-world side effects
- design for downstream effects, not only the local transaction

This repository is intentionally architecture-heavy because the most important work in these systems is often not writing another endpoint; it is deciding where state lives, how failures propagate, and how the system remains explainable after it scales.