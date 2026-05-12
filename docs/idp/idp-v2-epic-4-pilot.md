# IDP v2 — Epic 4 Pilot · SQL and Dimensional Modeling

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's *modeling discipline* — advanced SQL practice, Kimball dimensional models, alternative paradigms (Inmon, Data Vault), semantic-layer adoption, federated-query strategy, and the BI-consumer perspective that lets DE design marts that BI tools can consume cleanly. They've published the team's canonical references and shipped the Lab implementations that demonstrate each pattern.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 4.1 — Engineer Advanced SQL

> **What "Senior at this Skill" means.** A Senior here doesn't just *write* advanced SQL — they **define how the team writes it**. They author the canonical patterns (CTEs, window functions, joins), establish the methodologies (query-plan audit, refresh strategy), build the reusable artifacts (dbt macro libraries), and own the governance (mat-view ownership + cost-caps).

### Sub-skill 4.1.1: Design canonical CTE & lateral-join patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author and publish an internal reference note `docs/notes/cte-patterns.md` covering 5 canonical CTE patterns (recursive hierarchy, sliding window via lateral join, dedup with QUALIFY, cross-validation, materialized vs inlined) with warehouse-specific performance notes for Postgres, BigQuery, and Snowflake. Apply at least 2 of these patterns in real Lab dbt models so the trade-offs are demonstrated in production code, not just documented.

**Skill progression by level:**
- **Junior** — Read CTE syntax; trace through someone else's recursive CTE and explain what it returns.
- **Mid** — Apply non-trivial CTEs (recursive hierarchies, lateral joins, sliding windows) to real query problems.
- **🎯 Senior (TARGET)** — Design CTE-based modeling for moderate-to-complex business logic. Recognize when CTEs hurt performance (no materialization, repeated execution) and convert to temp tables or materialized views.
- **Staff** — Standardize team CTE patterns via a shared idiom library; mentor mid-level engineers on when to use which CTE flavor.
- **Principal** — Define organization-wide SQL idiom guidelines; govern cross-team CTE usage and naming conventions.

---

### Sub-skill 4.1.2: Define team window-function idioms

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author canonical note `docs/notes/window-functions-canon.md` with 10 production patterns (cohort retention, running totals, gap-and-island, sessionization, change-detection via LEAD/LAG, percentile/NTILE bucketing, etc.). Build a reusable dbt macro library `dbt_window_patterns/` wrapping the 3 most-repeated patterns with unit tests. Apply the patterns in 5 production-quality Lab dbt models on the `feature/window-patterns` branch — each model has unit tests, dbt docs, downstream consumers, and PR-level performance notes vs a naive non-window implementation.

**Skill progression by level:**
- **Junior** — Recognize ROW_NUMBER, RANK, LEAD/LAG by name.
- **Mid** — Apply LEAD/LAG and frame clauses (ROWS vs RANGE) in real queries for sessionization or running aggregates.
- **🎯 Senior (TARGET)** — Define the team's canonical window-function patterns. Fluent with frame clauses and their performance implications. Catch incorrect partitioning or ordering in PR review. Implement the patterns as production-quality, tested dbt models.
- **Staff** — Architect reusable query libraries / dbt macro packages used across teams.
- **Principal** — Govern cross-team window-function usage; calibrate educational standards across the org.

---

### Sub-skill 4.1.3: Engineer cross-warehouse pivot, unpivot & array-flattening patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author internal note `docs/notes/pivot-unnest-dialects.md` with side-by-side syntax for pivot/unpivot and array-flattening (UNNEST, FLATTEN, CROSS APPLY) across Postgres, BigQuery, Snowflake, and Spark SQL. Include a decision tree of "reshape in SQL vs orchestration vs BI tool" with 3 worked examples from real Lab queries.

