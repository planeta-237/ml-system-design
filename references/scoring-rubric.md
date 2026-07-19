# Scoring Rubric

Use this rubric only when the user asks for a score or when a review explicitly
requires calibrated scoring. The score is a decision-making tool: how safe,
understandable, evolvable, and operationally sound the ML system design is for
its stated goal.

## Scoring Method

1. Confirm the system type and evidence mode.
2. List evidence-backed findings by severity.
3. Assign each dimension independently.
4. Avoid double-counting one root cause across multiple dimensions.
5. Adjust for missing context: **Unknown is not the same as failed.**
6. Compare the final score with the anchors before publishing it.

If the artifact is a small prototype, notebook, or internal script, state
whether the score is **ML system design fitness** rather than overall
engineering quality. A low fitness score can coexist with an acceptable
contextual design when risk, change rate, and domain complexity are low.

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
- **7.5**: Recognizable ML system design, but use cases are getting fat,
  boundary DTOs are inconsistent, or monitoring is mostly dashboards without
  actionable alerts.
- **6.5**: Mixed design; some business rules are isolated, but framework types
  or persistence details leak into application code, and evaluation is weak.
- **5.0**: Maintainable only with care; major services mix orchestration,
  persistence, and external calls; no clear monitoring or experiment plan.
- **4.0-5.0**: common range for small prototypes or low-risk internal tools that
  are understandable but not shaped like a production ML system. Explain the style
  mismatch instead of treating every missing layer as urgent redesign.
- **3.0**: typical teaching example of bad design: no baseline, data leakage,
  HTTP response logic in business code, no monitoring, hard to reproduce.
- **1.0**: barely separable or unsafe: no meaningful boundaries plus severe
  data, security, or operational risks.

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

## Style-Mismatch Severity

Use lower severity when a finding is mainly "not a full ML system design":

- Missing monitoring in a tiny prototype is often **P2** unless it handles
  sensitive data or high-value decisions.
- A single Jupyter notebook without serving is **P1/P2** for exploration, but
  **P0** if it is intended to power a product without a serving plan.
- Active Record or simple persistence is acceptable for low-risk CRUD but
  becomes **P1** when it mixes business rules or external side effects.
- Escalate to **P1/P0** when the mismatch creates concrete risk: PII leakage,
  financial/safety impact, high change frequency, or irreversible side effects.

Score evidence, not confidence. Missing stage-critical evidence should cap the
score even when the proposal sounds plausible.
