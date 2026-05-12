# IDP v2 — Epic 12 Pilot · End-to-End Architecture and Systems Thinking

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's architecture discipline — they author ADRs and RFCs that outlast the decisions, design via Well-Architected frameworks, apply systems-thinking tools (feedback loops, leverage points, Cynefin), drive DataOps maturity, and handle multi-region + hybrid/multi-cloud strategy. They've shipped ≥10 ADRs and a Wardley Map of the Lab platform.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 12.1 — Author Architectural Documentation

> **What "Senior at this Skill" means.** A Senior here writes architecture as a discipline — ADRs for decisions, RFCs for proposals, C4 diagrams for system-level shape, Arc42 for full system descriptions. They produced ≥10 ADRs that survive job changes because they're decoupled from implementation detail.

### Sub-skill 12.1.1: Author ADRs in the Michael Nygard format

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/adr/_template.md` based on Michael Nygard's ADR format (Status, Context, Decision, Consequences). Author ≥10 ADRs in `docs/adr/` covering real Lab decisions (e.g., ADR-001-iceberg-default-format, ADR-002-batch-by-default, ADR-003-trunk-based-branching, etc.). Each ADR is < 1 page and decision-focused, not implementation-focused.

**Skill progression by level:**
- [ ] **Junior** — Recognize ADRs as architecture documents.
- [ ] **Mid** — Apply the template to a small decision.
- [ ] **🎯 Senior (TARGET)** — Author ≥10 ADRs; review architecture proposals for ADR-fit; mentor mid-level engineers on decision-vs-implementation framing.
- [ ] **Staff** — Architect cross-team ADR governance + retrospective review program.
- [ ] **Principal** — Govern org-wide ADR culture and historical-record discipline.

---

### Sub-skill 12.1.2: Author RFCs (Rust-style / IETF-style) for proposals

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/rfcs/_template.md` based on Rust RFC format (motivation, guide-level explanation, reference-level explanation, drawbacks, alternatives, prior art, unresolved questions). Document the RFC lifecycle (draft → review → accepted/rejected → archived). Apply by authoring 1 Lab RFC for a non-trivial decision.

**Skill progression by level:**
- [ ] **Junior** — Recognize RFCs as a proposal format.
- [ ] **Mid** — Apply existing RFC templates.
- [ ] **🎯 Senior (TARGET)** — Author the team's RFC template + lifecycle; ship 1 substantive RFC; mentor mid-level engineers on RFC-vs-ADR distinction.
- [ ] **Staff** — Architect cross-team RFC process at platform scale.
- [ ] **Principal** — Govern org-wide RFC program with executive participation.

---

### Sub-skill 12.1.3: Design C4 model diagrams (Context, Container, Component, Code)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/c4-model.md` summarizing the C4 model (System Context, Container, Component, Code/Class) and the team's diagram conventions. Apply C4 to the Lab platform: produce Context + Container diagrams as code (Structurizr DSL or Mermaid) versioned in `docs/architecture/c4/`.

**Skill progression by level:**
- [ ] **Junior** — Recognize C4 by name.
- [ ] **Mid** — Apply C4 Context diagrams to a new system under guidance.
- [ ] **🎯 Senior (TARGET)** — Design the Lab's C4 diagrams as code; review proposals for diagram-fit at each level; mentor mid-level engineers on level-appropriate detail.
- [ ] **Staff** — Architect cross-system C4 model federation.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 12.2 — Design Systems with Well-Architected Frameworks

> **What "Senior at this Skill" means.** A Senior here applies AWS / GCP / Azure Well-Architected Framework reviews to the team's systems, captures trade-offs explicitly, and has run at least one Well-Architected review of the Lab platform.

### Sub-skill 12.2.1: Apply Well-Architected Framework reviews (AWS / GCP / Azure)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/well-architected.md` summarizing AWS Well-Architected (6 pillars: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability) and GCP Cloud Architecture Framework. Apply a Well-Architected review to the Lab platform and publish findings in `docs/architecture/wa-review.md` with action items.

