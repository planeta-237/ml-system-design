# LLM Agent Patterns

Use this file when designing or reviewing LLM-agent, RAG, or tool-using systems.

## Agent anatomy

- [ ] Agent decomposed into: runtime, LLM, context/memory, tools, and reasoning loop.
- [ ] Prompt engineer and runtime engineer roles separated with a stable contract (e.g., YAML stories).
- [ ] Agent is not used if the task can be solved simpler without LLM.
- [ ] LLM treated as a stateless function; context constructed explicitly outside the model.

## Planning and reasoning

- [ ] Planning approach chosen: end-to-end model reasoning vs explicit plan.
- [ ] Explicit plan used for complex domains with clear business requirements.
- [ ] Reasoning tokens controlled: restricted for weak models and known flows, allowed for strong models and unpredictable flows.
- [ ] Plan is fixed and can be re-planned only through a separate correction step.

## Multi-agent systems

- [ ] Pattern used: Coordinator + parallel collaborators + Supervisor merge.
- [ ] Consensus/debate patterns avoided for production dialog systems.
- [ ] Router selects agents based on request and available agents.
- [ ] Supervisor resolves merge conflicts and decides when to return to the main track.
- [ ] Shared state / slots passed between parallel agents, not full history.
- [ ] State machine used only where behavior can be formalized; LLM remains the logic core.

## Guardrails

- [ ] Multi-layered guardrails: input validation → LLM call → output validation → tool result validation.
- [ ] Input checked for injection, jailbreak, toxicity, PII.
- [ ] Output validated against schema and tool arguments checked for sanity.
- [ ] Tool API minimized: only what the current step needs; no user_id or sensitive fields in tool parameters.
- [ ] Tool registry is state-aware: available tools and output schemas change by phase.
- [ ] Mid-turn stop-the-world check after each cycle to catch drift.
- [ ] Fallback, retry, or human escalation defined when guardrails trigger.

## Context management

- [ ] Context treated as a scarce resource; empirical production limit ~32K–64K tokens.
- [ ] History compressed by summarization, sliding window, or structured handoff.
- [ ] Context reset strategy exists for long-running sessions.
- [ ] Context rot monitored: model starts losing the thread or calling wrong tools.
- [ ] System prompt periodically refreshed so it does not get buried.

## Non-determinism

- [ ] System does not rely on 100% reproducibility even at temperature=0.
- [ ] Guardrails + retry logic catch and recover from off-path behavior.
- [ ] Best-of-N or stability metrics used where appropriate.
- [ ] Sources of non-determinism documented (GPU nodes, provider routing, prompt cache state).

## Testing with YAML stories

- [ ] Golden YAML stories define ideal trajectories with environment state and expected tool calls.
- [ ] Stories sliced so each turn can be tested independently.
- [ ] "Iron Man" fixtures simulate adversarial users (angry, indecisive, multi-intent).
- [ ] Prompt engineer tests YAML stories; runtime engineer tests code.
- [ ] LLM-as-judge calibrated with Cohen's kappa ≥ 0.6 vs human experts.
- [ ] Train/test split for stories to detect overfitting to the validation set.

## Metrics and evaluation

- [ ] Multi-dimensional metrics: correctness, efficiency (steps/tool calls), stability, safety, cost, latency.
- [ ] Evaluation context fixed so metric changes reflect real improvement, not prompt format drift.
- [ ] Diff of residuals, trajectory, and tool calls tracked across model versions.
- [ ] Human-in-the-loop boundary defined where agent is unreliable.

## Cost and latency optimization

- [ ] Multi-model routing: small model for simple intents, large model for reasoning/correction.
- [ ] Client-side cache (e.g., Redis + embedding similarity) instead of relying on provider prompt cache.
- [ ] Fillers or progress indicators for real-time/voice interfaces.
- [ ] Token and call cost tracked per session.

## Security and PII

- [ ] PII scrubbed before sending to external LLM; tokens mapped back at runtime.
- [ ] Backend proxy layer filters fields and array sizes before LLM sees them.
- [ ] Models handling sensitive data run in a controlled environment.

## Anti-patterns

| Anti-pattern | Why it fails | Better approach |
|---|---|---|
| Heavy frameworks hiding token-level reality | Loss of control | Lightweight custom runtime |
| Universal LLM API exposing too much data | Injection + noise | Minimal API per step |
| >5 tools on one agent | Wrong tool calls | Decompose or explicit plan |
| Provider prompt cache as primary cache | Unreliable routing | Client-side semantic cache |
| Single quality metric | Hidden cost/latency/safety issues | Multi-dimensional scorecard |
| Fine-tuning agent behavior | Poor results in practice | Prompt engineering + harness |
| State machine for everything | Exponential complexity | LLM core + state machine only where formalizable |
