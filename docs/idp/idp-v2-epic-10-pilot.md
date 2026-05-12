# IDP v2 — Epic 10 Pilot · Data Governance

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's discipline around catalog + lineage + ownership + contracts + data products. They've stood up the catalog (DataHub or OpenMetadata), shipped column-level lineage for the critical KPIs, published the ownership matrix, and treated at least 1 domain as a complete data product. Also covers feature stores + API gateways as data-product surface.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 10.1 — Operate Data Catalog & Documentation

> **What "Senior at this Skill" means.** A Senior here owns the team's catalog adoption — they evaluated DataHub vs OpenMetadata vs Amundsen vs Unity Catalog, stood up the choice in the Lab, integrated dbt metadata, and made sure every mart has owner + description + exposures.

### Sub-skill 10.1.1: Evaluate + engineering the team's data catalog (DataHub / OpenMetadata)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/data-catalog-landscape.md` comparing DataHub, OpenMetadata, Apache Amundsen, Apache Atlas, and Unity Catalog — across features (ingestion connectors, lineage, search, governance UI), cost, and operational complexity. Document the team's choice + rationale. Engineer the chosen catalog stack in the Lab via Docker Compose with ingestion recipes for dbt + Postgres + Iceberg.

**Skill progression by level:**
- [ ] **Junior** — Recognize the catalog tools by name.
- [ ] **Mid** — Apply existing catalog as a consumer.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab catalog; document the choice rationale; review proposals.
- [ ] **Staff** — Architect catalog-as-a-service at platform scale.
- [ ] **Principal** — Govern org-wide catalog strategy + retirement of competing tools.

---

### Sub-skill 10.1.2: Define metadata standards (OpenLineage, Apache Atlas types)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/metadata-standards.md` covering OpenLineage spec (events for START/COMPLETE/FAIL with explicit input/output references) and Apache Atlas type system. Document the team's metadata-emission policy: every DAG must emit OpenLineage events; every dbt model must populate `description` + `meta.owner`.

**Skill progression by level:**
- [ ] **Junior** — Recognize that metadata standards exist.
- [ ] **Mid** — Apply existing metadata conventions.
- [ ] **🎯 Senior (TARGET)** — Define the team's emission policy; review PRs for missing metadata; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team metadata schemas + governance.
- [ ] **Principal** — Govern org-wide metadata strategy.

---

### Sub-skill 10.1.3: Own documentation-as-code discipline (`__internal_doc`, exposures)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-docs-discipline.md` covering dbt's docs + exposures features, the team's `__internal_doc` template (sample at `transform/models/marts/core/_core__models.yml`), and the policy that every mart needs ownership + `__internal_doc` + at least 1 exposure. Apply across all Lab marts.

**Skill progression by level:**
- [ ] **Junior** — Recognize that dbt models can have docs.
- [ ] **Mid** — Apply description fields to new models.
- [ ] **🎯 Senior (TARGET)** — Own the team's docs-as-code discipline; review PRs for missing docs/owners; ship a CI gate.
- [ ] **Staff** — Architect docs-as-code pipelines + automated freshness checks.
- [ ] **Principal** — Govern org-wide documentation policy.

---

## Story 10.2 — Engineer Column-Level Lineage

> **What "Senior at this Skill" means.** A Senior here has shipped column-level lineage for at least one critical KPI — meaning they can answer "if I change this source column, what dashboards break?" with evidence, not guesswork.

### Sub-skill 10.2.1: Engineer column-level lineage for ≥1 critical KPI

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/lineage/kpi-mrr-column-lineage.md` showing the column-level lineage of 1 critical KPI (e.g., MRR or DAU) from source through all transformations to the BI dashboard. Use sqlglot + dbt manifest to generate the lineage. Document the methodology so others can replicate for other KPIs.

**Skill progression by level:**
- [ ] **Junior** — Recognize column-level vs table-level lineage.
- [ ] **Mid** — Apply existing lineage tooling.
- [ ] **🎯 Senior (TARGET)** — Engineer column-level lineage for 1 critical KPI; document the methodology; mentor mid-level engineers on lineage-driven impact analysis.
- [ ] **Staff** — Architect column-level lineage at platform scale (automated for all critical KPIs).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 10.2.2: Own lineage-driven impact analysis discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/lineage-impact-analysis.md` covering how to use lineage for: change-impact (which consumers break if a column is renamed), compliance (which dashboards expose PII), debugging (where a data-quality issue originated). Document the team's PR-review checklist for changes that affect lineage.