**Skill progression by level:**
- [ ] **Junior** — Recognize Well-Architected as a framework.
- [ ] **Mid** — Apply existing Well-Architected reviews as a participant.
- [ ] **🎯 Senior (TARGET)** — Lead 1 Well-Architected review of the Lab; produce action items; mentor mid-level engineers on the pillar lens.
- [ ] **Staff** — Architect Well-Architected program across multiple teams + tracking.
- [ ] **Principal** — Govern org-wide Well-Architected adoption + reporting.

---

### Sub-skill 12.2.2: Design the consistency × availability × cost trade-off triangle

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/trade-off-triangle.md` covering the classic 3-way trade-off — consistency, availability, cost — and how every architecture decision picks 2 at the expense of the 3rd. Document 5 worked examples from the Lab platform showing the explicit trade-off choice.

**Skill progression by level:**
- [ ] **Junior** — Recognize that architecture has trade-offs.
- [ ] **Mid** — Apply existing trade-off reasoning to small decisions.
- [ ] **🎯 Senior (TARGET)** — Use the triangle in design reviews; make trade-offs explicit in ADRs; mentor mid-level engineers on naming the trade-off.
- [ ] **Staff** — Architect cross-team trade-off framework with examples library.
- [ ] **Principal** — Govern org-wide trade-off discipline at executive level.

---

### Sub-skill 12.2.3: Own canonical capacity planning

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/capacity-planning.md` covering the team's capacity-planning method — workload forecasting (linear, ARIMA, Prophet), headroom calculation, scaling-event detection, and the cost-of-over-vs-under-provisioning. Apply to the Lab's compute + storage + warehouse with a 12-month forecast.

**Skill progression by level:**
- [ ] **Junior** — Recognize that capacity needs planning.
- [ ] **Mid** — Apply basic capacity reasoning to specific workloads.
- [ ] **Senior** — Apply capacity planning to 1 Lab subsystem.
- [ ] **🎯 Staff (TARGET)** — Author the team's capacity-planning method + 12-month Lab forecast; mentor Senior engineers; review proposals for capacity gaps.
- [ ] **Principal** — Govern org-wide capacity-planning program with finance integration.

---

## Story 12.3 — Apply Systems Thinking

> **What "Senior at this Skill" means.** A Senior here uses systems-thinking tools — feedback loops, Donella Meadows' leverage points, the Cynefin framework — as part of normal design conversations. They've shipped the team's pre-PR impact checklist that operationalizes systems thinking.

### Sub-skill 12.3.1: Apply feedback loops + Donella Meadows leverage points

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/systems-thinking.md` covering feedback loops (balancing vs reinforcing — the engine of all system behavior) and Donella Meadows' 12 leverage points (from "constants/parameters" at the weakest to "the power to transcend paradigms" at the strongest). Document 3 worked examples from the Lab — system behaviors with their feedback-loop structure.

**Skill progression by level:**
- [ ] **Junior** — Recognize feedback loops by name.
- [ ] **Mid** — Apply feedback-loop reasoning to a specific incident.
- [ ] **🎯 Senior (TARGET)** — Use systems-thinking in design conversations; identify which leverage point a proposal acts on; mentor mid-level engineers.
- [ ] **Staff** — Architect systems-thinking culture across teams.
- [ ] **Principal** — Govern org-wide strategy informed by systems thinking.

---

### Sub-skill 12.3.2: Apply the Cynefin framework (simple/complicated/complex/chaotic)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cynefin.md` covering Snowden's Cynefin framework — 4 domains (Clear/Simple, Complicated, Complex, Chaotic) with the appropriate decision approach for each (best practice / good practice / emergent practice / novel practice). Document 5 worked examples from the team's domain showing the right approach per situation.

**Skill progression by level:**
- [ ] **Junior** — Recognize Cynefin by name.
- [ ] **Mid** — Apply Cynefin domain identification under guidance.
- [ ] **🎯 Senior (TARGET)** — Use Cynefin to frame design conversations ("this is a Complex problem, not a Complicated one — we need to probe, not plan").
- [ ] **Staff** — Architect Cynefin-aware decision-making at team scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 12.3.3: Engineer the team's pre-PR impact checklist

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author the team's pre-PR impact checklist in `.github/pull_request_template.md` operationalizing systems thinking via 5 mandatory questions: (1) cost impact? (2) lineage impact? (3) SLA impact? (4) consumer-breaking impact? (5) LGPD/GDPR impact? Apply across the Lab repo.

