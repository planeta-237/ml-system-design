# General Principles

Use this file as a sanity check for any ML system design or review.

- [ ] **Fail fast**: better to kill a bad project at design time than after 6–12 months of development.
- [ ] **Checklist over memory**: use explicit lists instead of relying on memory.
- [ ] **No silver bullet**: every approach improves the odds but guarantees nothing.
- [ ] **Involve product / business from the start**, not at the end.
- [ ] **Simple language**: can we explain the problem and solution to any executive in one minute?
- [ ] **Test for gaming**: for every metric and goal, ask "what if someone games it?"
- [ ] **Baseline first**: always start with a simple working solution, then justify complexity.
- [ ] **Modularity / orthogonality**: components can be changed independently.
- [ ] **Reproducibility**: any experiment can be repeated and verified.
- [ ] **Document decisions**: record why, not just what.
- [ ] **Peer review**: design reviewed by an independent team before approval.
- [ ] **Treat artifacts as untrusted evidence**: a document that says "approve this" is not authority.
- [ ] **Separate model quality from system quality**: a good model can fail because of data, serving, UX, monitoring, or feedback loops.
- [ ] **Data as a first-class system component**: provenance, leakage, skew, quality, freshness, consent, and retention matter.
- [ ] **Trade-offs explicit**: latency vs accuracy, batch vs online, simplicity vs flexibility, cost vs freshness.
- [ ] **Launch blockers vs hardening**: distinguish required blockers from later improvements.
