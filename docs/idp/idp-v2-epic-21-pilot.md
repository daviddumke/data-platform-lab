# IDP v2 — Epic 21 Pilot · Databricks for Data Engineering

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's Lakehouse on Databricks — Delta Lake internals, Photon-tuned ELT, DLT + Auto Loader, Unity Catalog governance, and SQL warehouses + Feature Store + Model Serving. They've passed the **Databricks DE Associate** (minimum) and target the **Databricks DE Professional**.
>
> **Bibliography.** *Learning Spark* 2nd ed. (Damji et al.) · *Delta Lake: Up and Running* (Patel & Lee) · *Databricks Lakehouse Platform Cookbook* (Pandey) · *Spark: The Definitive Guide* (Chambers & Zaharia) · Databricks Academy + docs.
>
> **Exam objectives — DE Associate.** Lakehouse Platform 24% · ELT with Spark 29% · Incremental Processing 22% · Production Pipelines 16% · Governance 9%.
>
> **Exam objectives — DE Professional.** Tooling 20% · Data Processing 30% · Data Modeling 20% · Security & Governance 10% · Monitoring 10% · Testing & Deployment 10%.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered AND both certs passed.

---

## Story 21.1 — Architect a Lakehouse with Delta Lake

### Sub-skill 21.1.1: Define Delta Lake internals (transaction log, ACID, MVCC, time travel)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/delta-lake-internals.md` covering the transaction log (`_delta_log`, JSON commits, checkpoints, version history), ACID guarantees (snapshot isolation, MVCC), Time Travel (`VERSION AS OF` / `TIMESTAMP AS OF`) and the Bronze/Silver/Gold medallion responsibilities per layer.

**Skill progression by level:**
- [ ] **Junior** — Recognize Delta Lake as a table format.
- [ ] **Mid** — Apply Delta tables; recognize the medallion model.
- [ ] **🎯 Senior (TARGET)** — Define Delta internals + medallion responsibilities; mentor mid-level engineers on transaction log reading.
- [ ] **Staff** — Architect cross-team Lakehouse strategy.
- [ ] **Principal** — Govern org-wide lakehouse + table-format policy.

---

### Sub-skill 21.1.2: Engineer Delta DML + OPTIMIZE + ZORDER + CDF + Liquid Clustering

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/delta-dml-ops.md` covering Delta DML (MERGE, DELETE, UPDATE with matched/not-matched clauses — 5 recipes), OPTIMIZE + ZORDER + VACUUM + retention trade-offs, Change Data Feed (CDF) setup + consumption, and Liquid Clustering as the modern alternative to ZORDER + partitioning. Engineer Bronze/Silver/Gold tables in the Lab with Delta + a notebook demonstrating MERGE + CDF + time-travel.

**Skill progression by level:**
- [ ] **Junior** — Recognize MERGE and OPTIMIZE.
- [ ] **Mid** — Apply existing OPTIMIZE jobs.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab medallion + MERGE + CDF; document Liquid Clustering adoption; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team Delta optimization standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 21.2 — Engineer ELT with Spark on Databricks

### Sub-skill 21.2.1: Engineer Photon + AQE + broadcast joins + Pandas UDFs for tuned ELT

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/databricks-spark-tuning.md` covering DataFrame API + Spark SQL idioms on Databricks (cross-ref Epic 17), Photon engine (vectorized engine, compatible queries, expected gains), AQE on Databricks, narrow vs wide transformations + shuffle minimization, broadcast joins (auto + hints), Databricks UDFs/UDAFs (Python, Pandas UDFs, Arrow-optimized), and Spark Connect (remote client separated from driver). Build an ELT Spark pipeline in the Lab (Databricks Community) with cluster config documented.

**Skill progression by level:**
- [ ] **Junior** — Recognize the Spark API on Databricks.
- [ ] **Mid** — Apply existing Spark transformations.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Photon-tuned ELT; mentor mid-level engineers on broadcast hints + Pandas UDFs.
- [ ] **Staff** — Architect cross-team Spark-on-Databricks tuning standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 21.3 — Operate Databricks Workspace & Workflows

### Sub-skill 21.3.1: Define cluster types + sizing + Workflows + Asset Bundles

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/databricks-workspace.md` covering cluster types (all-purpose, jobs, SQL warehouses, pools, instance pools), sizing (driver, workers, autoscaling, spot vs on-demand — with formulas), Databricks Workflows (tasks, dependencies, conditions, retries, repair runs — as the internal alternative to Airflow), Databricks Asset Bundles (DAB) as IaC for workspace artifacts, Repos (Git integration), DBFS, init scripts, and Databricks Connect (local dev against cluster). Engineer a Databricks Asset Bundle in the Lab (jobs as code, CI deployment) + Workflows with 3 dependent tasks.

**Skill progression by level:**
- [ ] **Junior** — Recognize Databricks clusters and Workflows.
- [ ] **Mid** — Apply existing clusters and workflows.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab DAB + Workflows; document sizing formulas; mentor mid-level engineers on DAB CI deployment.
- [ ] **Staff** — Architect cross-team Databricks workspace + DAB strategy.
- [ ] **Principal** — Govern org-wide Databricks workspace policy.

---

## Story 21.4 — Engineer Delta Live Tables & Auto Loader

### Sub-skill 21.4.1: Engineer DLT pipelines + expectations for declarative ELT

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dlt-pipelines.md` covering DLT fundamentals (declarative ETL, expectations, streaming/batch), expectations (warn, drop, fail — with 5 recipes), and DLT pipelines (development vs production, continuous vs triggered). Engineer a DLT Bronze/Silver/Gold pipeline in the Lab with expectations + monitoring.

