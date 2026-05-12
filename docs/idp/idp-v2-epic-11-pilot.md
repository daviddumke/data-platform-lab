# IDP v2 — Epic 11 Pilot · Security and Compliance

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's security discipline — IAM with least-privilege, secrets management with rotation, PII classification + masking, and regulatory compliance (LGPD/GDPR + audit logging). They've shipped the team's RBAC, Vault, PII tagging, masking policies, and DSAR runbook.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 11.1 — Engineer Identity & Access Control

> **What "Senior at this Skill" means.** A Senior here owns the team's IAM discipline — least-privilege across cloud IAM + K8s RBAC + SSO/SAML/OIDC, with a quarterly access review that catches drift before it becomes an audit finding.

### Sub-skill 11.1.1: Engineer cloud-native IAM with least-privilege

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cloud-iam.md` covering AWS IAM (policies, roles, conditions, permission boundaries, SCPs, IAM Access Analyzer), GCP IAM (roles primitives vs predefined vs custom, conditions), Azure RBAC (built-in vs custom roles, scopes). Document the team's least-privilege pattern + anti-patterns ("admin everywhere", over-broad wildcards). Implement minimal RBAC across the Lab K8s with versioned manifests.

**Skill progression by level:**
- [ ] **Junior** — Recognize IAM as the cloud's permission system.
- [ ] **Mid** — Apply existing IAM policies to new resources.
- [ ] **🎯 Senior (TARGET)** — Engineer least-privilege IAM across Lab K8s; review PRs for permission creep; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-account / cross-org IAM strategy.
- [ ] **Principal** — Govern org-wide IAM policy + audit findings.

---

### Sub-skill 11.1.2: Design RBAC vs ABAC vs ReBAC + SSO/SAML/OIDC

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/rbac-abac-rebac.md` comparing role-based, attribute-based, and relationship-based access control models — with use cases for each (RBAC for org-aligned groups, ABAC for dynamic attributes, ReBAC for hierarchical / graph-based authorization). Document SSO + SAML + OIDC flows used by the team and the integration patterns with the catalog + warehouse.

**Skill progression by level:**
- [ ] **Junior** — Recognize RBAC as a model.
- [ ] **Mid** — Apply RBAC; recognize SAML/OIDC integrations.
- [ ] **🎯 Senior (TARGET)** — Define when to use RBAC vs ABAC vs ReBAC; engineer SSO/SAML integration in the Lab; review proposals.
- [ ] **Staff** — Architect cross-platform identity federation.
- [ ] **Principal** — Govern org-wide identity strategy.

---

### Sub-skill 11.1.3: Operate quarterly access reviews + audit discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/access-review.md` defining the team's quarterly access-review process — what to look at (orphaned accounts, over-privileged users, stale service accounts, expired credentials), how to execute, what to document. Publish the first review's results in `docs/access-reviews/2026Q3-review.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize that access drifts over time.
- [ ] **Mid** — Apply existing access-review procedures.
- [ ] **🎯 Senior (TARGET)** — Own the quarterly cadence; lead the first review; mentor mid-level engineers; document findings + remediation.
- [ ] **Staff** — Architect automated access-review tooling at platform scale.
- [ ] **Principal** — Govern org-wide access-management program.

---

## Story 11.2 — Operate Secrets Management

> **What "Senior at this Skill" means.** A Senior here owns the team's secrets discipline — Vault or cloud secrets manager, rotation automation, KMS-based envelope encryption, and pre-commit secret detection that catches accidental commits before they leak.

### Sub-skill 11.2.1: Engineer secrets manager adoption (Vault / cloud-native)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/secrets-managers.md` comparing HashiCorp Vault, AWS Secrets Manager, GCP Secret Manager, Azure Key Vault, and Kubernetes Secrets (the in-cluster minimum) — across features, cost, multi-region support, operational complexity. Engineer Vault in the Lab via Docker Compose with sidecar-injector pattern for pod-side secret consumption.

