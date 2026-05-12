# IDP v2 — Epic 23 Pilot · Airflow — Operation and Deep Engineering

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's Airflow deployment end-to-end — internals, advanced authoring (Assets, dynamic mapping, deferrable operators), providers, production operation (Helm + secrets + RBAC + metrics), DAG CI/CD, and the Airflow-vs-Dagster/Prefect trade-off call. They've passed **Astronomer Fundamentals** and **Operator** certs. (Complements Epic 5 — Orchestration discipline — with Airflow-specific depth.)
>
> **Bibliography.** *Data Pipelines with Apache Airflow* 2nd ed. (Harenslak & de Ruiter) · *Apache Airflow Best Practices* (Intorf) · Apache Airflow docs · Astronomer Academy + blog · Airflow Summit talks.
>
> **Exam objectives — Astronomer Fundamentals.** Concepts & architecture · DAG authoring basics · Operator + TaskFlow patterns · Variables, connections, XComs.
>
> **Exam objectives — Astronomer Operator.** Production deployments · Performance tuning · Multi-tenancy + security · Monitoring + alerting · DR.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered AND both certs passed.

---

## Story 23.1 — Understand Airflow Architecture & Internals

### Sub-skill 23.1.1: Define Airflow components, executor architecture, and the Triggerer

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-architecture.md` covering core components (Scheduler, Webserver, Triggerer, Workers, Metastore DB) with architecture diagram, DAG run lifecycle (queued → running → success/failed) as a state machine, Scheduler internals (DAG parsing, scheduling loop, mini-scheduler — bottlenecks to look for), Executor architecture (Local, Sequential, Celery, Kubernetes, Celery+K8s — selection criteria), and the Triggerer (deferrable operators, async waiting without a worker slot — with 3 cases where it shines).

**Skill progression by level:**
- [ ] **Junior** — Recognize Airflow as an orchestrator.
- [ ] **Mid** — Apply existing Airflow DAGs; recognize Scheduler vs Worker.
- [ ] **🎯 Senior (TARGET)** — Define the executor + Triggerer model; select the right executor per workload; mentor mid-level engineers on deferrable operators.
- [ ] **Staff** — Architect cross-team Airflow deployment standards.
- [ ] **Principal** — Govern org-wide orchestration runtime policy.

---

### Sub-skill 23.1.2: Engineer the full Airflow 3.x stack (Scheduler + Triggerer + KubernetesExecutor) in the Lab

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-internals.md` covering the Metastore schema (DAG, dag_run, task_instance, xcom, log — with debug queries), plugins architecture, and the REST API (2.x stable contract + automation recipes). Engineer the complete Airflow 3.x stack in the Lab via Helm chart + manifests (Scheduler + Triggerer + KubernetesExecutor).

**Skill progression by level:**
- [ ] **Junior** — Recognize the Airflow Metastore exists.
- [ ] **Mid** — Apply existing Airflow deployments.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Airflow 3.x stack; write debug queries against the Metastore; mentor mid-level engineers on the REST API.
- [ ] **Staff** — Architect cross-team Airflow infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 23.2 — Author Advanced DAGs

### Sub-skill 23.2.1: Engineer TaskFlow + dynamic task mapping + DAG factories

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-dag-authoring.md` covering TaskFlow API (decorator-based, type hints, automatic XCom — with recipes), dynamic task mapping (`expand`, `expand_kwargs`, partial — with 5 patterns), SubDAGs vs TaskGroups (and why SubDAGs are deprecated), Sensors vs Deferrable Operators (poke vs reschedule vs defer trade-offs), Branching + Trigger Rules (5 scenarios), XCom custom backend (S3/GCS, custom serializers — when > default), DAG documentation (doc_md, params with description, OpenLineage), and params with pydantic models (Airflow 2.6+). Engineer a DAG factory + dynamic task mapping in the Lab generating 10 DAGs.

**Skill progression by level:**
- [ ] **Junior** — Recognize TaskFlow syntax.
- [ ] **Mid** — Apply TaskFlow + basic dynamic mapping.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab DAG factory + dynamic mapping; mentor mid-level engineers on poke-vs-reschedule-vs-defer.
- [ ] **Staff** — Architect cross-team DAG authoring standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 23.2.2: Engineer Assets / Datasets scheduling (Airflow 2.4+ / 3.x migration)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-assets.md` covering Datasets / Assets scheduling (Airflow 2.4+ / 3.x — OR/AND logic), and the Airflow 3.x Assets model (consolidating Datasets) with the 2.x → 3.x migration path. Engineer Assets scheduling in the Lab (Airflow 3.x) with producer + consumer DAGs.

