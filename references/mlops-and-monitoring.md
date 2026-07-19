# MLOps And Monitoring

Use this file when the task involves training pipelines, deployment, model
registry, reproducibility, drift, alerting, retraining, or incident response.

## Observability

Observability is the ability to understand system state from its outputs. The
three pillars are metrics, logs, and traces.

- **Metrics:** time-series numbers (latency, throughput, error rate, drift).
- **Logs:** structured event records for debugging and audit.
- **Traces:** request chains across distributed services.

## SLI / SLO / SLA

- **SLI** (Service Level Indicator): a measurable metric (e.g., P95 latency).
- **SLO** (Service Level Objective): a target for the SLI (e.g., P95 < 200 ms).
- **SLA** (Service Level Agreement): a contractual consequence of missing SLOs.
- SLOs should be few, user-visible, and tied to error budgets.

## Checklist

- Training data, code, parameters, model artifact, metrics, and environment are
  versioned.
- Promotion criteria are explicit and include guardrail metrics.
- CI/CD covers tests for data contracts, feature code, training code, serving
  code, and inference compatibility.
- Training pipeline is a DAG with reproducible steps and generated artifacts
  (metrics, curves, error analysis, top-N cases).
- Model registry records lineage, approvals, owners, and rollback target.
- A data validation pipeline enforces constraints on upstream data and alerts on
  violations.
- Monitoring covers data quality, feature drift, prediction drift, model
  quality, product impact, latency, error rates, and cost.
- Alerts map to owners and runbooks; not every dashboard anomaly should page.
- Retraining is event-driven, scheduled, or manual by an explicit policy.
- Incidents can be mitigated by rollback, fallback, disabling automation, or
  human review.
- Runbooks and postmortem process exist for common incident classes.