**Skill progression by level:**
- **Junior** — Read pivot/unpivot syntax in one warehouse.
- **Mid** — Apply pivot/unpivot/UNNEST across at least 2 dialects.
- **🎯 Senior (TARGET)** — Engineer portable patterns (e.g., GROUP BY + conditional aggregates as a portable PIVOT). Decide when reshaping belongs in SQL vs orchestration vs BI tool based on cost, maintainability, and change rate.
- **Staff** — Standardize a dialect-portable team library covering all common reshapes.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.1.4: Design schemas with intentional JSON / array / struct types

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author note `docs/notes/nested-types.md` covering the decision criteria for using nested types vs flat columns + 5 flatten/aggregate recipes per warehouse (BigQuery STRUCT/ARRAY, Postgres jsonb operators, Snowflake VARIANT + FLATTEN). Build a starter dbt macro `dbt_json/` for the most-repeated JSON normalization patterns. Apply the schema choices in 1 Lab dataset that intentionally uses nested types where flat columns would lose information.

**Skill progression by level:**
- **Junior** — Read jsonb / STRUCT / VARIANT syntax.
- **Mid** — Apply nested-type queries for flatten / aggregate operations.
- **🎯 Senior (TARGET)** — Design schemas that intentionally use JSON / struct / array types where appropriate, rejecting them where flat columns serve better. Define team conventions for flatten-vs-preserve decisions.
- **Staff** — Define org-level JSON conventions and migration paths.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.1.5: Define the team's query-plan audit methodology

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author runbook `docs/runbooks/query-plan-audit.md` defining the audit methodology (what to look at first, what thresholds matter, when to escalate, when to rewrite). Apply the methodology end-to-end on 3 production-relevant slow queries from the Lab — diagnose, remediate, and document the plan diff + slot-ms / cost delta in `docs/perf/sql-audit-2026Q3.md`. Update the runbook based on what you learned during the 3 audits.

**Skill progression by level:**
- **Junior** — Recognize plan output; know what EXPLAIN does.
- **Mid** — Read plans for slow queries; identify the dominant cost driver.
- **🎯 Senior (TARGET)** — Define the team's audit methodology and demonstrate it via 3 worked audits with measurable cost-delta. Mentor mid-level engineers through their first plans.
- **Staff** — Architect a cross-engine tuning playbook + continuous performance-audit pipeline (scheduled plan + cost-regression detection).
- **Principal** — Calibrate slot / cost governance at the org level.

---

### Sub-skill 4.1.6: Design query patterns informed by join algorithms

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author note `docs/notes/join-optimization.md` covering join algorithm taxonomy (broadcast hash, sort-merge, nested loop, shuffle hash) + 5 patterns + 5 anti-patterns. Apply the optimization techniques in 3 real Lab queries with before/after join strategies and measurable cost-deltas (slot-ms or `bytes_billed`).

**Skill progression by level:**
- **Junior** — Know join types (inner, left, right, full, cross).
- **Mid** — Apply broadcast / hash hints when appropriate; recognize join algorithms in plans.
- **🎯 Senior (TARGET)** — Design query patterns that pre-filter large tables before joining, leverage partition pruning, and reorder joins by selectivity. Catch join-explosion bugs (M:N amplification, accidental cross joins) in PR review.
- **Staff** — Architect query patterns and team standards across engines.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.1.7: Define materialized-view strategy and governance

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author note `docs/notes/mat-view-strategy.md` with refresh-strategy decision tree (real-time-ish vs scheduled vs full refresh) and the trade-offs between mat-views, incremental dbt models, and full refresh by query shape. Document a governance template (owner, change-impact, cost-cap) and apply it to 3 Lab mat-views (one per refresh pattern) so each has a real owner, a documented change-impact policy, and a cost ceiling.

**Skill progression by level:**
- **Junior** — Know what materialized views are and when they apply.
- **Mid** — Apply mat-views with awareness of refresh costs.
- **🎯 Senior (TARGET)** — Define refresh strategy by query shape and freshness need. Choose between mat-views, incremental dbt models, and full refresh based on cost and maintainability. Document governance (owner, change-impact, cost-cap) and apply it to real Lab mat-views.
- **Staff** — Architect mat-view governance as an org policy.
- **Principal** — Govern mat-view policy and cost-cap at the org level.

---

## Story 4.2 — Design the Team's Dimensional-Modeling (Kimball)

> **What "Senior at this Skill" means.** A Senior here owns the team's Kimball discipline — star vs snowflake, fact-table grains, dimension variants, SCD strategy, conformed dimensions, and the bus matrix that keeps cross-domain analytics coherent.

