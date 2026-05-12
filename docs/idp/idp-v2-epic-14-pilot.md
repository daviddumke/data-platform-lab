# IDP v2 — Epic 14 Pilot · CI/CD and Data Workflow

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's CI/CD discipline — pre-commit hooks + linting, slim CI for dbt, advanced Git workflow + release management, and CI/CD platform-ecosystem fluency (GitHub Actions, GitLab CI, Jenkins). They've shipped the team's CI configuration that catches problems before merge.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 14.1 — Engineer Hooks & Linting

> **What "Senior at this Skill" means.** A Senior here has shipped the team's pre-commit hooks + commitlint + sqlfluff config that the entire team uses by default, with CI gates that prevent regressions.

### Sub-skill 14.1.1: Engineer the team's pre-commit framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/pre-commit-config.md` covering pre-commit framework architecture (hooks, stages, languages), the team's canonical hook set (ruff + mypy + sqlfluff + gitleaks + commitlint + check-yaml + trailing-whitespace), and the rollout strategy (gradual hook-by-hook adoption). Apply complete pre-commit in the Lab with versioned `.pre-commit-config.yaml`.

**Skill progression by level:**
- [ ] **Junior** — Recognize pre-commit as a tool.
- [ ] **Mid** — Apply existing pre-commit hooks.
- [ ] **🎯 Senior (TARGET)** — Engineer the canonical config; review PRs for hook compliance; mentor mid-level engineers on bypass anti-patterns.
- [ ] **Staff** — Architect cross-repo pre-commit standardization.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 14.1.2: Own SQLFluff configuration + dialect tuning

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/sqlfluff-config.md` covering SQLFluff dialects, rules, fix mode, and the team's canonical config (which rules enabled, which severity, dialect-specific overrides for BigQuery / Snowflake / Postgres). Document the config-vs-noisy-warnings trade-off.

**Skill progression by level:**
- [ ] **Junior** — Recognize SQLFluff by name.
- [ ] **Mid** — Apply existing SQLFluff config.
- [ ] **🎯 Senior (TARGET)** — Own the team's SQLFluff config; tune rules for signal vs noise; review PRs for fix-mode usage.
- [ ] **Staff** — Architect cross-repo SQLFluff standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 14.1.3: Engineer commitlint + conventional commits

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/conventional-commits.md` covering the conventional commits spec (`<type>(<scope>): <subject>` + types: feat, fix, refactor, chore, docs, test, ci), the team's scope conventions, and the automation impact (semantic-release, changelog generation). Engineer commitlint + husky integration in the Lab with hooks rejecting non-conformant commits.

**Skill progression by level:**
- [ ] **Junior** — Recognize conventional commits.
- [ ] **Mid** — Apply conventional commits manually.
- [ ] **🎯 Senior (TARGET)** — Engineer the commitlint setup; review PRs for commit hygiene; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-repo commit standards + semantic-release automation.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 14.2 — Engineer Slim CI for dbt

> **What "Senior at this Skill" means.** A Senior here has shipped slim CI (`--defer --state`) and data-diff in PRs — making dbt CI fast (run only changed models) and informative (show downstream data impact).

### Sub-skill 14.2.1: Engineer dbt slim CI with `--defer --state`

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dbt-slim-ci.md` covering dbt's slim CI mechanism (defer to production state, run only modified models + downstream), state-based artifact storage (S3/GCS for `manifest.json`), and the operational setup. Engineer slim CI in the Lab via GitHub Actions running on PR with state pulled from main branch.

**Skill progression by level:**
- [ ] **Junior** — Recognize that dbt CI can be optimized.
- [ ] **Mid** — Apply existing slim CI configuration.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab slim CI; document the setup + artifact storage; review PRs for CI efficiency.
- [ ] **Staff** — Architect cross-repo dbt CI infrastructure at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 14.2.2: Engineer data-diff workflow in PRs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/data-diff-ci.md` covering data-diff approaches (Datafold OSS, dbt-checkpoint, home-grown SQL diff), the team's PR-review integration (auto-run diff, post results as comment), and the trade-offs (cost of running diff vs value of catching unintended changes). Engineer a CI workflow that runs data-diff on dbt model changes + comments on the PR.

**Skill progression by level:**
- [ ] **Junior** — Recognize data-diff as a tool.
- [ ] **Mid** — Apply manual data-diff locally.
- [ ] **🎯 Senior (TARGET)** — Engineer the CI integration + comment bot; mentor mid-level engineers on diff-driven review; review PRs for diff coverage.
- [ ] **Staff** — Architect cross-team data-diff infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 14.3 — Define Git Workflow & Release Management

> **What "Senior at this Skill" means.** A Senior here has defined the team's Git branching strategy (likely trunk-based for data teams) and release-management process (release branches + hotfix flow + semantic-release).

### Sub-skill 14.3.1: Define branching strategy (trunk-based / GitHub-flow / GitFlow)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/branching-strategy.md` comparing the 3 strategies — trunk-based (one main branch, short-lived feature branches, recommended for data teams), GitHub-flow (similar but with deployment-per-merge), GitFlow (long-lived develop + release branches, mostly legacy). Document the team's choice + rationale. (Cross-ref Epic 1.2.6.)