**Skill progression by level:**
- [ ] **Junior** — Recognize PR-review checklists.
- [ ] **Mid** — Apply existing PR checklist.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's pre-PR impact checklist; review PRs for checklist completion; mentor mid-level engineers on the 5 questions.
- [ ] **Staff** — Architect cross-team PR-checklist standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 12.4 — Architect Multi-Region & Cross-Region Replication

> **What "Senior at this Skill" means.** A Senior here understands multi-region strategies (active-active, active-passive, geo-routing) and the cost-vs-latency-vs-compliance trade-off. They've published an RFC proposing a multi-region strategy for the Lab platform.

### Sub-skill 12.4.1: Design multi-region strategies (active-active, active-passive, geo-routing)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/multi-region.md` covering the 3 main strategies (active-active for global scale + HA; active-passive for HA with cheaper standby; geo-routing for latency optimization), with their consistency / cost / failover-complexity trade-offs. Document BigQuery multi-region semantics + BigQuery Omni for multi-cloud.

**Skill progression by level:**
- [ ] **Junior** — Recognize multi-region as a pattern.
- [ ] **Mid** — Apply existing multi-region configurations.
- [ ] **🎯 Senior (TARGET)** — Design the team's multi-region strategy; review proposals; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-region infrastructure at platform scale.
- [ ] **Principal** — Govern org-wide multi-region strategy with regulatory + business alignment.

---

### Sub-skill 12.4.2: Author a multi-region RFC (Staff-level)

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/rfcs/lab-001-multi-region.md` proposing a multi-region strategy for the Lab platform — covering compute + storage + warehouse, the cost-vs-latency-vs-compliance trade-offs, the migration path, and the rollback plan. Get peer review on the RFC.

**Skill progression by level:**
- [ ] **Junior** — *(out of progression — Staff-level artifact)*
- [ ] **Mid** — Read existing multi-region RFCs.
- [ ] **Senior** — Contribute review comments on a multi-region RFC.
- [ ] **🎯 Staff (TARGET)** — Author the Lab multi-region RFC; lead the review; influence platform-level multi-region decision.
- [ ] **Principal** — Govern org-wide multi-region strategy.

---

## Story 12.5 — Drive DataOps Maturity & Strategic Mapping

> **What "Senior at this Skill" means.** A Senior here applies DataOps + DORA metrics to the team's work and uses Wardley Mapping to inform platform-strategy conversations. They've shipped a Wardley Map of the Lab + DORA-metrics scorecard.

### Sub-skill 12.5.1: Apply the DataOps Manifesto + DORA metrics

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dataops-dora.md` summarizing the 18 DataOps Manifesto principles + their concrete operationalization, plus the 4 DORA metrics applied to data pipelines (deploy frequency, lead time, MTTR, change failure rate). Engineer the Lab's DataOps maturity scorecard + DORA dashboard with quarterly tracking.

**Skill progression by level:**
- [ ] **Junior** — Recognize DataOps + DORA by name.
- [ ] **Mid** — Apply existing DataOps practices.
- [ ] **🎯 Senior (TARGET)** — Operationalize DataOps + DORA on the Lab; produce the maturity scorecard; mentor mid-level engineers.
- [ ] **Staff** — Architect DataOps + DORA program across multiple teams.
- [ ] **Principal** — Govern org-wide DataOps + DORA reporting at executive level.

---

### Sub-skill 12.5.2: Author the team's Wardley Map for platform strategy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/wardley-mapping.md` summarizing Wardley Mapping (value-chain on Y, evolution stages on X: genesis → custom-built → product → commodity). Author the Lab's Wardley Map in `docs/architecture/wardley-map.md` showing where each component sits and the strategic implications (e.g., commodity components → outsource; custom-built → invest).

**Skill progression by level:**
- [ ] **Junior** — Recognize Wardley Mapping by name.
- [ ] **Mid** — Apply Wardley analysis under guidance.
- [ ] **🎯 Senior (TARGET)** — Author the Lab's Wardley Map; use it in strategy conversations; mentor mid-level engineers.
- [ ] **Staff** — Architect Wardley Maps at platform scale with portfolio-level strategy.
- [ ] **Principal** — Govern org-wide platform strategy informed by Wardley Mapping.