### Sub-skill 4.2.1: Design star vs snowflake schemas + surrogate-key conventions

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/star-vs-snowflake.md` covering the trade-offs (denormalized vs normalized dimensions, query simplicity vs storage, BI-tool ergonomics) and document the team's default (star, with exceptions called out per case). Author `docs/notes/surrogate-vs-natural-keys.md` defining the team's policy (surrogate keys for SCD-bearing dimensions, natural keys allowed for stable references) with `dbt_utils.generate_surrogate_key` as the canonical implementation.

**Skill progression by level:**
- [ ] **Junior** — Recognize star schema vs snowflake by diagram.
- [ ] **Mid** — Apply star schema for a fresh mart.
- [ ] **🎯 Senior (TARGET)** — Design the team's star-default + exception policy + surrogate-key convention. Review modeling PRs against it.
- [ ] **Staff** — Architect cross-domain modeling conventions at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.2.2: Engineer fact-table grains (transactional, periodic snapshot, accumulating)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/fact-table-grains.md` with worked Lab examples of each: transactional fact (e.g., `fct_orders`), periodic snapshot (e.g., `fct_inventory_daily`), accumulating snapshot (e.g., `fct_order_fulfillment_pipeline`). Document the decision rule: which grain fits which business question, when to maintain multiple grains for the same domain.

**Skill progression by level:**
- [ ] **Junior** — Recognize fact tables as containing measures.
- [ ] **Mid** — Apply transactional fact tables to event-style sources.
- [ ] **🎯 Senior (TARGET)** — Engineer all 3 grains in the Lab + document the decision rule; review PR designs that pick the wrong grain.
- [ ] **Staff** — Architect cross-domain fact-grain conventions at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.2.3: Design dimension variants (role-playing, junk, degenerate, mini, outrigger, bridge)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dimension-variants.md` with worked examples for each variant: role-playing (`dim_date` used as `order_date_key` and `ship_date_key`), junk (collapsing low-cardinality flags), degenerate (transaction IDs on the fact table), mini (frequently-changing attributes split off), outrigger (a dim referencing another dim), bridge (M:N relationships). Cite when each variant is the right answer.

**Skill progression by level:**
- [ ] **Junior** — Recognize basic dimension concept.
- [ ] **Mid** — Apply standard `dim_X` patterns; recognize role-playing.
- [ ] **🎯 Senior (TARGET)** — Design dimension variants appropriately per use case; review PRs for unnecessary dimension proliferation or missing bridge tables.
- [ ] **Staff** — Architect cross-domain dimension-variant standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.2.4: Define SCD strategy (Types 1–6)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/scd-strategy.md` covering SCD Types 1 (overwrite), 2 (versioned via valid_from/valid_to), 3 (limited history columns), 4 (history table), 5 (combination 1+4), 6 (combination 1+2+3). Document the team's default (SCD2 for slowly-changing customer/employee/product) and exceptions. Engineer SCD2 on a customer dimension in the Lab via dbt snapshots with `valid_from` / `valid_to` / `is_current`.

**Skill progression by level:**
- [ ] **Junior** — Recognize that dimensions can change over time.
- [ ] **Mid** — Apply SCD Type 1 (overwrite) and Type 2 with guidance.
- [ ] **🎯 Senior (TARGET)** — Define the team's SCD policy per dimension; engineer the canonical SCD2 implementation via dbt snapshots; review PRs that introduce SCD changes.
- [ ] **Staff** — Architect platform-level SCD tooling (e.g., SCD2 generators, retroactive history backfill).
- [ ] **Principal** — Govern cross-team SCD policy + historical-data retention.

---

### Sub-skill 4.2.5: Own conformed dimensions & bus-matrix discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/conformed-dimensions.md` defining the team's conformed dimensions (`dim_calendar`, `dim_customer`, `dim_product`, etc.) and the bus matrix that maps facts × conformed dims. Engineer `dim_calendar` + at least 3 conformed dimensions in the Lab. Publish `docs/bus-matrix.md` as a maintained team artifact.

