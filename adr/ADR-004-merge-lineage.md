# ADR-004: Preserve merge provenance before destructive consolidation

**Status:** Accepted

## Context

CRM deduplication changes identity structure. Once duplicate records are consolidated, information that existed only on the losing record can become difficult to reconstruct.

## Decision

Persist merge lineage and field-level survivorship context before executing destructive consolidation.

## Consequences

Positive:
- auditability
- safer incident analysis
- ability to explain why the survivor was chosen
- visibility into which record supplied each canonical field
- better support for downstream reconciliation

Trade-offs:
- more metadata to store
- merge execution requires an additional planning step
- lineage retention policies must be defined
