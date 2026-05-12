# IDP v2 — Epic 27 Pilot · Mentorship, Leadership, and Technical Responsibility

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills has shipped the team's coding standards, leads ≥1 RFC to a decision, owns ≥3 runbooks for critical Lab systems with a structural-fix culture (not just patches), and mentors at least one mid-level engineer with a documented growth conversation cadence. Two sub-skills are targeted at Principal level — the onboarding program and the cross-team Amazon 6-pager memo.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 27.1 — Author Technical Standards

### Sub-skill 27.1.1: Engineer the team's coding standards (Python, SQL, dbt, Terraform) + governance

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/coding-standards.md` summarizing the structure of canonical coding-standards documents (Google C++ Style Guide, Effective Python, Google SQL style — what to copy, what to skip) and defining standards review cadence (quarterly review, deprecation path, RFC required for changes). Engineer Lab coding standards (`.claude/rules/python.md`, `.claude/rules/sql.md`, `.claude/rules/dbt.md`, `.claude/rules/terraform.md`) with the governance section embedded.

**Skill progression by level:**
- [ ] **Junior** — Recognize coding standards exist.
- [ ] **Mid** — Apply existing standards.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's standards + governance cadence; mentor mid-level engineers on standards-vs-personal-preference.
- [ ] **Staff** — Architect cross-team standards governance.
- [ ] **Principal** — Govern org-wide engineering standards.

---

## Story 27.2 — Lead Technical Initiatives

### Sub-skill 27.2.1: Define the RFC process + leading 1 RFC to a recorded decision

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/rfc-process.md` defining the RFC process (proposal → review → decision → retrospective) with template. Lead 1 RFC + decision log in the Lab `docs/rfcs/lab-XXX.md` end-to-end (drafted, reviewed, decided, retrospected).

**Skill progression by level:**
- [ ] **Junior** — Recognize RFCs as a tool.
- [ ] **Mid** — Apply existing RFC templates as author or reviewer.
- [ ] **🎯 Senior (TARGET)** — Lead an RFC end-to-end with a recorded decision; mentor mid-level engineers through their first RFC.
- [ ] **Staff** — Architect cross-team RFC governance + cadence.
- [ ] **Principal** — Govern org-wide technical-decision-making policy.

---

### Sub-skill 27.2.2: Drive cross-team initiatives + stakeholder management (RACI, escalation, status updates)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/initiative-leadership.md` covering cross-team initiative leadership (alignment rituals, escalation paths, status update cadence) and stakeholder management (RACI matrices, sponsorship discovery, escalation timing). Implement weekly status updates for 4 weeks in the Lab (`docs/status-updates/2026-WW.md`) demonstrating the cadence on a real initiative.

**Skill progression by level:**
- [ ] **Junior** — Recognize "status update" as a ritual.
- [ ] **Mid** — Apply existing status-update templates.
- [ ] **🎯 Senior (TARGET)** — Drive a multi-week initiative with status cadence; mentor mid-level engineers on RACI + escalation timing.
- [ ] **Staff** — Architect cross-team initiative governance.
- [ ] **Principal** — Govern org-wide initiative-portfolio management.

---

## Story 27.3 — Own End-to-End Technical Responsibility

### Sub-skill 27.3.1: Define end-to-end ownership + structural-fix culture (you build it, you run it)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/e2e-ownership.md` covering the "you build it, you run it" pattern (on-call expectations, escalation paths, runbook ownership chain) and the structural-fix culture (post-incident root-cause-fix, not just patches — with a structural-fix note template). Engineer 3 runbooks for critical Lab systems (`docs/runbooks/`) + 1 structural-fix note after a simulated Lab incident (`docs/runbooks/incidents/fix-001.md`).

**Skill progression by level:**
- [ ] **Junior** — Recognize on-call as a practice.
- [ ] **Mid** — Apply existing runbooks during incidents.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab runbooks + structural-fix note; mentor mid-level engineers on root-cause vs patch.
- [ ] **Staff** — Architect cross-team ownership + on-call governance.
- [ ] **Principal** — Govern org-wide on-call + reliability culture.

---

## Story 27.4 — Lead Mentorship, Pairing & Code Review

### Sub-skill 27.4.1: Define the team's code review guide + pairing dynamics

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/code-review-pairing.md` summarizing Google's code review principles (CL size, what to look for, latency expectations, tone) and pairing / mob programming dynamics (driver/navigator, ping-pong, mob rotation, when each fits). Engineer a Lab code review guide `.claude/rules/code-review.md` for the team.

**Skill progression by level:**
- [ ] **Junior** — Recognize code review as a practice.
- [ ] **Mid** — Apply existing review guidelines.
- [ ] **🎯 Senior (TARGET)** — Define the team's review guide + pairing patterns; mentor mid-level engineers on review tone + scope.
- [ ] **Staff** — Architect cross-team code review + pairing governance.
- [ ] **Principal** — Govern org-wide review + collaboration policy.

---

### Sub-skill 27.4.2: Engineer mentorship + growth conversations (SBI feedback, IDPs, career ladders)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/mentorship-growth.md` covering feedback frameworks (SBI: Situation-Behavior-Impact, radical candor) and growth conversations (career ladders, IDPs — referencing this document!). Engineer mentoring notes in the Lab for 1 fictional mentee across 4 weeks (`docs/mentoring/2026-mentee-001.md`) demonstrating the cadence, feedback shape, and growth-conversation ritual.

