# IDP v2 — Epic 18 Pilot · Python for Data Engineering

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills writes Python the way it should be written *for engineering* — typed, packaged, tested, profiled, async-aware — not the way it's written for analysis. They've shipped the team's `lab/utils/` library with mypy-strict + ≥80% coverage + semantic-release, at least one Numba/Cython/Rust optimization with measured delta, an async pipeline with back-pressure, and a plugin system.
>
> **Bibliography.** *Fluent Python* (2nd ed., Ramalho) · *Architecture Patterns with Python* (Percival & Gregory) · *Robust Python* (Viafore) · *Effective Python* (3rd ed., Slatkin) · *High Performance Python* (2nd ed., Gorelick & Ozsvald) · *Python Concurrency with asyncio* (Fowler) · *Serious Python* (Danjou).
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 18.1 — Write Idiomatic Python for Engineering

> **What "Senior at this Skill" means.** A Senior here writes the idiomatic Python the team adopts — types, generators, decorators, context managers — and the team's reusable building blocks come from their library.

### Sub-skill 18.1.1: Define the typing strategy (mypy strict, Protocol, TypeGuard, ParamSpec) and the dataclass/attrs/pydantic choice

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-typing.md` covering PEP 484/612/647, mypy strict mode, gradual typing migration, generics, `Protocol`, `TypeGuard`, `ParamSpec`, and the dataclasses vs attrs vs pydantic v2 decision (with a validation benchmark). Engineer the Lab `lab/utils/` library with mypy strict + `py.typed` marker + mypy-strict CI gate.

**Skill progression by level:**
- [ ] **Junior** — Recognize type hints exist.
- [ ] **Mid** — Apply basic type hints; understand `Optional` / `List` / `Dict`.
- [ ] **🎯 Senior (TARGET)** — Define the team's typing strategy (mypy strict, Protocol-based design); ship `lab/utils/` with `py.typed` + CI gate; mentor mid-level engineers on `TypeGuard` and `ParamSpec`.
- [ ] **Staff** — Architect cross-team typing standards + library distribution.
- [ ] **Principal** — Govern org-wide typing policy.

---

### Sub-skill 18.1.2: Define generator + itertools + context manager idioms for memory-efficient pipelines

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-generators-contexts.md` covering 5 generator patterns (chunking, sliding window, streaming dedup, pipeline composition, back-pressure) plus context managers (`with`, `contextlib`, `__enter__`/`__exit__`, async variants for resource management). Apply the patterns in the Lab `lab/utils/streams.py` module.

**Skill progression by level:**
- [ ] **Junior** — Recognize generators and `with` statements.
- [ ] **Mid** — Apply generators for memory efficiency; write simple context managers.
- [ ] **🎯 Senior (TARGET)** — Define the team's streaming idioms; ship `lab/utils/streams.py`; mentor mid-level engineers on memory-efficient pipeline composition.
- [ ] **Staff** — Architect cross-team streaming-pipeline libraries.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.1.3: Engineer the canonical decorator library (retry, timed, traced, cached, idempotent)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-decorators.md` covering parameterized decorators, `functools.wraps`, class decorators, stacking, and descriptors + metaclasses (with anti-patterns: when NOT to use them). Engineer `lab/utils/decorators.py` with 5 canonical DE decorators (retry, timed, traced, cached, idempotent) + unit tests + docs.

**Skill progression by level:**
- [ ] **Junior** — Recognize `@decorator` syntax.
- [ ] **Mid** — Apply decorators; write simple unparameterized ones.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's decorator library; review PRs for `functools.wraps` hygiene; mentor mid-level engineers on parameterized decorators.
- [ ] **Staff** — Architect cross-team decorator standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.1.4: Define the GIL and the free-threaded Python 3.13+ implications for DE

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-gil.md` covering CPython internals, the GIL's release during I/O, the implications for threading vs multiprocessing vs asyncio, and the PEP 703 free-threaded Python 3.13+ roadmap with DE impact. Include the team's stance on adopting free-threaded builds.

**Skill progression by level:**
- [ ] **Junior** — Recognize "the GIL" as a Python limitation.
- [ ] **Mid** — Apply multiprocessing for CPU-bound work.
- [ ] **🎯 Senior (TARGET)** — Define the GIL deeply; explain the I/O release path; mentor mid-level engineers on threading-vs-multiprocessing-vs-asyncio choice.
- [ ] **Staff** — Architect cross-team Python concurrency standards including free-threaded migration.
- [ ] **Principal** — Govern org-wide Python runtime adoption policy.

