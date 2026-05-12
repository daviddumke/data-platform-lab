# IDP v2 — Epic 24 Pilot · dbt — Deep Transformation Engineering

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's dbt project end-to-end — modeling, testing (contracts + unit tests), advanced macros, packages, slim CI/CD + data diff, manifest-driven Airflow integration, and dbt Mesh + Semantic Layer. They've passed the **dbt Analytics Engineer** cert. (Complements Epic 4 — SQL/Modeling — and Epic 6 — Testing — with dbt-specific depth.)
>
> **Bibliography.** *Analytics Engineering with SQL and dbt* (Cyr & Dorsey) · *Data Engineering with dbt* (Zagni) · *Fundamentals of Analytics Engineering* (dbt Labs group book) · dbt Labs docs · dbt Discourse + Coalesce talks · "The Modern Data Stack" articles by dbt Labs.
>
> **Exam objectives — dbt Analytics Engineer.** Developing models · Debugging errors · Monitoring pipelines · Implementing tests · Deploying models · Maintaining docs · Promoting through environments · Establishing project + tooling.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered AND the dbt cert passed.

---

## Story 24.1 — Engineer dbt Fundamentals & Modeling

### Sub-skill 24.1.1: Define dbt project structure + materializations + sources + snapshots

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-project-canon.md` covering dbt project structure (models, seeds, snapshots, analyses, macros, tests, docs — canonical layout), `dbt_project.yml` (model paths, on-run-hooks, vars, project-level configs), materializations (view, table, incremental, ephemeral, materialized_view — with selection criteria), sources + source freshness + source overrides, refs + cross-project refs (dbt Mesh), exposures (declaring downstream consumers), snapshots (timestamp vs check strategy, valid_from/valid_to — SCD2 native), the staging/intermediate/marts layering convention (cross-ref Epic 3), and variables + targets + environments (dev/prod isolation). Build a complete dbt project in the Lab with versioned project + green CI.

**Skill progression by level:**
- [ ] **Junior** — Recognize dbt project structure.
- [ ] **Mid** — Apply existing dbt models; understand refs/sources.
- [ ] **🎯 Senior (TARGET)** — Define the team's canonical project structure; ship the Lab project; mentor mid-level engineers on layering + snapshots.
- [ ] **Staff** — Architect cross-team dbt project standards.
- [ ] **Principal** — Govern org-wide analytics-engineering policy.

---

### Sub-skill 24.1.2: Engineer incremental strategies per warehouse (append, merge, delete+insert, insert_overwrite)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-incremental.md` comparing incremental strategies (append, merge, delete+insert, insert_overwrite) per warehouse (BigQuery, Snowflake, Redshift, Postgres). Engineer an incremental model with 4 different strategies in the Lab + benchmark.

**Skill progression by level:**
- [ ] **Junior** — Recognize incremental materialization.
- [ ] **Mid** — Apply existing incremental models.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab 4-strategy comparison; mentor mid-level engineers on strategy choice per warehouse.
- [ ] **Staff** — Architect cross-team incremental standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 24.2 — Engineer dbt Testing (Contracts + Unit Tests)

### Sub-skill 24.2.1: Engineer generic + singular + dbt_expectations tests as the team's quality baseline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-tests.md` covering generic tests + custom generic tests via macros (cross-ref Epic 6), singular tests (SQL queries in `tests/` — 5 canonical patterns), `dbt_utils` test extension (expression_is_true, recency, sequential_values — top 10), `dbt_expectations` (Great Expectations-style assertions — when > generic tests), severity (error vs warn) + thresholds + store_failures, and the `dbt_artifacts` package for queryable test history.

**Skill progression by level:**
- [ ] **Junior** — Recognize generic tests (not_null, unique).
- [ ] **Mid** — Apply existing generic + singular tests.
- [ ] **🎯 Senior (TARGET)** — Define the team's test baseline; mentor mid-level engineers on severity + store_failures.
- [ ] **Staff** — Architect cross-team test standards.
- [ ] **Principal** — Govern org-wide data quality policy.

---

