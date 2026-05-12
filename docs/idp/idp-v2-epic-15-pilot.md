# IDP v2 — Epic 15 Pilot · Infrastructure as Code

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's IaC discipline — Terraform for provisioning, Kubernetes manifests + Helm + Kustomize for orchestration, GitOps for declarative deployment, and configuration management (Ansible) for the gap that Terraform doesn't fill. They've shipped reusable Terraform modules + Helm charts the team forks from.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 15.1 — Engineer Terraform at Scale

> **What "Senior at this Skill" means.** A Senior here writes Terraform that other engineers fork — reusable modules, well-managed state, with Terratest. They've shipped the team's `data_domain` module (BQ dataset + IAM + alerting as one unit) used across multiple Lab domains.

### Sub-skill 15.1.1: Own Terraform fundamentals + state backends

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/terraform-fundamentals.md` covering Terraform's data model (providers, resources, data sources, state, modules) and state backends (S3 + DynamoDB lock, GCS, Terraform Cloud). Document the team's state-management policy (per-environment state files, locking discipline, never edit state directly).

**Skill progression by level:**
- [ ] **Junior** — Recognize Terraform as IaC.
- [ ] **Mid** — Apply terraform commands; write basic resources.
- [ ] **🎯 Senior (TARGET)** — Own the team's state-management discipline; review PRs for state-corruption risk; mentor mid-level engineers on locking + drift.
- [ ] **Staff** — Architect cross-account Terraform state infrastructure.
- [ ] **Principal** — Govern org-wide IaC policy + state-management standards.

---

### Sub-skill 15.1.2: Engineer reusable Terraform modules

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/terraform-modules.md` covering module-authoring best practices (input variables with validation, output values, version pinning, documented `README.md`, semver). Engineer the team's `data_domain` reusable module that bundles BigQuery dataset + IAM bindings + alerting + cost-attribution tags as one unit, used by multiple Lab domains.

**Skill progression by level:**
- [ ] **Junior** — Recognize Terraform modules.
- [ ] **Mid** — Apply existing modules; understand input/output variables.
- [ ] **🎯 Senior (TARGET)** — Engineer the `data_domain` module + README + versioning; review PRs for module re-use opportunities; mentor mid-level engineers.
- [ ] **Staff** — Architect platform-wide module catalog with shared registry.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 15.1.3: Engineer Terraform testing (Terratest, native testing) + Terragrunt for DRY

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/terraform-testing.md` covering Terratest (Go-based integration tests that apply + verify + destroy real infra), Terraform's native testing (`terraform test`), and Terragrunt (for DRY across environments). Engineer Terratest for the `data_domain` module in `tests/` with CI integration. Document when Terragrunt earns its complexity.

**Skill progression by level:**
- [ ] **Junior** — Recognize Terraform testing as a concept.
- [ ] **Mid** — Apply existing Terratest tests under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer Terratest for Lab modules + CI integration; document the testing methodology; review PRs for testing coverage.
- [ ] **Staff** — Architect cross-team Terraform testing infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 15.2 — Engineer Kubernetes Manifests & Helm

> **What "Senior at this Skill" means.** A Senior here owns the team's K8s manifest + Helm chart practice — knows the K8s primitives, has authored the team's canonical Helm chart, and uses Kustomize for environment overlays.

### Sub-skill 15.2.1: Own K8s primitives (Pod, Deployment, Job, CronJob, StatefulSet)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/k8s-primitives.md` covering the K8s workload primitives (Pod, Deployment for stateless, StatefulSet for ordered/persistent, Job for one-shot, CronJob for scheduled) + when each fits. Document the team's preferred primitive per workload class.

**Skill progression by level:**
- [ ] **Junior** — Recognize the K8s primitives by name.
- [ ] **Mid** — Apply existing manifests; modify resource specs.
- [ ] **🎯 Senior (TARGET)** — Own the team's workload-primitive decisions; review PRs for primitive fit; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team K8s primitive conventions.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 15.2.2: Engineer Helm charts (templates, values, dependencies, hooks)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/helm.md` covering Helm chart architecture (Chart.yaml, templates/, values.yaml + values-*.yaml per env, dependencies + subcharts, hooks for ordering). Engineer the team's Helm chart for the Lab stack in `deploy/helm/lab/` with values per environment.

