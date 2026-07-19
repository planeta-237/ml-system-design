# A/B Testing and Experimentation

Use this file when designing or reviewing A/B tests, online experiments, or causal inference alternatives for ML systems.

## Hypothesis and design

- [ ] Hypothesis stated: "if we do X, metric M will change by Y% based on offline estimate / prior experiment".
- [ ] MDE (minimum detectable effect) defined and smaller than the expected effect.
- [ ] Sample size calculated using real historical data and variance.
- [ ] Type I (α) and Type II (β) errors and statistical power defined.
- [ ] Splitting strategy chosen: user / session / geo / switchback; control and test run simultaneously.
- [ ] A/A tests run to validate the experiment platform.
- [ ] Simulation done: p-value distribution under H0 is uniform, power checked on synthetic effect.

## Metrics and guardrails

- [ ] Primary, secondary, and guardrail metrics separated.
- [ ] Guardrails watch for early harm (churn, activity, fairness).
- [ ] Appropriate statistical test chosen (t-test, Welch, bootstrap, etc.).
- [ ] Experiment design pre-registered and not changed mid-flight.
- [ ] Multiple comparisons effect controlled (α correction or clear hierarchy).
- [ ] Absolute vs relative uplift distinguished and significance threshold explicit.

## Duration and interpretation

- [ ] Lagging metric window fits the experiment duration.
- [ ] Peeking avoided; sequential testing used if needed (MSPRT).
- [ ] Result reported with point estimate, confidence interval, and scenario analysis.
- [ ] Segment analysis done: effect is not assumed uniform across users.
- [ ] Reverse A/B or rollout-pause-rollout check considered after a positive result.
- [ ] Post-experiment report documents conclusions, problems, guardrails, and next steps.

## When A/B is not possible

- [ ] Causal inference alternatives considered: Causal Impact, Difference-in-Differences, Synthetic Control, Interrupted Time Series, Regression Discontinuity.
- [ ] Factorial design used when users are randomized into multiple overlapping experiments.
- [ ] Offline evaluation (replay, contextual bandits) used to estimate policy impact when online testing is risky.

## Decision tables

| Situation | Recommended design |
|---|---|
| Users can be randomized and metric is fast | Standard user-level A/B |
| Metric lags by days/weeks | Switchback or time-based cluster randomization |
| Only one geo/tenant; no concurrent control | Synthetic control or interrupted time series |
| External shock affects everyone at once | Difference-in-differences with a control group |
| Policy change at a known threshold | Regression discontinuity |
| Want to measure long-term policy impact | Causal Impact or cohort-based DID |
| Multiple overlapping experiments | Factorial design with pre-allocated buckets |
| Treatment may harm users if bad | Add strong guardrails + early stopping |
| Team cannot resist peeking | Pre-register sequential testing (MSPRT) |
| Low-traffic metric | Increase duration, use proxy metric, or bootstrap |