### Sub-skill 24.2.2: Engineer dbt unit tests (1.8+) + contracts as the team's data contract layer

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-unit-tests-contracts.md` covering dbt unit tests (1.8+ — inline fixtures, mocked refs/sources, recipe) and dbt contracts (`contract: enforced: true`, column types, constraints — guarantees). Engineer dbt unit tests on 5 Lab models + dbt contracts on 100% of Lab marts.

**Skill progression by level:**
- [ ] **Junior** — Recognize contracts and unit tests as concepts.
- [ ] **Mid** — Apply existing contracts.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab unit-test + contract coverage; mentor mid-level engineers on fixture design.
- [ ] **Staff** — Architect cross-team contract + unit-test standards.
- [ ] **Principal** — Govern org-wide data contract policy.

---

## Story 24.3 — Author Advanced Macros & Jinja

### Sub-skill 24.3.1: Engineer 5 canonical macros + adapter.dispatch + hooks for the team

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-macros.md` covering Jinja fundamentals (variables, control flow, filters, whitespace control — gotchas), macros (parameters, return values, statement vs print blocks — with 5 canonical macros), `dbt_utils` macros (generate_surrogate_key, pivot, get_column_values, star — top 15), `adapter.dispatch` for cross-database macros, pre-hooks + post-hooks + on-run-start/end (5 use cases), `query_tag` + `query_comment` for observability, and grants management via dbt (post-hook GRANT pattern). Engineer 5 custom macros in the Lab + uses + tests.

**Skill progression by level:**
- [ ] **Junior** — Recognize Jinja and dbt macros.
- [ ] **Mid** — Apply `dbt_utils` macros; write simple custom macros.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's 5 canonical macros; mentor mid-level engineers on `adapter.dispatch` and hooks.
- [ ] **Staff** — Architect cross-team macro libraries.
- [ ] **Principal** — Govern org-wide macro standards.

---

### Sub-skill 24.3.2: Architect custom dbt materializations

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-custom-materializations.md` covering the custom materialization model + when the investment is worth it. Architect a custom materialization in the Lab with docs.

**Skill progression by level:**
- [ ] **Junior** — Recognize built-in materializations.
- [ ] **Mid** — Apply existing materializations.
- [ ] **Senior** — Read custom materialization code; debug failures.
- [ ] **🎯 Staff (TARGET)** — Architect a custom materialization; mentor Senior engineers on materialization internals.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 24.4 — Operate dbt Packages & Ecosystem

### Sub-skill 24.4.1: Operate dbt_utils + dbt_expectations + dbt_external_tables + codegen + dbt_project_evaluator

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-packages.md` covering `dbt_utils` (top utility package — top 20 features), `dbt_expectations` (canonical expectations), `dbt_external_tables` (creating external tables via dbt), `codegen` (generate YAML + SQL boilerplate — recipes), `dbt_artifacts` (run history queryable — observability queries), `dbt_meta_testing` (test coverage of tests + descriptions), and `dbt_project_evaluator` (linter for best practices — rules). Engineer `dbt_project_evaluator` in the Lab CI with a green workflow.

**Skill progression by level:**
- [ ] **Junior** — Recognize `dbt_utils`.
- [ ] **Mid** — Apply `dbt_utils` macros.
- [ ] **🎯 Senior (TARGET)** — Operate the canonical package stack; engineer `dbt_project_evaluator` in CI; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team dbt package strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 24.4.2: Engineer an internal reusable dbt package

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-internal-package.md` covering the recipe to create an internal package (structure, publishing, versioning, distributing internally). Engineer an internal reusable package in the Lab + at least 1 consumer using it.

**Skill progression by level:**
- [ ] **Junior** — Recognize dbt packages exist.
- [ ] **Mid** — Apply existing packages.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab internal package; mentor mid-level engineers on package publishing.
- [ ] **Staff** — Architect cross-team internal-package standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 24.5 — Engineer dbt Operations & Deployment

### Sub-skill 24.5.1: Engineer slim CI + PR-scoped runs + data diff for fast safe deploys

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-slim-ci.md` covering dbt environments (dev, ci, prod) + target separation (`profiles.yml` patterns), slim CI (`--defer --state` — cross-ref Epic 14), PR-scoped CI (running only modified models + downstream), data diff in PRs (Datafold OSS, dbt-checkpoint), `dbt build` vs `dbt run + dbt test` (DAG-aware order trade-offs), and artifact storage (manifest.json, run_results.json — use cases: defer, lineage). Engineer slim CI complete in the Lab via GitHub Actions.

