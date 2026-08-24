# Entity Resolution Design Trade-offs

Entity resolution has two different optimization problems: finding plausible candidate pairs efficiently, and deciding whether a candidate pair represents the same real-world entity.

## Candidate generation

Common blocking keys include normalized email domain, phone suffix, postal code, name prefix, or phonetic token. Multiple blocking passes can improve recall without returning to all-pairs comparison.

## Scoring

Useful features include exact email/phone agreement, normalized-name similarity, address similarity, shared identifiers, and negative evidence. Scores should remain inspectable so false positives can be diagnosed.

## Operational metrics

A production system should track:
- candidate reduction ratio
- precision / recall on labeled samples
- merge reversal rate
- records per canonical cluster
- processing latency
- percentage of auto-match vs manual-review decisions

False-positive merges are usually more expensive than false negatives because they contaminate downstream customer identity, permissions, analytics, and transactions. Thresholds should reflect that asymmetry.