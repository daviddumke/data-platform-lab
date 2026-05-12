# IDP v2 — Epic 17 Pilot · Distributed Big Data Processing

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills can pick Spark (or its alternatives) deliberately, size clusters from first principles, read a Spark UI to diagnose slowness, and engineer skew-handling that produces a measured runtime delta. They've shipped a PySpark POC and at least one optimization with before/after evidence.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 17.1 — Understand Spark Fundamentals

> **What "Senior at this Skill" means.** A Senior here understands what happens inside Spark when a query runs — Catalyst plans, Tungsten execution, AQE adaptation — and can read a Spark UI like a query plan.

### Sub-skill 17.1.1: Define the Spark execution model (RDD / DataFrame / Dataset, lazy evaluation, actions vs transformations)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/spark-execution-model.md` covering RDD vs DataFrame vs Dataset (when each fits), lazy evaluation + DAG construction, actions vs transformations (and why `count()` is cheap on cached DFs but expensive otherwise), and narrow vs wide transformations. Include the mental model a Senior uses to predict shuffle behavior from code.

**Skill progression by level:**
- [ ] **Junior** — Recognize Spark as a distributed engine.
- [ ] **Mid** — Apply DataFrame API for transformations; understand lazy evaluation at a high level.
- [ ] **🎯 Senior (TARGET)** — Define the execution model; predict shuffle behavior from code shape; mentor mid-level engineers on lazy-evaluation traps.
- [ ] **Staff** — Architect cross-team Spark adoption + library standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 17.1.2: Define Catalyst optimizer + Tungsten + AQE internals

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/catalyst-tungsten-aqe.md` covering the Catalyst optimizer pipeline (parsed → analyzed → optimized → physical plan), Tungsten (off-heap memory, code generation), and Adaptive Query Execution (3.x features: skew-join handling, dynamic coalescing, dynamic join switching). Document what AQE does NOT fix.

**Skill progression by level:**
- [ ] **Junior** — Recognize Catalyst as Spark's optimizer.
- [ ] **Mid** — Apply Spark queries; trust the optimizer.
- [ ] **🎯 Senior (TARGET)** — Define the Catalyst pipeline and AQE behavior; read `EXPLAIN FORMATTED` output; mentor mid-level engineers on plan-reading.
- [ ] **Staff** — Architect cross-team Spark tuning standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 17.1.3: Define Spark UI reading methodology (stages, shuffle, GC, task skew)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/runbooks/spark-ui-audit.md` defining the Spark UI reading methodology — what to look at first (stage duration distribution, shuffle read/write, GC time, task duration outliers, input/output bytes), what thresholds matter, and how to map a slow stage back to a code line. Demonstrate on 2 Lab Spark jobs.

**Skill progression by level:**
- [ ] **Junior** — Recognize the Spark UI exists.
- [ ] **Mid** — Apply Spark UI to identify a slow stage.
- [ ] **🎯 Senior (TARGET)** — Define the audit methodology; demonstrate on 2 Lab jobs; mentor mid-level engineers through their first Spark UI debugging session.
- [ ] **Staff** — Architect cross-team Spark observability + continuous regression detection.
- [ ] **Principal** — Govern org-wide Spark performance + cost standards.

---

## Story 17.2 — Operate Spark, Databricks & Dataproc

> **What "Senior at this Skill" means.** A Senior here can size a Spark cluster from first principles, run Spark on Kubernetes via the Operator, and pick Databricks vs Dataproc vs self-managed K8s per workload.

### Sub-skill 17.2.1: Analyze cluster sizing (driver, executors, cores, memory, dynamic allocation)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/spark-cluster-sizing.md` covering the canonical formulas (executor memory = container memory × 0.9 − overhead; cores per executor 4-5 sweet spot; partitions = 2-4 × total cores), dynamic allocation tuning, and 3 worked examples sized for different workload shapes (wide shuffle, narrow streaming, broadcast-heavy ETL).

**Skill progression by level:**
- [ ] **Junior** — Recognize cluster sizing matters.
- [ ] **Mid** — Apply existing cluster configurations.
- [ ] **🎯 Senior (TARGET)** — Size clusters from first principles; document the formulas; mentor mid-level engineers on the "5-cores-per-executor" rule and why.
- [ ] **Staff** — Architect cross-team cluster-sizing standards + cost models.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 17.2.2: Engineer a PySpark POC in the Lab

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer a PySpark POC in the Lab processing NYC TLC (or equivalent open dataset >100GB) — a Jupyter/Databricks notebook plus an Airflow DAG submitting the job, partitioning strategy documented, output written as partitioned Parquet. Include a `docs/perf/lab-spark-poc.md` note covering runtime, shuffle volume, and cost.

