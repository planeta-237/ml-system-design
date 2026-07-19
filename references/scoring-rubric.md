# Scoring Rubric

Use this rubric only when the user asks for a score or when a review explicitly
requires calibrated scoring. The score is a decision-making tool: how safe,
understandable, evolvable, and operationally sound the ML system design is for
its stated goal.

## Contents

- Scoring method and severity levels
- Weighted dimensions and grade anchors
- Calibration examples
- Dimension guidance
- Lifecycle and scope calibration

## Scoring Method

1. Confirm the system type and evidence mode.
2. List evidence-backed findings by severity.
3. Assign each dimension independently.
4. Avoid double-counting one root cause across multiple dimensions.
5. Mark unsupported dimensions or criteria as **Unknown**; do not convert missing
   evidence to either zero or full credit.
6. Report evidence coverage. If the user requires a total despite material
   unknowns, label it provisional and state the assumptions or plausible range.
7. Compare the final score with the anchors before publishing it.

If the artifact is a small prototype, notebook, or internal script, state
whether the score is **ML system design fitness** rather than overall
engineering quality. A low fitness score can coexist with an acceptable
contextual design when risk, change rate, and domain complexity are low.

## Severity Levels

Use these labels to rank findings in reviews:

- **P0 — Blocker:** safety, legal, financial, or severe operational risk. The
  system should not launch or scale without fixing this. Examples: PII leakage,
  fake readiness probe, disabled auth, `eval()` on user input, irreversible
  actions without audit.
- **P1 — Important:** materially weakens the design or significantly increases
  risk. Should be fixed before production scale or before the next major rollout.
  Examples: missing monitoring, no fallback, no input limits, uncalibrated
  LLM-as-judge, manual model promotion without guardrails.
- **P2 — Improvement:** nice-to-have, polish, or lower-risk follow-up. Does not
  block launch but should be tracked. Examples: stale docs, extra test coverage,
  additional dashboards, code cleanup.

## Weighted Dimensions

| Dimension | Max | Full Credit | Major Deductions |
|-----------|-----|-------------|------------------|
| Product and Requirements Fit | 1.5 | Clear objective, users, decision, anti-goals, constraints, price of error, and measurable success metrics. | Vague goal; no anti-goals; missing constraints; metrics not tied to business value; problem not validated. |
| Data and Feature Design | 2.0 | Sources, labels, leakage, quality, freshness, privacy, governance, and training-serving consistency are addressed. | Labels undefined or unavailable; data leakage; no freshness plan; no PII/retention policy; offline-only features. |
| Modeling and Evaluation | 2.0 | Baselines, model choice, metric hierarchy, validation, error analysis, and online experiment plan are sound. | No baseline; wrong validation scheme; metrics not predictive of business; no failure analysis or online eval. |
| System Architecture | 1.5 | Clear batch/stream/online shape, API contracts, latency budget, scalability, fallbacks, rollback, and graceful degradation. | Missing serving plan; no latency budget or fallbacks; no rollback/canary; hidden monolith; no input limits. |
| MLOps and Monitoring | 1.5 | Reproducible pipelines, model registry, CI/CD, monitoring, drift detection, alerts, retraining, and incident response. | No versioning; no registry; no tests in CI; no drift or quality monitoring; missing runbooks. |
| Risk and Responsible AI | 1.0 | Safety, fairness, explainability, abuse, compliance, and human oversight handled for the domain risk. | Unaddressed safety/compliance; no fairness analysis; irreversible side effects without approval; no audit. |
| Communication and Trade-offs | 0.5 | Clear narrative, phased roadmap, explicit trade-offs, and decision rationale. | Trade-offs hidden; no roadmap; no rationale for key decisions; document is persuasive rather than evidence-based. |

## Grade Anchors

| Score | Grade | Meaning |
|-------|-------|---------|
| 9.3-10.0 | A+ | Reference-quality production design. Only small polish remains. |
| 8.5-9.2 | A | Strong, production-ready design with minor issues. |
| 7.5-8.4 | B | Good design with notable but manageable gaps. |
| 6.0-7.4 | C | Acceptable design, but important changes should be requested before launch. |
| 4.5-5.9 | D | Significant rework needed; risks are structural. |
| 0.0-4.4 | F | Fundamental design failure or unsafe coupling. |

## Calibration Examples

- **9.5**: Clear product goal, strong evidence, clean data/feature design,
  reproducible evaluation, production serving, monitoring, incident response, and
  explicit trade-offs.
- **8.5**: Sound architecture and evaluation; a few pragmatic shortcuts exist
  (e.g., manual retraining, partial canary, missing segment metrics).
