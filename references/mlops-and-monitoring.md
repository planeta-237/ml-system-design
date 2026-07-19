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

## Drift taxonomy

- **Data drift:** input feature distribution changes (e.g., new sensor, new
  user behavior, missing values spike).
- **Concept drift:** the relationship between inputs and labels changes
  (e.g., market regime shift, policy change).
- **Prediction drift:** output distribution changes without a corresponding
  input shift (e.g., model starts predicting more positives).
- **Label drift:** ground-truth label distribution changes; may require
  updated labels or a new validation set.
- **Upstream schema drift:** feature names, types, or units change in source
  systems.

## Checklist

- [ ] Training data, code, parameters, model artifact, metrics, and environment are
  versioned.
- [ ] Promotion criteria are explicit and include guardrail metrics.
- [ ] CI/CD covers tests for data contracts, feature code, training code, serving
  code, and inference compatibility.
- [ ] Training pipeline is a DAG with reproducible steps and generated artifacts
  (metrics, curves, error analysis, top-N cases).
- [ ] Model registry records lineage, approvals, owners, and rollback target.
- [ ] A data validation pipeline enforces constraints on upstream data and alerts on
  violations.
- [ ] Monitoring covers data quality, feature drift, prediction drift, model
  quality, product impact, latency, error rates, and cost.
- [ ] Alerts map to owners and runbooks; not every dashboard anomaly should page.
- [ ] Retraining is event-driven, scheduled, or manual by an explicit policy.
- [ ] Incidents can be mitigated by rollback, fallback, disabling automation, or
  human review.
- [ ] Runbooks and postmortem process exist for common incident classes.

## Retraining and rollback

- [ ] Retraining triggers are explicit: performance threshold, data drift,
  schedule, or business event.
- [ ] A holdout or shadow evaluation dataset validates the new model before
  promotion.
- [ ] Rollback target is pre-staged: previous model version, prompt version, or
  feature toggle state.
- [ ] Rollback is tested and can be executed in minutes, not hours.
- [ ] Champion/challenger or shadow mode can compare a new model to the
  production model before full traffic.

## Incident response

- [ ] On-call rotation and escalation path are documented.
- [ ] Common failure modes have runbooks: model degradation, data pipeline
  failure, dependency outage, drift alert, cost spike.
- [ ] Postmortems document root cause, impact, mitigation, and prevention
  actions; action items are tracked.
- [ ] Blameless culture: focus on system fixes, not personal fault.
