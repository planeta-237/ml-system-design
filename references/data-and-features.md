# Data And Features

Use this file when the task involves datasets, schemas, labels, feature stores,
data quality, leakage, privacy, governance, or feedback loops.

## Checklist

- [ ] Data sources, ownership, SLAs, retention, and access controls are named.
- [ ] Labels are defined, collectable, timely, and aligned with the product goal.
- [ ] ETL vs ELT approach chosen with compute-vs-storage trade-off in mind.
- [ ] Training, validation, and serving distributions are compared.
- [ ] Leakage risks are checked: future information, proxy labels, duplicated users,
  offline-only features, and target-derived fields.
- [ ] Freshness requirements are mapped to batch, streaming, or online features.
- [ ] Quality checks cover missingness, outliers, schema drift, duplicates, delayed
  events, and inconsistent identifiers.
- [ ] A data validation pipeline enforces constraints and raises alerts on
  violations.
- [ ] Training-serving consistency is checked: same units, formats, encodings, and
  computation paths.
- [ ] Representativeness and bias risks are assessed across important segments.
- [ ] Consent, PII, deletion, audit, and compliance requirements are addressed.
- [ ] Data and labels are versioned with metadata (who, when, tool version).
- [ ] Retrieval strategy matches data characteristics: vector search for semantic
  similarity, hybrid search for keyword/code lookups, exact match for IDs and
  history.

## Data Pipelines and Orchestration

- [ ] Orchestration is expressed as a DAG (directed acyclic graph) with explicit
  dependencies, retries, SLAs, and backfill support.
- [ ] Tasks are idempotent so reruns after failure do not corrupt data.
- [ ] Sensors or contract checks wait for upstream data readiness before
  starting downstream work.
- [ ] Data passing between tasks is bounded and typed (XCom-like mechanisms
  should not carry large payloads).
- [ ] Schema and quality contracts are enforced at pipeline boundaries, not
  only at the end.
- [ ] Backfills and reruns are tested; replay does not duplicate labels or
  produce inconsistent feature windows.
- [ ] Orchestrator fits the cadence: Airflow for batch workflows, Flink/Spark
  Streaming for streaming, not the other way around.

## Common Findings

- The model target optimizes a proxy that can diverge from product value.
- Offline features are not available at serving time.
- The design has no cold-start path for new users, items, regions, or tenants.
- Feedback loops can amplify historical bias or previous model decisions.
- ETL logic differs between training and serving, causing training-serving skew.
- Data contracts are missing or not enforced.
