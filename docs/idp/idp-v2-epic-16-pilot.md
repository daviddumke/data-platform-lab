# IDP v2 — Epic 16 Pilot · Containerization and Reproducibility

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's container discipline — Dockerfile patterns, multi-stage builds with security scanning + image signing, dev/prod parity via Compose + devcontainers, and Kubernetes deep-dive competence (networking, storage, scheduling, operators). They've shipped multi-stage scanned + signed images and the Lab's K8s manifests with NetworkPolicies + Ingress.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 16.1 — Engineer Container Images & Runtimes

> **What "Senior at this Skill" means.** A Senior here writes Dockerfiles that pass security scanning, builds multi-stage images that ship signed, and can pick Docker vs Podman vs Containerd vs LXC per use case.

### Sub-skill 16.1.1: Engineer Dockerfile best practices + multi-stage builds

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dockerfile-best-practices.md` covering Dockerfile patterns (layer ordering for cache efficiency, COPY ordering, ARG vs ENV, multi-stage builds with `--from=builder`), distroless and minimal base images, and BuildKit advanced features (`--mount=type=cache`, secrets, ssh). Engineer the Lab's canonical Dockerfile (Python-based) with multi-stage build reducing image size by ≥60% vs single-stage.

**Skill progression by level:**
- [ ] **Junior** — Recognize Dockerfile syntax.
- [ ] **Mid** — Apply Dockerfile basics; understand layer caching at a high level.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's canonical multi-stage Dockerfile; review PRs for image-size + cache-hit hygiene; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team Dockerfile standards + base-image strategy.
- [ ] **Principal** — Govern org-wide container-image policy.

---

### Sub-skill 16.1.2: Engineer image scanning + signing + supply-chain security

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/image-supply-chain.md` covering image scanning (Trivy, Grype, Snyk), image signing (cosign, Notary v2), distroless + minimal base images, and SBOM (Software Bill of Materials) generation. Engineer the Lab CI to: scan with Trivy (fail on HIGH/CRITICAL), sign with cosign, generate SBOM, and publish to registry.

**Skill progression by level:**
- [ ] **Junior** — Recognize image scanning as a concept.
- [ ] **Mid** — Apply existing Trivy scan in CI.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab supply-chain pipeline (scan + sign + SBOM); mentor mid-level engineers on signature verification; review proposals.
- [ ] **Staff** — Architect supply-chain infrastructure at platform scale (private registry policies, attestations).
- [ ] **Principal** — Govern org-wide supply-chain security policy.

---

### Sub-skill 16.1.3: Evaluate Podman, Containerd, LXC, Mesos alternatives

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/container-runtimes.md` covering Podman (daemonless, rootless, OCI-compatible drop-in for Docker), Containerd + nerdctl (the runtime that powers Docker and K8s — the low-level alternative), LXC/LXD (system containers for full-OS isolation), Apache Mesos as a historical alternative orchestrator, and the OCI spec (image-spec, runtime-spec, distribution-spec). Apply Podman as alternative builder in the Lab with a `Containerfile` + comparison vs Docker build.

**Skill progression by level:**
- [ ] **Junior** — Recognize Docker as the default; Podman/Containerd as alternatives.
- [ ] **Mid** — Apply Docker fluently; recognize the OCI spec.
- [ ] **🎯 Senior (TARGET)** — Engineer the Podman alternative in the Lab; document when each runtime wins; mentor mid-level engineers on rootless containers.
- [ ] **Staff** — Architect cross-team runtime decisions at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 16.2 — Engineer Dev/Prod Parity

> **What "Senior at this Skill" means.** A Senior here has shipped the team's Compose dev stack + devcontainer config + local K8s setup (kind / minikube / k3d) that lets a new engineer onboard in < 1 hour to a working Lab environment indistinguishable from production.

### Sub-skill 16.2.1: Engineer the team's Docker Compose dev stack

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/compose-dev-stack.md` covering Docker Compose for dev environments — service composition, volume mounts for live-reload, health checks, networks, and dev-tool integration (debugger ports). Engineer `docker-compose.dev.yml` for the Lab covering: Postgres + MinIO + Airflow + dbt + Metabase, with documented startup procedure.

