# LLM, RAG, And Agents

Use this file when the system uses LLMs, embeddings, RAG, fine-tuning, tool use,
memory, agents, autonomous actions, or generated content.

## Checklist

- The design states whether the LLM is the product, an interface, a reasoning
  component, a retrieval synthesizer, or an automation controller.
- RAG systems define corpus ownership, chunking, indexing, retrieval metrics,
  freshness, access control, citation behavior, and stale document handling.
- Planning approach chosen: explicit plan vs end-to-end model reasoning.
- Multi-agent systems use a coordinator + collaborators + supervisor pattern.
- Guardrails are layered: input validation → LLM call → output validation →
  tool result validation.
- Tool permissions, idempotency, approval gates, audit logs, sandboxing, rate
  limits, and rollback for side effects are defined.
- Tool API is minimized: only the data needed for the current step is exposed.
- Memory systems define scope, retention, deletion, consent, poisoning risks,
  and user-visible controls.
- Context management handles context window limits, resets, compression, and
  context rot.
- Evaluation includes task success, groundedness, refusal/safety behavior,
  regression sets, jailbreak/adversarial tests, latency, and cost.
- LLM-as-judge is calibrated against human experts (e.g., Cohen's kappa ≥ 0.6).
- Fine-tuning has a data quality and evaluation argument that beats prompting,
  retrieval, or smaller targeted models.
- PII scrubbing and backend data filtering are in place before data reaches the
  LLM.

For runtime patterns, testing, and anti-patterns see `llm-agents-patterns.md`.

## Common Findings

- No eval harness exists, so prompt changes cannot be promoted safely.
- Retrieval quality is assumed from anecdotal examples instead of measured.
- Agent tools can perform irreversible actions without approval or audit.
- The system confuses model confidence with grounded evidence.
