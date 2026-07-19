# Metrics and Loss Functions

Use this file when designing or reviewing the metric hierarchy, offline/online metrics, and loss functions for an ML system.

## Metric hierarchy

A single ML metric is rarely enough. Build a pyramid of metrics that connects model behavior to business value.

```
Business metrics         Revenue, LTV, CAC, churn
Product metrics          DAU, conversion, engagement
Operational metrics      Latency, throughput, error rate
ML model metrics         Precision, recall, AUC, log loss, calibration
```

Each level should explain the level above. If an ML metric rises but the product
metric falls, the proxy is wrong or the model is not driving the intended
behavior.

- [ ] Metric hierarchy / tree / pyramid defined.
- [ ] **North Star** metric identified — one metric that captures product value.
- [ ] North Star is a **leading** metric when possible, not only a lagging one.
- [ ] Metrics decomposed by level: business → product → operational → ML model.
- [ ] Formula decomposed: know what inputs drive each top-level metric.
- [ ] Multiple comparisons effect considered when using many metrics.
- [ ] Absolute vs relative lift distinguished and the decision rule made explicit.

## Counter-metrics and guardrails

Every primary metric needs a counter-metric that protects against gaming it.

| Primary metric | Counter-metric / guardrail |
|---|---|
| Click-through rate | Bounce rate, time-to-bounce |
| Conversion | Time to convert, support tickets, refund rate |
| Precision | Coverage, recall |
| Recall | Precision, false-positive rate |
| Engagement | Unsubscribe, churn, report rate |
| Latency | Error rate, fallback rate, cost per request |

- [ ] Vanity metrics avoided (e.g., total users without active users).
- [ ] Metric duplication avoided (e.g., MAU and DAU without ratio or trend).
- [ ] Conflicting KPIs across teams are surfaced and resolved explicitly.
- [ ] **Guardrail** metrics defined to protect the system from unintended harm.

## Offline vs online metrics

- [ ] Offline metric is a **predictor** of the online metric.
- [ ] Offline metric is **sensitive** enough to detect changes without 10× effect sizes.
- [ ] Clear link: improving which proxy metric drives which business metric.
- [ ] Rare events accounted for: low conversion requires more data to measure.
- [ ] Value chain constructed when applicable (e.g., revenue → purchases → conversion → clicks → impressions).
- [ ] Offline metric gives the **right to run A/B**: evidence that offline gain correlates with online effect.
- [ ] Loss improvement translates into metric improvement.
- [ ] Secondary effects considered (cannibalization, segment shifts, feedback loops).

## Metric types

- [ ] Input vs indicator, leading vs lagging distinguished.
- [ ] Time scope per metric clear: per time / session / cohort / user.
- [ ] What-if analysis done: minimum input change for maximum target impact.

## Loss functions

- [ ] Loss is differentiable and globally continuous if using gradient methods.
- [ ] Loss choice justified by business logic, not just default (MSE / cross-entropy).
- [ ] Impact of loss on error distribution considered (outliers vs robust).
- [ ] Class imbalance handled (focal loss, weighting, sampling).
- [ ] Combined losses used when needed.
- [ ] Loss not dominated by outliers.

## Diagnosing metrics and loss

- [ ] Metric computation correctness verified: expected range, no NaN, no division by zero, correct normalization.
- [ ] Link between loss decrease and target metric growth checked.
- [ ] Train / validation curves used to diagnose overfitting and underfitting.
- [ ] Hierarchy stress-tested: can we game the metric? Is there a counterexample?

## Decision tables

| Goal | Loss / metric to consider |
|---|---|
| Predict a continuous value, outliers are rare | MSE |
| Predict a continuous value, robust to outliers | MAE, Huber, quantile loss |
| Need prediction intervals | Quantile loss, negative log-likelihood |
| Predict probability | Log-loss / BCE |
| Class imbalance | Focal loss, weighted cross-entropy, class sampling |
| Cost of false positives ≠ false negatives | Expected cost at threshold, F-beta, AUPRC |
| Ranking / recommendation | NDCG, MAP, MRR, recall@k, precision@k |
| Forecasting with seasonality | MAE/MAPE by horizon, pinball loss, bias/coverage |
| Generation / LLM | Task success, groundedness, safety, human preference, cost |

| Symptom | Likely cause | Action |
|---|---|---|
| Train loss ↓, validation loss ↑ | Overfitting | More data, regularization, simpler model, early stopping |
| Loss ↓, business metric flat | Wrong proxy or metric gaming | Re-link metric to business outcome, add constraints |
| Loss oscillates or NaN | Bad data, too-high LR, numeric issue | Check data, gradient clipping, lower LR, scale features |
| Offline metric ↑, A/B metric flat | Offline-online mismatch | Revalidate proxy correlation, check serving features |
| Metric suddenly spikes without code change | External event, data drift, broken pipeline | Investigate upstream data and environment |

