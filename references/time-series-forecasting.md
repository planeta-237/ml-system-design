# Time Series Forecasting

Use this file when the system predicts future values of a time-dependent
signal: demand, traffic, stock, resource consumption, or any sequential metric.

## Problem Framing

- Define the forecast horizon and granularity (e.g., next 7 days at hourly
  level) and how far in advance decisions must be made.
- Identify whether the output is a point forecast, a prediction interval, or a
  full probability distribution.
- State whether the system needs hierarchical reconciliation (e.g., store →
  region → country) or multiple related series.
- Clarify what action the forecast drives; a number without a decision is not
  a product.

## Checklist

- [ ] Data is checked for seasonality, trend, cycles, holidays, and structural
  breaks before choosing a model family.
- [ ] Missing values, outliers, and zero/negative constraints are handled with
  domain-aware rules, not just imputation.
- [ ] Baseline models (ARIMA, ETS, Prophet, naive/seasonal naive) are run before
  ML/DL approaches.
- [ ] Feature engineering includes lag features, rolling statistics, calendar
  features, and external regressors when available.
- [ ] Train/validation/test splits respect time order; no future information leaks.
- [ ] Evaluation metric matches the business loss (MAPE, WAPE, RMSE, MASE,
  pinball loss, coverage, or custom cost of under/over-forecasting).
- [ ] Forecast intervals or probabilistic outputs are produced when planning
  under uncertainty.
- [ ] Hierarchical forecasts are reconciled (bottom-up, top-down, or optimal
  reconciliation) when needed.
- [ ] Cold-start and sparse series have a fallback (similar-series pooling,
  classification by pattern, or rule-based baseline).
- [ ] Retraining policy is defined (schedule, trigger, or continuous update) and
  monitored for drift in residuals or coverage.
- [ ] Downstream systems can consume a forecast format that includes horizon,
  granularity, and uncertainty.
- [ ] Monitoring tracks forecast accuracy, bias, and whether actuals fall outside
  prediction intervals more often than expected.

## Common Findings

- No baseline comparison; complex model is chosen without evidence.
- Future information leaks through features or rolling windows that include the
  target period.
- Evaluation uses standard RMSE even when over-forecasting is much more
  expensive than under-forecasting.
- Model is not updated after a regime change or demand shock.
- Point forecasts are used for safety-stock planning without intervals.
- Hierarchical forecasts sum incorrectly across levels.

## Key Trade-offs

- **Bias vs variance:** simple models generalize better for short horizons or
  sparse data.
- **Latency vs accuracy:** heavy DL models may not be worth the gain over
  Prophet for hourly re-forecasting.
- **AutoML vs interpretability:** automated forecasting is fast but harder to
  debug when a business asks why the number changed.
- **Point vs probabilistic:** intervals add value but require more evaluation
  discipline and calibration.

## Relevant Skill References

- `metrics-and-loss.md` for selecting and calibrating forecast metrics.
- `data-and-features.md` for feature engineering, leakage, and freshness.
- `modeling-and-evaluation.md` for validation strategy and baseline selection.
- `mlops-and-monitoring.md` for drift, retraining, and alerting.
