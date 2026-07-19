# ML System Design Skill

A Codex skill for reviewing, designing, and explaining production ML systems and AI product architectures.

Use it for ML system design interviews, architecture reviews, design docs,
recommender/search/ranking/classification/forecasting/generative AI systems,
data and feature pipelines, offline and online evaluation, model serving,
monitoring, MLOps, reliability, privacy, cost, latency, scalability, and
trade-off analysis.

## Modes

- **Design mode** — propose an ML system architecture for a product, feature, or interview prompt.
- **Review mode** — evaluate an existing design doc, codebase, diagram, or architecture proposal.
- **Teaching mode** — explain ML system design concepts, trade-offs, or patterns without forcing a score.

## Install

Copy the skill folder into your Codex skills directory:

```bash
cp -R ml-system-design ~/.codex/skills/
```

Then invoke it with:

```text
Use $ml-system-design to review the ML system architecture for ...
```

## Contents

- `ml-system-design/SKILL.md`: main skill instructions, modes, principles, and routing.
- `ml-system-design/agents/openai.yaml`: UI metadata.
- `ml-system-design/references/`: detailed reference files loaded on demand.
  - Design and review workflows
  - Problem space, metrics, A/B testing, general principles
  - Data, modeling, serving, MLOps, monitoring
  - LLM/RAG/agents, agent patterns, common anti-patterns
  - Recommendation systems, time-series forecasting, AI product lifecycle
  - Scoring rubric and output templates

  Full list of references:

  | File | Use when |
  |------|----------|
  | `ai-product-lifecycle.md` | product discovery, stage-gate, hypothesis-driven design |
  | `ab-testing.md` | A/B or causal experiment design |
  | `common-anti-patterns.md` | quick risk checklist for ML and LLM systems |
  | `data-and-features.md` | data, labels, feature pipelines, leakage, quality |
  | `design-workflow.md` | creating a new ML system design |
  | `general-principles.md` | sanity-check principles |
  | `llm-agents-patterns.md` | LLM/agent runtime patterns, guardrails, testing |
  | `llm-rag-agents.md` | LLM, RAG, fine-tuning, agents, guardrails |
  | `metrics-and-loss.md` | metric hierarchy, offline/online metrics, loss functions |
  | `modeling-and-evaluation.md` | baselines, model choice, validation, evaluation |
  | `mlops-and-monitoring.md` | CI/CD, pipelines, registry, drift, monitoring |
  | `output-templates.md` | formatting design, review, scorecard, teaching outputs |
  | `problem-space.md` | problem framing, anti-goals, success criteria |
  | `production-readiness.md` | pre-launch checks |
  | `recommendation-systems.md` | recommender, search, ranking, feed |
  | `review-workflow.md` | reviewing an existing design or repo |
  | `scoring-rubric.md` | assigning or calibrating a numeric score |
  | `serving-and-architecture.md` | serving, APIs, latency, scaling, storage |
  | `time-series-forecasting.md` | demand forecasting, prediction intervals |

## Release Archive

The source folder is the primary artifact. A `.skill` archive can be created for distribution:

```bash
zip -r -FS ml-system-design.skill ml-system-design -x '*/.DS_Store'
```
