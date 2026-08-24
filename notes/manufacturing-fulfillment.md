# Made-to-Measure Manufacturing and Fulfillment

A made-to-measure apparel order is not complete when payment succeeds. The software system has to coordinate a physical production chain while preserving the exact fit and garment inputs used to make the item.

## Order-to-delivery flow

```text
FitID snapshot
Garment spec snapshot
        ↓
Production job
        ↓
Fabric / cutting
        ↓
Stitching
        ↓
Quality control
        ↓
Pack / carrier handoff
        ↓
Delivery
        ↓
Fit feedback
```

## State that must be preserved

- FitID version used at checkout
- garment specification version
- customization choices
- production partner
- QC result and notes
- shipment/tracking identity
- delivered timestamp
- feedback linked to the same versions

## Failure boundaries

Software retries cannot blindly repeat physical actions. Creating a second production job is very different from replaying an idempotent API read.

Commands that cross into manufacturing therefore need durable business keys and explicit acknowledgement state. A timeout should trigger reconciliation before a duplicate physical instruction is emitted.

## QC as a gate

QC should be an explicit state transition, not a free-form note attached after the fact. Failed QC returns the job to a repair/rework path; only a passed version becomes eligible for fulfillment.

## Feedback closes the loop

Once delivered, the order becomes evidence. Region-level fit feedback should remain attached to the FitID version and garment-spec version that produced the physical item, allowing future decisions to learn from the real outcome instead of only from clicks.