**Skill progression by level:**
- [ ] **Junior** — Recognize the concept of dimensions being shared across facts.
- [ ] **Mid** — Apply existing conformed dimensions correctly in new facts.
- [ ] **🎯 Senior (TARGET)** — Own the team's conformed-dimension set and bus matrix; review PRs that introduce parallel dimension definitions; mentor mid-level engineers on dim conformance.
- [ ] **Staff** — Architect cross-team conformed dimensions at multi-domain scale.
- [ ] **Principal** — Govern org-wide conformed-dimension policy + naming standards.

---

## Story 4.3 — Evaluate Alternative Modeling Paradigms (Inmon, Data Vault)

> **What "Senior at this Skill" means.** A Senior here can defend the team's Kimball default by knowing what the alternatives offer and where they win. They've evaluated Inmon CIF, Data Vault 2.0, and Activity Schema on the same Lab domain so the trade-offs are concrete.

### Sub-skill 4.3.1: Compare Inmon CIF vs Kimball

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/inmon-vs-kimball.md` covering Inmon's 3NF enterprise data warehouse with downstream datamarts vs Kimball's dimensional bus architecture. Document each paradigm's strengths (Inmon: data integrity + flexibility; Kimball: query simplicity + BI ergonomics) and the team's default + exception cases.

**Skill progression by level:**
- [ ] **Junior** — Recognize Inmon and Kimball as two paradigms.
- [ ] **Mid** — Apply the team's chosen paradigm; recognize the difference in code.
- [ ] **🎯 Senior (TARGET)** — Defend the team's choice with trade-off analysis; review architectural proposals against the comparison.
- [ ] **Staff** — Architect hybrid paradigms (Inmon for raw + Kimball for marts) at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.3.2: Engineer Data Vault 2.0 as an alternative

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/data-vault.md` covering the Hub-Link-Satellite model, business vault layer, hash-key conventions, and the use cases where Data Vault wins (heavy auditability needs, source-system volatility, regulated industries). Engineer Data Vault on 1 Lab domain alongside its Kimball-star equivalent so the trade-offs are visible.

**Skill progression by level:**
- [ ] **Junior** — Recognize Data Vault as an alternative paradigm.
- [ ] **Mid** — Apply a Hub-Link-Satellite triad under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer Data Vault on a Lab domain + Kimball comparison; document the trade-offs; recommend per domain.
- [ ] **Staff** — Architect Data Vault adoption at platform scale (raw vault + business vault).
- [ ] **Principal** — Govern org-wide Data Vault adoption strategy.

---

### Sub-skill 4.3.3: Understand Activity Schema (Narrator-style)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/activity-schema.md` covering the Activity Schema approach (a single wide table of customer/entity activities, ordered by time, joined to itself for analytics). Document where it beats Kimball (rapid analyst iteration, fewer joins) and where it falls short (cost at scale, query complexity for OLAP cubes).

**Skill progression by level:**
- [ ] **Junior** — Recognize Activity Schema by name.
- [ ] **Mid** — Apply Activity Schema queries under guidance.
- [ ] **🎯 Senior (TARGET)** — Understand the Activity Schema trade-offs; cite it as an option in modeling discussions; recommend per use case.
- [ ] **Staff** — *(out of natural progression for this sub-skill)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 4.4 — Design Semantic Layer & Metrics

> **What "Senior at this Skill" means.** A Senior here defines whether the team adopts a semantic layer (MetricFlow / Cube / LookML / dbt Semantic Layer), establishes the metric-governance discipline, and resolves cross-domain metric duplication via reconciliation.

### Sub-skill 4.4.1: Define the team's semantic-layer adoption strategy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/semantic-layer.md` comparing dbt Semantic Layer (MetricFlow), Cube, LookML, and headless-BI architectures — with the team's adoption decision + rationale. Apply dbt Semantic Layer in the Lab with at least 5 declared metrics consumed by Metabase + Superset, demonstrating cross-tool metric consistency.

**Skill progression by level:**
- [ ] **Junior** — Recognize semantic layer as a category.
- [ ] **Mid** — Apply existing semantic-layer metric definitions when writing queries.
- [ ] **🎯 Senior (TARGET)** — Define adoption strategy + ship the Lab implementation; review proposals that bypass the semantic layer.
- [ ] **Staff** — Architect semantic-layer-as-a-service across teams.
- [ ] **Principal** — Govern org-wide metric definition + ownership at the semantic-layer level.

---

