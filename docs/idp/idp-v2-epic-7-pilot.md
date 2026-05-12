# IDP v2 — Epic 7 Pilot · Observability and Operational Reliability

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns how the team sees its pipelines in production — structured logs, metrics, traces, SLI/SLO with error budgets, postmortem culture, and the observability-stack choice (Prometheus + Grafana + OTel is canon, with Loki / ELK / Datadog / Splunk as comparison points). They've shipped the platform-health dashboard, the SLO catalog, and at least one postmortem with structural fixes.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 7.1 — Engineer Logs, Metrics & Traces

> **What "Senior at this Skill" means.** A Senior here owns the three pillars of observability — structured logging discipline, metrics taxonomy, distributed tracing via OpenTelemetry — at a level where on-call debugging is a matter of running the right query against existing instrumentation, not adding instrumentation during an incident.

### Sub-skill 7.1.1: Engineer structured logging discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/structured-logging.md` covering JSON-structured logs, correlation IDs (trace-id propagation), log-level conventions (ERROR for actionable, WARN for surprising-but-recoverable, INFO for state changes, DEBUG dev-only), and the team's logging template. Engineer the helper `lab/logging.py` and apply structured logging across all Lab DAGs.

**Skill progression by level:**
- [ ] **Junior** — Recognize structured vs unstructured logs.
- [ ] **Mid** — Apply structured logging using a library.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's logging helper + template; review PRs for unstructured `print()` calls; mentor on correlation-ID propagation.
- [ ] **Staff** — Architect cross-service log-format conventions + transport at platform scale.
- [ ] **Principal** — Govern org-wide logging policy + retention.

---

### Sub-skill 7.1.2: Own metrics taxonomy + collection

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/metrics-taxonomy.md` covering the 4 Prometheus metric types (counter, gauge, histogram, summary) — with use cases for each (counter for events, gauge for current state, histogram for distributions like latency, summary for client-side quantiles). Document the team's metric naming convention (`pipeline_<name>_<unit>_<aggregation>`) and labels strategy.

**Skill progression by level:**
- [ ] **Junior** — Recognize the metric types by name.
- [ ] **Mid** — Apply a counter or gauge in code.
- [ ] **🎯 Senior (TARGET)** — Own the team's taxonomy + naming + label discipline; review PRs that introduce new metrics; mentor on cardinality risk.
- [ ] **Staff** — Architect cross-service metrics conventions at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 7.1.3: Engineer distributed tracing via OpenTelemetry

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/opentelemetry-tracing.md` covering OTel architecture (SDK, collector, exporters), spans + traces + baggage, sampling strategies (head vs tail, probabilistic vs rate-limited). Engineer OTel tracing in the Lab for 1 end-to-end pipeline with traces visible in Jaeger or Tempo.

**Skill progression by level:**
- [ ] **Junior** — Recognize distributed tracing as a concept.
- [ ] **Mid** — Apply OTel auto-instrumentation under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer OTel end-to-end in the Lab; tune sampling; mentor mid-level engineers on trace-driven debugging.
- [ ] **Staff** — Architect tracing at platform scale (collector federation, multi-tenant Jaeger/Tempo).
- [ ] **Principal** — Govern org-wide tracing policy and sampling cost.

---

## Story 7.2 — Author Operational Metrics & Dashboards

> **What "Senior at this Skill" means.** A Senior here owns Prometheus + PromQL fluency well enough to write the team's alerting rules and Grafana dashboards-as-code. They've shipped the platform-health dashboard that on-call uses during incidents.

### Sub-skill 7.2.1: Engineer Prometheus + PromQL fluency

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/prometheus-promql.md` covering Prometheus architecture (scrape, retention, federation), PromQL fundamentals (instant vs range vectors, rate, irate, increase, histogram_quantile), recording rules (pre-aggregation for fast dashboards), and alerting rules. Engineer the Lab Prometheus + Grafana stack with shipped scrape configs + recording rules + alerts.

**Skill progression by level:**
- [ ] **Junior** — Recognize Prometheus and PromQL by name.
- [ ] **Mid** — Apply basic PromQL queries.
- [ ] **🎯 Senior (TARGET)** — Engineer recording rules + alerts; write PromQL fluently in incident response; mentor mid-level engineers.
- [ ] **Staff** — Architect Prometheus federation + long-term storage (Thanos/Cortex) at platform scale.
- [ ] **Principal** — Govern org-wide metrics platform strategy.

---

### Sub-skill 7.2.2: Author Grafana dashboards-as-code

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/grafana-dashboards-as-code.md` covering dashboards-as-code patterns (JSON export, Grafonnet, terraform-provider-grafana), variables + annotations, the team's dashboard standards (every dashboard has: scope, owner, intended audience, refresh cadence). Engineer the Lab "platform health" dashboard with versioned JSON in the repo.

