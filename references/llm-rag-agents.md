# LLM, RAG, And Agents

Use this file when the system uses LLMs, embeddings, RAG, fine-tuning, tool use,
memory, agents, autonomous actions, or generated content.

## Checklist

- The design states whether the LLM is the product, an interface, a reasoning
  component, a retrieval synthesizer, or an automation controller.
- RAG systems define corpus ownership, chunking, indexing, retrieval metrics,
  freshness, access control, citation behavior, and stale document handling.
- Evaluation includes task success, groundedness, refusal/safety behavior,
  regression sets, jailbreak/adversarial tests, latency, and cost.
- Tool-using agents define permissions, idempotency, approval gates, audit logs,
  sandboxing, rate limits, and rollback for side effects.
- Memory systems define scope, retention, deletion, consent, poisoning risks,
  and user-visible controls.
- Fine-tuning has a data quality and evaluation argument that beats prompting,
  retrieval, or smaller targeted models.

## Common Findings

- No eval harness exists, so prompt changes cannot be promoted safely.
- Retrieval quality is assumed from anecdotal examples instead of measured.
- Agent tools can perform irreversible actions without approval or audit.
- The system confuses model confidence with grounded evidence.
