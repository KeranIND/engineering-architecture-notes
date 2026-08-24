# FitID Measurement Provenance

A measurement value without provenance is not enough for a fit system.

Chanamill can receive measurements from several capture paths: guided/manual entry, phone-based capture, in-person scanning, and later corrected measurements based on real delivered garments.

## Model

```text
measurement value
  + capture method
  + confidence
  + device / session
  + timestamp
  + FitID version
  + correction lineage
```

## Why provenance matters

A 102 cm chest value produced by an in-person scan and the same value entered manually are not identical observations operationally. Their confidence, reproducibility, and eligibility for automatic decisions can differ.

## Rules

- never overwrite the previous measurement snapshot in place
- version FitID after material measurement changes
- store capture method per observation
- preserve confidence and rejected observations
- record the exact FitID version used by an order
- keep post-delivery corrections separate from original observations

That makes recommendations, manufacturing decisions and later fit feedback reproducible.