**Skill progression by level:**
- [ ] **Junior** — Recognize Grafana dashboards.
- [ ] **Mid** — Apply existing dashboards; add panels.
- [ ] **🎯 Senior (TARGET)** — Author the team's dashboards-as-code; ship the platform-health dashboard; review proposals for dashboard sprawl.
- [ ] **Staff** — Architect dashboard-as-code tooling at platform scale (libraries, generators, audit).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 7.2.3: Define the team's pipeline + cost metrics catalogue

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/pipeline-cost-metrics.md` defining the team's top-10 pipeline metrics (success rate, latency P50/P95/P99, throughput, freshness, retry count, ...) + cost-per-job as a first-class observability metric. Document the formula for cost-per-job (BigQuery `bytes_billed * $5 / TB`, Snowflake credits × $rate, etc.).

**Skill progression by level:**
- [ ] **Junior** — Recognize success-rate and latency.
- [ ] **Mid** — Apply the existing top-10 metrics to new pipelines.
- [ ] **🎯 Senior (TARGET)** — Define the team's metrics catalogue + cost-per-job formula; review PRs for missing metrics; mentor on metric-driven debugging.
- [ ] **Staff** — Architect cross-team cost-attribution + dashboards.
- [ ] **Principal** — Govern org-wide cost-observability strategy.

---

## Story 7.3 — Define SLI, SLO & Error Budgets

> **What "Senior at this Skill" means.** A Senior here defines the team's SLI/SLO catalog with error budgets, ships burn-rate alerts, and applies Google SRE concepts (toil reduction, error budget policy) to the team's day-to-day work.

### Sub-skill 7.3.1: Define SLI/SLO/SLA framework + error budgets

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/sli-slo-sla.md` covering the differences (SLI = the metric, SLO = internal target, SLA = external contract), error-budget math (1 - SLO = budget; budget burn rate over windows), and the team's SLO menu (success rate, freshness, latency). Apply formal SLI/SLO to 3 critical Lab pipelines, published in `docs/slo-catalog.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize SLI / SLO / SLA as different concepts.
- [ ] **Mid** — Apply existing SLO definitions to new pipelines.
- [ ] **🎯 Senior (TARGET)** — Define the team's SLO catalog + error-budget math; mentor mid-level engineers; review proposals for SLO assignments.
- [ ] **Staff** — Architect cross-team SLO infrastructure + composite SLOs.
- [ ] **Principal** — Govern org-wide reliability strategy + customer-facing SLAs.

---

### Sub-skill 7.3.2: Engineer burn-rate alerting

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/burn-rate-alerting.md` covering multi-burn-rate alerting (the Google SRE approach: alert on fast burn over short window OR slow burn over long window), the formulas, and tuning to avoid both false positives and missed incidents. Engineer Prometheus alerting rules for burn-rate in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize burn rate as a concept.
- [ ] **Mid** — Apply a basic SLO threshold alert.
- [ ] **🎯 Senior (TARGET)** — Engineer multi-burn-rate alerts in PromQL; tune to minimize alert fatigue; document the methodology.
- [ ] **Staff** — Architect burn-rate alerting at platform scale across teams.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 7.3.3: Apply Google SRE concepts (toil, error-budget policy)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/sre-concepts-for-de.md` summarizing the SRE book chapters 3–5 (toil reduction, error-budget policy, embracing risk, postmortems) and translating them to DE context. Document the team's error-budget policy: what happens when budget is exhausted (freeze new features, focus on reliability), how toil is measured + reduced.

**Skill progression by level:**
- [ ] **Junior** — Recognize toil + SRE concepts by name.
- [ ] **Mid** — Apply SRE principles informally.
- [ ] **🎯 Senior (TARGET)** — Operationalize the SRE concepts in the team's day-to-day; lead error-budget conversations; reduce toil systematically.
- [ ] **Staff** — Architect SRE-style operational discipline across teams.
- [ ] **Principal** — Govern org-wide SRE adoption + culture.

---

## Story 7.4 — Lead Incident Management & Postmortems

> **What "Senior at this Skill" means.** A Senior here leads incident response when it happens — defines severity, runs the postmortem (blameless), and ensures the team adopts structural fixes (not just patches). They've authored the team's runbooks for the 3 most-critical systems.

### Sub-skill 7.4.1: Define incident severity + comms protocol

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/incident-severity.md` defining the team's P0–P3 severity tiers with examples, escalation chain, communication protocol (Slack channel naming, stakeholder updates, customer comms cadence). Document the comms template for each severity.

**Skill progression by level:**
- [ ] **Junior** — Recognize incident severity tiers.
- [ ] **Mid** — Apply existing severity definitions during an incident.
- [ ] **🎯 Senior (TARGET)** — Define the severity policy + comms protocol; lead the team during a real or simulated incident; mentor mid-level engineers on incident response.
- [ ] **Staff** — Architect cross-team incident management with shared on-call rotation.
- [ ] **Principal** — Govern org-wide incident-response standards.

---

### Sub-skill 7.4.2: Lead blameless postmortems

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/postmortem-template.md` with the team's blameless postmortem structure (timeline, contributing factors, what went well, what went poorly, action items with owners + dates) and the 5-whys analysis. Lead 1 simulated postmortem in the Lab (`docs/runbooks/incidents/lab-001.md`) with structural action items.