---

### Sub-skill 12.5.3: Design evolutionary architecture (fitness functions)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/evolutionary-architecture.md` summarizing Ford/Parsons/Kua's evolutionary architecture concept + fitness functions (executable architecture-quality checks). Apply by defining 3 fitness functions for the Lab (e.g., "every mart must have an owner", "no pipeline > P95 latency by N%", "no source > N-day staleness").

**Skill progression by level:**
- [ ] **Junior** — Recognize evolutionary architecture by name.
- [ ] **Mid** — Apply existing fitness functions.
- [ ] **🎯 Senior (TARGET)** — Design fitness functions; integrate into CI; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team fitness-function infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 12.6 — Architect Hybrid & Multi-Cloud Strategy

> **What "Senior at this Skill" means.** A Senior here understands when hybrid (on-prem ↔ cloud) and multi-cloud (multiple clouds simultaneously) are the right answers, and how to mitigate vendor lock-in via open formats. They've shipped a hybrid POC in the Lab + an RFC proposing multi-cloud strategy.

### Sub-skill 12.6.1: Design hybrid cloud strategies (Outposts, Anthos, Azure Stack)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/hybrid-cloud.md` covering hybrid concepts (on-prem ↔ cloud bridges, edge data, dual-write windows), AWS Outposts, Azure Stack Hub + Azure Arc, GCP Anthos, VMware on cloud (VMC on AWS, AVS, GCVE). Document when hybrid is justified (regulatory data residency, latency-sensitive edge, gradual migration). Engineer a Lab hybrid POC (on-prem MinIO + cloud BigQuery) with cost-vs-latency analysis.

**Skill progression by level:**
- [ ] **Junior** — Recognize hybrid cloud as a concept.
- [ ] **Mid** — Apply existing hybrid configuration.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab hybrid POC; document justification; review proposals.
- [ ] **Staff** — Architect cross-region hybrid at platform scale.
- [ ] **Principal** — Govern org-wide hybrid strategy.

---

### Sub-skill 12.6.2: Design vendor-lock-in mitigation via open formats + abstraction layers

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/vendor-lock-in-mitigation.md` covering concrete mitigation strategies: open table formats (Iceberg over proprietary), federated query engines (Trino over BigQuery-only SQL), open observability (OpenTelemetry over Datadog-only), and abstraction layers (dbt over warehouse-native SQL). Document the cost of mitigation (operational complexity) vs the benefit (cloud portability).

**Skill progression by level:**
- [ ] **Junior** — Recognize vendor lock-in as a risk.
- [ ] **Mid** — Apply existing portable patterns.
- [ ] **🎯 Senior (TARGET)** — Define the team's lock-in posture; review proposals for portability-vs-pragmatism trade-off.
- [ ] **Staff** — Architect platform-wide portability strategy.
- [ ] **Principal** — Govern org-wide vendor + portability strategy.

---

### Sub-skill 12.6.3: Author a multi-cloud strategy RFC (Staff-level)

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/rfcs/lab-002-multi-cloud.md` proposing a multi-cloud strategy for the Lab (or a deliberate single-cloud-with-portability strategy). Cover egress-cost analysis, cross-cloud governance, identity federation (Workload Identity, SAML federation), and the migration path. Get peer review.

**Skill progression by level:**
- [ ] **Junior** — *(out of progression — Staff-level artifact)*
- [ ] **Mid** — Read existing multi-cloud RFCs.
- [ ] **Senior** — Contribute review comments to the RFC.
- [ ] **🎯 Staff (TARGET)** — Author the multi-cloud RFC; lead the review; influence platform decision.
- [ ] **Principal** — Govern org-wide multi-cloud strategy with executive alignment.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 6 Story-level 🎯 boxes are ticked** — which requires the 15 sub-skill 🎯 boxes (some at Staff). Mastery evidence: ≥10 ADRs + 1 RFC + C4 diagrams of the Lab, 1 Well-Architected review with action items, capacity-planning doc + 12-month forecast, systems-thinking + Cynefin notes, pre-PR impact checklist, multi-region RFC, DORA-metrics scorecard, Lab Wardley Map, 3 fitness functions in CI, hybrid POC, multi-cloud RFC.