### Sub-skill 4.4.2: Own metric governance & cross-domain reconciliation

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/metric-governance.md` covering the team's metric-ownership model (who can create, who must approve, how versioning works), naming conventions, and the cross-domain reconciliation process when two domains define "revenue" differently. Document an audit checklist for catching metric duplication.

**Skill progression by level:**
- [ ] **Junior** — Recognize that "the same metric" can mean different things in different parts of the org.
- [ ] **Mid** — Apply existing metric definitions correctly; flag duplication when seen.
- [ ] **🎯 Senior (TARGET)** — Own the team's metric-governance discipline; lead reconciliation when duplicates surface; review PRs that introduce new metrics.
- [ ] **Staff** — Architect org-wide metric governance + change-management workflow.
- [ ] **Principal** — Govern metric strategy at multi-domain scale with executive stakeholders.

---

## Story 4.5 — Operate Federated Query Engines

> **What "Senior at this Skill" means.** A Senior here owns the team's choice and operation of federated-query engines — Trino is the dominant pick, with Presto / Hive / Dremio as comparison points. They've shipped a Lab Trino stack with 3 catalogs (Postgres + Iceberg + ClickHouse) and document when federation beats ETL.

### Sub-skill 4.5.1: Engineer Trino as the team's federation layer

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/trino.md` covering Trino's architecture (catalogs, connectors, coordinator/worker, fault-tolerant execution), connector configuration, and operational concerns (query cost, slot management, security). Engineer a Lab Trino stack with 3 catalogs (Postgres + Iceberg + ClickHouse) and demonstrate cross-catalog federated queries.

**Skill progression by level:**
- [ ] **Junior** — Recognize Trino as a federated SQL engine.
- [ ] **Mid** — Apply Trino queries against a single catalog.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Trino stack with multi-catalog federation; document operational concerns; review proposals that involve Trino adoption.
- [ ] **Staff** — Architect Trino-as-a-service across teams with shared coordinator + multi-tenant security.
- [ ] **Principal** — Govern federation strategy at the org level.

---

### Sub-skill 4.5.2: Compare Presto, Hive, Dremio & Starburst Galaxy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/federation-alternatives.md` covering the Presto vs Trino fork history (practical differences), Apache Hive query engine (legacy ubiquity), Dremio + Apache Arrow Flight, AWS Athena Federated Query, and commercial Starburst Galaxy. Document when each alternative beats Trino.

**Skill progression by level:**
- [ ] **Junior** — Recognize the names.
- [ ] **Mid** — Apply Athena Federated Query or Hive for a single source.
- [ ] **🎯 Senior (TARGET)** — Evaluate alternatives + recommend per context; review architectural proposals.
- [ ] **Staff** — Architect cross-vendor federation strategy at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.5.3: Define query-federation vs ETL trade-offs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/federation-vs-etl.md` covering the trade-offs (consistency: federation reads stale; performance: ETL warmer for repeated queries; governance: federation crosses boundaries; cost: depends on access pattern). Document the team's decision rule for when to federate vs when to ETL.

**Skill progression by level:**
- [ ] **Junior** — Recognize federation and ETL as alternatives.
- [ ] **Mid** — Apply the existing team default for new use cases.
- [ ] **🎯 Senior (TARGET)** — Define the decision rule; review proposals for federation-vs-ETL fit.
- [ ] **Staff** — Architect federation + ETL coexistence at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.5.4: Own cross-engine SQL dialect literacy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/sql-dialect-cheatsheet.md` with side-by-side syntax for Postgres, BigQuery, Snowflake, Trino, Spark SQL, and Hive — focused on the critical differences (DATE arithmetic, window function syntax, JSON access, array/struct handling, regex). Use this when reviewing cross-engine PRs.

**Skill progression by level:**
- [ ] **Junior** — Recognize that dialects differ.
- [ ] **Mid** — Apply one dialect fluently; consult docs for others.
- [ ] **🎯 Senior (TARGET)** — Read all 6 dialects fluently; reference the cheatsheet in review; spot dialect-specific bugs in PRs.
- [ ] **Staff** — Architect dialect-agnostic abstractions where possible (e.g., dbt + Jinja).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 4.6 — Understand Data Visualization & BI Tools (Consumer Perspective for Data Engineering)

