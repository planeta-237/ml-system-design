# Production Readiness

Use this file before launch or when reviewing whether an ML system is ready
for production traffic.

## Health, observability, and CI/CD

- [ ] **Real readiness probe** checks critical dependencies: database, queue,
  model provider, feature stores, upstream APIs. It returns non-200 when a
  dependency is unavailable.
- [ ] **Liveness probe** distinguishes "stuck" from "healthy but slow".
- [ ] **CI/CD** runs tests, lint, type checks, and security scans on every merge.
- [ ] **Model/prompt promotion** is gated by automated evaluation, not only manual
  approval.
- [ ] **Centralized logging and metrics** are wired to alerting and on-call rotation.
- [ ] **Every alert maps to an owner and a runbook**; not every dashboard anomaly
  pages.

## Security and data handling

- [ ] **No production test hooks**: no magic strings, debug endpoints, or
  `!!!TESTONLY` paths reachable in production.
- [ ] **Authentication/authorization enforced** and not mocked by default.
- [ ] **PII and sensitive data** are not logged in plain text.
- [ ] **Inputs sent to external LLM/model providers** are scrubbed or tokenized.
- [ ] **Dangerous code patterns** (`eval()`, `exec()`, pickle loading on
  user-influenced data) are avoided.
- [ ] **API inputs have size limits and rate limits** to prevent abuse and cost spikes.

## Serving and resilience

- [ ] **Latency budget and SLOs** (P50/P95/P99) are defined and documented.
- [ ] **Timeouts, retries, and circuit breakers** are configured for external
  dependencies.
- [ ] **Fallback or graceful degradation** exists when the model/provider is unavailable.
- [ ] **Model loading is not a single blocking step at startup**; lazy loading or
  warm pools are used.
- [ ] **Feature toggles** allow disabling the model or switching to a fallback.

## Release and rollback

- [ ] **Rollback plan** exists and is tested (model version, prompt version, feature
  toggle, database migration).
- [ ] **Canary or shadow deployment** supports new model/prompt versions.
- [ ] **Business rules** (thresholds, multipliers, allowlists) are configurable without
  a code deploy.
- [ ] **Post-release monitoring** is planned for the first hours/days after rollout.

## Common findings

- Health endpoint returns `OK` without actually checking the database or queue.
- CI/CD quality gates are commented out or missing.
- Full request payloads, including PII, are logged.
- `MOCK_AUTH` or similar test flags are enabled by default.
- `eval()` or pickle loading is used on user-influenced data.
- Models are loaded synchronously at startup, blocking readiness.
- No rate limiting or input size limits on public endpoints.
- Business rules are hardcoded as magic numbers.
