# Closed-Loop Systems for Physical-World Work

A recurring systems pattern in the problems I care about is: start with humans and real operations, capture structured ground truth, then automate the repeatable parts over time.

For Chanamill, the loop is:

```text
measure person
    ↓
create FitID
    ↓
match / configure garment
    ↓
manufacture
    ↓
deliver
    ↓
observe fit outcome
    ↓
feed evidence back into future decisions
```

## Why the loop matters

A model trained only on static measurements misses what actually happened after the garment was produced and worn. Delivered-fit outcomes create stronger evidence than assumptions made at checkout.

## Human-in-the-loop principle

Humans remain useful where:
- measurement confidence is low
- a fit decision is ambiguous
- production constraints require judgment
- QC detects an exception
- feedback conflicts with prior assumptions

The system should capture those interventions as data rather than treating them as invisible manual work.

This approach also generalizes beyond apparel to other labor-intensive operational systems where machine automation benefits from first learning from skilled human decisions.