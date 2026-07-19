# Modeling And Evaluation

Use this file when reviewing or designing baselines, model families, metrics,
offline validation, online experiments, or failure analysis.

## Checklist

- A simple baseline is defined before complex modeling.
- A ladder of baselines exists: constant / rule-based / linear / complex model.
- Model choice follows data volume, latency, interpretability, cost, and failure
  cost constraints.
- Metric hierarchy connects model metrics to product and business metrics.
- Offline metrics match the decision being optimized and include segment-level
  analysis.
- Validation avoids temporal leakage and user/item contamination.
- Nested cross-validation used for hyperparameter tuning when appropriate.
- Adversarial validation checks whether train and test distributions differ.
- Calibration, uncertainty, thresholds, and abstention behavior are considered
  where decisions have meaningful cost.
- Error analysis is systematic: top-N best/worst cases, residual patterns, and
  segment-level errors.
- Bias-variance diagnosis done and model complexity matched to data size.
- Online evaluation includes A/B tests, ramp plans, guardrails, and rollback.
- Failure analysis names false positive and false negative consequences.
- Evaluation artifacts are reproducible enough to support promotion decisions.

## Metric Examples

- Ranking: NDCG, MAP, MRR, recall@k, precision@k, diversity, coverage.
- Classification: precision, recall, F1, AUROC, AUPRC, calibration, expected
  cost at threshold.
- Forecasting: MAE, RMSE, MAPE/sMAPE, pinball loss, bias, coverage.
- Generation: task success, groundedness, toxicity/safety, latency, cost,
  human preference, regression suite pass rate.