**Skill progression by level:**
- [ ] **Junior** — Recognize lineage as a tool for understanding dependencies.
- [ ] **Mid** — Apply lineage during PR review under guidance.
- [ ] **🎯 Senior (TARGET)** — Own the impact-analysis discipline; review PRs that change column shapes for downstream impact; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team impact-analysis tooling.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 10.3 — Govern Contracts & Ownership

> **What "Senior at this Skill" means.** A Senior here owns the team's data-contract discipline — dbt contracts at 100% on marts, the ownership matrix that says who's responsible per domain, and the stewardship cadence that keeps governance alive.

### Sub-skill 10.3.1: Own data-contract adoption (dbt + ProtoBuf + Schemata)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/data-contracts.md` covering dbt contracts (`contract: enforced: true`), Schemata as a contract-spec format, ProtoBuf for binary contracts, and the contract lifecycle (proposal → review → adoption → evolution → deprecation). Apply contracts on 100% of Lab data products with versioned YAMLs. (Cross-ref Epic 6.3.1.)

**Skill progression by level:**
- [ ] **Junior** — Recognize data contracts as a concept.
- [ ] **Mid** — Apply contracts to new marts.
- [ ] **🎯 Senior (TARGET)** — Own the team's contract adoption + lifecycle; review PRs for contract correctness; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team contract governance + automated compatibility checks.
- [ ] **Principal** — Govern org-wide data-contract policy + dispute resolution.

---

### Sub-skill 10.3.2: Define the team's ownership matrix (RACI for data)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/data-ownership.md` defining for each Lab domain: primary owner, backup owner, escalation path, and the RACI (Responsible / Accountable / Consulted / Informed) for changes. Document the team's "every dataset has a name attached" policy.

**Skill progression by level:**
- [ ] **Junior** — Recognize that datasets need owners.
- [ ] **Mid** — Apply existing ownership to PR assignments.
- [ ] **🎯 Senior (TARGET)** — Define the ownership matrix; review PRs for ownership clarity; mentor mid-level engineers on RACI.
- [ ] **Staff** — Architect cross-team RACI + automated owner-notification on change.
- [ ] **Principal** — Govern org-wide ownership policy + accountability chains.

---

### Sub-skill 10.3.3: Own stewardship cadence + governance councils

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/governance/stewardship-cadence.md` defining the team's quarterly stewardship review (each domain reviews: contracts current? owners current? PII inventory correct? dependencies clean?). Publish the minutes of the first session in `docs/governance/2026Q3-stewardship-minutes.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize stewardship as a concept.
- [ ] **Mid** — Apply existing stewardship rituals.
- [ ] **🎯 Senior (TARGET)** — Own the team's stewardship cadence; lead the first review; mentor mid-level engineers on what to look for.
- [ ] **Staff** — Architect cross-team governance councils at platform scale.
- [ ] **Principal** — Govern org-wide governance program with executive participation.

---

## Story 10.4 — Architect Data Products & Data Mesh

> **What "Senior at this Skill" means.** A Senior here can apply Zhamak Dehghani's Data Mesh framework concretely — they've treated at least 1 Lab domain as a complete data product (with input + output ports, observability, control plane, contracts, ownership).

### Sub-skill 10.4.1: Design the team's Data Product Spec

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/templates/data-product-spec.md` documenting the team's Data Product Spec template — input ports (sources), output ports (consumers), observability hooks, control plane (governance/SLA), ownership, contract. Apply the spec to 1 complete Lab domain (e.g., `orders`) as a reference: `docs/data-products/orders.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize "data product" as a term.
- [ ] **Mid** — Apply existing data-product conventions.
- [ ] **🎯 Senior (TARGET)** — Design the team's Data Product Spec; treat 1 domain as a complete data product; review proposals.
- [ ] **Staff** — Architect Data Mesh across multiple domains.
- [ ] **Principal** — Govern org-wide Data Mesh adoption strategy.

---

### Sub-skill 10.4.2: Apply Data Mesh principles (domain ownership, data-as-product, self-serve platform, federated governance)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/data-mesh-principles.md` summarizing Zhamak Dehghani's 4 principles + their concrete operationalization in the team. Document where the team is on each axis (e.g., domain ownership: partial; data-as-product: in progress; self-serve platform: aspirational; federated governance: limited).