---

## Story 18.2 — Engineer Python Packaging & Dependencies

> **What "Senior at this Skill" means.** A Senior here owns the team's packaging discipline — `pyproject.toml`, uv/Poetry, dependency resolution, automated publishing — and has shipped at least one internal library with semantic-release.

### Sub-skill 18.2.1: Define the packaging toolchain (pyproject.toml, uv vs Poetry vs Hatch, Python version management)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-packaging.md` covering `pyproject.toml` (PEP 517/518/621/660), Poetry vs uv vs Hatch vs pip-tools (real trade-offs + install-time benchmarks), and Python version management (pyenv, asdf, mise, uv python). Engineer the Lab with `uv + pyproject.toml + uv.lock` committed and the team's `.python-version` strategy documented.

**Skill progression by level:**
- [ ] **Junior** — Recognize `pyproject.toml` and `pip install`.
- [ ] **Mid** — Apply existing pyproject + lock files.
- [ ] **🎯 Senior (TARGET)** — Define the team's packaging toolchain; ship the Lab uv setup; mentor mid-level engineers on lock-file discipline.
- [ ] **Staff** — Architect cross-team packaging standards + private registries.
- [ ] **Principal** — Govern org-wide packaging policy.

---

### Sub-skill 18.2.2: Define dependency resolution + semantic versioning + automated publishing

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-publishing.md` covering dependency resolution (SAT solver, version solver, conflict diagnosis — why resolvers hang), semantic versioning + `semantic-release` for internal libraries, and publishing to PyPI / Test PyPI / private registries (Artifactory, AWS CodeArtifact, GCS) with `twine` + token rotation. Engineer automated publishing for 1 Lab internal library (GitHub Actions workflow + tag-based release).

**Skill progression by level:**
- [ ] **Junior** — Recognize PyPI as a registry.
- [ ] **Mid** — Apply existing publish workflows.
- [ ] **🎯 Senior (TARGET)** — Engineer semantic-release + PyPI publishing for a Lab library; document the resolver conflict diagnosis playbook; mentor mid-level engineers on SemVer discipline.
- [ ] **Staff** — Architect cross-team release infrastructure + private registry strategy.
- [ ] **Principal** — Govern org-wide library distribution + versioning policy.

---

### Sub-skill 18.2.3: Design Python monorepo (uv workspaces, Pants, Bazel)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-monorepo.md` comparing uv workspaces, Pants, Bazel with adoption criteria. Engineer a Python monorepo in the Lab (taps + utils + shared tests) using uv workspaces or Pants.

**Skill progression by level:**
- [ ] **Junior** — Recognize monorepo vs polyrepo as a debate.
- [ ] **Mid** — Apply existing monorepo conventions.
- [ ] **🎯 Senior (TARGET)** — Design the Lab Python monorepo; document the trade-offs; mentor mid-level engineers on workspace tooling.
- [ ] **Staff** — Architect cross-team monorepo strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 18.3 — Engineer Testing for Data Code

> **What "Senior at this Skill" means.** A Senior here ships the team's testing baseline — pytest + testcontainers + Hypothesis + coverage gate + load testing — and the test suite catches real bugs before prod.

### Sub-skill 18.3.1: Define the pytest + mocking baseline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/pytest-canon.md` covering pytest (fixtures, parametrize, conftest hierarchy, useful plugins) and mocking patterns (`unittest.mock`, `pytest-mock`, `responses`, `freezegun`, `pytest-httpx`) with 5 anti-patterns to avoid. Apply in the Lab as the baseline test framework.

**Skill progression by level:**
- [ ] **Junior** — Recognize pytest.
- [ ] **Mid** — Apply fixtures + parametrize; write basic mocks.
- [ ] **🎯 Senior (TARGET)** — Define the team's pytest baseline; review PRs for mock anti-patterns; mentor mid-level engineers on conftest hierarchy.
- [ ] **Staff** — Architect cross-team test framework standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.3.2: Engineer integration testing with testcontainers + Hypothesis property-based tests

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/testcontainers-hypothesis.md` covering `testcontainers-python` (Postgres, Kafka, MinIO ephemeral environments), Hypothesis (strategies, shrinking, stateful testing) with 3 worked examples where property tests catch bugs unit tests miss, and snapshot testing with `syrupy`. Engineer testcontainers in the Lab to test a real tap against ephemeral Postgres + apply Hypothesis to 1 critical Lab transformation.

**Skill progression by level:**
- [ ] **Junior** — Recognize integration tests.
- [ ] **Mid** — Apply existing integration test setups.
- [ ] **🎯 Senior (TARGET)** — Engineer testcontainers + Hypothesis in the Lab; document the property-test wins; mentor mid-level engineers on property-based thinking.
- [ ] **Staff** — Architect cross-team integration test infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.3.3: Define coverage strategy + async testing + mutation testing

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/coverage-async-mutation.md` covering coverage (line vs branch vs path, when 100% is a trap), async testing (`pytest-asyncio`, `anyio.pytest`), and mutation testing (`mutmut`, `cosmic-ray`) with adoption criteria. Build a coverage gate of 80% line + 70% branch on Lab CI (GitHub Actions with threshold).

