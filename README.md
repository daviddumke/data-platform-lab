# data-platform-lab

A portfolio-style lab for designing, building, and operating modern data platforms end-to-end — from ingestion through transformation, orchestration, streaming, and deployment, alongside the documentation and decision artifacts that real platform work produces.

## Layout

```
data-platform-lab/
├── docs/        documentation, decisions, runbooks, lineage, talks, publications
├── lab/         working code: ingestion, transformation, orchestration, streaming, clients, utils
├── deploy/      Helm charts, Kustomize, Terraform, Argo CD manifests
├── tests/       pytest suites
└── tooling      .pre-commit-config.yaml, .github/workflows/, docker-compose.dev.yml, .devcontainer/
```

### `docs/`
- [`architecture/`](docs/architecture/) — C4 diagrams and Well-Architected reviews
- [`adr/`](docs/adr/) — Architecture Decision Records
- [`rfcs/`](docs/rfcs/) — Requests for Comments
- [`runbooks/`](docs/runbooks/) — operational runbooks and incident write-ups
- [`lineage/`](docs/lineage/) — column-level lineage of key KPIs
- [`exec/`](docs/exec/) — one-pagers for non-technical audiences
- [`talks/`](docs/talks/) — slides and recordings
- [`publications.md`](docs/publications.md) — external articles and OSS contributions
- [`onboarding/`](docs/onboarding/) — onboarding program
- [`memos/`](docs/memos/) — cross-team memos
- [`perf/`](docs/perf/) — performance and cost-delta reports
- [`notes/`](docs/notes/) — canonical reference notes per topic
- [`certs/`](docs/certs/) — cert retrospectives
- [`proposals/`](docs/proposals/) — strategy proposals

### `lab/`
- [`ingestion/`](lab/ingestion/) — Singer taps and Kafka Connect configs
- [`transformation/`](lab/transformation/) — dbt project
- [`orchestration/`](lab/orchestration/) — Airflow and Dagster
- [`streaming/`](lab/streaming/) — Flink and Spark jobs
- [`clients/`](lab/clients/) — REST, GraphQL, and gRPC clients
- [`utils/`](lab/utils/) — shared libraries (circuit breaker, retry, etc.)

### `deploy/`
- [`helm/`](deploy/helm/) — Helm charts
- [`k8s/`](deploy/k8s/) — Kustomize `base/` and `overlays/`
- [`terraform/`](deploy/terraform/) — Terraform modules and envs
- [`argocd/`](deploy/argocd/) — GitOps manifests

## Status

Scaffold only — directories and placeholder files are in place; real artifacts will be added incrementally.
