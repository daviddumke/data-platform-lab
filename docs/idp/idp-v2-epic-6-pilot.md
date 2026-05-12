# IDP v2 — Epic 6 Pilot · Data Testing Engineering

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's data-testing discipline — generic-test coverage policy, the singular tests + macros library, contracts + Great Expectations / Soda for source quality, and anomaly + drift detection. They've published the testing canon and shipped the watchers that detect production data-quality regressions before consumers notice.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 6.1 — Engineer Generic Test Coverage

> **What "Senior at this Skill" means.** A Senior here defines the team's expected test coverage — PK + unique + accepted_values + relationships across all marts, source freshness across all sources, with severity thresholds that escalate appropriately.

### Sub-skill 6.1.1: Engineer generic-test coverage + severity policy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-generic-tests.md` covering the team's mandatory coverage (not_null + unique on every PK, accepted_values on every categorical, relationships on every FK fact-to-dim), severity levels (error vs warn), and threshold tuning. Apply 100% PK coverage + ≥30 accepted_values across the Lab dbt project. Document a CI gate that rejects new marts without PK coverage.

**Skill progression by level:**
- [ ] **Junior** — Recognize dbt's generic-test types.
- [ ] **Mid** — Apply not_null + unique to new tables.
- [ ] **🎯 Senior (TARGET)** — Define the coverage policy + ship the CI gate; review PRs for missing tests; mentor mid-level engineers on severity tuning.
- [ ] **Staff** — Architect cross-team test-coverage standards + dashboards.
- [ ] **Principal** — Govern org-wide data-testing policy.

---

### Sub-skill 6.1.2: Define source freshness as an external contract

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/source-freshness.md` covering dbt source freshness configuration, the team's freshness-SLA policy per source class (P0 sources: 1 hr freshness; P1: 6 hr; P2: 24 hr), and integration with alerting. Apply source freshness on 100% of Lab sources with versioned YAMLs.

**Skill progression by level:**
- [ ] **Junior** — Recognize source freshness as a concept.
- [ ] **Mid** — Apply freshness to new sources under guidance.
- [ ] **🎯 Senior (TARGET)** — Define the freshness-SLA policy + ship 100% coverage; review PRs for missing freshness; mentor on freshness-vs-availability trade-offs.
- [ ] **Staff** — Architect cross-team freshness monitoring + dashboards.
- [ ] **Principal** — Govern source-freshness SLAs at org level.

---

## Story 6.2 — Author Custom Tests & Macros

> **What "Senior at this Skill" means.** A Senior here writes the team's singular tests and reusable test macros — the test code that catches the bugs generic tests miss (orphan FKs, time monotonicity, partition skew, late-arriving data, freshness-vs-volume).

### Sub-skill 6.2.1: Author 6 canonical singular tests for the team

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer 6 canonical singular tests in the Lab `tests/` directory: orphan FK detection, time monotonicity (a column should only increase), partition skew detection, dedup correctness, completeness (vs upstream source count), freshness-vs-volume correlation. Author `docs/notes/canonical-singular-tests.md` documenting the SQL pattern for each + when to add a new singular test.

**Skill progression by level:**
- [ ] **Junior** — Recognize singular tests vs generic tests.
- [ ] **Mid** — Write a basic singular test.
- [ ] **🎯 Senior (TARGET)** — Author the team's canonical 6 + document the pattern; review PRs for missing singular tests in complex domains.
- [ ] **Staff** — Architect cross-team singular-test library + shared patterns.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 6.2.2: Engineer reusable parameterized test macros

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer the reusable test macro `test_no_late_arriving_data` (parameterized over the time column + lookback window) and apply it to ≥5 fact tables in the Lab. Author `docs/notes/test-macro-patterns.md` covering how to design parameterizable macros, when to extract a generic vs keep singular.

**Skill progression by level:**
- [ ] **Junior** — Recognize parameterized macros.
- [ ] **Mid** — Apply existing test macros to new models.
- [ ] **🎯 Senior (TARGET)** — Engineer reusable test macros; mentor mid-level engineers on test-macro design; review PRs for macro re-use opportunities.
- [ ] **Staff** — Architect cross-team test-macro library published as a dbt package.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 6.3 — Operate Contracts, Great Expectations & Soda

> **What "Senior at this Skill" means.** A Senior here knows when dbt contracts are enough vs when Great Expectations / Soda earn their operational cost. They've shipped contracts at 100% coverage and Great Expectations on the team's highest-risk sources.

### Sub-skill 6.3.1: Own dbt contracts adoption + enforcement

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-contracts.md` covering `contract: enforced: true` guarantees (column types + constraints checked at compile), the team's enforcement policy (100% of marts; staging exempt), and migration playbook from no-contract → contract. Apply contracts on 100% of Lab marts via versioned YAMLs.

