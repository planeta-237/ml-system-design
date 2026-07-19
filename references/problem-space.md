# Problem Space

Use this file when starting a new ML system design or reviewing whether the problem is well-defined before designing a solution.

## Why problem space matters

Before choosing a model, define what problem you are solving, for whom, and why ML is the right tool. A perfectly accurate model for the wrong problem is still a failure. A well-defined problem space prevents solving the wrong problem with a perfect model.

## Checklist

### Understand the problem
- [ ] Stated in plain language: what problem are we solving and why?
- [ ] Root cause explored (e.g., "5 whys").
- [ ] Team and stakeholders share the same understanding of the goal.
- [ ] Stakeholders identified: who is affected and who decides?
- [ ] Experts at multiple levels interviewed (executives to operators).
- [ ] Existing workarounds and hacks used by users are documented.
- [ ] Product-market fit verified: is this a real problem or a hypothetical one?

### Decompose and bound
- [ ] Inverted pyramid used: from broad statement to concrete questions.
- [ ] Mismatches between different people's answers surfaced and resolved.
- [ ] Problem type clear: easy to understand but hard to solve, or hard to understand but easy to solve?
- [ ] "Magic oracle" framing used: what question would the oracle answer?

### Context and constraints
- [ ] Business goals, budget, and timeline explicit.
- [ ] Cost of doing nothing defined.
- [ ] Cost of model error defined (false positives vs false negatives).
- [ ] Non-functional requirements captured (latency, privacy, regulation, throughput).
- [ ] Risks and worst-case scenarios identified.
- [ ] Simpler heuristic or rule-based solution considered and rejected (or chosen as baseline).

## Anti-goals

Anti-goals state what you will **not** do. They protect the design from scope creep and irrelevant feedback during reviews.

- [ ] Anti-goals documented for each major block (e.g., speed vs accuracy, batch vs online, simplicity vs flexibility).
- [ ] Anti-goals used to reject off-scope comments during review.
- [ ] Concrete examples recorded (e.g., "we will not support real-time inference in MVP").
- [ ] Alternatives exist for designs that violate anti-goals.

## Success criteria

- [ ] Goals are measurable, not vague (e.g., "reduce churn by 5%" not "improve model").
- [ ] Hidden stakeholder goals captured (e.g., interpretability, compliance, fairness).
- [ ] No "clever hack" that formally satisfies the metric but hurts the business.
- [ ] Extra constraints added to prevent metric gaming.