**Skill progression by level:**
- [ ] **Junior** — Recognize Datasets / Assets as a scheduling primitive.
- [ ] **Mid** — Apply existing Asset-scheduled DAGs.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Asset pipeline; document the 2.x → 3.x migration; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team Asset-based scheduling strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 23.3 — Operate the Airflow Providers Ecosystem

### Sub-skill 23.3.1: Operate the main cloud + data providers (Kubernetes, AWS, Google, Snowflake, Databricks, Spark, Kafka, dbt)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-providers.md` covering canonical operators for `providers-cncf-kubernetes` (KubernetesPodOperator, KubernetesExecutor), `providers-amazon` (S3, Glue, EMR, Redshift, Athena, SNS, SQS), `providers-google` (BigQuery, GCS, Dataflow, Dataproc, Composer), `providers-snowflake` (cross-ref Epic 22), `providers-databricks` (cross-ref Epic 21), `providers-dbt-cloud` (cross-ref Epic 24), `providers-apache-spark` + `apache-livy`, and `providers-apache-kafka`. Engineer 3 providers in the Lab — one end-to-end DAG per cloud (AWS + GCP + Databricks/Snowflake).

**Skill progression by level:**
- [ ] **Junior** — Recognize Airflow providers as installable plugins.
- [ ] **Mid** — Apply existing provider operators.
- [ ] **🎯 Senior (TARGET)** — Operate the team's main providers; engineer the Lab cross-cloud DAGs; mentor mid-level engineers on provider operator selection.
- [ ] **Staff** — Architect cross-team provider standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 23.3.2: Engineer a custom Airflow provider

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/custom-airflow-provider.md` covering the recipe to build a custom provider (entry-point structure, hook + operator patterns, packaging, tests). Engineer a custom provider in the Lab (repo + tests + publish).

**Skill progression by level:**
- [ ] **Junior** — Recognize the existence of custom providers.
- [ ] **Mid** — Apply existing custom hooks.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab custom provider end-to-end; mentor mid-level engineers on hook/operator separation.
- [ ] **Staff** — Architect cross-team custom-provider strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 23.4 — Operate Airflow in Production

### Sub-skill 23.4.1: Engineer Airflow on Kubernetes (Helm, Postgres, Scheduler tuning, multi-tenancy, secrets)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-production.md` covering deployment patterns (Astronomer Cloud, MWAA, Composer, self-managed comparison), Airflow on Kubernetes via Helm chart (official Apache + Astronomer — canonical setup), Scheduler tuning (`parsing_processes`, `dag_dir_list_interval`, `scheduler_idle_sleep_time`), Postgres metastore tuning (pool, connection limits, vacuum), multi-tenancy (Roles + permissions, fine-grained DAG-level access), and secrets backends (AWS Secrets Manager, GCP Secret Manager, Vault, K8s Secrets). Engineer the Lab deployment via Helm chart + Postgres backend + Airflow RBAC + Vault secrets backend.

**Skill progression by level:**
- [ ] **Junior** — Recognize Airflow runs on Kubernetes.
- [ ] **Mid** — Apply existing Helm-deployed Airflow.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab production stack (Helm + Postgres + RBAC + secrets); mentor mid-level engineers on Scheduler tuning.
- [ ] **Staff** — Architect cross-team Airflow production strategy.
- [ ] **Principal** — Govern org-wide orchestration platform policy.

