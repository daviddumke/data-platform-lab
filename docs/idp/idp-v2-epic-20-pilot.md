# IDP v2 — Epic 20 Pilot · GCP for Data Engineering

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills can architect a production GCP data platform across Pub/Sub + Dataflow + BigQuery + Composer + Dataplex — aligned to the **Google Professional Data Engineer (PDE)** exam. They've shipped ≥2 services per Story in the Lab and passed the PDE.
>
> **Bibliography.** *Official Google Cloud Certified Professional Data Engineer Study Guide* (Sybex) · *Data Engineering on Google Cloud* Coursera spec · *Google BigQuery: The Definitive Guide* (Lakshmanan & Tigani) · *Architecting Modern Data Platforms* (Sah & Dahiya) · Google Cloud Architecture Framework — Data Analytics pillar · Google Cloud Next talks.
>
> **Exam objectives.** Designing systems ~22% · Ingesting & processing ~25% · Storing ~20% · Preparing & using for analysis ~15% · Maintaining & automating ~18%.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered AND PDE passed.

---

## Story 20.1 — Operate GCP Ingestion Services

### Sub-skill 20.1.1: Engineer Pub/Sub + Dataflow for streaming ingestion

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-streaming-ingest.md` covering Pub/Sub (topics, subscriptions, push vs pull, ordering keys, dead-letter, exactly-once delivery — vs Kafka), Pub/Sub Lite economics, and Dataflow (Apache Beam runner, unified batch + streaming, autoscaling, Beam programming model). Engineer a Pub/Sub + Dataflow streaming pipeline in the Lab via Compose with emulator.

**Skill progression by level:**
- [ ] **Junior** — Recognize Pub/Sub and Dataflow.
- [ ] **Mid** — Apply existing Pub/Sub publishers and Beam pipelines.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Pub/Sub + Dataflow setup; select between Pub/Sub and Pub/Sub Lite; mentor mid-level engineers on Beam.
- [ ] **Staff** — Architect cross-team streaming strategy.
- [ ] **Principal** — Govern org-wide streaming platform policy.

---

### Sub-skill 20.1.2: Engineer Datastream + DTS + Eventarc for CDC + SaaS ingestion

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-batch-cdc-ingest.md` covering Datastream (CDC Postgres/MySQL/Oracle → BigQuery/GCS), BigQuery Data Transfer Service (SaaS sources), Storage Transfer Service, and Cloud Functions + Eventarc for event-driven ingestion. Engineer Datastream Postgres → BigQuery CDC in the Lab with replication validation.

**Skill progression by level:**
- [ ] **Junior** — Recognize Datastream and DTS.
- [ ] **Mid** — Apply existing DTS jobs.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Datastream CDC pipeline; mentor mid-level engineers on replication validation.
- [ ] **Staff** — Architect cross-team CDC + SaaS-ingest strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 20.2 — Operate GCP Storage Services

### Sub-skill 20.2.1: Define GCS + BigQuery storage + BigLake for the data-lake-house foundation

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-data-lake.md` covering Cloud Storage (classes, lifecycle, retention, signed URLs, requester-pays), BigQuery storage internals (capacitor format, time-travel, fail-safe, partitioning, clustering), and BigLake (unified governance over GCS + Iceberg/Hudi/Delta). Engineer a BigQuery dataset partitioned + clustered in the Lab and a BigLake table over GCS + Iceberg.

**Skill progression by level:**
- [ ] **Junior** — Recognize GCS and BigQuery storage.
- [ ] **Mid** — Apply existing GCS + BigQuery tables.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab partitioned + clustered + BigLake foundation; mentor mid-level engineers on capacitor + time-travel.
- [ ] **Staff** — Architect cross-team data-lake-house strategy.
- [ ] **Principal** — Govern org-wide GCP storage policy.

---

### Sub-skill 20.2.2: Select between Spanner, Cloud SQL, Firestore, Bigtable, AlloyDB for operational stores

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-operational-stores.md` covering Cloud Spanner (globally distributed SQL, leader election, interleaved tables), Cloud SQL (HA, read replicas), Firestore (Native vs Datastore mode, indexes, transactions), Bigtable (NoSQL wide-column, HBase-compatible, row-key design), and AlloyDB (Postgres + columnar engine vs Cloud SQL). Selection criteria per workload.