**Skill progression by level:**
- [ ] **Junior** — Recognize coverage as a metric.
- [ ] **Mid** — Apply existing coverage tools.
- [ ] **🎯 Senior (TARGET)** — Define the team's coverage strategy + async test patterns; build the Lab CI gate; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team coverage + mutation testing standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.3.4: Engineer load testing + smoke testing for data services

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/load-smoke-tests.md` covering load testing for data services (k6, Locust, JMeter — for data APIs, feature stores, query gateways) with scenario scripts canon, and post-deploy smoke testing patterns. Engineer a Locust load test against 1 Lab data API + record p99 / failure rate.

**Skill progression by level:**
- [ ] **Junior** — Recognize load testing exists.
- [ ] **Mid** — Apply existing load test scripts.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Locust test + smoke probes; document the p99/failure-rate baseline; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team load + smoke test infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 18.4 — Optimize Python Performance & Profiling

> **What "Senior at this Skill" means.** A Senior here can profile Python code, identify the bottleneck, pick the right optimization (vectorization, JIT, Rust), and measure the delta. They've shipped at least one Numba/Cython/Rust optimization with documented benchmark.

### Sub-skill 18.4.1: Define profiling methodology (cProfile, py-spy, scalene, memory profilers)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/runbooks/python-profiling.md` defining when to use which profiler (cProfile for call counts, py-spy for sampling without instrumenting, scalene for memory+CPU, austin for low-overhead) plus memory profiling (`memory_profiler`, `tracemalloc`, `objgraph`, `pympler`) for leak detection. Demonstrate on 1 slow Lab transformation with a `docs/perf/lab-001-py-profiling.md` report.

