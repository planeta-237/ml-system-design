# Serving And Architecture

Use this file when the task involves system shape, APIs, serving, storage,
latency, scalability, resilience, fallbacks, or rollout strategy.

## Architecture Choices

- **Batch scoring**: use when freshness requirements are relaxed and throughput
  dominates latency.
- **Online inference**: use when predictions depend on request-time context or
  freshness.
- **Streaming features/scoring**: use when event freshness materially changes
  product value.
- **Hybrid**: combine precomputed candidates or features with online reranking
  when latency and freshness both matter.

## Checklist

- Request path, data path, and training path are drawn separately.
- API contracts are stable, versioned, and separate internal from external
  interfaces.
- Online dependencies, timeouts, retries, rate limits, and fallbacks are named.
- Latency budget (P50, P95, P99) and throughput targets defined.
- Feature availability is consistent between training and serving.
- Caching strategy is explicit and does not hide stale or unsafe predictions.
- Rollout supports shadow, canary, A/B, gradual ramp, and rollback where useful.
- Feature toggles exist to disable the model or switch to a fallback quickly.
- Capacity, cost, latency SLOs, and graceful degradation behavior are defined.
- The design avoids making the model service a hidden monolith that owns product
  policy, data contracts, and business workflow.