**Skill progression by level:**
- [ ] **Junior** — Recognize the GCP operational stores.
- [ ] **Mid** — Apply existing Cloud SQL / Firestore.
- [ ] **🎯 Senior (TARGET)** — Select the right store per workload; mentor mid-level engineers on Bigtable row-key design.
- [ ] **Staff** — Architect cross-team operational store strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 20.3 — Operate GCP Processing Services

### Sub-skill 20.3.1: Engineer BigQuery as the core processing engine (slots, BQML, Omni)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/bigquery-processing.md` covering advanced BigQuery SQL (window functions, scripts, procedures, JS/SQL UDFs, BI Engine — cross-ref Epic 4), slots (on-demand vs reservations vs autoscaling editions, fair scheduling), BigQuery ML (CREATE MODEL, predict, evaluate, Boosted Tree / AutoML / TF import), and BigQuery Omni (multi-cloud query: AWS S3 + Azure Blob). Engineer a slot reservation + workload management in the Lab via Terraform.

**Skill progression by level:**
- [ ] **Junior** — Recognize BigQuery as a SQL warehouse.
- [ ] **Mid** — Apply existing BigQuery queries.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab slot reservation + workload management; mentor mid-level engineers on slot economics.
- [ ] **Staff** — Architect cross-team BigQuery slot strategy.
- [ ] **Principal** — Govern org-wide BigQuery cost + slot policy.

---

### Sub-skill 20.3.2: Operate Dataproc + Dataform + Dataflow templates

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-processing-alt.md` covering Dataproc (managed Spark/Hadoop, Serverless, Metastore — cluster modes), Dataform (managed dbt-like, SQLX, dependency graph — vs dbt), and Dataflow templates (classic + Flex Templates). Engineer a Dataproc Serverless Spark job in the Lab + a Dataform project versioned.

**Skill progression by level:**
- [ ] **Junior** — Recognize Dataproc and Dataform.
- [ ] **Mid** — Apply existing Dataproc clusters.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Dataproc Serverless + Dataform setup; mentor mid-level engineers on Dataform-vs-dbt.
- [ ] **Staff** — Architect cross-team processing alternatives strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 20.4 — Operate GCP Orchestration

### Sub-skill 20.4.1: Engineer Cloud Composer + Cloud Workflows for orchestration

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-orchestration.md` covering Cloud Composer (managed Airflow — environments, autoscaling, plugins; vs MWAA vs self-managed — cross-ref Epic 23), Cloud Workflows (serverless YAML-based orchestration — where it beats Composer), and Cloud Scheduler. Engineer a Cloud Composer environment via Terraform + Cloud Workflows orchestrating 3 jobs in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize Composer and Workflows.
- [ ] **Mid** — Apply existing Composer DAGs.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Composer + Workflows setup; select between them per workload; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team orchestration strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 20.4.2: Define Cloud Monitoring + Logging + Trace + Error Reporting + Cloud Build

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-observability.md` covering Cloud Monitoring + Cloud Logging + Cloud Trace + Error Reporting (canonical setup for data pipelines) and Cloud Build + Artifact Registry for CI/CD. Apply in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize Cloud Monitoring.
- [ ] **Mid** — Apply existing dashboards.
- [ ] **🎯 Senior (TARGET)** — Define the canonical observability stack + Cloud Build CI/CD; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team observability strategy.
- [ ] **Principal** — Govern org-wide GCP observability policy.

---

## Story 20.5 — Govern GCP Security & Compliance

### Sub-skill 20.5.1: Define IAM + KMS + Secret Manager + VPC Service Controls + Audit Logs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-security.md` covering IAM (roles primitives vs predefined vs custom, principal types, conditions), KMS + envelope encryption, Secret Manager + rotation, VPC Service Controls (security perimeters for data services), and Cloud Audit Logs (admin, data access, system events) with detection queries.

