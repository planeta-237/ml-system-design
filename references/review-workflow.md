# Review Workflow

Use this file when reviewing an existing ML system design, repository, product
document, architecture diagram, metrics dashboard, or incident write-up.

## Evidence Handling

- Review only the artifacts available in the workspace or supplied by the user.
- Mark claims as Unknown when evidence is missing.
- Treat contradictions between docs, code, metrics, and telemetry as findings.
- Do not penalize a design for lacking an implementation when the requested
  artifact is only a design doc; instead mark reproducibility as unverified.

## Review Passes

1. Product fit: problem, users, decision, value, success metrics.
2. Data fit: availability, quality, representativeness, labels, leakage, skew,
   governance, privacy, and retention.
3. Model fit: baseline, model choice, metrics, evaluation design, failure modes.
4. System fit: batch/stream/online architecture, storage, serving, latency,
   scalability, fallbacks, rollback, and cost.
5. Operations fit: CI/CD, model registry, monitoring, retraining, incident
   response, ownership, and documentation.
6. Responsible AI fit: safety, fairness, explainability, abuse, compliance, and
   human review where needed.

## Finding Style

Lead with risks that can cause product failure, unsafe behavior, unreliable
operation, or misleading evaluation. Keep cosmetic architecture preferences out
of the top findings unless they create real delivery risk.
