# IDP v2 — Epic 8 Pilot · Reliability Engineering and Performance

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's pipeline reliability + performance discipline — failure-mode taxonomies, DLQ + replay infrastructure, query optimization with measurable cost-delta, scaling + capacity decisions, and HA/DR strategy. They've shipped the quarantine + replay tool and led at least one DR drill.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 8.1 — Engineer Failure-Handling & Recovery

> **What "Senior at this Skill" means.** A Senior here can name the failure modes (transient / persistent / partial / silent) before they happen, has shipped the quarantine + replay tool the team uses to recover from data poisoning, and runs the occasional chaos drill to verify the recovery story isn't just on paper.

### Sub-skill 8.1.1: Define the team's failure-mode taxonomy + idempotency discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/failure-modes.md` with the team's taxonomy — transient (network blip, rate-limit, transient API 500), persistent (auth revoked, source schema breaking change), partial (some records succeed, some fail), silent (data shape wrong but pipeline succeeded). Cross-link to idempotency discipline (1.3.4) — show how `idempotency + at-least-once = exactly-once` plays out in real pipelines.

**Skill progression by level:**
- [ ] **Junior** — Recognize that pipelines fail in different ways.
- [ ] **Mid** — Apply retries for transient failures; escalate persistent.
- [ ] **🎯 Senior (TARGET)** — Define the team's failure-mode taxonomy; use it in design reviews to ask "which class of failure does this code handle?"; mentor mid-level engineers on silent-failure detection (the hardest class).
- [ ] **Staff** — Architect platform-level failure taxonomies + automated classification.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 8.1.2: Engineer quarantine + replay tooling

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer the Lab quarantine pattern — a `_quarantine` schema where DLQ records land — and a Python CLI replay tool (`lab/tools/replay.py`) that lists, inspects, edits, and replays quarantined records back into the pipeline. Author `docs/runbooks/quarantine-replay.md` covering the workflow + the team's policy for when records get quarantined vs dropped vs retried.

**Skill progression by level:**
- [ ] **Junior** — Recognize quarantine and DLQ as concepts.
- [ ] **Mid** — Apply a basic DLQ pattern under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the canonical quarantine + replay tool; document the workflow + policy; review pipeline PRs for missing DLQ.
- [ ] **Staff** — Architect cross-pipeline DLQ infrastructure with shared inspection/replay UI.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 8.1.3: Own chaos-engineering drills for pipelines

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/pipeline-chaos.md` covering chaos-engineering principles applied to data pipelines (kill a random pod mid-DAG, simulate a source-API timeout, drop a Kafka partition), with the team's drill cadence (quarterly Game Day). Execute 1 chaos drill in the Lab and publish the report in `docs/chaos/drill-2026Q3.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize chaos engineering as a concept.
- [ ] **Mid** — Apply existing chaos tooling during a drill.
- [ ] **🎯 Senior (TARGET)** — Own the team's drill cadence; design and execute 1 chaos drill; document lessons; mentor mid-level engineers on resilience-testing.
- [ ] **Staff** — Architect platform-level chaos infrastructure (chaos-as-code, automated weekly drills).
- [ ] **Principal** — Govern org-wide chaos-engineering program.

---

## Story 8.2 — Optimize Queries

> **What "Senior at this Skill" means.** A Senior here finds the team's most expensive queries and fixes them — with documented cost-delta. They've shipped a top-10 optimization report and the team's audit methodology for catching future regressions.

### Sub-skill 8.2.1: Engineer query-cost optimization with measurable delta

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/query-cost-optimization.md` covering the 5 most-common cost drivers (full scans, exploded joins, frequent refreshes, missing partition pruning, oversized result sets) and the canonical fixes for each. Apply top-10 query optimization in the Lab and publish the cost-delta report at `docs/perf/2026Q2.md` with before/after slot-ms or `bytes_billed`.

**Skill progression by level:**
- [ ] **Junior** — Recognize that queries have cost.
- [ ] **Mid** — Apply basic optimization (partition filters, LIMIT pushdown).
- [ ] **🎯 Senior (TARGET)** — Engineer top-10 optimization with measured delta; document the methodology; review PRs for cost-killers.
- [ ] **Staff** — Architect platform-level cost-regression detection + continuous optimization.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 8.2.2: Own incremental-model + lookback-window discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/incremental-models.md` covering dbt incremental strategies (append, merge, delete+insert, insert_overwrite per warehouse), lookback-window patterns (3-day lookback for late-arriving data), and the failure modes (gaps, duplicates, expensive backfills). Document the team's "when incremental beats full-refresh" decision rule.

**Skill progression by level:**
- [ ] **Junior** — Recognize incremental vs full-refresh as alternatives.
- [ ] **Mid** — Apply incremental models with a lookback window.
- [ ] **🎯 Senior (TARGET)** — Own the team's incremental discipline; review PRs for missing lookback or wrong strategy; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-domain incremental-model conventions.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 8.2.3: Engineer approximate-algorithm adoption (HLL, t-digest)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/approximate-aggregations.md` covering when approximate algorithms (HyperLogLog for distinct count, t-digest for quantiles) deliver 10×+ cost reduction with acceptable accuracy. Document the decision rule + concrete Lab examples comparing `COUNT(DISTINCT)` vs `APPROX_COUNT_DISTINCT` with measured cost-delta. (Cross-ref Epic 1.5.3 — the foundational understanding.)

