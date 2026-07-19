# Common Anti-Patterns

Use this file as a quick risk checklist for designs and reviews.

## Traditional ML

| Anti-pattern | Why it fails | Better approach |
|---|---|---|
| **No baseline** | Cannot tell if complexity is worth it | Start with constant / rule-based / linear baseline |
| **Proxy metric drift** | Offline metric rises while business value falls | Tie every metric to business outcome and guardrails |
| **Offline-only evaluation** | Model looks great until A/B shows no effect | Validate offline-online correlation before A/B gate |
| **Training-serving skew** | Same features computed differently at serving | Enforce identical paths, units, formats, and code |
| **Feature bloat** | More features, no measured gain, more fragility | Add features only after proving value and stability |
| **No data validation** | Bad upstream data silently degrades predictions | Data validation pipeline with alerts and contracts |
| **Over-infrastructure for small data** | Heavy pipelines for 1K-row datasets | Match tooling to data size and growth |
| **Uncalibrated confidence** | High confidence treated as high correctness | Calibrate, threshold, or abstain when cost matters |
| **No fallback** | Model failure becomes system failure | Fallback, rule-based backup, or graceful degradation |
| **Model quality = system quality** | Good model fails due to serving, UX, monitoring | Treat data, serving, monitoring as first-class components |
| **Ignoring feedback loops** | Model trains on its own previous decisions | Add policy logging, exploration, and causal-aware validation |
| **Metric gaming** | Model finds a shortcut to satisfy the metric | Add constraints and adversarial checks |

## LLM / Agent systems

| Anti-pattern | Why it fails | Better approach |
|---|---|---|
| **Heavy frameworks hiding tokens** | Loss of control over context and cost | Lightweight custom runtime |
| **Universal LLM API** | Injection risk, noise, leaked data | Minimal API per step; no sensitive fields in tool params |
| **>5 tools on one agent** | Wrong tool calls and confusion | Decompose into sub-agents or use explicit plan |
| **Provider prompt cache as main cache** | Routing makes cache unreliable | Client-side semantic cache (e.g., Redis + embeddings) |
| **Single quality metric** | Hides cost, latency, safety issues | Multi-dimensional scorecard |
| **Fine-tuning agent behavior** | Usually worse than prompt + harness | Prompt engineering + YAML stories + eval harness |
| **State machine for everything** | Exponential complexity | LLM as logic core, state machine only where formalizable |
| **No eval harness** | Prompt changes cannot be promoted safely | Regression tests, LLM-as-judge, golden stories |
| **Retrieval assumed from anecdotes** | Quality varies across queries | Measure retrieval metrics (recall, MRR, NDCG) |
| **Irreversible tool actions without approval** | Safety and audit risk | Approval gates, idempotent tools, audit logs |
| **No PII scrubbing** | Sensitive data sent to external LLM | Scrub PII, map tokens back at runtime |
| **Over-reliance on end-to-end reasoning** | Model loses thread in complex flows | Explicit plan + structured handoff between steps |

## How to use this file

- During review: map findings to these anti-patterns and cite concrete evidence.
- During design: explicitly state which anti-patterns you are avoiding and how.
