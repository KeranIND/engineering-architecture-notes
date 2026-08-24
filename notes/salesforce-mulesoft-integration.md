# Salesforce + MuleSoft Integration Boundaries

My enterprise work has included Salesforce application logic, Apex/LWC workflows, REST integrations and MuleSoft-based transformation between business applications.

The design concern is not simply moving JSON between systems. The boundary has to preserve business identity, tolerate retries, isolate failures and make transformations observable.

## Pattern

```text
Source system
   ↓
Canonical request contract
   ↓
MuleSoft / integration layer
   ├── validation
   ├── transformation
   ├── enrichment
   ├── idempotency key
   └── error classification
   ↓
Salesforce / downstream API
   ↓
Business workflow
```

## Rules I prefer

- keep system-specific schemas at the edges
- use a canonical internal contract where practical
- make retryability explicit per failure class
- never assume a timeout means the downstream write failed
- persist correlation IDs across hops
- separate technical success from business acceptance
- make transformations inspectable rather than buried in opaque mappings

## Why this matters

A locally successful API call can still create bad operational state if ownership, opportunity, customer identity or downstream workflow assumptions are violated. Integration architecture must therefore carry business context, not only payload data.
