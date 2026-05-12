# IDP v2 — Epic 22 Pilot · Snowflake for Data Engineering

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's Snowflake stack — micro-partition + clustering economics, COPY/Snowpipe/Streams/Tasks/Dynamic Tables, RBAC + masking + RLS, Query Profile audits, and Snowpark procedures. They've passed **SnowPro Core** (minimum) and target **SnowPro Advanced: Data Engineer**.
>
> **Bibliography.** *Snowflake: The Definitive Guide* (Avila Kay & Yamma) · *Snowflake Cookbook* (Qureshi) · *Mastering Snowflake Solutions* (Morton) · Snowflake University + docs · Snowflake Summit talks.
>
> **Exam objectives — SnowPro Core.** Architecture ~25% · Access & Security ~20% · Performance ~15% · Loading/Unloading ~10% · Transformations ~20% · Data Protection & Sharing ~10%.
>
> **Exam objectives — SnowPro Advanced DE.** Data Movement ~28% · Performance ~22% · Storage & Protection ~10% · Security ~10% · Transformation ~30%.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered AND both certs passed.

---

## Story 22.1 — Understand Snowflake Architecture

### Sub-skill 22.1.1: Define the 3-layer architecture + micro-partitions + clustering + warehouses + caches

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowflake-architecture.md` covering the 3-layer architecture (Cloud Services, Compute via Virtual Warehouses, Storage), micro-partitions (immutable, ~50-500MB, automatic clustering), clustering keys + automatic clustering (when to adopt), Virtual Warehouses (sizes XS-6XL, multi-cluster, scaling policy), caches (result, local disk, metadata — hit rate optimization), Query Acceleration Service, and editions (Standard / Enterprise / Business Critical / VPS). Build Snowflake free trial setup + 3 sized warehouses in the Lab with validation queries.

**Skill progression by level:**
- [ ] **Junior** — Recognize Snowflake's separation of storage and compute.
- [ ] **Mid** — Apply existing Snowflake warehouses.
- [ ] **🎯 Senior (TARGET)** — Define the architecture deeply; engineer the Lab warehouse setup; mentor mid-level engineers on micro-partitions + clustering economics.
- [ ] **Staff** — Architect cross-team Snowflake adoption strategy.
- [ ] **Principal** — Govern org-wide warehouse + clustering policy.

---

## Story 22.2 — Engineer Snowflake Data Loading

### Sub-skill 22.2.1: Engineer COPY + Stages + Snowpipe + Snowpipe Streaming for all ingest patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowflake-loading.md` covering COPY INTO (file formats CSV/JSON/Parquet/Avro/ORC/XML, options, error handling — with recipes), Stages (named internal, named external, user, table), Snowpipe (continuous loading via SQS/Pub/Sub notifications), and Snowpipe Streaming (low-latency via SDK, channel-based — vs file-based). Engineer COPY + Snowpipe + Snowpipe Streaming in the Lab — 3 ingest patterns documented.

**Skill progression by level:**
- [ ] **Junior** — Recognize COPY and Snowpipe.
- [ ] **Mid** — Apply existing COPY jobs.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab 3 ingest patterns; select between Snowpipe and Snowpipe Streaming; mentor mid-level engineers on stages.
- [ ] **Staff** — Architect cross-team Snowflake ingest strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 22.2.2: Engineer External Tables + Iceberg tables in Snowflake

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowflake-external-iceberg.md` covering External Tables (query files in cloud storage without loading), Iceberg tables in Snowflake (managed + unmanaged catalogs), and unloading (COPY INTO @stage). Engineer an Iceberg table in the Lab queried via Snowflake AND via Spark.

**Skill progression by level:**
- [ ] **Junior** — Recognize External Tables.
- [ ] **Mid** — Apply existing External Tables.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Iceberg setup queried from 2 engines; mentor mid-level engineers on managed vs unmanaged catalogs.
- [ ] **Staff** — Architect cross-team Iceberg + Snowflake interop strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 22.3 — Engineer Streams, Tasks & Dynamic Tables

### Sub-skill 22.3.1: Engineer Streams + Tasks for CDC + scheduled SQL

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowflake-streams-tasks.md` covering Streams (change tracking — standard, append-only, insert-only; offsets + consumption), Tasks (scheduled SQL execution, DAG via predecessors, serverless tasks), and the Stream + Task pattern for internal CDC. Engineer a Stream + Task pipeline in the Lab with table evolution.

**Skill progression by level:**
- [ ] **Junior** — Recognize Streams and Tasks.
- [ ] **Mid** — Apply existing Tasks.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Stream + Task pipeline; mentor mid-level engineers on offset consumption.
- [ ] **Staff** — Architect cross-team Snowflake CDC strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 22.3.2: Engineer Dynamic Tables + Time Travel + Zero-Copy Cloning

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowflake-dynamic-time-clone.md` covering Dynamic Tables (declarative incremental refresh, target lag — alternative to Streams+Tasks), Time Travel (DML history, AT/BEFORE clauses, retention period), Zero-Copy Cloning (databases, schemas, tables, instant clones), and Fail-safe (7 days post-time-travel, Enterprise+). Engineer a Dynamic Table in the Lab + compare with equivalent Stream/Task + Zero-Copy Clone for dev environment.

**Skill progression by level:**
- [ ] **Junior** — Recognize Dynamic Tables and Time Travel.
- [ ] **Mid** — Apply existing Dynamic Tables.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Dynamic Table + clone; document the comparison; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team Dynamic Table strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 22.4 — Govern Snowflake Security

### Sub-skill 22.4.1: Engineer RBAC + functional/access roles + network policies + audit

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowflake-rbac.md` covering RBAC (Roles, hierarchies, GRANT, role activation), Functional vs Access roles pattern, Network policies + Private Link + SSO/SCIM, Account Usage + Information Schema (audit + observability — canonical queries), and Access History + Object Dependencies (audit patterns). Engineer functional + access roles + masking in the Lab via Terraform.

