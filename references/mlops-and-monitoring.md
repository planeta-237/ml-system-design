# MLOps And Monitoring

Use this file when the task involves training pipelines, deployment, model
registry, reproducibility, drift, alerting, retraining, or incident response.

## Checklist

- Training data, code, parameters, model artifact, metrics, and environment are
  versioned.
- Promotion criteria are explicit and include guardrail metrics.
- CI/CD covers tests for data contracts, feature code, training code, serving
  code, and inference compatibility.
- Model registry records lineage, approvals, owners, and rollback target.
- Monitoring covers data quality, feature drift, prediction drift, model
  quality, product impact, latency, error rates, and cost.
- Alerts map to owners and runbooks; not every dashboard anomaly should page.
- Retraining is event-driven, scheduled, or manual by an explicit policy.
- Incidents can be mitigated by rollback, fallback, disabling automation, or
  human review.