**Skill progression by level:**
- [ ] **Junior** — Recognize the strategies by name.
- [ ] **Mid** — Apply the team's chosen strategy correctly.
- [ ] **🎯 Senior (TARGET)** — Define the strategy + rationale; review PRs for branch hygiene; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-repo branching standards.
- [ ] **Principal** — Govern org-wide source-control policy.

---

### Sub-skill 14.3.2: Design release branches + hotfix flow

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/runbooks/release-flow.md` covering the team's release process — when to cut a release branch, the hotfix flow for production-blocking bugs, the rollback procedure. For data teams with continuous deployment, document the equivalent: tagged releases, change-review-period before merge to main.

**Skill progression by level:**
- [ ] **Junior** — Recognize that releases need process.
- [ ] **Mid** — Apply the existing release process.
- [ ] **🎯 Senior (TARGET)** — Define the release-flow doc; lead the first release + retrospective; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team release management with shared automation.
- [ ] **Principal** — Govern org-wide release policy.

---

### Sub-skill 14.3.3: Engineer semantic-release + changelog automation

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/semantic-release.md` covering semantic-release configuration (read conventional commits → determine version bump → generate changelog → tag release), and the integration with PyPI / internal package registry. Apply to 1 Lab Python package.

**Skill progression by level:**
- [ ] **Junior** — Recognize semantic-release by name.
- [ ] **Mid** — Apply existing semantic-release configuration.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's semantic-release setup; document the changelog generation; review PRs for version-impact correctness.
- [ ] **Staff** — Architect cross-repo semantic-release at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 14.4 — Select CI/CD Platforms

> **What "Senior at this Skill" means.** A Senior here can defend the team's CI/CD platform choice by knowing the alternatives — GitHub Actions, GitLab CI, Jenkins, CircleCI, cloud-native CI (CodePipeline, Cloud Build, Azure DevOps) — and has run the same pipeline in two of them for comparison.

### Sub-skill 14.4.1: Own GitHub Actions + GitLab CI fluency

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/github-vs-gitlab-ci.md` covering GitHub Actions (workflows, jobs, matrix, reusable workflows, OIDC to cloud) and GitLab CI/CD (pipelines, stages, includes, child pipelines, runners, GitLab Runner architecture). Document the team's choice + positioning.

**Skill progression by level:**
- [ ] **Junior** — Recognize the two platforms.
- [ ] **Mid** — Apply the team's chosen platform.
- [ ] **🎯 Senior (TARGET)** — Own fluency in both; review proposals; mentor mid-level engineers on reusable workflows + matrix builds.
- [ ] **Staff** — Architect cross-repo CI patterns at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 14.4.2: Evaluate Jenkins / CircleCI / cloud-native CI alternatives

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/ci-alternatives.md` covering Jenkins (legacy ubiquity, Jenkinsfile, declarative vs scripted, shared libraries), CircleCI (orbs, contexts, executors), and cloud-native CI (AWS CodePipeline, GCP Cloud Build, Azure DevOps Pipelines). Document when each beats GitHub Actions + GitLab CI.

**Skill progression by level:**
- [ ] **Junior** — Recognize the names.
- [ ] **Mid** — Apply one of them under guidance.
- [ ] **🎯 Senior (TARGET)** — Evaluate alternatives + recommend per context; review proposals.
- [ ] **Staff** — Architect CI-platform-selection strategy at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 14.4.3: Engineer OIDC-based cloud authentication from CI

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/ci-oidc.md` covering OpenID Connect federation from CI runners to cloud (no static credentials) — AWS IAM Roles Anywhere or AWS IAM IDP, GCP Workload Identity Federation, Azure federated credentials. Engineer OIDC-based auth in the Lab CI workflows.

**Skill progression by level:**
- [ ] **Junior** — Recognize that CI needs to authenticate to cloud.
- [ ] **Mid** — Apply existing OIDC config or static credentials.
- [ ] **🎯 Senior (TARGET)** — Engineer OIDC federation in the Lab; document the setup; mentor mid-level engineers on rotating away from static credentials.
- [ ] **Staff** — Architect platform-wide OIDC federation policy.
- [ ] **Principal** — Govern org-wide CI-to-cloud identity policy.

---

### Sub-skill 14.4.4: Engineer the same pipeline in 2 CI platforms (comparison artifact)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer the same pipeline in GitHub Actions AND GitLab CI in the Lab on `compare-ci` branch with a comparative ADR documenting verbosity, ergonomics, secrets handling, parallelism patterns, and cost.

**Skill progression by level:**
- [ ] **Junior** — *(out of progression — Senior-level applied work)*
- [ ] **Mid** — Apply 1 CI platform fluently.
- [ ] **🎯 Senior (TARGET)** — Engineer the comparison + ADR; influence platform CI choice.
- [ ] **Staff** — *(out of progression — covered by 14.4.2)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 4 Story-level 🎯 boxes are ticked** — which requires the 10 sub-skill 🎯 Senior boxes. Mastery evidence: complete pre-commit + commitlint config, SQLFluff team config, slim CI + data-diff workflow, branching-strategy doc, release-flow runbook, semantic-release on 1 Lab package, OIDC federation in CI, GitHub Actions vs GitLab CI comparison ADR.
