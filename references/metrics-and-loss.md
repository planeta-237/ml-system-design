# Metrics and Loss Functions

Use this file when designing or reviewing the metric hierarchy, offline/online metrics, and loss functions for an ML system.

## Metric hierarchy

A single ML metric is rarely enough. Build a pyramid of metrics that connects model behavior to business value.

- [ ] Metric hierarchy / tree / pyramid defined.
- [ ] **North Star** metric identified — one metric that captures product value.
- [ ] North Star is a **leading** metric when possible, not only a lagging one.
- [ ] Metrics decomposed by level: business → product → operational → ML model.
- [ ] Formula decomposed: know what inputs drive each top-level metric.
- [ ] Multiple comparisons effect considered when using many metrics.
- [ ] Absolute vs relative lift distinguished and the decision rule made explicit.

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
- [ ] **Guardrail** metrics defined to protect the system from unintended harm.

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
