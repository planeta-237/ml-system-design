# Modeling And Evaluation

Use this file when reviewing or designing baselines, model families, metrics,
offline validation, online experiments, or failure analysis.

## Checklist

- A simple baseline is defined before complex modeling.
- Model choice follows data volume, latency, interpretability, cost, and failure
  cost constraints.
- Offline metrics match the decision being optimized and include segment-level
  analysis.
- Validation avoids temporal leakage and user/item contamination.
- Calibration, uncertainty, thresholds, and abstention behavior are considered
  where decisions have meaningful cost.
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