**Skill progression by level:**
- [ ] **Junior** — Recognize Snowflake roles.
- [ ] **Mid** — Apply existing role grants.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab functional + access roles pattern; mentor mid-level engineers on role hierarchies.
- [ ] **Staff** — Architect cross-team Snowflake RBAC strategy.
- [ ] **Principal** — Govern org-wide Snowflake security policy.

---

### Sub-skill 22.4.2: Engineer Dynamic Data Masking + Row Access Policies + Object Tagging

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowflake-masking-rls.md` covering Dynamic Data Masking (sensitive columns masked by role), Row Access Policies (RLS — with 3 patterns), and Object Tagging + Tag-based masking. Engineer Object Tagging + tag-based masking in the Lab with validation queries.

**Skill progression by level:**
- [ ] **Junior** — Recognize masking exists.
- [ ] **Mid** — Apply existing masking policies.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab tag-based masking; mentor mid-level engineers on RLS patterns.
- [ ] **Staff** — Architect cross-team data governance strategy.
- [ ] **Principal** — Govern org-wide masking + RLS policy.

---

## Story 22.5 — Optimize Snowflake Performance & Costs

### Sub-skill 22.5.1: Engineer Query Profile audits + warehouse sizing + Resource Monitors + Search Optimization

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/runbooks/snowflake-query-audit.md` defining the Query Profile audit methodology (most expensive nodes, partition pruning, spillage — with 5 real reads), warehouse sizing strategy (start small, scale up if needed), multi-cluster warehouses (concurrency vs scaling out), Resource Monitors + credit quotas, Search Optimization Service (point-lookup workloads), Materialized Views (limitations, sync, recommendation engine), and credit consumption + auto-suspend tuning. Engineer Resource Monitor + cost alerts in the Lab + Query Profile audit on 5 slow queries with before/after report.

**Skill progression by level:**
- [ ] **Junior** — Recognize Query Profile.
- [ ] **Mid** — Apply existing Resource Monitors.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab audits + Resource Monitor; mentor mid-level engineers through their first Query Profile read.
- [ ] **Staff** — Architect cross-team Snowflake FinOps strategy.
- [ ] **Principal** — Govern org-wide Snowflake cost + performance policy.

---

## Story 22.6 — Engineer Snowpark, Apps & Data Sharing, Pass Both Certs

### Sub-skill 22.6.1: Engineer Snowpark + Data Sharing + Marketplace + Cortex

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowpark-sharing-cortex.md` covering Snowpark Python (DataFrame API, UDFs, stored procedures, packages — vs Spark trade-offs), Data Sharing (provider + consumer pattern), Snowflake Marketplace + Data Exchange (private), and Cortex AI/ML functions (LLM functions, embeddings, ML model registry). Engineer a Snowpark Python procedure in the Lab + Data Share between 2 accounts.

**Skill progression by level:**
- [ ] **Junior** — Recognize Snowpark and Marketplace.
- [ ] **Mid** — Apply existing Snowpark UDFs.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Snowpark procedure + Data Share; mentor mid-level engineers on Snowpark-vs-Spark.
- [ ] **Staff** — Architect cross-team Snowpark + Data Sharing strategy.
- [ ] **Principal** — Govern org-wide data-sharing policy.

---

### Sub-skill 22.6.2: Architect Snowpark Container Services + Native Apps

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/snowpark-containers-native-apps.md` covering Snowpark Container Services (managed containers inside Snowflake — use cases) and Native Apps (apps with logic + UI shareable via Marketplace — architecture).

**Skill progression by level:**
- [ ] **Junior** — Recognize Container Services and Native Apps as concepts.
- [ ] **Mid** — Apply existing Snowflake-hosted apps.
- [ ] **Senior** — Read Container Services manifests; debug app deployments.
- [ ] **🎯 Staff (TARGET)** — Architect a Container Service or Native App; mentor Senior engineers.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 22.6.3: Pass SnowPro Core + Advanced DE certs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Complete Snowflake University SnowPro Core + Advanced DE learning paths, take 3 practice exams per cert (≥85% before sitting), pass SnowPro Core (minimum) and target SnowPro Advanced DE. Publish `docs/certs/snowpro.md` retrospective.

**Skill progression by level:**
- [ ] **Junior** — *(out of natural progression for this sub-skill)*
- [ ] **Mid** — Apply Snowflake daily.
- [ ] **🎯 Senior (TARGET)** — Pass SnowPro Core (minimum) + Advanced DE (target); publish retrospective; mentor mid-level engineers preparing.
- [ ] **Staff** — *(out of natural progression for this sub-skill)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 6 Story-level 🎯 boxes are ticked** — which requires 10 sub-skill 🎯 boxes (one at Staff) including both SnowPro certs. Mastery evidence: 3-layer architecture + 3 sized warehouses; COPY + Snowpipe + Snowpipe Streaming + Iceberg; Streams + Tasks + Dynamic Tables + Zero-Copy Clone; functional + access roles + tag-based masking; Query Profile audits + Resource Monitors; Snowpark procedure + Data Share; SnowPro Core + Advanced DE certs passed.