**Skill progression by level:**
- [ ] **Junior** — Recognize secrets-manager category.
- [ ] **Mid** — Apply existing secrets manager as a consumer.
- [ ] **🎯 Senior (TARGET)** — Engineer Vault in the Lab + sidecar injection; review PRs for inline-secrets violations; mentor mid-level engineers.
- [ ] **Staff** — Architect secrets-manager-as-a-service at platform scale (multi-tenant, multi-region).
- [ ] **Principal** — Govern org-wide secrets strategy + breach response.

---

### Sub-skill 11.2.2: Design key management (KMS, envelope encryption, HSM)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/key-management.md` covering KMS architecture (customer-managed keys, envelope encryption, key policies, grants, multi-region keys), HSM-backed keys (FIPS 140-2 / 3 compliance), and the team's encryption-at-rest policy. Document key-rotation cadence.

**Skill progression by level:**
- [ ] **Junior** — Recognize KMS by name.
- [ ] **Mid** — Apply existing KMS-encrypted storage.
- [ ] **🎯 Senior (TARGET)** — Design the team's key-management strategy; review PRs for missing encryption; mentor on envelope encryption.
- [ ] **Staff** — Architect key-management strategy at multi-region + multi-account scale.
- [ ] **Principal** — Govern org-wide encryption + HSM strategy.

---

### Sub-skill 11.2.3: Engineer secret rotation + leak prevention (gitleaks, detect-secrets)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/secret-rotation.md` covering the team's rotation cadence (60-day default, shorter for high-privilege), automation patterns (Vault dynamic secrets, AWS RDS native rotation), and emergency-rotation runbook. Engineer pre-commit gitleaks/detect-secrets in the Lab with CI gate that rejects commits containing detected secrets.

**Skill progression by level:**
- [ ] **Junior** — Recognize secret leaks as a risk.
- [ ] **Mid** — Apply existing rotation procedures.
- [ ] **🎯 Senior (TARGET)** — Engineer rotation automation + leak prevention; ship the CI gate; document the emergency runbook.
- [ ] **Staff** — Architect cross-team rotation infrastructure with automated detection.
- [ ] **Principal** — Govern org-wide secret-leak response.

---

## Story 11.3 — Secure PII & Sensitive Data

> **What "Senior at this Skill" means.** A Senior here can identify PII in the team's data, classify it, apply masking + tokenization where appropriate, and implement column-level + row-level security to enforce access. They've tagged 100% of PII columns and shipped masking policies.

### Sub-skill 11.3.1: Define PII classification + tagging discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/pii-classification.md` covering the taxonomy — direct PII (name, email, phone, SSN), indirect/quasi-PII (IP, fingerprint, location-pair), sensitive (health, financial, biometric), and the team's tagging convention (`meta: { pii: true, pii_class: direct }` in dbt YAML). Apply `pii: true` tags on 100% of sensitive columns in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize PII as a category.
- [ ] **Mid** — Apply existing PII tags.
- [ ] **🎯 Senior (TARGET)** — Define the classification + tagging discipline; review PRs for missing tags; mentor mid-level engineers on indirect-PII recognition.
- [ ] **Staff** — Architect cross-team PII inventory + automated discovery.
- [ ] **Principal** — Govern org-wide PII policy + data-minimization strategy.

---

### Sub-skill 11.3.2: Engineer masking + tokenization + format-preserving encryption

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/masking-tokenization.md` covering masking techniques (deterministic, format-preserving, k-anonymity), tokenization (replace sensitive value with token + secure mapping), encryption (column-level), and hashing (one-way for joins). Document when each fits. Engineer masking policies in the Lab (BigQuery dynamic data masking or Snowflake) + IAM binding to apply by role.

**Skill progression by level:**
- [ ] **Junior** — Recognize masking and tokenization as concepts.
- [ ] **Mid** — Apply existing masking under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab masking policies + IAM binding; document the policy decision tree; review PRs for masking correctness.
- [ ] **Staff** — Architect cross-warehouse masking infrastructure + audit logging.
- [ ] **Principal** — Govern org-wide masking + tokenization strategy.

---

### Sub-skill 11.3.3: Design column-level + row-level security (CLS + RLS)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cls-rls.md` covering column-level security (CLS — restrict access to specific columns by role) + row-level security (RLS — restrict rows by user context) implementations across BigQuery, Snowflake, Postgres. Apply CLS+RLS in 1 Lab mart with documented test cases.

