# Downstream-Safe CRM Merge Design

A duplicate-record merge is not merely a database cleanup operation. In enterprise CRM systems, records are referenced by ownership rules, opportunities, activities, integrations, routing, analytics, and external systems.

## Core problem

A merge that produces the correct surviving customer record can still be operationally wrong if downstream context is lost.

Before consolidation, the system should identify:

- record ownership
- open opportunities and pipeline relationships
- task/activity history
- routing state
- integration identifiers
- source-system provenance
- permissions and sharing implications
- external references

## Safe merge sequence

```text
candidate pair
    ↓
match evidence
    ↓
downstream impact discovery
    ↓
survivor decision
    ↓
field survivorship plan
    ↓
relationship re-parenting plan
    ↓
merge execution
    ↓
post-merge validation
    ↓
lineage / audit record
```

## Design principle

**Preserve business context before destroying duplicate structure.**

Once two records are collapsed, context that existed only on the losing record can become difficult or impossible to reconstruct.

## Operational controls

- dry-run mode
- explicit merge plan
- high-risk relationship checks
- audit trail
- deterministic survivor rules
- post-merge invariants
- retry-safe integration updates
- manual-review path for ambiguous cases

This note reflects the systems thinking required in large CRM deduplication work while intentionally omitting employer-specific objects, field names, and implementation details.