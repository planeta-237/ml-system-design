# LLM Agent Patterns

Use this file when designing or reviewing LLM-agent, RAG, or tool-using systems.

## Contents

- Agent anatomy, planning, and multi-agent decisions
- Guardrails and context management
- Non-determinism and trajectory testing
- Metrics, cost, latency, security, and anti-patterns

## Agent anatomy

- [ ] Agent decomposed into: runtime, LLM, context/memory, tools, and reasoning loop.
- [ ] Prompt behavior and runtime behavior have an explicit, versioned contract;
  ownership may be separate or shared depending on team size.
- [ ] Agent is not used if the task can be solved simpler without LLM.
- [ ] LLM treated as a stateless function; context constructed explicitly outside the model.

## Planning and reasoning

- [ ] Planning approach chosen: end-to-end model reasoning vs explicit plan.
- [ ] Explicit plans are considered when tasks have multiple dependent steps,
  costly actions, or auditable business requirements.
- [ ] Reasoning effort and step budgets are measured and bounded according to task
  complexity, latency, cost, and model capability.
- [ ] Re-planning occurs at defined checkpoints or after validated failures;
  completed side effects and invariants remain visible to the planner.

## Multi-agent systems

- [ ] A single agent or deterministic workflow is the baseline; multi-agent design
  is justified by measurable gains in quality, isolation, or latency.
- [ ] Pattern fits the dependency graph: route independent intents, parallelize
  independent work, or use manager/workers for decomposable tasks.
- [ ] Ownership of shared state, conflicts, retries, cancellation, stopping, and
  final synthesis is explicit.
- [ ] Each worker receives the minimum task-local context and returns a bounded,
  typed result instead of inheriting full history by default.
- [ ] Deterministic policy, permissions, and irreversible transitions live in
  code or a state machine; the LLM handles decisions that genuinely require
  semantic judgment.
- [ ] Debate, voting, or evaluator loops are used only when evaluation shows their
  quality gain exceeds additional latency, cost, and correlated-error risk.

## Guardrails

- [ ] Multi-layered guardrails: input validation → LLM call → output validation → tool result validation.
- [ ] External content is treated as untrusted: separate data from instructions,
  enforce permissions outside the model, and test injection/jailbreak defenses.
  Do not assume a classifier can reliably detect every attack.
- [ ] Output validated against schema and tool arguments checked for sanity.
- [ ] Tool API and arguments are minimized, authorized, and scoped to the active
  user or tenant. Pass identifiers or sensitive fields only when required, with
  validation, least privilege, and audit controls.
- [ ] Tool registry is state-aware: available tools and output schemas change by phase.
- [ ] Validate state and policy boundaries after high-risk steps and before
  irreversible side effects; avoid redundant checks on harmless steps.
- [ ] Fallback, retry, or human escalation defined when guardrails trigger.

## Context management

- [ ] Context treated as a scarce resource; set an empirical budget per model and
  task using quality, latency, and cost measurements rather than a fixed token
  threshold.
- [ ] History compressed by summarization, sliding window, or structured handoff.
- [ ] Context reset strategy exists for long-running sessions.
- [ ] Context rot monitored: model starts losing the thread or calling wrong tools.
- [ ] Stable high-priority instructions remain authoritative; reconstruct or
  summarize lower-priority history when long sessions degrade task performance.

## Non-determinism

- [ ] System does not rely on 100% reproducibility even at temperature=0.
- [ ] Guardrails + retry logic catch and recover from off-path behavior.
- [ ] Best-of-N or stability metrics used where appropriate.
- [ ] Sources of non-determinism documented (GPU nodes, provider routing, prompt cache state).

## Testing with trajectory stories

- [ ] Versioned story fixtures (YAML, JSON, or test code) define representative
  trajectories with environment state, expected outcomes, and critical tool calls.
- [ ] Stories sliced so each turn can be tested independently.
- [ ] Adversarial fixtures cover conflicting instructions, prompt injection,
  ambiguity, emotional pressure, multi-intent requests, and partial failures.
- [ ] Ownership covers both model-behavior trajectories and deterministic runtime
  invariants, regardless of how the team divides roles.
- [ ] LLM-as-judge validated on representative human-labeled examples with a
  task-appropriate agreement or decision metric, uncertainty, and error analysis.
- [ ] Train/test split for stories to detect overfitting to the validation set.

## Metrics and evaluation

- [ ] Multi-dimensional metrics: correctness, efficiency (steps/tool calls), stability, safety, cost, latency.
- [ ] Evaluation context fixed so metric changes reflect real improvement, not prompt format drift.
- [ ] Diff of residuals, trajectory, and tool calls tracked across model versions.
- [ ] Human-in-the-loop boundary defined where agent is unreliable.

## Cost and latency optimization

- [ ] Multi-model routing: small model for simple intents, large model for reasoning/correction.
- [ ] Caching is used only for responses safe to reuse. Define tenant/user scope,
  cache key semantics, freshness, invalidation, authorization, and false-match
  handling; treat provider prompt caching as an optimization, not a correctness
  dependency.
- [ ] Fillers or progress indicators for real-time/voice interfaces.
- [ ] Token and call cost tracked per session.

## Security and PII

- [ ] Sensitive fields are minimized and protected according to policy and
  provider controls; redact or tokenize values the task does not require.
- [ ] Backend proxy layer filters fields and array sizes before LLM sees them.
- [ ] Models handling sensitive data run in a controlled environment.

## Anti-patterns

| Anti-pattern | Why it fails | Better approach |
|---|---|---|
| Framework abstractions hide prompts, context, retries, or tool calls | Loss of observability and control | Require traceability or use a thinner runtime |
| Universal LLM API exposes unnecessary data or actions | Injection, privacy, and confused-deputy risk | Capability-scoped tools per task or phase |
| Many overlapping tools lack clear routing or schemas | Ambiguous tool selection and larger attack surface | Clarify contracts, group capabilities, route, or decompose |
| Provider prompt cache is a correctness dependency | Provider behavior, routing, and retention can change | Treat it only as an optimization; design explicit safe caching if needed |
| Single quality metric | Hidden cost/latency/safety issues | Multi-dimensional scorecard |
| Fine-tuning before a reproducible evaluation harness and simpler baselines | Costly iteration without evidence | Establish prompting/retrieval baselines and evals first |
| State machine models open-ended semantic behavior in exhaustive detail | State explosion and brittle transitions | Encode deterministic policy in states and leave bounded semantic choices to the model |