**Skill progression by level:**
- [ ] **Junior** — Recognize Helm as a K8s package manager.
- [ ] **Mid** — Apply existing Helm charts.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's Helm chart + values discipline; review chart PRs; mentor mid-level engineers on templating anti-patterns.
- [ ] **Staff** — Architect cross-team Helm chart library + private registry.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 15.2.3: Engineer Kustomize overlays + Helm-vs-Kustomize decision

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/kustomize-vs-helm.md` covering Kustomize (overlay-based, no templating, K8s-native) vs Helm (template-based, more powerful but with templating-quirks risk), and the team's "when to use which" decision. Engineer Kustomize dev/prod overlays in `deploy/k8s/{base,overlays}/` in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize Kustomize as an alternative.
- [ ] **Mid** — Apply existing Kustomize overlays.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's Kustomize base + overlays; define the Helm-vs-Kustomize decision; review proposals.
- [ ] **Staff** — Architect cross-team K8s manifest-tooling strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 15.3 — Operate GitOps (ArgoCD, Flux)

> **What "Senior at this Skill" means.** A Senior here has shipped GitOps in the Lab — Git is the source of truth, ArgoCD or Flux reconciles to cluster. They understand the trade-offs of both tools.

### Sub-skill 15.3.1: Design GitOps principles + ArgoCD adoption

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/gitops.md` covering GitOps principles (declarative, versioned, pull-based, continuous reconciliation), ArgoCD architecture (Applications, ApplicationSets, sync policies, sync waves, projects), and the team's deployment-vs-rollback workflow. Engineer ArgoCD in the Lab syncing manifests from Git to cluster + Application manifests for the Lab stack.

**Skill progression by level:**
- [ ] **Junior** — Recognize GitOps as a concept.
- [ ] **Mid** — Apply existing ArgoCD Applications.
- [ ] **🎯 Senior (TARGET)** — Engineer ArgoCD in the Lab; document the sync-policy decisions; mentor mid-level engineers on declarative-deployment patterns.
- [ ] **Staff** — Architect cross-cluster GitOps infrastructure.
- [ ] **Principal** — Govern org-wide GitOps adoption.

---

### Sub-skill 15.3.2: Evaluate Flux as ArgoCD alternative

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/flux-vs-argocd.md` covering Flux (HelmRelease, Kustomization, image-automation, less UI-heavy) and the trade-offs vs ArgoCD (Flux is more declarative-CRD-pure; ArgoCD has better UI). Document when Flux beats ArgoCD.

**Skill progression by level:**
- [ ] **Junior** — Recognize Flux as a GitOps tool.
- [ ] **Mid** — Apply Flux under guidance.
- [ ] **🎯 Senior (TARGET)** — Evaluate Flux vs ArgoCD; recommend per context; review proposals.
- [ ] **Staff** — Architect cross-tool GitOps strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 15.4 — Operate Configuration Management

> **What "Senior at this Skill" means.** A Senior here owns the gap that Terraform doesn't fill — what *inside* the VMs/hosts (vs what infra exists). They've shipped Ansible playbooks for at least 1 Lab environment, with a clear understanding of when configuration management vs immutable infrastructure wins.

### Sub-skill 15.4.1: Engineer Ansible playbooks (the canonical config-management tool)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/ansible.md` covering Ansible's data model (inventory, playbooks, roles, modules, Ansible Vault), idempotent module design, and the team's playbook conventions. Engineer Ansible playbooks in the Lab to configure a VM with the full stack (Python, dbt, dependencies, system services) with versioned inventory.

**Skill progression by level:**
- [ ] **Junior** — Recognize Ansible as a config-management tool.
- [ ] **Mid** — Apply existing playbooks.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Ansible playbooks; document the playbook conventions; review PRs for idempotency.
- [ ] **Staff** — Architect cross-team Ansible infrastructure with shared roles.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 15.4.2: Evaluate Chef, Puppet, SaltStack as alternatives

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/config-mgmt-alternatives.md` covering Chef (Ruby DSL, Chef Server architecture), Puppet (declarative manifests, agent-based vs masterless), and SaltStack (event-driven, salt-ssh, beacons + reactors). Document the team's preferred choice (likely Ansible) + when alternatives win.

**Skill progression by level:**
- [ ] **Junior** — Recognize the alternatives by name.
- [ ] **Mid** — Apply one of them when required.
- [ ] **🎯 Senior (TARGET)** — Evaluate alternatives; defend the Ansible choice; review proposals.
- [ ] **Staff** — Architect cross-tool config-management strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 15.4.3: Define configuration management vs immutable infrastructure decision

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/config-mgmt-vs-immutable.md` covering the decision: configuration management (Ansible-style, mutate existing hosts) vs immutable infrastructure (rebuild from image / container — Packer + Terraform). Document the team's policy: immutable by default for cloud workloads, config-management for on-prem/hybrid + edge cases. Engineer a hybrid Terraform-creates-infra + Ansible-configures-it flow in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize the two approaches.
- [ ] **Mid** — Apply existing infrastructure conventions.
- [ ] **🎯 Senior (TARGET)** — Define the decision policy; ship the hybrid flow; review proposals for fit.
- [ ] **Staff** — Architect cross-team infrastructure-mutability standards.
- [ ] **Principal** — Govern org-wide infrastructure-mutability policy.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 4 Story-level 🎯 boxes are ticked** — which requires the 11 sub-skill 🎯 Senior boxes. Mastery evidence: state-management policy doc, `data_domain` Terraform module + Terratest, Lab Helm chart, Kustomize dev/prod overlays, ArgoCD running in the Lab + comparison vs Flux, Ansible playbooks + inventory, config-mgmt-vs-immutable policy + hybrid Lab flow.
