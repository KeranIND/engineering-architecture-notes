# Idempotency in Distributed Workflows

Retries are unavoidable in distributed systems. The design question is whether a retry repeats an intended action or creates a second side effect.

## Principle

A command with the same semantic identity should be safe to process more than once.

A typical pattern:

```text
request + idempotency key
        ↓
lookup prior result
   ├── found → return it
   └── missing
         ↓
      execute
         ↓
 persist result atomically
         ↓
      return
```

## Boundary choices

An idempotency key should represent the business operation, not merely an HTTP request. `create-order:customer-123:checkout-456` is stronger than a random retry token if the system needs to reason about intent.

## Failure cases to design for

- process crashes after side effect but before response
- message is delivered twice
- client retries after timeout
- two workers race on the same key
- downstream provider accepts a request but upstream times out

## Production implementation

For a real service, an in-memory map is insufficient. The key and result need durable storage with a uniqueness constraint or atomic compare-and-set behavior. TTL policy should reflect how long duplicate intent can realistically recur.

The key idea: **exactly-once delivery is rarely available end to end; idempotent processing is how systems approximate exactly-once business effects.**
