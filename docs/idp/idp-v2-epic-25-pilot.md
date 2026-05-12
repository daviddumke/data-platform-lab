# IDP v2 — Epic 25 Pilot · Product Vision and Business Orientation

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills treats every dataset and pipeline as a product with a clearly named owner, business context, and a sharpened scope. They can run RICE/WSJF on a backlog, walk a stakeholder through a trade-off, and decide what NOT to build. They've shipped at least one strategy proposal, scope-reduction RFC, walking skeleton, and feature-flagged dbt model in the Lab.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 25.1 — Apply Business Understanding

> **What "Senior at this Skill" means.** A Senior here connects every mart and KPI to a business context — DDD bounded contexts, North Star metrics, OKRs — so technical decisions trace back to business reasoning.

### Sub-skill 25.1.1: Define Domain-Driven Design + event storming for data products

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/ddd-event-storming.md` covering Domain-Driven Design (bounded contexts, ubiquitous language) applied to data — with at least 1 worked example showing how a DDD bounded context maps to a dbt domain — and the event storming method for discovering business events that should become facts. Mentor mid-level engineers on naming + boundaries.

**Skill progression by level:**
- [ ] **Junior** — Recognize "bounded context" as a term.
- [ ] **Mid** — Apply existing domain naming.
- [ ] **🎯 Senior (TARGET)** — Define DDD + event storming for data products; mentor mid-level engineers on bounded-context boundaries.
- [ ] **Staff** — Architect cross-team domain model + ubiquitous-language governance.
- [ ] **Principal** — Govern org-wide data-product domain policy.

---

### Sub-skill 25.1.2: Engineer KPI + OKR design and the `business.context` layer on Lab marts

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/kpis-okrs.md` covering KPI design (SMART, North Star, leading vs lagging) and OKR structure (Objectives + 3-5 Key Results) with a framework for picking the right one. Build `business.context` on all Lab marts (YAMLs populated with domain owner + business question + leading/lagging classification) + engineer 1 strategy-oriented proposal `docs/proposals/strategy-2026.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize KPIs and OKRs as concepts.
- [ ] **Mid** — Apply existing KPI definitions.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab `business.context` coverage + strategy proposal; mentor mid-level engineers on leading-vs-lagging design.
- [ ] **Staff** — Architect cross-team KPI/OKR review cadence.
- [ ] **Principal** — Govern org-wide North Star + cascading-OKR strategy.

---

## Story 25.2 — Drive Scope & Priority Negotiation

### Sub-skill 25.2.1: Engineer RICE / MoSCoW / WSJF as the team's prioritization vocabulary

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/prioritization-frameworks.md` covering RICE (Reach × Impact × Confidence / Effort), MoSCoW (Must, Should, Could, Won't), Cost of Delay / WSJF formula, and selection criteria per situation. Implement a PR template in the Lab with a "Trade-offs" section (`.github/pull_request_template.md`) that forces RICE/MoSCoW thinking into every PR.

**Skill progression by level:**
- [ ] **Junior** — Recognize prioritization frameworks exist.
- [ ] **Mid** — Apply RICE or MoSCoW under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's prioritization vocabulary; ship the PR template; mentor mid-level engineers on WSJF.
- [ ] **Staff** — Architect cross-team prioritization governance.
- [ ] **Principal** — Govern org-wide investment / capacity allocation.

---

### Sub-skill 25.2.2: Drive trade-off communication + scope-reduction RFCs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/tradeoff-comms.md` covering the scope/time/quality triangle and how to run a hard conversation with a stakeholder (the moves: name the constraint, list the options, recommend, ask for the call). Engineer 1 scope-reduction RFC in the Lab `docs/rfcs/lab-005-scope-reduction.md` cutting a real Lab feature.

**Skill progression by level:**
- [ ] **Junior** — Recognize that scope is negotiable.
- [ ] **Mid** — Apply existing scope-reduction patterns.
- [ ] **🎯 Senior (TARGET)** — Drive the scope-reduction RFC; mentor mid-level engineers on the trade-off conversation.
- [ ] **Staff** — Architect cross-team scope governance + RFC review cadence.
- [ ] **Principal** — Govern org-wide investment-vs-cut decisions.

---

## Story 25.3 — Drive Simplification & MVP Thinking

### Sub-skill 25.3.1: Engineer walking-skeleton / tracer-bullet pipelines + feature flags for data

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/walking-skeleton-flags.md` covering YAGNI / KISS / DRY (and when each is a trap), walking skeleton / tracer bullet pattern (deliver the thinnest E2E slice first), and feature flags + progressive rollout for data (GrowthBook / LaunchDarkly / dbt-macro gates). Engineer a walking skeleton (minimal E2E pipeline) on a `walking-skeleton` Lab branch + a feature flag on 1 dbt model via a macro.

**Skill progression by level:**
- [ ] **Junior** — Recognize YAGNI and "MVP first" as principles.
- [ ] **Mid** — Apply MVP thinking under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab walking skeleton + feature-flag macro; mentor mid-level engineers on when "MVP" is a trap.
- [ ] **Staff** — Architect cross-team walking-skeleton + feature-flag standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 25.4 — Design Experimentation & Data-Driven Decisions

### Sub-skill 25.4.1: Define A/B testing fundamentals + lift + attribution

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/experimentation.md` covering A/B testing fundamentals (sample size, p-values, novelty effects — referencing Kohavi's *Trustworthy Online Controlled Experiments*) and lift + attribution modeling (last-touch, time-decay, position-based, Markov-chain — canonical models with use cases). Apply on 1 Lab decision point.

**Skill progression by level:**
- [ ] **Junior** — Recognize A/B testing as a concept.
- [ ] **Mid** — Apply existing experiment results.
- [ ] **🎯 Senior (TARGET)** — Define A/B + lift + attribution; review experimental designs for novelty effects + underpowered tests; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team experimentation platform + statistical review.
- [ ] **Principal** — Govern org-wide experimentation strategy.

---

### Sub-skill 25.4.2: Architect causal inference basics (DAGs, confounders, IVs)

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/causal-inference.md` covering causal DAGs, confounders, instrumental variables, and the difference between correlation and causation in observational data — referencing Pearl's *Causality* and Cunningham's *Causal Inference: The Mixtape*. Apply on 1 Lab dataset where A/B testing is impossible.

**Skill progression by level:**
- [ ] **Junior** — Recognize causal-inference as a concept beyond A/B testing.
- [ ] **Mid** — Apply existing causal models.
- [ ] **Senior** — Read causal DAGs; identify obvious confounders.
- [ ] **🎯 Staff (TARGET)** — Architect causal-inference methodology for the team; mentor Senior engineers on observational-causal pitfalls.
- [ ] **Principal** — Govern org-wide statistical inference + reproducibility policy.

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 4 Story-level 🎯 boxes are ticked** — which requires 7 sub-skill 🎯 boxes (one at Staff). Mastery evidence: DDD + event-storming note with worked example; `business.context` on all Lab marts + strategy proposal; PR template with trade-offs section + scope-reduction RFC; walking-skeleton branch + feature-flag macro; A/B + attribution note applied to a Lab decision; causal-inference methodology for observational analysis.
