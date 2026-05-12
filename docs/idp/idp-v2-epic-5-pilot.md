# IDP v2 — Epic 5 Pilot · Orchestration

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns how the team's pipelines are scheduled, isolated, and recovered. They define the DAG-authoring pattern (factory + TaskFlow + Asset-driven), the resilience discipline (retries, alerting hierarchy, SLA catalog), the advanced orchestration patterns (dynamic mapping, event-driven), and the orchestrator-choice decision. They've shipped the team's DAG factory and event-driven POC. (Deep Airflow mastery lives separately in Epic 23.)
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 5.1 — Own the Team's DAG-Authoring Pattern

> **What "Senior at this Skill" means.** A Senior here defines how every DAG in the team is written — factory-generated from YAML, declared via TaskFlow + Asset scheduling, isolating heavy work via KubernetesPodOperator. They've shipped the canonical factory + the operator-usage patterns that the rest of the team forks from.

### Sub-skill 5.1.1: Engineer the team's DAG-factory pattern (TaskFlow + factories)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dag-factory.md` covering Airflow fundamentals (DAG, Operator, Task, Sensor, Hook, XCom) at a reference level + the team's declarative DAG-factory pattern (TaskFlow API + YAML/Python-config-driven generation). Engineer the Lab DAG factory generating ≥10 DAGs from YAML. Review tap PRs for factory conformance.

**Skill progression by level:**
- [ ] **Junior** — Recognize Airflow's core abstractions (DAG, Operator, Task).
- [ ] **Mid** — Apply hand-written DAGs with TaskFlow.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's DAG factory; review PRs for factory conformance; mentor mid-level engineers on TaskFlow idioms.
- [ ] **Staff** — Architect cross-team factory tooling (shared library, plugin system).
- [ ] **Principal** — Govern org-wide orchestration patterns and migration strategy.

---

### Sub-skill 5.1.2: Design executor + KubernetesPodOperator usage

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-executors.md` comparing executors (Sequential, Local, Celery, KubernetesExecutor, Celery+K8s hybrid) and `docs/notes/k8s-pod-operator.md` covering KubernetesPodOperator usage — when its cold-start overhead is worth the isolation gain (heavy Spark jobs, polyglot tooling, isolated resource limits). Apply KubernetesPodOperator in the Lab to isolate 1 Spark job with versioned manifest.

**Skill progression by level:**
- [ ] **Junior** — Recognize the executor concept; identify which is in use.
- [ ] **Mid** — Apply KubernetesPodOperator with default config.
- [ ] **🎯 Senior (TARGET)** — Design the team's executor choice + KPO usage policy; review PRs for over- or under-isolation.
- [ ] **Staff** — Architect cross-cluster executor strategy (e.g., dedicated pools per workload class).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 5.1.3: Engineer Asset/Dataset-driven scheduling (Airflow 3.x)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/asset-driven-scheduling.md` covering Airflow 3.x Asset/Dataset scheduling logic (OR vs AND scheduling, asset lineage, producer/consumer model). Apply Asset-driven scheduling in the Lab where producers emit and consumers react automatically.

**Skill progression by level:**
- [ ] **Junior** — Recognize Asset/Dataset scheduling as an alternative to cron.
- [ ] **Mid** — Apply Asset-driven DAGs with default config.
- [ ] **🎯 Senior (TARGET)** — Engineer Asset-driven scheduling across producer/consumer DAGs; document the team's pattern; review PRs for incorrect Asset declarations.
- [ ] **Staff** — Architect Asset-driven scheduling as the platform default with cross-team Asset lineage visibility.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 5.2 — Engineer Orchestrator Resilience & SLA

> **What "Senior at this Skill" means.** A Senior here owns the team's pipeline-resilience discipline — retry strategy, alerting hierarchy with fatigue management, deadline-based SLAs, pool/concurrency tuning. They've shipped the canonical alerting and the SLA catalog that codifies team expectations.