- **7.5**: Coherent data, modeling, and serving plan, but one important area such
  as online evaluation, fallback behavior, or actionable monitoring is thin.
- **6.5**: Viable design with material gaps in labels, validation, rollout, or
  operations; production use needs targeted rework.
- **5.0**: The ML task is understandable, but evidence is weak and multiple
  production-critical areas such as data quality, evaluation, serving, and
  monitoring are undefined.
- **3.0**: typical teaching example of bad design: no baseline, data leakage,
  an invalid validation scheme, no rollback or monitoring, and poor
  reproducibility.
- **1.0**: The task or labels are incoherent and severe data, safety, security, or
  operational risks remain unaddressed.

## Dimension Guidance

### Product and Requirements Fit (0-1.5)

- **1.5**: Clear, measurable goals; anti-goals and constraints documented;
  price of error explicit; stakeholders and success criteria identified.
- **1.0**: Goals are clear but constraints or anti-goals are thin; some hidden
  stakeholder goals missed.
- **0.5**: Vague goal; metrics are proxies without business linkage; no
  anti-goals.
- **0.0**: No clear problem statement; design is a solution looking for a
  problem.

### Data and Feature Design (0-2.0)

- **2.0**: Labels aligned with product; leakage checked; freshness mapped to
  features; quality checks; PII/governance addressed; training-serving
  consistency verified.
- **1.5**: Mostly solid; one or two gaps in leakage, freshness, or governance.
- **1.0**: Important gaps: missing labels, no skew check, or weak privacy
  controls.
- **0.5**: Data treated as an afterthought; no provenance or validation.
- **0.0**: No data source or label strategy; high risk of leakage or misuse.

### Modeling and Evaluation (0-2.0)

- **2.0**: Baseline first; model choice justified; metric hierarchy connects
  to business; validation avoids leakage; error analysis and online experiment
  plan exist.
- **1.5**: Good offline evaluation; missing online plan or segment analysis.
- **1.0**: No baseline or validation has leakage; metrics do not predict
  business outcomes.
- **0.5**: Evaluation is ad hoc; no reproducibility.
- **0.0**: No evaluation plan or wrong task framing.

### System Architecture (0-1.5)

- **1.5**: Clear online/batch/stream shape; API contracts; latency budget;
  fallbacks; rollback; input limits; graceful degradation.
- **1.0**: Architecture exists but lacks fallbacks, latency budget, or rollback.
- **0.5**: Major gaps: no serving plan, no input limits, or model service is a
  hidden monolith.
- **0.0**: No coherent architecture or unsafe by default.

### MLOps and Monitoring (0-1.5)

- **1.5**: Versioned artifacts, reproducible pipelines, registry, CI/CD, drift
  and quality monitoring, alerts with runbooks, retraining policy.
- **1.0**: Some pipelines/versioning but monitoring or CI/CD is weak.
- **0.5**: Manual training, no registry, no monitoring beyond uptime.
- **0.0**: No reproducibility or operational visibility.

### Risk and Responsible AI (0-1.0)

- **1.0**: Risks proportional to domain: safety, fairness, explainability,
  compliance, human oversight, and audit where needed.
- **0.7**: Minor gaps or undocumented assumptions.
- **0.3**: Important operational or compliance risks present.
- **0.0**: Severe leakage, abuse, or safety risks unaddressed.

### Communication and Trade-offs (0-0.5)

- **0.5**: Clear narrative, phased roadmap, explicit trade-offs, and rationale.
- **0.3**: Clear but lacks roadmap or trade-off analysis.
- **0.1**: Some structure but mostly assertions.
- **0.0**: Unreviewable or purely promotional document.

## Lifecycle and Scope Calibration

Judge requirements against the artifact's lifecycle stage and declared scope:

- Missing production monitoring in an offline feasibility prototype is often
  **P2** or not applicable; missing evaluation data can still be **P1**.
- A notebook without serving is acceptable for exploration. It becomes **P0/P1**
  only when it is used for consequential production decisions without a safe
  execution, review, or rollback path.
- Do not penalize a batch system for lacking online serving, or a human-reviewed
  decision-support tool for lacking full automation.
- For an early design doc, score whether stage-critical decisions and validation
  plans are explicit; mark implementation evidence as Unknown.
- Escalate to **P1/P0** when the mismatch creates concrete risk: PII leakage,
  financial/safety impact, high change frequency, or irreversible side effects.

Score evidence, not confidence. Do not claim a production-ready grade when
stage-critical evidence is missing; report a provisional result, evidence gaps,
and what would resolve them.