**Skill progression by level:**
- [ ] **Junior** — Recognize blameless postmortem as a culture.
- [ ] **Mid** — Apply the postmortem template after a small incident.
- [ ] **🎯 Senior (TARGET)** — Lead postmortems with rigor; drive structural fixes; mentor mid-level engineers on writing them.
- [ ] **Staff** — Architect cross-team postmortem-learning programs + tracking.
- [ ] **Principal** — Govern org-wide postmortem culture + executive escalation.

---

### Sub-skill 7.4.3: Author runbooks for critical systems

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author runbooks for 3 critical Lab systems in `docs/runbooks/` — each runbook covers: system overview, normal-operation expectations, common failure modes + diagnostic queries, recovery procedures, escalation contacts. Update runbooks after each incident based on what was missing.

**Skill progression by level:**
- [ ] **Junior** — Read existing runbooks during on-call.
- [ ] **Mid** — Apply a runbook step-by-step; suggest updates.
- [ ] **🎯 Senior (TARGET)** — Author the team's 3 critical-system runbooks; review and update them post-incident; mentor mid-level engineers on runbook authoring.
- [ ] **Staff** — Architect a cross-team runbook library + automation (runbook-as-code).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 7.5 — Select an Observability Stack

> **What "Senior at this Skill" means.** A Senior here can defend the team's Prometheus + Grafana + OTel choice by knowing the alternatives — ELK / Loki / Splunk / Datadog / Sentry — and recognizing when each beats the default at different employers.

### Sub-skill 7.5.1: Own ELK / Loki / EFK fluency for log aggregation

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/elk-loki-efk.md` covering the ELK stack (Elasticsearch + Logstash + Kibana), the EFK variant (Fluentd or Fluent Bit replacing Logstash), and Grafana Loki (log-aggregation aligned with Prometheus's label model). Apply ELK or Loki in the Lab for centralized logs from all DAGs. Apply Sentry for error tracking across Python services.

**Skill progression by level:**
- [ ] **Junior** — Recognize ELK and Loki by name.
- [ ] **Mid** — Apply Kibana or Loki Explore for log search.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab logging stack + Sentry integration; document Logstash-vs-Fluentd choice; mentor mid-level engineers on log-driven debugging.
- [ ] **Staff** — Architect log-aggregation at platform scale (multi-tenant, retention, cost).
- [ ] **Principal** — Govern org-wide logging platform strategy.

---

### Sub-skill 7.5.2: Compare Splunk / Datadog / New Relic / Honeycomb (commercial enterprise observability)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/commercial-observability.md` comparing Splunk + Splunk Cloud (enterprise-dominant, expensive), Datadog (unified APM + logs + infra + RUM), New Relic, and Honeycomb (high-cardinality observability). Document where each beats Prometheus + Grafana + OTel + ELK and where the cost rarely justifies it.

**Skill progression by level:**
- [ ] **Junior** — Recognize the names.
- [ ] **Mid** — Apply Datadog or Splunk if it's the company's choice.
- [ ] **🎯 Senior (TARGET)** — Evaluate commercial vendors against OSS + cost; participate in vendor-selection discussions; recognize lock-in risk.
- [ ] **Staff** — Architect cross-team observability vendor strategy + migration paths.
- [ ] **Principal** — Govern org-wide observability vendor decisions at significant budget scale.

---

### Sub-skill 7.5.3: Define observability stack selection criteria

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/observability-selection.md` with the team's decision matrix (cost, vendor lock-in, OSS vs SaaS, retention, multi-tenant support, query power, alerting integration) and the recommendation: OSS Prometheus + Grafana + Loki + OTel by default; commercial only when scale or compliance requires.

**Skill progression by level:**
- [ ] **Junior** — Recognize that observability tools differ.
- [ ] **Mid** — Apply existing team conventions.
- [ ] **🎯 Senior (TARGET)** — Define the selection matrix; review proposals for new vendor adoption; mentor mid-level engineers on the trade-offs.
- [ ] **Staff** — Architect cross-team observability platform decisions with TCO modeling.
- [ ] **Principal** — Govern org-wide observability portfolio.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 5 Story-level 🎯 boxes are ticked** — which requires the 15 sub-skill 🎯 Senior boxes. Mastery evidence: structured logging across all DAGs, OTel tracing on 1 pipeline, Prometheus + Grafana stack with platform-health dashboard, SLO catalog with burn-rate alerts, 3 critical-system runbooks, 1 simulated postmortem with structural fixes, ELK/Loki + Sentry shipped in the Lab.