**Skill progression by level:**
- [ ] **Junior** — Recognize Data Mesh principles by name.
- [ ] **Mid** — Apply existing data-as-product practices.
- [ ] **🎯 Senior (TARGET)** — Operationalize the 4 principles; lead the team's adoption discussions; review proposals.
- [ ] **Staff** — Architect Data Mesh program at platform scale with concrete migration plan.
- [ ] **Principal** — Govern org-wide Data Mesh strategy with executive alignment.

---

### Sub-skill 10.4.3: Engineer policy-as-code (OPA) for federated governance

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/policy-as-code.md` covering Open Policy Agent (Rego policies) for federated computational governance — encoding governance rules as machine-checkable policies (e.g., "no PII in non-tagged datasets", "every mart needs a contract"). Engineer OPA rego policies + a CI check that enforces them on the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize policy-as-code as a concept.
- [ ] **Mid** — Apply existing OPA policies.
- [ ] **Senior** — Author basic OPA policies; integrate into CI.
- [ ] **🎯 Staff (TARGET)** — Engineer the team's OPA infrastructure + CI integration; mentor on policy-as-code patterns; review policy proposals.
- [ ] **Principal** — Govern org-wide policy-as-code program.

---

## Story 10.5 — Engineer Feature Stores & API Gateways for Data Products

> **What "Senior at this Skill" means.** A Senior here understands feature stores (Feast / Tecton / SageMaker Feature Store) + API gateways (Kong / Apigee / AWS API Gateway) as the *surface* through which data products are consumed by ML and external apps. They've shipped at least 1 Feast feature view + 1 API gateway exposing a data product.

### Sub-skill 10.5.1: Engineer feature stores (Feast as the open-source reference)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/feature-stores.md` covering feature-store concepts (offline store, online store, feature views, point-in-time correctness), the training-serving skew problem and how feature stores solve it, and the alternatives landscape (Feast OSS, Tecton commercial, Databricks Feature Engineering, AWS SageMaker Feature Store). Apply Feast in the Lab with 1 offline + online feature view serving for a sample ML pipeline.

**Skill progression by level:**
- [ ] **Junior** — Recognize feature stores as ML infrastructure.
- [ ] **Mid** — Apply Feast under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Feast setup; document the training-serving skew solution; mentor ML-adjacent engineers.
- [ ] **Staff** — Architect feature-store-as-a-service across ML teams.
- [ ] **Principal** — Govern org-wide feature-store + ML-data-product strategy.

---

### Sub-skill 10.5.2: Engineer API gateways for data products (Kong, Apigee, AWS API GW)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/api-gateways-for-data.md` covering API gateway patterns for data products — auth (OAuth, API keys), rate limiting (per-tenant quotas), edge transformation, observability (metrics + tracing). Apply Kong or Apigee in the Lab exposing 1 data product with auth + rate limiting.

**Skill progression by level:**
- [ ] **Junior** — Recognize API gateways as a concept.
- [ ] **Mid** — Apply an API gateway under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab API gateway exposing 1 data product; document the patterns; review proposals.
- [ ] **Staff** — Architect API-gateway-as-a-service at platform scale.
- [ ] **Principal** — Govern org-wide data-API strategy.

---

### Sub-skill 10.5.3: Define GraphQL federation + data-contracts-as-code

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/graphql-federation.md` covering GraphQL federation patterns (Apollo Federation, Hasura) for unified data-product surfaces, plus data-contracts-as-code formats (Schemata, dbt contracts, ProtoBuf). Document when GraphQL federation beats REST for data products (multi-source aggregation, client-driven query shapes).

**Skill progression by level:**
- [ ] **Junior** — Recognize GraphQL federation by name.
- [ ] **Mid** — Apply existing federated GraphQL schemas.
- [ ] **🎯 Senior (TARGET)** — Define when federation beats REST; document data-contracts-as-code formats; review proposals.
- [ ] **Staff** — Architect federated GraphQL at platform scale across data products.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 5 Story-level 🎯 boxes are ticked** — which requires the 14 sub-skill 🎯 Senior boxes. Mastery evidence: DataHub or OpenMetadata stack running in the Lab, column-level lineage for 1 critical KPI, 100% contracts on Lab marts, ownership matrix + stewardship minutes, 1 complete Data Product Spec applied, 1 Feast feature view, 1 API gateway exposing a data product, OPA policy-as-code integration in CI.
