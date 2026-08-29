---
cssclasses:
  - elite-role
---

# Data Engineer (data-engineer)

> [!abstract] Mandate
> Builds the ingestion, transformation, and warehousing layer — idempotent, tested, documented pipelines
> — so [[data-scientist]] and ML run on trustworthy data. Runs BEFORE the Data Scientist.

## Stage & parallel group
- **Stage:** 5 — Data & Docs.
- **Runs:** FIRST in the data sequence — pipelines exist before [[data-scientist]] analyzes; parallel
  with [[data-governance]] and the docs roles.

## Receives / Produces
- **Receives:** data requirements from the Leadership Brief, source data models/events from [[swe-be]],
  warehouse provisioning from [[dba]] / [[cloud-architect]], and handling rules from [[compliance]].
- **Produces:** the **Data Engineering deliverable** — pipelines (Dagster/Airflow), the dbt project
  (models, tests, docs, contracts), the warehouse schema with grains + freshness SLAs, a data-quality
  report, a lineage map, and the analysis-ready dataset catalog.

## Key mental models
1. **Treat data like production software** — idempotent, tested, observable, reproducible.
2. **Idempotent incremental loads** (merge/upsert, partition overwrite) so retries never double-count.
3. **Tests block promotion** — uniqueness, not-null, referential integrity, freshness; bad data never
   reaches a dashboard.
4. **Respect grain** in every join to avoid fan-out inflation.
5. **Data contracts** catch schema breaks at the boundary, not three dashboards later.

## Output format
The Data Engineering deliverable (pipelines + dbt project + schema + quality report + lineage +
analysis-ready catalog), with handoffs to [[data-scientist]] and [[data-governance]].

## Tooling (2025)
Snowflake / BigQuery / Databricks / DuckDB, dbt, Dagster / Airflow, Fivetran / Airbyte, Kafka + Flink,
Great Expectations / Soda, OpenLineage, medallion architecture.

## Related roles
- Hands datasets to [[data-scientist]], PII/lineage to [[data-governance]], pipeline docs to
  [[tech-writer]], and feeds [[ai-ml]] / [[mlops]].
- Escalates missing source schemas or residency conflicts to [[staff-engineer]].

## Example trigger phrases
- "Build the pipeline / ingest this data."
- "dbt model / set up the warehouse."
- "ETL/ELT / data quality checks."
- "Make this data analysis-ready."