**Skill progression by level:**
- [ ] **Junior** — Recognize SBI and IDP as concepts.
- [ ] **Mid** — Apply mentorship under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab mentorship cadence + 4-week notes; mentor mid-level engineers on SBI feedback delivery.
- [ ] **Staff** — Architect cross-team mentorship program.
- [ ] **Principal** — Govern org-wide career-ladder + mentorship policy.

---

## Story 27.5 — Drive Organization-Wide Standardization

### Sub-skill 27.5.1: Drive Staff-engineer archetype self-mapping (Will Larson model)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/staff-archetypes.md` summarizing Will Larson's Staff Engineer archetypes (Tech Lead, Architect, Solver, Right Hand) with self-mapping — which archetype currently fits, which to lean into, why. Reference *Staff Engineer: Leadership Beyond the Management Track* (Larson).

**Skill progression by level:**
- [ ] **Junior** — Recognize that Staff+ tracks exist.
- [ ] **Mid** — Apply archetype self-awareness under guidance.
- [ ] **🎯 Senior (TARGET)** — Drive self-mapping + a growth path toward 1 archetype; mentor mid-level engineers on career-ladder navigation.
- [ ] **Staff** — Embody an archetype; coach Seniors choosing among them.
- [ ] **Principal** — Govern org-wide Staff+ career framework.

---

### Sub-skill 27.5.2: Govern onboarding-program design + delivering a Lab data-engineer onboarding program

**Target:** `Principal`

**Activity & Artifact (Senior DoD):** Author `docs/notes/onboarding-design.md` covering onboarding program governance (week-by-week checklist, mentor pairing, 30/60/90 milestones, feedback cadence). Establish a Lab onboarding program for a data engineer `docs/onboarding/data-engineer.md` + checklist + cadence.

**Skill progression by level:**
- [ ] **Junior** — Recognize onboarding as a structured process.
- [ ] **Mid** — Apply existing onboarding checklists.
- [ ] **Senior** — Improve an existing onboarding path; mentor 1 newcomer.
- [ ] **Staff** — Design onboarding for one team.
- [ ] **🎯 Principal (TARGET)** — Govern the org-wide onboarding program; deliver the Lab data-engineer onboarding; mentor Senior+ engineers running team-level onboardings.

---

### Sub-skill 27.5.3: Govern organizational influence + delivering 1 cross-team memo (Amazon 6-pager style)

**Target:** `Principal`

**Activity & Artifact (Senior DoD):** Author `docs/notes/org-influence.md` covering organizational-influence patterns (writing memos, cross-team RFCs, town-hall narrative arcs) and the Amazon 6-pager memo format (narrative, no slides; 6 pages max; data + recommendation). Establish 1 cross-team memo (Amazon 6-pager style) in the Lab `docs/memos/2026Q3-platform-direction.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize cross-team memos as a format.
- [ ] **Mid** — Apply existing memo templates.
- [ ] **Senior** — Write a team-scope memo influencing a decision.
- [ ] **Staff** — Write a cross-team memo influencing a multi-team decision.
- [ ] **🎯 Principal (TARGET)** — Govern the org-wide memo + town-hall practice; deliver the Lab 6-pager; mentor Staff engineers on memo crafting.

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 5 Story-level 🎯 boxes are ticked** — which requires 8 sub-skill 🎯 boxes (two at Principal — the onboarding program and the Amazon 6-pager memo). Mastery evidence: 4 versioned coding-standards rules files; 1 RFC led end-to-end + 4 weeks of status updates; 3 runbooks + 1 structural-fix note; Lab code review guide + 4-week mentorship notes for 1 fictional mentee; Staff-archetype self-mapping; Lab data-engineer onboarding program + cross-team 6-pager memo published.

---

## Coda — IDP-Level Mastery

**The full IDP v2 is mastered at Senior level when all 27 Epic-level 🎯 boxes are ticked**, with the 9 certifications passed (Epics 19–24) and the Principal-target sub-skills in Epics 25–27 completed for those who want to evidence readiness for the Staff+ transition. The pace is set by the engineer: cert-driven (~5 years for all 9 certs), per-Epic focal (~9 years for all 27 Epics at 4 months / Epic), or intensive (~7 years at 3 sub-skills / week).
