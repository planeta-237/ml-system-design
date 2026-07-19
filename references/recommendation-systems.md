# Recommendation Systems

Use this file when the system is a recommender, search/ranking system, feed,
or any product that selects and orders items for users.

## Core Pipeline

```
Candidate Generation / Retrieval → Feature Hydration → Ranking → Post-Processing / Blending
```

- **Candidate generation / retrieval:** combine one or more sources—rules, graph
  edges, popularity, lexical retrieval, or embedding models—to reduce a large
  corpus to a recall-oriented candidate set. At scale this may use a two-tower
  model with ANN (HNSW, IVF, etc.).
- **Feature hydration:** fetch bounded, serving-time user, item, and context
  features needed by ranking without large request-path joins.
- **Ranking:** heavier model(s) that predict per-item engagement or utility and
  produce a final ordered list.
- **Post-processing:** diversity, freshness, deduplication, business rules,
  author limits, out-of-network reweighting.
- **Blending:** mixing organic content with ads, sponsored content, or other
  feeds.

## Checklist

- [ ] Retrieval and ranking are treated as separate concerns with different
  latency, freshness, and model requirements.
- [ ] Retrieval supports the scale (ANN / brute-force / exact match) and is
  measured with recall@K, not just latency.
- [ ] Ranking objective aligns with the product goal: one primary score or a
  weighted combination of actions with clear business justification.
- [ ] Counter-metrics are tracked alongside the primary objective (e.g.,
  coverage, diversity, bounce rate, dwell time).
- [ ] User and item features are available at serving time; no offline-only
  features leak into ranking.
- [ ] Hydration strategy is efficient: embeddings, MinHash sketches, bloom
  filters, counters, or precomputed signals instead of raw large joins.
- [ ] Cold-start and new-user paths are explicit (default topics, popular,
  onboarding signals, separate model cluster).
- [ ] Diversity and freshness mechanisms are not afterthoughts (DPP, author
  decay, recency boost, impression filtering).
- [ ] Impression and engagement history are used to avoid repetition and
  enable learning-to-rank updates.
- [ ] Ads / sponsored content are blended with brand safety and suitability
  rules, not just ranked by engagement.
- [ ] Safety and policy layers (spam, harmful content, blocklists) sit before
  or alongside ranking, with fail-closed defaults.
- [ ] A/B routing, experiment flags, and fallback clusters are built into the
  scorer and retrieval clients.
- [ ] Latency budget (P50/P95/P99) and throughput targets are defined for each
  stage (retrieval, ranking, hydration, blending).

## Common Findings

- Retrieval quality is assumed good because ranking is strong; recall is not
  measured.
- Single model tries to do both candidate retrieval and final ranking.
- Ranking optimizes a proxy click metric that hurts long-term engagement or
  advertiser value.
- No diversity or freshness controls, causing filter bubbles and stale feeds.
- Ads are blended without brand safety or suitability checks.
- Cold-start users receive the same feed as everyone else.
- A/B experiments are not isolated at retrieval and ranking stages.
- Feature hydration is implemented with heavy joins that do not scale.

## Key Trade-offs

- **Recall vs latency:** better ANN parameters improve recall but increase
  serving cost.
- **Engagement vs satisfaction:** short-term clicks may reduce long-term
  retention.
- **Organic vs paid:** ads can fund the product but must respect user trust
  and advertiser constraints.
- **Model complexity vs debuggability:** hand-tuned weighted sums are easier to
  reason about and audit than end-to-end learned rankers.

## Relevant Skill References

- `metrics-and-loss.md` for metric hierarchies and counter-metrics.
- `serving-and-architecture.md` for latency budgets, caching, and scaling.
- `ab-testing.md` for experiment design and isolation.
- `mlops-and-monitoring.md` for production monitoring and alerting.
