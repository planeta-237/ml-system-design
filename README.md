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
  - Recommendation systems and time-series forecasting
  - Scoring rubric and output templates

## Release Archive

The source folder is the primary artifact. A `.skill` archive can be created for distribution:

```bash
zip -r -FS ml-system-design.skill ml-system-design -x '*/.DS_Store'
```
