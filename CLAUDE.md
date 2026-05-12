# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository status

`data-platform-lab` is a **scaffold**. The directory tree is in place, but almost everything under it is a `.gitkeep` placeholder. There is no code to build, no tests to run, and no tooling configured yet. The `README.md` reflects this ("Scaffold only — directories and placeholder files are in place; real artifacts will be added incrementally").

Practically, this means:

- There are no build, lint, or test commands. Do not invent them.
- `lab/`, `tests/`, `deploy/`, `.devcontainer/`, and `.github/workflows/` contain only `.gitkeep` files.
- `.pre-commit-config.yaml`, `docker-compose.dev.yml`, and `.devcontainer/devcontainer.json` exist but are **empty (0 bytes)**.
- There is no `pyproject.toml`, `Makefile`, `package.json`, `requirements.txt`, or `dbt_project.yml`.

## Intended layout

`README.md` has the canonical tree. In short:

- `docs/` — documentation, ADRs, RFCs, runbooks, lineage, performance notes, IDP roadmap.
- `lab/` — working code: `ingestion/`, `transformation/` (dbt), `orchestration/` (Airflow/Dagster), `streaming/` (Flink/Spark), `clients/`, `utils/`.
- `deploy/` — `helm/`, `k8s/` (Kustomize), `terraform/`, `argocd/`.
- `tests/` — pytest suites.
- Repo root — tooling: pre-commit, GitHub Actions, docker-compose, devcontainer.

When you add the first real artifacts to one of these areas, update this file with the actual commands and a short note on the architecture being introduced.

## Where real content lives today

The only substantive content is `docs/idp/` — a Senior Data Engineer development roadmap. Start at:

- `docs/idp/idp-v2-full.md` — master index. 27 Epics → ~126 Stories → ~285 Senior-targeted sub-skills, with 9 industry certifications mapped across Epics 19–24.
- `docs/idp/idp-v2-epic-<N>-pilot.md` — per-Epic pilot files (1, 3–27 are present today).

The IDP defines what this repo is meant to produce. When the user asks for "the streaming epic" or "Epic 9," they mean `docs/idp/idp-v2-epic-9-pilot.md`. All other `docs/` subdirectories (`adr/`, `architecture/`, `runbooks/`, `lineage/`, `rfcs/`, etc.) are empty and awaiting their first entries.

## When the scaffold becomes real

As code, tests, or deploy artifacts land:

1. Update this file with the actual commands (build, test, lint, run a single test, run a dbt model, etc.) at the same time.
2. Prefer editing this file over adding sibling onboarding docs.
3. Add a short architecture section only when the system spans enough files that future Claude can't get the picture from one read.