**Skill progression by level:**
- [ ] **Junior** — Recognize dbt CI exists.
- [ ] **Mid** — Apply existing dbt CI.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab slim CI + data diff; mentor mid-level engineers on `--defer --state`.
- [ ] **Staff** — Architect cross-team dbt CI/CD standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 24.5.2: Engineer blue-green deployment + manifest-driven Airflow integration

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-blue-green-airflow.md` covering blue-green deployment of dbt (swap schemas — pattern + cutover) and dbt + Airflow integration patterns (manifest-driven DAG generation — cross-ref Epic 23). Engineer blue-green deployment in the Lab (scripts + ADR) + a manifest-driven Airflow DAG generated from `manifest.json`.

**Skill progression by level:**
- [ ] **Junior** — Recognize blue-green deployment as a concept.
- [ ] **Mid** — Apply existing dbt + Airflow integrations.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab blue-green + manifest-driven DAG; document the ADR; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team dbt deployment strategy.
- [ ] **Principal** — Govern org-wide deployment policy.

---

## Story 24.6 — Architect dbt Cloud, Mesh & Semantic Layer, Pass the Cert

### Sub-skill 24.6.1: Architect dbt Mesh (multi-project + cross-project refs + contracts)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-mesh.md` covering dbt Cloud (IDE, Jobs, Run history, Notifications, dbt Cloud API — vs dbt-core), dbt Mesh (multi-project architecture, cross-project refs, contracts, access modifiers — data mesh applied), and dbt Cloud Discovery API + Explorer (lineage, performance). Engineer 2 dbt projects integrated via dbt Mesh in the Lab with cross-refs + contracts.

**Skill progression by level:**
- [ ] **Junior** — Recognize dbt Cloud and dbt Mesh as concepts.
- [ ] **Mid** — Apply existing dbt Cloud setups.
- [ ] **🎯 Senior (TARGET)** — Architect the Lab dbt Mesh; mentor mid-level engineers on access modifiers + cross-project contracts.
- [ ] **Staff** — Architect cross-team dbt Mesh strategy.
- [ ] **Principal** — Govern org-wide data mesh policy.

---

### Sub-skill 24.6.2: Engineer the dbt Semantic Layer + MetricFlow for headless BI

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-semantic-layer.md` covering dbt Semantic Layer + MetricFlow (declarative metrics, headless BI — architecture). Engineer the dbt Semantic Layer with 5 metrics in the Lab + consumption via Metabase.

**Skill progression by level:**
- [ ] **Junior** — Recognize the Semantic Layer concept.
- [ ] **Mid** — Apply existing metrics definitions.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Semantic Layer + Metabase consumption; mentor mid-level engineers on MetricFlow.
- [ ] **Staff** — Architect cross-team Semantic Layer strategy.
- [ ] **Principal** — Govern org-wide metrics governance.

---

### Sub-skill 24.6.3: Architect dbt-rpc / dbt Server for real-time metric serving

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-rpc-server.md` covering dbt-rpc / dbt Server for serving metrics in real-time — advanced use cases (low-latency BI, app integration).

**Skill progression by level:**
- [ ] **Junior** — Recognize dbt-rpc exists.
- [ ] **Mid** — Apply existing dbt-rpc setups.
- [ ] **Senior** — Read dbt-rpc deployment configs; debug failures.
- [ ] **🎯 Staff (TARGET)** — Architect dbt-rpc / dbt Server adoption; mentor Senior engineers.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 24.6.4: Pass the dbt Analytics Engineer cert

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Complete dbt Labs Fundamentals + Advanced learning paths, take 3 practice exams (≥85% before sitting), pass the dbt Analytics Engineer cert. Publish `docs/certs/dbt-ae.md` retrospective.

**Skill progression by level:**
- [ ] **Junior** — *(out of natural progression for this sub-skill)*
- [ ] **Mid** — Apply dbt daily.
- [ ] **🎯 Senior (TARGET)** — Pass dbt Analytics Engineer; publish retrospective; mentor mid-level engineers preparing.
- [ ] **Staff** — *(out of natural progression for this sub-skill)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 6 Story-level 🎯 boxes are ticked** — which requires 11 sub-skill 🎯 boxes (two at Staff) including the dbt Analytics Engineer cert. Mastery evidence: Lab dbt project with staging/intermediate/marts + 4-strategy incremental benchmark; 100% mart contracts + 5 unit-tested models; 5 custom macros + 1 custom materialization; `dbt_project_evaluator` in CI + internal reusable package; slim CI + blue-green deployment + manifest-driven Airflow DAG; dbt Mesh (2 projects) + Semantic Layer (5 metrics via Metabase); dbt Analytics Engineer cert passed.
