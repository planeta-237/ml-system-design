# Output Templates

Use this file when formatting the final response for a design, review, scorecard,
or teaching answer.

## Design Output

```markdown
## Architecture Shape
- Goal, users, decision, and why ML is appropriate.

## Requirements
- Product metrics, model metrics, guardrails, latency, freshness, cost, privacy.

## Data Flow
- Sources -> validation -> features/labels -> training/evaluation -> serving.

## Modeling And Evaluation
- Baseline, model family, metrics, offline validation, online experiment plan.

## Serving And Operations
- Request path, dependencies, fallbacks, rollout, monitoring, retraining.

## Risks And Trade-offs
- Launch blockers, deferred work, and phased roadmap.
```

## Review Output

```markdown
## Findings
- [P0/P1/P2] Finding title - concrete evidence and impact.

## Score
- Optional score with dimension breakdown, only when requested.

## Strengths
- Evidence-backed positives worth preserving.

## Recommendations
- Prioritized fixes or design changes.

## Open Questions
- Questions whose answers would materially change the review.
```

## Teaching Output

Answer directly first. Add a small example or decision table only if it clarifies
the concept. Do not expand into a full design unless the user asks.
