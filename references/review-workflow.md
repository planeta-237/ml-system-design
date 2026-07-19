# Review Workflow

Use this file when reviewing an existing ML system design, repository, product
document, architecture diagram, metrics dashboard, or incident write-up.

## Scope Note

This skill focuses on **ML system design review**: architecture, data, modeling,
evaluation, serving, MLOps, and responsible AI. It is not a substitute for
ordinary code review. Flag code-level issues only when they create system-level
risks (e.g., PII in logs, test hooks in production, `eval()` in request paths).

## Quick Recon

Before the deep review, spend a few minutes reading the project artifacts in this
order:

1. `README.md`, `CLAUDE.md`, `INDEX.md` — what the system is and who it is for.
2. Project config (`pyproject.toml`, `package.json`, `go.mod`, etc.) — stack and
   dependencies.
3. CI/CD config (`.gitlab-ci.yml`, `.github/workflows`, `Makefile`) — quality
   gates and deployment process.
4. Settings / config files — environment variables, feature flags, model names.
5. Entry points and API routes — main request paths.
6. Tests — what behavior is already validated and what is mocked.
7. Docs — architecture, eval methodology, monitoring plan.

Use this recon to decide which reference files to load next.

## Evidence Handling

- Review only the artifacts available in the workspace or supplied by the user.
- Mark claims as Unknown when evidence is missing.
- Treat contradictions between docs, code, metrics, and telemetry as findings.
- Do not penalize a design for lacking an implementation when the requested
  artifact is only a design doc; instead mark reproducibility as unverified.

## Review Passes

1. Product fit: problem, users, decision, value, anti-goals, constraints,
   price of error, and success metrics.
2. Data fit: availability, quality, representativeness, labels, leakage, skew,
   training-serving consistency, governance, privacy, and retention.
3. Model fit: baseline, model choice, metrics, metric hierarchy, calibration,
   error analysis, evaluation design, and failure modes.
4. System fit: batch/stream/online architecture, storage, serving, latency
   budget, API contracts, scalability, fallbacks, graceful degradation,
   rollback, feature toggles, and cost.
5. Operations fit: CI/CD, model registry, monitoring, retraining, incident
   response, ownership, and documentation.
6. Experimentation fit: A/B or causal design, MDE, power, peeking, segment
   analysis, and guardrails.
7. Responsible AI fit: safety, fairness, explainability, abuse, compliance, and
   human review where needed.
8. For agentic systems: planning, tool use, guardrails, context management,
   non-determinism, testing with stories, and multi-agent coordination.

## Finding Style

Lead with risks that can cause product failure, unsafe behavior, unreliable
operation, or misleading evaluation. Keep cosmetic architecture preferences out
of the top findings unless they create real delivery risk.