**Skill progression by level:**
- [ ] **Junior** — Recognize IAM and KMS.
- [ ] **Mid** — Apply existing IAM bindings.
- [ ] **🎯 Senior (TARGET)** — Define the canonical security baseline; mentor mid-level engineers on VPC Service Controls.
- [ ] **Staff** — Architect cross-team GCP security strategy.
- [ ] **Principal** — Govern org-wide GCP security policy.

---

### Sub-skill 20.5.2: Engineer Dataplex + Cloud DLP + BigQuery column/row-level security

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gcp-data-governance.md` covering Dataplex (data mesh governance — lakes, zones, assets, data quality), Cloud DLP (PII discovery + de-identification + masking), and BigQuery column-level + row-level security + policy tags. Engineer VPC SC + policy tags + DLP scan in the Lab via Terraform + Dataplex lake/zone/asset structure with lineage view.

**Skill progression by level:**
- [ ] **Junior** — Recognize Dataplex and DLP.
- [ ] **Mid** — Apply existing policy tags.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Dataplex + DLP + policy-tag setup; mentor mid-level engineers on row/column-level security.
- [ ] **Staff** — Architect cross-team data governance strategy.
- [ ] **Principal** — Govern org-wide data governance policy.

---

## Story 20.6 — Master BigQuery & Pass PDE

### Sub-skill 20.6.1: Master BigQuery internals (Colossus, Dremel, query plans, partitioning, clustering, mat views)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/bigquery-deep-dive.md` covering BigQuery architecture (Colossus, Jupiter network, Dremel, Borg, capacitor), query plan reading (stages, slot-ms, shuffle, bytes shuffled — with 5 real audits), partition strategies (date, integer range, ingestion-time), clustering on up to 4 columns + pruning, materialized views + incremental refresh + smart tuning, scripts + procedures + assertions, Search indexes + JSON type + array operations, and Editions (Standard/Enterprise/Enterprise Plus) break-even calc. Engineer slot reservation + Enterprise edition in the Lab + a materialized view with smart tuning + benchmark.

**Skill progression by level:**
- [ ] **Junior** — Recognize BigQuery as a managed warehouse.
- [ ] **Mid** — Apply BigQuery queries with partitioning.
- [ ] **🎯 Senior (TARGET)** — Master BigQuery internals; ship the Lab slot reservation + mat view with benchmark; mentor mid-level engineers on query plan reading.
- [ ] **Staff** — Architect cross-team BigQuery deep-dive standards.
- [ ] **Principal** — Govern org-wide BigQuery + warehouse policy.

---

### Sub-skill 20.6.2: Pass the Google Professional Data Engineer (PDE) exam

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Complete the Coursera "Data Engineering on Google Cloud" specialization + 3 practice exams (≥85% before sitting), pass the PDE. Publish a `docs/certs/pde.md` retrospective.

**Skill progression by level:**
- [ ] **Junior** — *(out of natural progression for this sub-skill)*
- [ ] **Mid** — Apply GCP services daily.
- [ ] **🎯 Senior (TARGET)** — Pass PDE; publish retrospective; mentor mid-level engineers preparing.
- [ ] **Staff** — *(out of natural progression for this sub-skill)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 6 Story-level 🎯 boxes are ticked** — which requires 11 sub-skill 🎯 boxes including the PDE pass. Mastery evidence: Pub/Sub + Dataflow + Datastream pipelines; GCS + BigQuery partitioned + BigLake foundation; BigQuery slot reservation + BQML + Omni; Dataproc Serverless + Dataform; Composer + Workflows orchestration; VPC SC + Dataplex + DLP + policy tags; BigQuery materialized view with smart tuning benchmark; PDE cert passed.