**Skill progression by level:**
- [ ] **Junior** — Recognize CLS and RLS as concepts.
- [ ] **Mid** — Apply existing CLS/RLS rules.
- [ ] **🎯 Senior (TARGET)** — Engineer Lab CLS+RLS; design marts to support them; review proposals.
- [ ] **Staff** — Architect cross-warehouse CLS+RLS conventions + automated enforcement.
- [ ] **Principal** — Govern org-wide access-control policy.

---

## Story 11.4 — Govern Regulatory Compliance (LGPD/GDPR)

> **What "Senior at this Skill" means.** A Senior here owns the team's compliance discipline — LGPD baseline, GDPR parallels, audit-logging integration, DSAR runbook (right-to-erasure) — at a level where audit findings don't surprise the team.

### Sub-skill 11.4.1: Define LGPD baseline (and GDPR parallels)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/lgpd-baseline.md` covering LGPD (Brazilian regulation) requirements: legal bases (consent, contract, legitimate interest, etc.), data subject rights (access, rectification, deletion, portability), DPO role, ANPD oversight. Cross-reference GDPR parallels (lawful basis, DSAR, right-to-erasure). Document the team's LGPD compliance checklist per dataset.

**Skill progression by level:**
- [ ] **Junior** — Recognize LGPD/GDPR as data-protection laws.
- [ ] **Mid** — Apply existing LGPD conventions when adding new sources.
- [ ] **🎯 Senior (TARGET)** — Define the team's LGPD baseline; review proposals for compliance fit; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team LGPD compliance program.
- [ ] **Principal** — Govern org-wide LGPD/GDPR strategy + DPO coordination.

---

### Sub-skill 11.4.2: Engineer audit-logging sink + detection queries

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/audit-logging.md` covering BigQuery audit logs, AWS CloudTrail, GCP Cloud Audit Logs, and the team's audit-events policy (every admin action, every PII access, every privilege grant). Engineer an audit logging sink in the Lab (e.g., CloudTrail → S3 → Athena) + detection queries for high-risk events.

**Skill progression by level:**
- [ ] **Junior** — Recognize audit logs as a concept.
- [ ] **Mid** — Apply existing audit-log queries.
- [ ] **🎯 Senior (TARGET)** — Engineer audit-log sink + detection queries; mentor mid-level engineers on log analysis; review proposals.
- [ ] **Staff** — Architect cross-source audit-log aggregation + SIEM integration.
- [ ] **Principal** — Govern org-wide audit + compliance reporting.

---

### Sub-skill 11.4.3: Own the DSAR runbook (right-to-erasure)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/runbooks/dsar.md` covering the team's DSAR (Data Subject Access Request) process — how to find all data about a subject (using lineage + PII tags), how to fulfill access/rectification/deletion requests, what the SLA is, what the audit trail looks like. Document the team's approach to right-to-erasure in event streams + historical backups (the hardest case).

**Skill progression by level:**
- [ ] **Junior** — Recognize DSAR + right-to-erasure as concepts.
- [ ] **Mid** — Apply existing DSAR procedures.
- [ ] **🎯 Senior (TARGET)** — Own the DSAR runbook; execute 1 simulated DSAR end-to-end; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-system DSAR tooling + automation.
- [ ] **Principal** — Govern org-wide DSAR program + regulatory reporting.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 4 Story-level 🎯 boxes are ticked** — which requires the 12 sub-skill 🎯 Senior boxes. Mastery evidence: minimal K8s RBAC in the Lab, first quarterly access review, Vault stack with sidecar injection, key-management strategy doc, gitleaks pre-commit + CI gate, 100% PII tags on Lab columns, masking + IAM binding in 1 mart, CLS+RLS in 1 mart, LGPD baseline doc, audit-log sink + detection queries, DSAR runbook + 1 simulated DSAR.