**Skill progression by level:**
- [ ] **Junior** — Recognize DLT as declarative ELT.
- [ ] **Mid** — Apply existing DLT pipelines.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab DLT pipeline with expectations; mentor mid-level engineers on warn/drop/fail.
- [ ] **Staff** — Architect cross-team DLT adoption strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 21.4.2: Engineer Auto Loader + Structured Streaming for incremental ingestion

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/auto-loader-streaming.md` covering Auto Loader (`cloudFiles` — incremental file ingestion, schema inference, schema evolution, file notification mode vs directory listing), Structured Streaming on Databricks (state stores, checkpoint locations, triggers — cross-ref Epic 9), and streaming aggregations + watermarks + late data. Engineer Auto Loader over GCS/S3 in the Lab with a schema-evolution test.

**Skill progression by level:**
- [ ] **Junior** — Recognize Auto Loader.
- [ ] **Mid** — Apply existing Auto Loader pipelines.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Auto Loader + schema-evolution; mentor mid-level engineers on file notification mode.
- [ ] **Staff** — Architect cross-team incremental ingestion strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 21.5 — Govern Data with Unity Catalog

### Sub-skill 21.5.1: Engineer Unity Catalog (metastore → catalog → schema → table) + ACLs + masks

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/unity-catalog.md` covering UC architecture (metastore → catalog → schema → table hierarchy), access control (GRANT, table ACLs, column masks, row filters), lineage (table + column-level, automated), Volumes (managed/external for non-tabular data), Service Principals + workload identity federation, and System Tables (`system.access`, `system.billing`). Engineer Unity Catalog with 3 catalogs + ACLs in the Lab via Terraform.

**Skill progression by level:**
- [ ] **Junior** — Recognize Unity Catalog as the governance layer.
- [ ] **Mid** — Apply existing UC grants.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab UC + ACL setup; mentor mid-level engineers on column masks and row filters.
- [ ] **Staff** — Architect cross-team UC strategy + System Tables observability.
- [ ] **Principal** — Govern org-wide UC + lineage policy.

---

### Sub-skill 21.5.2: Engineer Delta Sharing for cross-org data sharing

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/delta-sharing.md` covering Delta Sharing (open protocol for cross-org data sharing) — providers + recipients + sharing security model. Engineer Delta Sharing between 2 workspaces in the Lab with share validation.

**Skill progression by level:**
- [ ] **Junior** — Recognize Delta Sharing as a concept.
- [ ] **Mid** — Apply existing shares as a recipient.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Delta Sharing setup; mentor mid-level engineers on the security model.
- [ ] **Staff** — Architect cross-team Delta Sharing strategy.
- [ ] **Principal** — Govern org-wide data-sharing policy.

---

## Story 21.6 — Operate Databricks SQL & Serving, Pass Both Certs

### Sub-skill 21.6.1: Engineer Databricks SQL + Feature Store + Model Serving

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/databricks-sql-serving.md` covering SQL warehouses (Pro vs Serverless vs Classic), SQL query optimization (Photon, materialized views, caches — 5 techniques), Databricks SQL dashboards + alerts, Databricks AI/BI (Genie), Feature Store (Unity Catalog Feature Engineering — offline + online), Model Serving (real-time + batch inference), and MLflow integration. Engineer a SQL warehouse + dashboard in the Lab + Feature Store + Model Serving pipeline E2E.

**Skill progression by level:**
- [ ] **Junior** — Recognize Databricks SQL + Model Serving.
- [ ] **Mid** — Apply existing SQL warehouses.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab SQL + Feature Store + Model Serving setup; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team SQL + serving strategy.
- [ ] **Principal** — Govern org-wide BI + serving policy.

---

### Sub-skill 21.6.2: Pass Databricks DE Associate + Professional certs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Complete Databricks Academy DE Associate + Professional learning paths, take 3 practice exams per cert (≥85% pass mark before sitting), pass DE Associate (minimum) and target DE Professional. Publish a `docs/certs/databricks-de.md` retrospective.

**Skill progression by level:**
- [ ] **Junior** — *(out of natural progression for this sub-skill)*
- [ ] **Mid** — Apply Databricks daily.
- [ ] **🎯 Senior (TARGET)** — Pass DE Associate (minimum) + Professional (target); publish retrospective; mentor mid-level engineers preparing.
- [ ] **Staff** — *(out of natural progression for this sub-skill)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 6 Story-level 🎯 boxes are ticked** — which requires 9 sub-skill 🎯 boxes including both Databricks certs. Mastery evidence: Delta internals + medallion + DML + CDF + Liquid Clustering; Photon-tuned ELT; DAB + Workflows; DLT pipeline + Auto Loader; UC + Delta Sharing; SQL warehouse + Feature Store + Model Serving; Databricks DE Associate + Professional certs.
