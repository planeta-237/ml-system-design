# Data And Features

Use this file when the task involves datasets, schemas, labels, feature stores,
data quality, leakage, privacy, governance, or feedback loops.

## Checklist

- Data sources, ownership, SLAs, retention, and access controls are named.
- Labels are defined, collectable, timely, and aligned with the product goal.
- Training, validation, and serving distributions are compared.
- Leakage risks are checked: future information, proxy labels, duplicated users,
  offline-only features, and target-derived fields.
- Freshness requirements are mapped to batch, streaming, or online features.
- Quality checks cover missingness, outliers, schema drift, duplicates, delayed
  events, and inconsistent identifiers.
- Representativeness and bias risks are assessed across important segments.
- Consent, PII, deletion, audit, and compliance requirements are addressed.

## Common Findings

- The model target optimizes a proxy that can diverge from product value.
- Offline features are not available at serving time.
- The design has no cold-start path for new users, items, regions, or tenants.
- Feedback loops can amplify historical bias or previous model decisions.