**Skill progression by level:**
- [ ] **Junior** — Recognize Docker Compose as a dev tool.
- [ ] **Mid** — Apply existing Compose files; modify services.
- [ ] **🎯 Senior (TARGET)** — Engineer the canonical dev stack; review PRs for Compose hygiene; mentor mid-level engineers on debugging-vs-prod-parity tension.
- [ ] **Staff** — Architect cross-team Compose-based dev environments.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 16.2.2: Engineer devcontainer + local K8s (kind, minikube, k3d)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/devcontainers.md` covering the `.devcontainer/devcontainer.json` spec (VS Code Dev Containers + GitHub Codespaces), and local K8s tooling (kind for K8s-in-Docker, minikube for full single-node, k3d for k3s-in-Docker). Engineer the Lab's `.devcontainer/` versioned config + a `kind` cluster manifest for local K8s testing.

**Skill progression by level:**
- [ ] **Junior** — Recognize devcontainers as a concept.
- [ ] **Mid** — Apply existing devcontainer setups.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab devcontainer + local K8s setup; document the onboarding procedure (target: < 1hr to working env); mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team devcontainer + Codespaces strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 16.3 — Architect Kubernetes Workloads

> **What "Senior at this Skill" means.** A Senior here owns the K8s details that production pipelines actually need — networking, storage, scheduling, operators — and has shipped them in the Lab.

### Sub-skill 16.3.1: Engineer K8s networking (services, ingress, NetworkPolicies, CNI)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/k8s-networking.md` covering Service types (ClusterIP, NodePort, LoadBalancer, Headless), Ingress controllers (nginx, Traefik, Contour, Gateway API), NetworkPolicies (default-deny pattern + explicit allow), and CNI plugins (Calico, Cilium with eBPF, Flannel). Engineer NetworkPolicies + Ingress in the Lab with default-deny + explicit allow rules.

**Skill progression by level:**
- [ ] **Junior** — Recognize K8s Services and Ingress.
- [ ] **Mid** — Apply existing networking manifests.
- [ ] **🎯 Senior (TARGET)** — Engineer NetworkPolicies + Ingress in the Lab; review PRs for missing network isolation; mentor mid-level engineers on CNI choice.
- [ ] **Staff** — Architect platform-wide networking strategy (service mesh, CNI selection, multi-cluster).
- [ ] **Principal** — Govern org-wide K8s networking + security policy.

---

### Sub-skill 16.3.2: Engineer K8s storage + scheduling (PV, PVC, taints, tolerations, affinity)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/k8s-storage-scheduling.md` covering PersistentVolumes + PVCs + StorageClass + CSI drivers, and scheduling controls (taints, tolerations, node affinity, pod affinity/anti-affinity, topology spread constraints). Document use cases: how to schedule heavy Spark jobs on dedicated nodes via taints + tolerations.

**Skill progression by level:**
- [ ] **Junior** — Recognize PV/PVC and scheduling primitives.
- [ ] **Mid** — Apply existing storage + scheduling manifests.
- [ ] **🎯 Senior (TARGET)** — Engineer storage + scheduling for the Lab's heavy workloads; review PRs for scheduling-fit; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-cluster storage + scheduling strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 16.3.3: Engineer K8s operators + CRDs

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/k8s-operators.md` covering the Operator pattern (controller + CRD = custom resource type with reconciliation logic), the Kubebuilder + Operator SDK frameworks, and use cases (database operators, Spark operator, custom workflow operators). Engineer a simple custom CRD + operator in the Lab (in Go or Python) for a Lab-specific resource.

**Skill progression by level:**
- [ ] **Junior** — Recognize CRDs and operators as concepts.
- [ ] **Mid** — Apply existing operators (Spark Operator, Strimzi for Kafka).
- [ ] **Senior** — Read operator code; debug operator failures.
- [ ] **🎯 Staff (TARGET)** — Engineer a custom CRD + simple operator in the Lab; document the reconciliation pattern; mentor Senior engineers.
- [ ] **Principal** — Govern org-wide operator-development standards.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 3 Story-level 🎯 boxes are ticked** — which requires the 9 sub-skill 🎯 boxes (some at Staff). Mastery evidence: canonical multi-stage Dockerfile + Trivy + cosign + SBOM pipeline, Podman alternative builder, Compose dev stack + devcontainer + kind local K8s, NetworkPolicies + Ingress + storage + scheduling manifests, 1 custom CRD + operator.
