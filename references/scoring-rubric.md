# Scoring Rubric

Use this file only when the user asks for a score or when a review explicitly
requires calibrated scoring.

## 10-Point Model

| Dimension | Max | What to Check |
|-----------|-----|---------------|
| Product and Requirements Fit | 1.5 | clear objective, users, decision, success metrics, constraints |
| Data and Feature Design | 2.0 | sources, labels, leakage, quality, skew, freshness, privacy, governance |
| Modeling and Evaluation | 2.0 | baseline, model choice, metrics, validation, experiments, failure analysis |
| System Architecture | 1.5 | batch/online shape, APIs, storage, scaling, latency, fallbacks, rollback |
| MLOps and Monitoring | 1.5 | pipelines, registry, reproducibility, deployment, drift, alerts, retraining |
| Risk and Responsible AI | 1.0 | safety, fairness, explainability, compliance, abuse, human oversight |
| Communication and Trade-offs | 0.5 | clear narrative, phased roadmap, explicit trade-offs |

## Anchors

- **9.0-10.0**: production-grade design with strong evidence and clear operations.
- **7.5-8.9**: strong design with manageable gaps.
- **6.0-7.4**: plausible design but important risks remain unresolved.
- **4.0-5.9**: major gaps in data, evaluation, architecture, or operations.
- **0.0-3.9**: unreviewable, unsafe, or not meaningfully an ML system design.

## Examples

- **9.0–10.0**: Clear product goal, strong evidence, clean data/feature design,
  reproducible evaluation, production serving, monitoring, and incident response.
  Few minor gaps.
- **7.5–8.9**: Sound architecture; missing details like canary rollout,
  segment-level metrics, or cost model, but manageable.
- **6.0–7.4**: Plausible but unresolved issues: unclear labels, no online eval,
  weak monitoring, or no fallback.
- **4.0–5.9**: Major gaps: data leakage, missing serving architecture, no
  baseline, or unaddressed safety.
- **0.0–3.9**: Unreviewable, unsafe, or not meaningfully an ML system design.

Score evidence, not confidence. Missing stage-critical evidence should cap the
score even when the proposal sounds plausible.
