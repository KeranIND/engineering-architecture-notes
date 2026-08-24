# Fit Intelligence vs Style and Behavioral Preference

Chanamill has multiple recommendation signals that should not be collapsed into one number.

## Fit signal

Answers: **Will this garment physically fit the customer the way they want?**

Inputs:
- body measurements
- preferred ease
- garment finished measurements
- fabric/stretch metadata
- construction/silhouette

## Style signal

Answers: **Does this item match the customer's aesthetic intent?**

Inputs can include:
- color
- silhouette
- occasion
- style intent
- creator/designer preference

## Behavioral signal

Answers: **What has the customer historically engaged with?**

Inputs can include:
- views
- saves
- purchases
- skips
- returns

## Decision architecture

```text
fit assessment ───────┐
style preference ─────┼→ final recommendation policy
behavioral affinity ──┤
availability / cost ──┘
```

Keeping the components separate preserves explainability. A product can be stylistically relevant but physically risky; the system should be able to say so explicitly rather than hiding the conflict inside one opaque ranking score.