### Sub-skill 5.2.1: Engineer retry + circuit-breaker discipline at the DAG level

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-retry.md` covering retry strategies (linear, exponential, custom callable), retry exhaustion handling, and the team's policy: which task types deserve retries, which fail-fast. Document the integration with the circuit-breaker pattern (cross-ref to sub-skill 1.3.4) for upstream protection.

**Skill progression by level:**
- [ ] **Junior** — Recognize that tasks have retry configuration.
- [ ] **Mid** — Apply exponential backoff + jitter retries to tasks.
- [ ] **🎯 Senior (TARGET)** — Define the team's retry-discipline policy; review PRs for missing or excessive retries; mentor on retry-storms.
- [ ] **Staff** — Architect cross-DAG resilience patterns (e.g., circuit-breaker across upstream/downstream).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 5.2.2: Define alerting hierarchy + fatigue management

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/alerting-hierarchy.md` defining the team's P0–P3 severity tiers, escalation chain, and fatigue-management policy (alert grouping, deduplication, snooze, post-incident alert tuning). Engineer P0–P3 alerting in the Lab via Slack webhook with deduplication + on-call routing.

**Skill progression by level:**
- [ ] **Junior** — Recognize severity tiers as a concept.
- [ ] **Mid** — Apply existing alerting rules; create a basic alert.
- [ ] **🎯 Senior (TARGET)** — Define the hierarchy + ship the Lab alerting; review alert configs for fatigue risk.
- [ ] **Staff** — Architect cross-team alerting infrastructure (PagerDuty/Opsgenie integration, intelligent routing).
- [ ] **Principal** — Govern org-wide alerting policy + on-call rotation.

---

### Sub-skill 5.2.3: Define SLA catalog + deadline-based patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/sla-catalog.md` defining the team's SLA per pipeline (P0 marts: < 6 hr freshness; P1: < 24 hr; P2: best-effort) and the Airflow `deadline` callback usage that fires alerts when SLA is at risk before the run completes. Document pools, concurrency, and priority-weight tuning for SLA preservation.

**Skill progression by level:**
- [ ] **Junior** — Recognize SLA as a concept.
- [ ] **Mid** — Apply existing SLA conventions to new pipelines.
- [ ] **🎯 Senior (TARGET)** — Define the team's SLA catalog + deadline patterns + pool/concurrency tuning; review SLA assignments for accuracy.
- [ ] **Staff** — Architect cross-team SLA management with shared infrastructure (priority queues, surge capacity).
- [ ] **Principal** — Govern org-wide SLA policy at the data-product level.

---

## Story 5.3 — Architect Advanced Orchestration (Dynamic, Event-Driven)

> **What "Senior at this Skill" means.** A Senior here designs the team's dynamic and event-driven patterns — dynamic task mapping for variable workloads, webhook-triggered scheduling, branching logic. They've shipped both pattern types in the Lab as references.

### Sub-skill 5.3.1: Engineer dynamic task mapping for variable workloads

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dynamic-task-mapping.md` covering Airflow 2.3+ dynamic task mapping (`expand`, `expand_kwargs`, `partial`), use cases (fan-out over a discovered list, parallel processing of variable file sets), and limitations. Engineer a dynamic DAG in the Lab that fans out over a list of taps with documented ADR.

**Skill progression by level:**
- [ ] **Junior** — Recognize dynamic task mapping by example.
- [ ] **Mid** — Apply `expand` on a known list.
- [ ] **🎯 Senior (TARGET)** — Engineer the canonical dynamic-mapping pattern; mentor mid-level engineers; review PRs for over-use vs under-use.
- [ ] **Staff** — Architect dynamic-mapping patterns at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 5.3.2: Design event-driven scheduling patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/event-driven-scheduling.md` covering Airflow Datasets + Assets, external sensors, and webhook-triggered DAGs (via REST API + FastAPI receiver). Engineer an event-driven POC in the Lab: webhook → FastAPI receiver → Dataset event → DAG consumer.

