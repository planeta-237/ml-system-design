# Output Templates

Use this file when formatting the final response for a design, review, scorecard,
or teaching answer.

## Design Output Template

```markdown
## Problem Space and Goal
- Product problem, users, decision, and why ML is appropriate.
- Anti-goals and constraints.

## Requirements and Success Metrics
- Product metrics, model metrics, guardrails, latency, freshness, cost, privacy.

## Data Flow
- Sources -> validation -> features/labels -> training/evaluation -> serving.

## Modeling And Evaluation
- Baseline, model family, metric hierarchy, offline validation, online experiment plan.

## Serving And Operations
- Request path, dependencies, fallbacks, rollout, monitoring, retraining.

## Risks And Trade-offs
- Launch blockers, deferred work, and phased roadmap.
```

## Review Output Template

```markdown
## Findings
- [P0/P1/P2] Finding title - concrete evidence and impact.

## Score (optional)
- Score with dimension breakdown, only when requested.

## Strengths
- Evidence-backed positives worth preserving.

## Recommendations
- Prioritized fixes or design changes.

## Open Questions
- Questions whose answers would materially change the review.
```

## Scoring Rubric Template

Use this template when a numeric score is requested.

```markdown
| Dimension | Max | Score | Evidence | Notes |
|-----------|-----|-------|----------|-------|
| Product and Requirements Fit | 1.5 | | Verified / Partial / Unknown | |
| Data and Feature Design | 2.0 | | Verified / Partial / Unknown | |
| Modeling and Evaluation | 2.0 | | Verified / Partial / Unknown | |
| System Architecture | 1.5 | | Verified / Partial / Unknown | |
| MLOps and Monitoring | 1.5 | | Verified / Partial / Unknown | |
| Risk and Responsible AI | 1.0 | | Verified / Partial / Unknown | |
| Communication and Trade-offs | 0.5 | | Verified / Partial / Unknown | |
| **Total** | **10.0** | | Coverage: | Provisional when material evidence is Unknown |
```

## Teaching Output Template

Answer directly first. Add a small example or decision table only if it clarifies
the concept. Do not expand into a full design unless the user asks.

```markdown
## Direct Answer
- Brief, concrete answer to the question.

## Example (optional)
- One small example or comparison table.

## When to Apply / When to Avoid
- Context for using the concept.
```
