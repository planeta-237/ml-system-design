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

See `references/llm-agents-patterns.md` for the full LLM/agent runtime patterns,
guardrails, testing, and anti-patterns checklist. The most common risks are:

- Heavy frameworks hiding token-level reality.
- Universal LLM API exposing too much data.
- Too many tools on one agent.
- Relying on provider prompt cache as the primary cache.
- Single quality metric hiding cost, latency, or safety issues.
- Fine-tuning agent behavior before trying prompt engineering + harness.
- State machine for everything.
- No eval harness for prompt changes.
- Retrieval quality assumed from anecdotes instead of measured.
- Irreversible tool actions without approval or audit.
- No PII scrubbing before external LLM calls.
- Over-reliance on end-to-end reasoning instead of explicit plans.

## How to use this file

- During review: map findings to these anti-patterns and cite concrete evidence.
- During design: explicitly state which anti-patterns you are avoiding and how.
