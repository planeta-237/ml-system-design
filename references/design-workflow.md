# Design Workflow

Use this file when creating a new ML system design or answering an ML system
design interview prompt.

## High-level framework

A repeatable design cycle for AI/ML systems:

```
Product Requirements → System Design → Evaluation & Monitoring → Optimization
```

- **Product Requirements:** what to build, for whom, business constraints,
  success metrics, and human-in-the-loop needs.
- **System Design:** data strategy, model/components, architecture patterns,
  serving, and operational constraints.
- **Evaluation & Monitoring:** offline evaluation, online experiments, guardrails,
  observability, and drift detection.
- **Optimization:** accuracy, latency, cost, reliability, and user experience
  iterated after launch.

Start with the simplest pattern that satisfies the requirements. Prefer control
flow and human review for high-stakes decisions; add autonomy only after the
system is validated.

## Steps

1. Clarify the product objective, users, actions, and decision to automate or
   support. Frame the problem space: root cause, stakeholders, anti-goals,
   constraints, and price of error.
2. Define success metrics: product metrics, model metrics, guardrail metrics,
   cost, latency, freshness, reliability, and safety.
3. Identify data sources, labels, feedback loops, cold-start paths, privacy
   constraints, and data retention needs.
4. Start with a simple baseline that can ship or validate the problem.
5. Choose the model family only after data and product constraints are clear.
6. Design the offline path: ingestion, validation, training, evaluation, model
   registry, reproducibility, and promotion.
7. Design the online path: request flow, feature access, serving, caching,
   fallbacks, rate limits, and product integration.
8. Design monitoring: data quality, model quality, drift, latency, cost,
   business impact, and safety.
9. Name explicit trade-offs, launch blockers, and phased implementation.

## Default Design Sections

- Problem space and anti-goals.
- Goal and assumptions.
- Requirements and constraints.
- Data and labels.
- Architecture and data flow.
- Modeling approach and baselines.
- Evaluation and experimentation.
- Serving and product integration.
- Monitoring, retraining, and operations.
- Risks, trade-offs, and phased roadmap.