**Skill progression by level:**
- [ ] **Junior** — Recognize PySpark as the API.
- [ ] **Mid** — Apply PySpark for non-trivial transformations.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab PySpark POC end-to-end (notebook + DAG + perf doc); mentor mid-level engineers on partitioning choices.
- [ ] **Staff** — Architect cross-team Spark adoption standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 17.2.3: Compare Databricks vs Dataproc vs Spark-on-K8s and engineering the K8s option

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/spark-runtime-choice.md` comparing Databricks (managed, Unity Catalog, DLT, Photon), Dataproc (GCE clusters + Serverless), and Spark on Kubernetes via the Spark Operator (self-managed, OSS, full control). Engineer Spark-on-K8s in the Lab with the Spark Operator manifest + a sample job + cost comparison vs Dataproc.

**Skill progression by level:**
- [ ] **Junior** — Recognize Databricks, Dataproc, and K8s as Spark runtimes.
- [ ] **Mid** — Apply existing Spark runtime; recognize Spark Operator as an option.
- [ ] **🎯 Senior (TARGET)** — Engineer Spark-on-K8s in the Lab; document when each runtime wins; mentor mid-level engineers on the trade-off.
- [ ] **Staff** — Architect cross-team Spark runtime strategy.
- [ ] **Principal** — Govern org-wide Spark + lakehouse runtime standards.

---

## Story 17.3 — Optimize Big Data Workloads

> **What "Senior at this Skill" means.** A Senior here can name the 5 most common Big Data performance killers, engineer the fix for each, and measure the delta.

### Sub-skill 17.3.1: Define skew handling (salting, AQE skew-join, broadcast escape)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/spark-skew.md` covering skew detection (Spark UI task-duration distribution + max/median ratio), the canonical fixes (salting the heavy key, AQE skew-join, broadcast escape for tiny-side joins, two-stage aggregation), and worked decision criteria. Engineer skew handling on 1 real Lab job with a `docs/perf/lab-skew-job.md` before/after report (runtime + shuffle bytes + cost).

**Skill progression by level:**
- [ ] **Junior** — Recognize "data skew" as a concept.
- [ ] **Mid** — Apply existing skew-handling recipes.
- [ ] **🎯 Senior (TARGET)** — Define skew handling; engineer the fix on a real Lab job with measured cost-delta; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team skew-detection automation.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 17.3.2: Define partition strategy (repartition vs coalesce, file-size sweet spot, partition pruning)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/spark-partitioning.md` covering repartition (full shuffle) vs coalesce (narrow), the 128MB-1GB file-size sweet spot for Parquet, partition pruning (HMS metadata + Iceberg/Delta stats), partition pruning's failure modes (cast, function calls on partition cols), and `spark.sql.shuffle.partitions` tuning. Apply to 1 Lab job with measured delta.

**Skill progression by level:**
- [ ] **Junior** — Recognize partitioning as a Spark concept.
- [ ] **Mid** — Apply partitioning + recognize repartition vs coalesce.
- [ ] **🎯 Senior (TARGET)** — Define partition strategy; engineer the canonical file-size rule; mentor mid-level engineers on partition pruning failures.
- [ ] **Staff** — Architect cross-team partition strategy (table layout standards).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 17.3.3: Define join algorithms + caching strategies for Big Data

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/spark-joins-cache.md` covering broadcast hash join vs sort-merge join vs shuffled hash join (decision criteria + thresholds), `broadcast()` hint + `spark.sql.autoBroadcastJoinThreshold` tuning, and caching strategies (MEMORY_ONLY, MEMORY_AND_DISK, OFF_HEAP, DISK_ONLY — when each fits). Document anti-patterns (cache once, cache too much, never `unpersist()`).

**Skill progression by level:**
- [ ] **Junior** — Recognize Spark joins exist.
- [ ] **Mid** — Apply broadcast hint when one side is small.
- [ ] **🎯 Senior (TARGET)** — Define join algorithm choice + caching strategy; mentor mid-level engineers on broadcast threshold tuning + cache anti-patterns.
- [ ] **Staff** — Architect cross-team join + cache standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 3 Story-level 🎯 boxes are ticked** — which requires the 9 sub-skill 🎯 Senior boxes. Mastery evidence: Spark execution-model + Catalyst/AQE note + Spark UI audit runbook, cluster-sizing note + PySpark Lab POC + Spark-on-K8s engineered, skew/partition/join optimization notes with at least 1 Lab job optimized with measured cost-delta.
