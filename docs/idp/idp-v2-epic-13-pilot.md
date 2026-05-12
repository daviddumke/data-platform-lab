# IDP v2 — Epic 13 Pilot · FinOps and Cost Optimization

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's cost discipline — cost-per-job visibility, optimization with measured delta, budget alerts, and capacity forecasting. They've shipped the team's cost dashboard and led the optimization that cut the top-10 expensive queries.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 13.1 — Engineer Cost Visibility

> **What "Senior at this Skill" means.** A Senior here has shipped cost-per-job, cost-per-domain dashboards, and the alerting tiers that catch cost regressions before they get billed.

### Sub-skill 13.1.1: Apply the FinOps Foundation framework (Inform, Optimize, Operate)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/finops-framework.md` summarizing the FinOps Foundation framework — Inform (visibility, attribution), Optimize (right-size, reservation, rate cards), Operate (budgets, anomaly detection, accountability). Document where the team is on each phase.

**Skill progression by level:**
- [ ] **Junior** — Recognize FinOps as a discipline.
- [ ] **Mid** — Apply existing cost-attribution conventions.
- [ ] **🎯 Senior (TARGET)** — Operationalize the FinOps framework on the Lab; mentor mid-level engineers on cost-conscious design; review proposals for cost implications.
- [ ] **Staff** — Architect FinOps program across multiple teams + executive reporting.
- [ ] **Principal** — Govern org-wide FinOps strategy + budget allocation.

---

### Sub-skill 13.1.2: Engineer cost-per-query + cost-per-job observability

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cost-per-query.md` covering cost formulas per warehouse (BigQuery `bytes_billed * $5 / TB`, Snowflake credits × $rate, Databricks DBU × $rate). Engineer the Lab `jobs_executados` model from INFORMATION_SCHEMA.JOBS + `alertas_custo_jobs` with severity tiers (5/10/50 GB thresholds). Document tagging discipline (GCP labels, AWS tags) for attribution.

**Skill progression by level:**
- [ ] **Junior** — Recognize that queries have cost.
- [ ] **Mid** — Apply existing cost-attribution tags.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab cost-per-job model + alerting; document the tagging strategy; review PRs for tag hygiene.
- [ ] **Staff** — Architect cross-team cost-attribution infrastructure with chargeback support.
- [ ] **Principal** — Govern org-wide cost-attribution model.

---

### Sub-skill 13.1.3: Engineer cost dashboards (by domain, by owner, by sprint)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer a Lab cost dashboard (Power BI or Superset) aggregating cost by domain × owner × sprint × pipeline. Include 90-day trend, top-10 expensive jobs, and budget-vs-actual. Cross-link to the platform-health dashboard (Epic 7.2.2).

**Skill progression by level:**
- [ ] **Junior** — Recognize cost dashboards exist.
- [ ] **Mid** — Apply existing dashboards as a consumer.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's cost dashboard; share with stakeholders; iterate based on feedback.
- [ ] **Staff** — Architect cross-team cost dashboards with executive rollup.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 13.2 — Optimize Costs

> **What "Senior at this Skill" means.** A Senior here can find the team's most expensive cost drivers and engineer fixes with measured delta — proven, not theoretical.

### Sub-skill 13.2.1: Define top causes of cost + canonical fixes

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cost-anti-patterns.md` covering the top causes of warehouse cost (full table scans, exploded joins, frequent refreshes of large mart tables, oversized result sets, unused mat-views) and the canonical fix for each. (Cross-ref Epic 8.2.1.)

**Skill progression by level:**
- [ ] **Junior** — Recognize that cost has common causes.
- [ ] **Mid** — Apply existing optimization tactics.
- [ ] **🎯 Senior (TARGET)** — Define the team's anti-pattern catalogue; review PRs for cost-killers; mentor mid-level engineers.
- [ ] **Staff** — Architect platform-level cost-regression detection.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 13.2.2: Engineer warehouse-pricing decisions (BQ flat-rate vs on-demand vs autoscaling; Snowflake warehouse sizing)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/warehouse-pricing.md` covering BigQuery on-demand vs flat-rate vs autoscaling reservations (Standard / Enterprise / Enterprise Plus editions), Snowflake warehouse sizing + auto-suspend tuning, Databricks DBU economics. Document the team's break-even calculation method. Apply to the Lab with cost-delta documented after each optimization.

**Skill progression by level:**
- [ ] **Junior** — Recognize warehouse pricing models.
- [ ] **Mid** — Apply existing warehouse configurations.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's pricing-tier decision + break-even calculations; ship Lab top-10 optimization with cost-delta in `docs/perf/cost-2026Q3.md`.
- [ ] **Staff** — Architect cross-warehouse pricing strategy + reservation portfolio.
- [ ] **Principal** — Govern org-wide warehouse-pricing strategy with finance integration.

---

## Story 13.3 — Define Budgets & Forecasting

> **What "Senior at this Skill" means.** A Senior here has shipped budget alerts + a 12-month capacity forecast that informs the team's quarterly planning.

### Sub-skill 13.3.1: Define budget alerts + capacity forecasting (linear, ARIMA, Prophet)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/capacity-forecast.md` comparing forecasting methods (linear extrapolation, ARIMA, Prophet) — when each fits, accuracy expectations, when manual override beats forecasts. Engineer a 12-month forecast for the Lab (notebook + Terraform-managed GCP budget alerts) covering compute + storage + warehouse cost.

**Skill progression by level:**
- [ ] **Junior** — Recognize forecasting as a tool.
- [ ] **Mid** — Apply linear extrapolation under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab's 12-month forecast + budget alerts; document the method choice; mentor mid-level engineers on forecast accuracy.
- [ ] **Staff** — Architect cross-team forecasting infrastructure + finance integration.
- [ ] **Principal** — Govern org-wide capacity-planning + finance reporting.

---

### Sub-skill 13.3.2: Design reserved capacity vs Spot economics

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/reserved-vs-spot.md` covering Reserved Instances vs Savings Plans vs Spot Instances economics — the break-even math, the operational concerns of Spot interruption, the appropriate workload classes for each. Document Snowflake reservations + Databricks committed-use discounts.

**Skill progression by level:**
- [ ] **Junior** — Recognize Reserved / Savings / Spot as pricing options.
- [ ] **Mid** — Apply existing reservation plans.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's reservation strategy; document the break-even math; review proposals.
- [ ] **Staff** — Architect cross-account reservation portfolio.
- [ ] **Principal** — Govern org-wide reservation strategy with finance integration.

---

### Sub-skill 13.3.3: Own chargeback vs showback discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/chargeback-showback.md` covering the difference (chargeback = actual cross-team billing; showback = visibility only) and the team's choice. Document the cost-attribution mechanism + accountability chain.

**Skill progression by level:**
- [ ] **Junior** — Recognize chargeback and showback.
- [ ] **Mid** — Apply existing showback dashboards.
- [ ] **🎯 Senior (TARGET)** — Define the team's chargeback-vs-showback policy + accountability chain; mentor mid-level engineers on attribution.
- [ ] **Staff** — Architect cross-team chargeback infrastructure with finance.
- [ ] **Principal** — Govern org-wide chargeback + budget-policy.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 3 Story-level 🎯 boxes are ticked** — which requires the 8 sub-skill 🎯 Senior boxes. Mastery evidence: cost-per-job model + alerting tiers, cost dashboard by domain/owner/sprint, anti-pattern catalogue, top-10 optimization report with cost-delta, 12-month forecast + Terraform budget alerts, reservation strategy doc, chargeback/showback policy.