**Skill progression by level:**
- [ ] **Junior** — Recognize dbt contracts as a feature.
- [ ] **Mid** — Apply contracts to new marts.
- [ ] **🎯 Senior (TARGET)** — Own contract enforcement at 100%; lead the migration; review PRs for contract-bypass.
- [ ] **Staff** — Architect cross-team contract governance + change-management workflow.
- [ ] **Principal** — Govern org-wide data-contract policy.

---

### Sub-skill 6.3.2: Operate Great Expectations / Soda for source quality

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gx-vs-soda-vs-dbt.md` comparing Great Expectations (suites, batches, checkpoints), Soda Core / Soda Cloud, and dbt tests — with the team's decision rule for when each beats dbt tests (GX for sources with no dbt model, Soda for SaaS observability integration). Apply Great Expectations on 1 Lab source with checkpoint + CI integration.

**Skill progression by level:**
- [ ] **Junior** — Recognize Great Expectations and Soda by name.
- [ ] **Mid** — Apply a basic GX suite under guidance.
- [ ] **🎯 Senior (TARGET)** — Operate GX or Soda on a real source; define when each beats dbt; review proposals for testing-tool sprawl.
- [ ] **Staff** — Architect cross-source testing infrastructure with consolidated reporting.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 6.3.3: Engineer data-diff workflow for PRs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/data-diff.md` covering data-diff workflows (Datafold open-source, dbt-checkpoint, home-grown SQL diff) and the team's PR-review integration (auto-run diff on dbt model changes, post results as PR comment). Engineer a Lab CI workflow that runs data-diff on PR open and comments.

**Skill progression by level:**
- [ ] **Junior** — Recognize data-diff as a concept.
- [ ] **Mid** — Apply manual data-diff during local development.
- [ ] **🎯 Senior (TARGET)** — Engineer the CI integration; document the team's review-with-diff workflow; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team data-diff infrastructure at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 6.4 — Engineer Anomaly Detection & DQ KPIs

> **What "Senior at this Skill" means.** A Senior here ships the watchers that detect data-quality regressions in production — volume anomalies, schema drift, freshness-volume correlation — and codifies the team's data-quality KPI framework (completeness, validity, timeliness, consistency, uniqueness).

### Sub-skill 6.4.1: Engineer volume anomaly detection

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/volume-anomaly-detection.md` covering Z-score, IQR, and EWMA (exponentially weighted moving average) methods for volume-anomaly detection, with the formulas and threshold-tuning approach. Engineer the Lab model `anomaly_volume.sql` + an Airflow alert that fires when daily volume deviates > N stddev from baseline.

**Skill progression by level:**
- [ ] **Junior** — Recognize that volume regressions are detectable.
- [ ] **Mid** — Apply a basic Z-score threshold.
- [ ] **🎯 Senior (TARGET)** — Engineer the detector + alert; tune thresholds to balance precision/recall; review proposals for new detectors.
- [ ] **Staff** — Architect cross-table anomaly detection at platform scale (correlation across tables).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 6.4.2: Engineer schema-drift detection

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/schema-drift-detection.md` covering the team's pattern for catching schema drift in sources (new column appeared, column type changed, column dropped) — both for ingestion (Singer schema discovery comparison) and for downstream marts (dbt compile diff). Engineer a Lab DAG `quality/schema_drift.py` that runs nightly and alerts Slack on drift.

**Skill progression by level:**
- [ ] **Junior** — Recognize schema drift as a failure mode.
- [ ] **Mid** — Apply a manual schema comparison.
- [ ] **🎯 Senior (TARGET)** — Engineer the detector + Slack alert; document the response runbook; review PRs for un-tracked schema changes.
- [ ] **Staff** — Architect cross-source schema-drift detection with automated migration support.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 6.4.3: Define the team's DQ KPI framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dq-kpi-framework.md` covering the 5 canonical DQ KPIs — completeness (% non-null), validity (% passing format/range checks), timeliness (% within freshness SLA), consistency (cross-source reconciliation), uniqueness (% deduped) — with formulas + targets per layer. Engineer a Lab dashboard showing the 5 KPIs across mart tables.

**Skill progression by level:**
- [ ] **Junior** — Recognize the 5 KPI names.
- [ ] **Mid** — Apply existing KPI definitions to new sources.
- [ ] **🎯 Senior (TARGET)** — Define the framework + ship the dashboard; mentor mid-level engineers on KPI selection; review proposals for KPI sprawl.
- [ ] **Staff** — Architect cross-domain DQ KPI rollups with consumer-facing scorecards.
- [ ] **Principal** — Govern org-wide data-quality SLA framework.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 4 Story-level 🎯 boxes are ticked** — which requires the 10 sub-skill 🎯 Senior boxes. Mastery evidence: 100% PK + freshness coverage, 6 canonical singular tests, ≥1 reusable test macro, 100% contracts, 1 Great Expectations source, data-diff CI workflow, volume + schema-drift watchers, DQ KPI dashboard.