**Skill progression by level:**
- [ ] **Junior** — Recognize approximate functions exist.
- [ ] **Mid** — Apply `APPROX_COUNT_DISTINCT` in queries.
- [ ] **🎯 Senior (TARGET)** — Engineer the adoption decision; ship Lab examples with cost-delta; review PRs that could benefit from approximation.
- [ ] **Staff** — Architect cross-pipeline approximation infrastructure (shared HLL sketches across rollups).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 8.3 — Engineer Scaling & Capacity

> **What "Senior at this Skill" means.** A Senior here knows when vertical scaling beats horizontal (and vice versa), can engineer auto-scaling at the K8s + warehouse level, and has shipped HPA on the team's Airflow workers.

### Sub-skill 8.3.1: Define vertical vs horizontal scaling + sharding decisions

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/scaling-decisions.md` covering when vertical scaling wins (single-node memory-bound work, OLTP), when horizontal wins (analytics, embarrassingly parallel), and the role of sharding/partitioning as the scaling-out mechanism (cross-ref 1.3.5). Document the team's decision rule + 3 worked Lab examples.

**Skill progression by level:**
- [ ] **Junior** — Recognize vertical vs horizontal scaling.
- [ ] **Mid** — Apply existing scaling configuration to new workloads.
- [ ] **🎯 Senior (TARGET)** — Define the team's scaling-decision framework; review architecture for misapplied scaling strategy.
- [ ] **Staff** — Architect platform-wide scaling infrastructure (auto-scaling fleets, capacity planning).
- [ ] **Principal** — Govern org-wide capacity-planning + cost-allocation.

---

### Sub-skill 8.3.2: Engineer autoscaling (HPA, VPA, cluster autoscaler)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/k8s-autoscaling.md` covering HPA (horizontal pod autoscaling on CPU / memory / custom metrics), VPA (vertical pod autoscaling), and the cluster autoscaler. Engineer HPA in the Lab for Airflow Celery workers scaling on queue size, with versioned manifest + tested scale-up/down behavior.

**Skill progression by level:**
- [ ] **Junior** — Recognize K8s autoscaling as a concept.
- [ ] **Mid** — Apply existing HPA configuration.
- [ ] **🎯 Senior (TARGET)** — Engineer HPA in the Lab; tune thresholds; mentor mid-level engineers on stable autoscaling (no thrashing).
- [ ] **Staff** — Architect platform-level autoscaling patterns + cost guardrails.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 8.4 — Architect HA & Disaster Recovery

> **What "Senior at this Skill" means.** A Senior here owns the team's RPO/RTO discipline, backup strategy, and at least one rehearsed DR drill that proved recovery works in practice — not just on paper.

### Sub-skill 8.4.1: Define RPO/RTO + backup strategy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/rpo-rto-backup.md` covering RPO (Recovery Point Objective — how much data loss is acceptable) vs RTO (Recovery Time Objective — how long until restored) per service class, backup strategies (full, incremental, differential, PITR for databases), and the team's backup matrix (system × frequency × retention × restore-time). Engineer automated Postgres backup for the Lab with cron + S3 destination.

**Skill progression by level:**
- [ ] **Junior** — Recognize RPO and RTO as concepts.
- [ ] **Mid** — Apply existing backup conventions; verify backups exist.
- [ ] **🎯 Senior (TARGET)** — Define the RPO/RTO matrix + ship the Lab backup automation; review system designs for backup adequacy.
- [ ] **Staff** — Architect platform-wide backup infrastructure with automated verification.
- [ ] **Principal** — Govern org-wide backup + retention policy.

---

### Sub-skill 8.4.2: Engineer cross-region replication

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cross-region-replication.md` covering BigQuery multi-region semantics, S3 Cross-Region Replication (CRR), Postgres read replicas across regions, and the cost-vs-availability trade-offs. Document the team's replication policy per service class.

**Skill progression by level:**
- [ ] **Junior** — Recognize cross-region replication as an HA pattern.
- [ ] **Mid** — Apply existing replication configurations.
- [ ] **🎯 Senior (TARGET)** — Define the team's replication policy; review system designs for HA coverage; understand the cost-delta of multi-region.
- [ ] **Staff** — Architect platform-level multi-region strategy (active-active, active-passive patterns).
- [ ] **Principal** — Govern org-wide multi-region + DR strategy with stakeholder alignment.

---

### Sub-skill 8.4.3: Lead rehearsed DR drills (restore exercise + runbook validation)

**Target:** `Senior → Staff`

**Activity & Artifact (Senior DoD):** Author `docs/runbooks/dr-drill-procedure.md` covering the team's DR drill protocol — what to restore, what to verify, what to time. Conduct 1 simulated DR drill in the Lab restoring the Postgres backup into a fresh instance and verifying data integrity + downstream pipelines. Publish results in `docs/runbooks/dr-drill-2026Q3.md` including the runbook gaps found.

**Skill progression by level:**
- [ ] **Junior** — Recognize that DR plans need rehearsal.
- [ ] **Mid** — Apply a DR procedure during a guided drill.
- [ ] **🎯 Senior (TARGET)** — Lead 1 DR drill end-to-end + publish results + update runbooks based on gaps found.
- [ ] **Staff** — Architect cross-system DR drills + automated quarterly cadence.
- [ ] **Principal** — Govern org-wide DR drill program with executive reporting.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 4 Story-level 🎯 boxes are ticked** — which requires the 11 sub-skill 🎯 Senior boxes. Mastery evidence: failure-mode taxonomy, quarantine + replay tool, 1 chaos drill report, top-10 query optimization report with cost-delta, incremental-model discipline, approximate-algorithm adoption, HPA configuration, RPO/RTO backup matrix, 1 DR drill report.