**Skill progression by level:**
- [ ] **Junior** — Recognize profiling exists.
- [ ] **Mid** — Apply cProfile to identify hot functions.
- [ ] **🎯 Senior (TARGET)** — Define the profiler choice methodology; demonstrate on Lab code; mentor mid-level engineers through their first py-spy session.
- [ ] **Staff** — Architect cross-team continuous-profiling infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.4.2: Define vectorization (numpy, pandas, polars, pyarrow) for hot paths

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-vectorization.md` covering numpy/pandas/polars/pyarrow vectorization patterns with 3 transformations rewritten before/after (loop → vectorized) and measured speedup. Apply in the Lab on at least 1 hot path.

**Skill progression by level:**
- [ ] **Junior** — Recognize vectorization as a concept.
- [ ] **Mid** — Apply pandas/numpy vectorized operations.
- [ ] **🎯 Senior (TARGET)** — Define the team's vectorization patterns; apply in the Lab with measured speedup; mentor mid-level engineers on avoiding `apply()`.
- [ ] **Staff** — Architect cross-team vectorization standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.4.3: Engineer JIT compilation (Numba, Cython, mypyc) for hot paths

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-jit.md` covering Numba JIT (when it works, when it doesn't — numpy-only types), Cython for type-annotated Python → C, and `mypyc` for ahead-of-time compilation. Engineer Numba or Cython on a Lab hot path with a documented benchmark in `docs/perf/lab-002-py-jit.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize JIT as a concept.
- [ ] **Mid** — Apply Numba on simple loops.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab JIT optimization; document the benchmark; mentor mid-level engineers on JIT type restrictions.
- [ ] **Staff** — Architect cross-team JIT standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.4.4: Architect Rust extensions via PyO3 + maturin

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-rust-extensions.md` covering PyO3 + maturin for Rust extensions, the "when-to-rust" decision criteria (Python ergonomics break down vs. native-extension overhead), and the FFI boundary cost. Architect a Rust extension via PyO3 in the Lab (e.g., JSON-lines parsing) with a benchmark vs pure Python in `docs/perf/lab-003-rust-extension.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize Rust as a Python-extension option.
- [ ] **Mid** — Apply existing Rust extensions (pyarrow, polars, ruff).
- [ ] **Senior** — Read PyO3 Rust code; debug extension issues.
- [ ] **🎯 Staff (TARGET)** — Architect a Rust extension in the Lab with measured benchmark; mentor Senior engineers on the FFI cost.
- [ ] **Principal** — Govern org-wide native-extension policy.

---

## Story 18.5 — Select Canonical Python Libraries for Data Engineering

> **What "Senior at this Skill" means.** A Senior here picks the right Python library per workload (pandas vs Polars vs DuckDB vs PyArrow; psycopg vs asyncpg; httpx vs requests; pydantic vs dataclasses) and has shipped at least one migration with measured wins.

### Sub-skill 18.5.1: Select between pandas, Polars, PyArrow, DuckDB for data processing

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dataframe-libraries.md` covering pandas for *engineering* (chunked reads, `category` dtypes, `pd.eval`, avoiding `apply`), Polars (lazy frames, expression API, streaming engine), PyArrow (Tables, IPC, Parquet/Feather, compute kernels, Dataset API), and DuckDB (in-process OLAP, SQL on Parquet/CSV) with "when each wins" criteria. Build Polars as a pandas alternative in the Lab on 1 transformation + benchmark, and engineer DuckDB as the testing engine for dbt unit tests on the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize pandas as the default; Polars and DuckDB as alternatives.
- [ ] **Mid** — Apply pandas fluently; recognize PyArrow as a Parquet layer.
- [ ] **🎯 Senior (TARGET)** — Select the right library per workload; ship the Lab Polars migration + DuckDB test engine; mentor mid-level engineers on the "when each wins" criteria.
- [ ] **Staff** — Architect cross-team dataframe-library standards.
- [ ] **Principal** — Govern org-wide library-adoption policy.

---

### Sub-skill 18.5.2: Select between SQLAlchemy 2.0, psycopg v3, asyncpg for DB access

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-db-libraries.md` covering SQLAlchemy 2.0 (Core vs ORM, async engine, connection pooling, dialect quirks), `psycopg` v3 + `asyncpg` for Postgres (COPY, server-side cursors, prepared statements), and ingestion-pattern recipes. Apply in the Lab on at least 1 ingestion path.

**Skill progression by level:**
- [ ] **Junior** — Recognize SQLAlchemy and psycopg as Python DB libraries.
- [ ] **Mid** — Apply SQLAlchemy Core or psycopg for basic queries.
- [ ] **🎯 Senior (TARGET)** — Select the right DB library per workload; engineer the Lab ingestion patterns; mentor mid-level engineers on COPY and server-side cursors.
- [ ] **Staff** — Architect cross-team DB-access library standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.5.3: Select between httpx, tenacity, pydantic v2, structlog/loguru, click/typer

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-de-stack.md` covering `httpx` (sync + async, retries, transport customization, mock client for tests, migration from requests), `tenacity` for idiomatic retry, Pydantic v2 (validators, computed fields, serialization, performance vs v1), `structlog` or `loguru` for structured logging, and `click` or `typer` for professional CLIs. Engineer Pydantic v2 models as the schema validation layer in all Lab ingestions.

**Skill progression by level:**
- [ ] **Junior** — Recognize httpx and pydantic by name.
- [ ] **Mid** — Apply existing httpx + pydantic patterns.
- [ ] **🎯 Senior (TARGET)** — Select the team's canonical DE stack; engineer Pydantic v2 validation across Lab ingestions; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team stack standards.
- [ ] **Principal** — Govern org-wide library standards.

---

## Story 18.6 — Engineer Async, Concurrency & Queues

> **What "Senior at this Skill" means.** A Senior here writes async pipelines that don't deadlock and uses concurrency primitives deliberately. They've shipped at least one async tap with back-pressure + bounded queues.

### Sub-skill 18.6.1: Define asyncio + anyio fundamentals (event loop, tasks, gather, semaphores, portability)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/asyncio-fundamentals.md` covering the event loop, tasks, `gather`, `as_completed`, semaphores, the asyncio mental model, and `anyio` for asyncio/trio portability. Document the canonical pitfalls (blocking calls in async code, forgotten `await`, task cancellation).

**Skill progression by level:**
- [ ] **Junior** — Recognize `async`/`await` syntax.
- [ ] **Mid** — Apply asyncio for basic concurrent I/O.
- [ ] **🎯 Senior (TARGET)** — Define the team's asyncio model + anyio portability; mentor mid-level engineers on canonical pitfalls.
- [ ] **Staff** — Architect cross-team asyncio standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.6.2: Engineer async I/O-bound ingestion with bounded queues + back-pressure

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/async-ingestion.md` covering `aiohttp` + `asyncpg` for I/O-bound ingestion, bounded queues + back-pressure in async pipelines, and the producer/consumer recipe. Engineer an async tap (httpx + asyncpg) in the Lab with bounded queue + back-pressure + benchmark vs sync version.

**Skill progression by level:**
- [ ] **Junior** — Recognize async ingestion as a pattern.
- [ ] **Mid** — Apply async HTTP for parallel fetches.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab async tap with back-pressure; document the benchmark; mentor mid-level engineers on bounded-queue discipline.
- [ ] **Staff** — Architect cross-team async ingestion frameworks.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 18.6.3: Select between Celery, RQ, Dramatiq, arq + CPU-bound parallelism strategy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-task-queues.md` comparing Celery vs RQ vs Dramatiq vs arq (sync vs async, broker requirements, observability), `concurrent.futures` (ThreadPool / ProcessPool) and their limits, and `multiprocessing` + shared memory + Manager objects for CPU-bound parallelization. Engineer arq as an async background-task queue in the Lab with a worker + DAG enqueuing jobs.

**Skill progression by level:**
- [ ] **Junior** — Recognize Celery / task queues as a pattern.
- [ ] **Mid** — Apply existing Celery setup.
- [ ] **🎯 Senior (TARGET)** — Select the right task-queue per workload; engineer Lab arq setup; mentor mid-level engineers on CPU-bound vs I/O-bound choices.
- [ ] **Staff** — Architect cross-team task-queue infrastructure.
- [ ] **Principal** — Govern org-wide task-queue strategy.

---

## Story 18.7 — Architect Python Patterns for Data Engineering

> **What "Senior at this Skill" means.** A Senior here architects Python pipelines that are testable, swappable, and extensible — Repository, Unit of Work, Service Layer, plugin systems. They've shipped at least one plugin-based system in the Lab.

### Sub-skill 18.7.1: Architect Cosmic Python patterns (Repository, UoW, Service Layer, hexagonal architecture)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/cosmic-python-de.md` applying Cosmic Python patterns (Repository, Unit of Work, Service Layer) to ingestion pipelines, plus hexagonal architecture (ports/adapters in DE), plus dependency injection (manual, `injector`, `dishka`). Engineer hexagonal architecture in 1 Lab microservice with a documented decision log.

**Skill progression by level:**
- [ ] **Junior** — Recognize the pattern names.
- [ ] **Mid** — Apply Repository / Service Layer in simple cases.
- [ ] **🎯 Senior (TARGET)** — Architect Cosmic Python patterns in 1 Lab microservice; document the decision log; mentor mid-level engineers on ports/adapters.
- [ ] **Staff** — Architect cross-team Python pattern adoption.
- [ ] **Principal** — Govern org-wide Python architecture standards.

---

### Sub-skill 18.7.2: Engineer a plugin system (entry points, importlib.metadata) for taps/connectors

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-plugin-systems.md` covering entry points, `importlib.metadata`, and the Strategy/Factory patterns for pluggable extractors — the pattern Singer/Meltano use under the hood. Engineer a plugin system for taps in the Lab with entry points + 2 demonstrating plugins.

**Skill progression by level:**
- [ ] **Junior** — Recognize plugins as a concept.
- [ ] **Mid** — Apply existing plugin systems (Singer, dbt adapters).
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab plugin system; document the entry-point pattern; mentor mid-level engineers on Strategy/Factory.
- [ ] **Staff** — Architect cross-team plugin standards.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 7 Story-level 🎯 boxes are ticked** — which requires the 20 sub-skill 🎯 boxes (one at Staff). Mastery evidence: `lab/utils/` library with mypy strict + ≥80% coverage + semantic-release published, decorator + generator + context-manager idioms shipped, uv monorepo + automated publishing, testcontainers + Hypothesis + 80% coverage gate + Locust load test, Numba/Cython + Rust-via-PyO3 optimization with measured benchmark, Polars migration + DuckDB test engine + Pydantic v2 validation layer, async tap with bounded queue + back-pressure, arq queue + plugin system + hexagonal microservice.