**Skill progression by level:**
- [ ] **Junior** — Recognize event-driven as different from cron.
- [ ] **Mid** — Apply Dataset scheduling under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the canonical event-driven POC; document when event-driven beats cron; mentor on the pattern.
- [ ] **Staff** — Architect event-driven orchestration at platform scale (event bus, replay support).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 5.3.3: Own branching + short-circuit operator usage

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/branching-short-circuit.md` covering branching and short-circuit operators (`BranchPythonOperator`, `ShortCircuitOperator`, trigger rules), use cases, and common bugs (trigger-rule mismatches, downstream skipping). Document the team's idioms for conditional pipeline flow.

**Skill progression by level:**
- [ ] **Junior** — Recognize branching operators by name.
- [ ] **Mid** — Apply branching with default trigger rules.
- [ ] **🎯 Senior (TARGET)** — Own the team's branching idioms; review PRs for trigger-rule correctness; mentor mid-level engineers on conditional flow.
- [ ] **Staff** — Architect conditional-flow tooling at platform scale (visual flow editors).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 5.4 — Evaluate Orchestration Alternatives

> **What "Senior at this Skill" means.** A Senior here can defend the team's Airflow choice by evaluating Dagster + Prefect (head-to-head), and recognizing the niche fits for Argo + NiFi + Mage + Temporal. They've shipped at least one alternative-orchestrator POC.

### Sub-skill 5.4.1: Compare Dagster + Prefect as Airflow alternatives

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-vs-dagster-vs-prefect.md` comparing Dagster (software-defined assets, op vs job, type checks, modern dev UX), Prefect 2.x (flows + tasks runtime, hybrid execution model), and Airflow on the same workload. Apply the same pipeline in Airflow AND Dagster in the Lab on `compare-orchestrators` branch with a comparative ADR.

**Skill progression by level:**
- [ ] **Junior** — Recognize Dagster and Prefect by name.
- [ ] **Mid** — Apply Dagster or Prefect for a simple pipeline.
- [ ] **🎯 Senior (TARGET)** — Engineer the comparison + ADR; defend the team's Airflow choice with concrete trade-offs.
- [ ] **Staff** — Architect platform-level orchestrator selection / migration strategy.
- [ ] **Principal** — Govern org-wide orchestrator strategy.

---

### Sub-skill 5.4.2: Evaluate Argo / NiFi / Mage / Temporal niche fits

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/niche-orchestrators.md` covering Argo Workflows (K8s-native YAML), Apache NiFi (visual data flow), Mage (notebook-style), and Temporal.io (durable stateful workflows — cross-ref Epic 9.5). Document when each niche tool beats Airflow. Apply 1 NiFi flow in the Lab as a reference (visual flow → Kafka).

**Skill progression by level:**
- [ ] **Junior** — Recognize the niche tools by name.
- [ ] **Mid** — Apply one of them under guidance.
- [ ] **🎯 Senior (TARGET)** — Evaluate the niche fits; ship a NiFi flow POC; recommend per use case.
- [ ] **Staff** — Architect niche-tool adoption with clear scope (e.g., "Temporal for long-running stateful, Airflow for everything else").
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 5.5 — Engineer Python for Orchestration

> **What "Senior at this Skill" means.** A Senior here writes pipeline Python with the rigor of production application code — typed, packaged, tested. They've shipped the team's DAG-integrity tests and the internal `include/` library that the rest of the team imports from.

### Sub-skill 5.5.1: Engineer DAG testing discipline (parse-time, integrity, mocked)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dag-testing.md` covering parse-time tests (no syntax errors, no cycles, naming conventions, ownership), unit tests via mocked operators, integration tests via `astro dev`. Engineer the Lab DAG integrity tests in `tests/test_dag_integrity.py` running in CI with green status.

**Skill progression by level:**
- [ ] **Junior** — Recognize that DAGs can be tested.
- [ ] **Mid** — Apply parse-time tests under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's integrity test suite; integrate into CI; review PRs for missing tests; mentor on testing patterns.
- [ ] **Staff** — Architect cross-team DAG-testing infrastructure (shared CI, conformance enforcement).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 5.5.2: Own type discipline + internal packaging for pipeline code

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/pipeline-python-discipline.md` covering type hints + mypy strict, Pydantic models for DAG params + config, and the structure of an internal `include/` library (factories, utilities, callbacks, config). Apply the discipline across the Lab's `airflow/dags/include/` with a published version + tests.

**Skill progression by level:**
- [ ] **Junior** — Recognize type hints in Python code.
- [ ] **Mid** — Apply type hints to function signatures.
- [ ] **🎯 Senior (TARGET)** — Own the team's pipeline-Python rigor; engineer the `include/` library structure; mentor on Pydantic + mypy strict.
- [ ] **Staff** — Architect cross-team Python package infrastructure (shared libraries, publish to internal PyPI).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 5 Story-level 🎯 boxes are ticked** — which requires the 13 sub-skill 🎯 Senior boxes. Mastery evidence: the DAG factory, the SLA catalog, the dynamic + event-driven POCs, the Airflow vs Dagster comparison ADR, the NiFi flow, and the DAG integrity test suite. Deeper Airflow mastery (internals, providers ecosystem, production deployment) lives in Epic 23.
