# FitID as a Versioned Identity Model

FitID is useful only if a decision can be reproduced later. A shopper's measurements and preferences can change; a garment specification can also change between production runs.

## Rule

Do not attach an order to "the current FitID." Freeze the exact FitID version used when the order decision was made.

```text
FitID v12
  chest: ...
  waist: ...
  fit preference: regular
        ↓
Garment Spec v7
        ↓
Fit Assessment A31
        ↓
Order O91
```

If the customer later updates to FitID v13, order O91 still points to v12.

## Why

Versioned snapshots make it possible to:
- reproduce the original recommendation
- compare expected vs delivered fit
- separate measurement changes from garment-spec changes
- learn from feedback without corrupting history
- audit why a specific recommendation was made

This is the identity-layer principle behind Chanamill's FitID architecture.