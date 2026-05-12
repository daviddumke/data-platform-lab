# IDP v2 — Epic 26 Pilot · Technical Communication and Influence

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills writes the team's authoritative technical docs (ADRs, RFCs, runbooks, one-pagers, mdBook site), translates technical work into language a non-engineer executive understands, and has begun building external visibility (≥3 published articles + ≥1 OSS contribution). One sub-skill is targeted at Principal level — delivering a conference talk.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 26.1 — Author Technical Documentation as Code

> **What "Senior at this Skill" means.** A Senior here owns the team's documentation system — ADRs/RFCs/one-pagers/runbooks correctly chosen, Diátaxis applied, diagrams as code versioned, and a published mdBook/MkDocs site exists for the Lab.

### Sub-skill 26.1.1: Define the ADR / RFC / one-pager / runbook format choice + Diátaxis taxonomy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/doc-types.md` covering the differences between ADR (Architecture Decision Record), RFC (Request for Comments), one-pager, and runbook — and when each fits — with a flowchart. Apply the Diátaxis framework (tutorials, how-tos, reference, explanation) to organize the Lab's existing docs into a 4-quadrant index.

**Skill progression by level:**
- [ ] **Junior** — Recognize ADR / RFC / runbook as terms.
- [ ] **Mid** — Apply existing ADR or RFC templates.
- [ ] **🎯 Senior (TARGET)** — Define the team's doc-type choice + Diátaxis organization; review PRs that mix doc types; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team documentation governance.
- [ ] **Principal** — Govern org-wide documentation policy.

---

### Sub-skill 26.1.2: Engineer an mdBook/MkDocs site + diagrams as code for the Lab

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/docs-as-code.md` comparing mdBook, Docusaurus, MkDocs (Material) for technical sites and Mermaid, PlantUML, Structurizr, D2 for diagrams as code. Engineer an mdBook or MkDocs public site for the Lab published on GitHub Pages with at least 5 Mermaid/D2 diagrams versioned alongside the prose. Engineer 5 rules files (`.claude/rules/*.md` style) versioned in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize docs-as-code as a concept.
- [ ] **Mid** — Apply existing static-site generators.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab site + diagrams as code + rules files; mentor mid-level engineers on diagram-source review.
- [ ] **Staff** — Architect cross-team docs-as-code infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 26.2 — Communicate to Non-Technical Audiences

### Sub-skill 26.2.1: Define the Minto Pyramid + storytelling-with-data principles for executive communication

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/exec-comms.md` covering the Minto Pyramid (idea-first, top-down communication), storytelling with data (Cole Nussbaumer Knaflic's 5 principles), and C-level slide design (10/20/30 rule, takeaway-driven — referencing Duarte's *Resonate* and Reynolds' *Presentation Zen*). Mentor mid-level engineers on idea-first writing.

**Skill progression by level:**
- [ ] **Junior** — Recognize the Minto Pyramid.
- [ ] **Mid** — Apply takeaway-first writing under guidance.
- [ ] **🎯 Senior (TARGET)** — Define the team's exec-comms style; mentor mid-level engineers on idea-first writing + slide takeaway design.
- [ ] **Staff** — Architect cross-team exec-comms standards.
- [ ] **Principal** — Govern org-wide exec-comms style.

---

### Sub-skill 26.2.2: Engineer a talk for simulated leadership + an executive one-pager for the Lab

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer 1 talk for simulated leadership (fictional executive audience — slides + recording in `docs/talks/`) applying Minto Pyramid + 10/20/30 rule. Engineer an executive one-pager for the Lab `docs/exec/lab-onepager.md` (1 page, 5 bullets, 1 chart, 1 ask).

**Skill progression by level:**
- [ ] **Junior** — Recognize one-pagers as a format.
- [ ] **Mid** — Apply existing one-pager templates.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab simulated-leadership talk + executive one-pager; mentor mid-level engineers on the "1 page, 1 ask" discipline.
- [ ] **Staff** — Architect cross-team executive briefing standards.
- [ ] **Principal** — Govern org-wide executive narrative + strategy storytelling.

---

## Story 26.3 — Drive Thought Leadership

### Sub-skill 26.3.1: Drive a sustainable writing habit + ≥3 published articles + ≥1 OSS contribution

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/writing-habit.md` covering sustainable cadence for blog / building-in-public writing (frequency, topic-pipeline, drafting workflow) and open-source contribution etiquette (PR/issue best practices). Drive ≥3 published technical articles (Medium/LinkedIn/dev.to/own blog) + ≥1 OSS contribution (issue, PR, or doc to a recognized repo) — track in `docs/publications.md` with URLs.

**Skill progression by level:**
- [ ] **Junior** — Recognize blogging and OSS as career signals.
- [ ] **Mid** — Apply existing publication workflows.
- [ ] **🎯 Senior (TARGET)** — Drive ≥3 articles + ≥1 OSS contribution; mentor mid-level engineers on draft-publish cadence.
- [ ] **Staff** — Architect cross-team external-visibility program.
- [ ] **Principal** — Govern org-wide thought-leadership strategy.

---

### Sub-skill 26.3.2: Govern conference talk crafting + delivering ≥1 meetup or conference talk

**Target:** `Principal`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cfp-talks.md` covering CFP writing method (abstract structure, story arc, target track selection, rehearsal cadence). Establish ≥1 talk delivered at a meetup or conference (recording + abstract in `docs/talks/`).

**Skill progression by level:**
- [ ] **Junior** — Recognize CFPs as a path.
- [ ] **Mid** — Apply existing talk templates.
- [ ] **Senior** — Submit + deliver an internal/meetup talk.
- [ ] **Staff** — Deliver a recognized industry-conference talk.
- [ ] **🎯 Principal (TARGET)** — Govern the team's CFP + speaking pipeline; deliver ≥1 conference talk; mentor Senior+ engineers on CFP writing.

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 3 Story-level 🎯 boxes are ticked** — which requires 5 sub-skill 🎯 boxes including 1 Principal-target (the conference talk). Mastery evidence: doc-type + Diátaxis taxonomy note; mdBook/MkDocs Lab site published on GitHub Pages with diagrams-as-code + 5 versioned `.claude/rules/` files; exec-comms note + simulated-leadership talk + executive one-pager; ≥3 published articles + ≥1 OSS contribution + ≥1 meetup/conference talk delivered.