> **What "Senior at this Skill" means.** A Senior here doesn't build dashboards as their main job — but they understand BI consumer tools well enough that their marts are *consumable*. They can answer "why is this Power BI report slow?" because they know DirectQuery vs Import, can model dimensions for RLS, and can predict which tools will struggle with their schema.

### Sub-skill 4.6.1: Compare the BI tool landscape decision matrix

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/bi-tool-landscape.md` comparing Tableau, Power BI, Looker, Looker Studio, Apache Superset, Metabase, AWS QuickSight, and Mode — with positioning (enterprise vs SMB, on-prem vs SaaS, semantic-layer vs query-direct, pricing model). Map common DE tasks (build a KPI dashboard, expose a data product, ad-hoc analysis) to recommended tools.

**Skill progression by level:**
- [ ] **Junior** — Recognize the tool names.
- [ ] **Mid** — Apply 1-2 tools personally.
- [ ] **🎯 Senior (TARGET)** — Compare the landscape; recommend per use case; participate in BI-tool selection decisions.
- [ ] **Staff** — Architect BI-tool strategy at platform scale (consolidation, governance).
- [ ] **Principal** — Govern BI-portfolio strategy at the org level.

---

### Sub-skill 4.6.2: Own Power BI mastery for DE consumers (DirectQuery + DAX + RLS + semantic model)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/power-bi-for-de.md` covering Power BI's semantic model (Tables, Relationships, Measures), DAX basics (CALCULATE, FILTER, time intelligence), DirectQuery vs Import vs Dual mode trade-offs, RLS implementation, and how to design marts that Power BI consumes well. Engineer 1 Power BI semantic model + DirectQuery dashboard against Lab marts with shipped `.pbix` + DAX measures in version control.

**Skill progression by level:**
- [ ] **Junior** — Recognize Power BI as a BI tool.
- [ ] **Mid** — Apply basic Power BI dashboards against existing data.
- [ ] **🎯 Senior (TARGET)** — Engineer a Power BI semantic model + DirectQuery dashboard; design marts informed by Power BI consumption patterns; review BI-tool issues that have a DE cause.
- [ ] **Staff** — Architect Power BI as a platform consumer of marts (workspace governance, certified datasets).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.6.3: Own open-source BI (Superset, Metabase) & dashboards-as-code

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/oss-bi.md` covering Apache Superset (charts, dashboards, SQL Lab, native filters) and Metabase (auto-dashboards, embedded analytics). Engineer 1 Superset dashboard-as-code against Lab marts (YAML config exported) and 1 Metabase auto-generated dashboard for comparison.

**Skill progression by level:**
- [ ] **Junior** — Recognize Superset and Metabase.
- [ ] **Mid** — Apply basic charts in either tool.
- [ ] **🎯 Senior (TARGET)** — Engineer dashboards-as-code in Superset; compare auto-dashboards vs hand-crafted; recommend per use case.
- [ ] **Staff** — Architect Superset/Metabase as a platform service.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 4.6.4: Design DE → BI handoff (semantic models, RLS, naming)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/de-to-bi-handoff.md` covering how mart structure affects BI tools — denormalization patterns (when to flatten), naming conventions (BI-tool-friendly column names, hierarchical naming `dim__customer__country`), row-level security (RLS) and object-level security (OLS) implications, and the freshness-cost-correctness triangle of extract vs DirectQuery vs Live.

**Skill progression by level:**
- [ ] **Junior** — Recognize that mart structure affects BI usability.
- [ ] **Mid** — Apply BI-tool-friendly naming when modeling.
- [ ] **🎯 Senior (TARGET)** — Design marts with explicit BI-consumer awareness; review PRs for BI-handoff issues; mentor mid-level engineers on the BI consumer view.
- [ ] **Staff** — Architect DE-BI contract conventions across teams.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 6 Story-level 🎯 boxes are ticked** — which requires the 7 sub-skills of Story 4.1 plus the ~17 sub-skills of Stories 4.2-4.6. Mastery evidence: published notes (`docs/notes/*.md`), the bus matrix (`docs/bus-matrix.md`), and Lab implementations (SQL macro libraries, conformed dims, Data Vault POC, dbt Semantic Layer, Trino federation stack, Power BI dashboard).
