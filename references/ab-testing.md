# A/B Testing and Experimentation

Use this file when designing or reviewing A/B tests, online experiments, or causal inference alternatives for ML systems.

## Hypothesis and design

- [ ] Hypothesis stated: "if we do X, metric M will change by Y% based on offline estimate / prior experiment".
- [ ] MDE (minimum detectable effect) defined and smaller than the expected effect.
- [ ] Sample size calculated using real historical data and variance.
- [ ] Type I (α) and Type II (β) errors and statistical power defined.
- [ ] Randomization unit chosen from the product mechanics: user, account, session,
  item, device, geo, cluster, or time block. Interference, identity stability,
  carryover, and contamination are addressed.
- [ ] Concurrent control and treatment are preferred. Use switchback or
  cluster/time randomization only when unit-level randomization is invalid or
  impractical; define washout and account for temporal correlation.
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
- [ ] Peeking avoided; if decisions are made while data accumulates, the test and
  stopping boundaries come from a pre-specified sequential design.
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
| Metric lags by days/weeks | Extend exposure and attribution windows; use a validated leading proxy only for earlier decisions |
| Shared marketplace, fleet, or geo has strong interference | Cluster or switchback design with washout and carryover analysis |
| Only one geo/tenant; no concurrent control | Interrupted time series if the pre-period is stable; synthetic control only with credible donor units |
| External shock affects everyone at once | Difference-in-differences with a control group |
| Policy change at a known threshold | Regression discontinuity |
| Want to measure long-term policy impact | Prefer a long-running randomized holdout; otherwise use a justified longitudinal causal design |
| Multiple overlapping experiments | Factorial design with pre-allocated buckets |
| Treatment may harm users if bad | Pre-specify safety guardrails, stopping rules, and rollback |
| Decisions must be made while data accumulates | Pre-register a suitable sequential design and stopping rule |
| Low-traffic metric | Increase duration, reduce variance, aggregate carefully, or use a validated higher-frequency proxy |
