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
- **LLM inference**: consider cost, latency, and throughput trade-offs; KV
  cache management, continuous batching, and model routing are often critical.

## Backend System Design Patterns

- **Load balancing:** distribute traffic across instances (round robin, least
  connections, IP hash, weighted, consistent hashing). Always pair with health
  checks.
- **Horizontal scaling:** add stateless instances behind a load balancer. Keep
  data in external storage so instances can be replaced.
- **Caching:** use Redis/Memcached/CDN for hot reads; define TTL, cache
  invalidation, and fallback-on-miss behavior. Avoid caching decisions that
  depend on fresh safety checks.
- **CDN:** serve static content closer to users; reduces origin load and
  latency.
- **Message queues:** decouple producers and consumers, absorb traffic spikes,
  and enable async processing (uploads, thumbnails, notifications). Kafka,
  RabbitMQ, SQS, etc.
- **API gateway:** single entry point for routing, auth/z, rate limiting, and
  response aggregation. Internal services live in a private network.
- **Microservices:** split by domain when teams and ownership boundaries grow;
  not a default for small systems.
- **Database scaling:** read replicas for read-heavy loads, sharding for data
  size, partitioning for time-series or tenant isolation.
- **Rate limiting:** protect services and upstream APIs with fixed window,
  sliding window, token bucket, or leaky bucket algorithms.
- **AuthN/AuthZ:** authentication proves identity; authorization proves rights.
  Tokens (JWT) carry claims; RBAC/ABAC/ACL define policies.

## LLM Inference Optimization

- [ ] Cost/latency/throughput trade-offs quantified for the expected load.
- [ ] KV cache is managed to avoid memory waste and long-tail latency.
- [ ] Batching strategy chosen: static, dynamic, or continuous batching.
- [ ] Model optimization considered: quantization, pruning, distillation, or
  speculative decoding.
- [ ] Serving framework matched to requirements: vLLM, TensorRT-LLM, TGI,
  Triton, or custom runtime.
- [ ] Model routing selects the smallest adequate model for each request class.

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