---

### Sub-skill 23.4.2: Engineer Airflow observability (log centralization, metrics, OpenTelemetry, REST API)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-observability.md` covering log centralization (S3, GCS, Elasticsearch), metrics export (statsd, OpenTelemetry, Prometheus exporter), and Airflow REST API + JWT auth for automation. Engineer log centralization + Prometheus metrics in the Lab + a Grafana dashboard.

**Skill progression by level:**
- [ ] **Junior** — Recognize Airflow logs exist.
- [ ] **Mid** — Apply existing log + metrics setup.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab log centralization + metrics dashboard; mentor mid-level engineers on REST API automation.
- [ ] **Staff** — Architect cross-team Airflow observability strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 23.5 — Engineer Testing & CI/CD for DAGs

### Sub-skill 23.5.1: Engineer DAG integrity tests + unit tests + deployment pipeline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/airflow-testing-cicd.md` covering DAG integrity tests (parse time, no cycles, naming conventions, ownership), unit testing of operators (DAG context mocked), integration testing with Astronomer's `astro dev`, the `pytest-airflow` plugin, and DAG versioning + deployment CI/CD pipeline. Engineer DAG integrity + unit tests in the Lab CI + a DAG deployment pipeline.

**Skill progression by level:**
- [ ] **Junior** — Recognize DAG tests as a concept.
- [ ] **Mid** — Apply existing parse-time integrity tests.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab DAG CI/CD pipeline; mentor mid-level engineers on operator unit testing.
- [ ] **Staff** — Architect cross-team DAG CI/CD standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 23.6 — Evaluate Orchestrator Alternatives, Pass Astronomer Certs

### Sub-skill 23.6.1: Define Airflow vs Dagster vs Prefect vs Mage/Kestra vs cloud-native trade-offs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/orchestrator-comparison.md` covering Airflow vs Dagster (software-defined assets vs DAGs), Airflow vs Prefect 2.x (dynamic workflows), Airflow vs Mage / Kestra, and when to use Airflow vs cloud-native (Step Functions, Workflows, Data Factory) — with a flowchart. Engineer the same pipeline in Airflow AND Dagster in the Lab on a `compare-orchestrators` branch + ADR (cross-ref Epic 5).

**Skill progression by level:**
- [ ] **Junior** — Recognize Airflow + Dagster + Prefect as alternatives.
- [ ] **Mid** — Apply existing Airflow; recognize Dagster.
- [ ] **🎯 Senior (TARGET)** — Define the orchestrator trade-off; ship the Lab parallel implementation + ADR; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team orchestrator strategy.
- [ ] **Principal** — Govern org-wide orchestration policy.

---

### Sub-skill 23.6.2: Pass Astronomer Airflow Fundamentals + Operator certs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Complete Astronomer Academy Fundamentals + Operator learning paths, take 3 practice exams per cert (≥85% before sitting), pass both. Publish `docs/certs/astronomer.md` retrospective.

**Skill progression by level:**
- [ ] **Junior** — *(out of natural progression for this sub-skill)*
- [ ] **Mid** — Apply Airflow daily.
- [ ] **🎯 Senior (TARGET)** — Pass Astronomer Fundamentals + Operator; publish retrospective; mentor mid-level engineers preparing.
- [ ] **Staff** — *(out of natural progression for this sub-skill)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 6 Story-level 🎯 boxes are ticked** — which requires 10 sub-skill 🎯 boxes including both Astronomer certs. Mastery evidence: Airflow 3.x Lab stack (Helm + Postgres + Triggerer + KubernetesExecutor); DAG factory + dynamic mapping + Assets; 3 cloud providers + 1 custom provider; production RBAC + Vault + log centralization + Prometheus dashboard; DAG CI/CD pipeline; orchestrator comparison ADR with Dagster parallel implementation; Astronomer Fundamentals + Operator passed.
