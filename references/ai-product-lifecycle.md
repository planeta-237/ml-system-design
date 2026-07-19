# AI Product Lifecycle

Use this file when the task touches product discovery, portfolio decisions,
stage-gate validation, hypothesis-driven design, or deciding whether an AI/ML
feature should be built at all.

This reference is **not** a substitute for product management, but it gives
ML system designers the language and checkpoints to keep technical work aligned
with business validation.

## Stage-Gate process

A structured way to move from idea to scale with explicit kill/pivot decisions.

```
Ideation → Concept Validation → Prototype Development → Beta Testing → MLP Launch → Scale & Optimize
```

Each stage ends with a **Gate** decision: **Go / Pivot / Kill / Conditional Go**.

| Stage | Goal | Key artifacts | Gate decision |
|-------|------|-------------|---------------|
| **Ideation** | Form and screen the idea | Problem statement, TAM, initial value hypothesis, technical feasibility hunch | Go / Pivot / Kill |
| **Concept Validation** | Confirm the problem and concept | User/market research, SAM, solution concept, data availability, technical risks | Go / Pivot / Kill |
| **Prototype Development** | Build a working AI prototype | Working model/pipeline, technical metrics, UX prototype, resource plan, alignment checks | Go / Conditional / Kill |
| **Beta Testing** | Launch MVP to a limited group | Real-environment metrics, behavioral feedback, SOM, alignment in real conditions | Go / Conditional / Kill |
| **MLP Launch** | Launch a lovable product | Product metrics, technical stability, security/alignment plan, integration, scaling limits | Go / Optimize / Sunset |
| **Scale & Optimize** | Grow and improve | Scale metrics, ROI, long-term model health, drift, user satisfaction | Continue / Maintain / Sunset |

## Market sizing

- **TAM** — Total Addressable Market: theoretical maximum demand.
- **SAM** — Serviceable Addressable Market: reachable part given constraints.
- **SOM** — Serviceable Obtainable Market: realistic near-term share.

Use these to sanity-check the effort: a tiny SOM with a multi-month model build
is usually a weak candidate unless it unlocks a larger SAM later.

## Fast Track

For products with low technical uncertainty, combine stages:

```
Ideation → Discovery (Concept + Prototype) → Delivery (Beta + MLP) → Scale
```

Use Fast Track when the technology is proven, the team has references, and the
main risk is product-market fit, not technical feasibility.

## Hypothesis-Driven Development (HDD)

Every product or feature decision should be framed as a testable hypothesis.

**Formula:**

> If we do **[X]** for **[persona]**, they will **[observable behavior]**, measured by **[metric]**.

**Decision rule:** define a **line in the sand** before running the test.

- Above the line → **persevere** (double down, scale, integrate).
- Below the line → **pivot** (change solution, problem, persona, or abandon).

## Double diamond: from problem to solution

- [ ] **Right problem:** understand the persona and jobs-to-be-done (JTBD) before
  proposing a solution. Bad signal: users say "yes, I would use it." Good
  signal: users describe the pain in their own words and already spend time or
  money on workarounds.
- [ ] **Right solution:** test demand with an MVP/experiment before building full
  usability. Do not confuse "users like the UI" with "users will change
  behavior."
- [ ] **Right usability:** validate interaction only after demand is confirmed.

## Customer Experience (CX) map

For each step of the user's journey, define:

- [ ] Stage meaning (Acquisition, Onboarding, Engagement, Outcome, Retention).
- [ ] DV — dependent variable (metric you want to move).
- [ ] Cut-off / line in the sand.
- [ ] IVs — ideas to test.
- [ ] Aggregate metrics lie; segment and cohort your analysis.

## When to use with ML system design

| Situation | Use |
|---|---|
| Portfolio of AI ideas | Stage-Gate to allocate investment and kill weak ideas early. |
| Single feature or model | HDD to frame the hypothesis and minimum test before building a pipeline. |
| Model change in production | HDD + A/B: hypothesis, line in the sand, guardrails. |
| Launching a new AI product | Stage-Gate stages + production-readiness checklist. |
| Debug a flat product metric | CX map + top-down debugging: experiment design → usability → demand → problem. |

## Common anti-patterns

| Anti-pattern | Why it fails | Better approach |
|---|---|---|
| Build first, validate later | Wasted engineering on unproven demand | HDD with kill metric before coding |
| No kill criteria | Team keeps iterating without evidence | Line in the sand defined upfront |
| Confusing likes with demand | Users politely say yes, then do not use | Test observable behavior, not preference |
| Optimizing usability before demand | Pretty product no one needs | Double diamond: problem → demand → usability |
| One big annual roadmap | Misses learning and market shifts | Quarterly stage-gate reviews with pivot/kill options |
| Success theater | Vanity metrics hide lack of impact | North Star + counter-metrics + cohorts |

## Relevant skill references

- `problem-space.md` for framing the problem, anti-goals, and success criteria.
- `metrics-and-loss.md` for North Star, counter-metrics, and metric hierarchy.
- `ab-testing.md` for experiment design, MDE, and guardrails.
- `design-workflow.md` for translating a validated product into a system design.
- `production-readiness.md` for launch gates.
