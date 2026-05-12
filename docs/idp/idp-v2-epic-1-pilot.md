# IDP v2 — Epic 1 Pilot · Fundamentals and Theory

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the *theoretical spine* of the team — the conceptual frameworks that inform every architecture decision downstream. They can derive (not just memorize) the trade-offs in CAP, schema evolution, modeling paradigms, distributed-systems impossibility results, and storage-format choices. They built the operational competence (Linux/Shell/Git, polyglot literacy, DSA fluency) that lets them move across stacks without re-learning fundamentals.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 1.1 — Own the Team's Data-Systems Theory Foundations

> **What "Senior at this Skill" means.** A Senior here doesn't just *know* CAP, idempotency, and schema-on-read — they **use these models as decision tools** for every new system the team builds. When a junior asks "should this be batch or streaming?", the Senior can walk through the framework on a whiteboard. They've published the team's reference notes that mid-level engineers consult before architecture reviews.

### Sub-skill 1.1.1: Define the team's batch-vs-streaming-vs-micro-batch decision framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/batch-vs-streaming.md` with the 3 paradigms' latency/throughput/cost/complexity trade-offs, 1 worked example of each (a batch ELT, a Spark micro-batch, a Flink streaming pipeline) from the Lab, and the team's decision tree: "if the source emits < N events/sec AND latency-tolerance > T minutes → batch; otherwise...". Document the delivery-semantics escalation (at-most → at-least → exactly-once via idempotency) and the 3 canonical dedup patterns (natural-key upsert, hash-based, STATE tokens) that operationalize idempotency.

**Skill progression by level:**
- **Junior** — Recognize the 3 paradigms by name; read a pipeline and identify which one it is.
- **Mid** — Apply each paradigm to a fitting source; know the trade-offs roughly.
- **🎯 Senior (TARGET)** — Define the team's decision framework; ship the reference note; review architecture proposals against it; spot mismatches in PRs ("this should be batch, not streaming, because...").
- **Staff** — Architect cross-paradigm reconciliation (Lambda → Kappa migration patterns) at the platform level.
- **Principal** — Govern the org's batch-vs-streaming policy and cost-attribution model.

---

### Sub-skill 1.1.2: Own consistency & CAP/PACELC discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/consistency-models.md` covering ACID vs BASE (the 4 + 3 properties, and where each fits), the CAP triangle, PACELC (latency-vs-consistency in the absence of partitions), and 5 consistency models (strong, eventual, causal, monotonic-read, read-your-writes) with the systems that exhibit each. Diagram the team's Lab stack against the CAP+PACELC spectrum: where Postgres sits, where BigQuery sits, where Kafka sits, where S3 sits — published as `docs/architecture/cap-pacelc-lab.md`.

**Skill progression by level:**
- **Junior** — Recognize ACID and CAP as concepts.
- **Mid** — Apply ACID guarantees vs BASE eventual consistency to operational vs analytical workloads.
- **🎯 Senior (TARGET)** — Define the team's consistency-model decision framework; produce the CAP+PACELC mapping of the actual stack; use it in architecture reviews to surface invisible assumptions.
- **Staff** — Architect cross-system consistency contracts (e.g., outbox-pattern guarantees between OLTP and event-streaming).
- **Principal** — Govern org-wide consistency-vs-latency trade-off policy.

---

### Sub-skill 1.1.3: Define schema-evolution & event-design contracts

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/schema-evolution.md` covering backward / forward / full / no compatibility for Avro, Protobuf, and JSON Schema — with worked examples of what each allows (add nullable field, rename, type-widen, etc.). Document event sourcing and CQRS patterns and when to use them vs CRUD. Author `docs/notes/time-semantics.md` covering event-time, processing-time, ingestion-time, watermarks, and late-arriving-data strategies. Apply these contracts to 1 Lab pipeline using Schema Registry-enforced Avro.

**Skill progression by level:**
- **Junior** — Recognize that schemas change and producers/consumers may evolve at different rates.
- **Mid** — Apply backward-compatible field additions; read a Protobuf definition.
- **🎯 Senior (TARGET)** — Define the team's compatibility policy per topic; choose event-sourcing vs CRUD per domain; design event payloads with explicit time semantics + late-data handling.
- **Staff** — Architect cross-team contract-evolution coordination (dual-publish, consumer-driven migration).
- **Principal** — Govern org-wide schema-evolution standards + dispute resolution.

---

### Sub-skill 1.1.4: Design the modeling-paradigm decision framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/modeling-paradigms.md` comparing Kimball dimensional, Inmon CIF (3NF + datamarts), Data Vault 2.0 (Hubs + Links + Satellites), and Activity Schema (Narrator-style) — with worked examples of each on the same Lab domain so the trade-offs are visible. Document when to denormalize vs preserve 3NF (for OLTP), when OLAP shapes win, when HTAP makes sense.

**Skill progression by level:**
- **Junior** — Recognize star schema vs 3NF.
- **Mid** — Apply Kimball dimensional modeling for an analytics use case.
- **🎯 Senior (TARGET)** — Define the team's modeling-paradigm decision tree; lead the choice per domain; review modeling PRs against it.
- **Staff** — Architect cross-domain conformed dimensions or Data Vault that holds across teams.
- **Principal** — Govern org-wide modeling standards + retention/governance integration.

---

### Sub-skill 1.1.5: Own architecture-paradigm choice (Lambda vs Kappa vs Lakehouse + back-pressure)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/architecture-paradigms.md` comparing Lambda (dual batch + speed layer), Kappa (single streaming layer), and Lakehouse (unified table format), with their respective consistency, cost, complexity, and operational profiles. Document back-pressure and flow-control mechanisms in Airflow / Kafka / gRPC — the failure modes when back-pressure is absent (buffer overflow, OOM, cascading failure). Apply one architecture paradigm to the Lab end-to-end.

**Skill progression by level:**
- **Junior** — Recognize the 3 architecture paradigms by name.
- **Mid** — Apply Lambda or Lakehouse for a project; understand basic back-pressure.
- **🎯 Senior (TARGET)** — Define when to choose each paradigm; implement back-pressure controls explicitly; review architecture proposals for cost vs operational reality.
- **Staff** — Architect organization-wide migration paths (Lambda → Lakehouse) with phased cutover.
- **Principal** — Govern architecture-paradigm strategy at multi-year horizons.

---

### Sub-skill 1.1.6: Define storage-format & tiering strategy (columnar/row, compression, encoding)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/storage-formats.md` comparing columnar vs row-based (Parquet vs ORC vs Avro), compression codecs (Snappy / gzip / zstd / LZ4) with their compression-ratio + CPU-cost trade-offs, and encoding schemes (dictionary / RLE / delta) with their applicable data shapes. Document the team's hot/warm/cold tiering policy (MinIO lifecycle in Lab → S3 Intelligent-Tiering + Glacier in prod). Apply storage tiering in the Lab and measure cost-delta over 30 days.

**Skill progression by level:**
- **Junior** — Recognize columnar vs row formats and what compression does.
- **Mid** — Apply Parquet + Snappy by default; understand basic tier choice.
- **🎯 Senior (TARGET)** — Define the team's format/compression/encoding policy per data shape; implement tiering with measurable cost-delta; review storage decisions in design.
- **Staff** — Architect format-migration paths (CSV → Parquet → Iceberg) across the platform.
- **Principal** — Govern org-wide storage strategy + capacity planning.

---

## Story 1.2 — Own Linux, Shell & Git Operations

> **What "Senior at this Skill" means.** A Senior here can SSH into any host the team owns, debug a process running at 3am, write a robust shell script that doesn't break under edge cases, and explain Git's internal data model to a Junior. These are the operational fundamentals the rest of the team relies on the Senior to demonstrate — not just talk about.

### Sub-skill 1.2.1: Own Linux process & resource discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/linux-fundamentals.md` covering the process model (fork/exec, signals, exit codes, zombies/orphans, container behavior), file descriptors and I/O (stdin/stdout/stderr, pipes, redirection, `2>&1` vs `&>`, here-docs), permissions/inodes/setuid/umask, networking debugging (ss, lsof, netstat, "connection refused" failure modes), filesystem internals (inodes vs blocks, the "disk full but `df` shows space" trap), virtual memory (RSS vs VSZ, OOM killer signals in K8s), and CPU concepts (cores vs threads, load average, context switches). The note is the team's go-to reference when on-call debugging Linux issues.

**Skill progression by level:**
- **Junior** — Recognize basic Linux commands; navigate a filesystem.
- **Mid** — Apply common Linux tools to debug a service; interpret `top`/`htop`.
- **🎯 Senior (TARGET)** — Own the team's Linux reference; debug pod OOMs and disk-exhausted incidents in production; mentor mid-level engineers through their first incident response.
- **Staff** — Architect platform-wide OS-level standards (kernel-tuning, sysctls, container-runtime conventions).
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.2.2: Engineer robust shell scripting

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author the canonical Lab script template `scripts/template.sh` demonstrating `set -euo pipefail`, IFS hygiene, trap-based cleanup, error reporting, and structured logging. Author `docs/notes/shell-anti-patterns.md` documenting 5 common shell anti-patterns (unquoted vars, parsing `ls`, ignoring exit codes, etc.) with the safe alternative for each. Document the team's shell-vs-Python decision rule: when shell is right, when to escalate to a real language.

**Skill progression by level:**
- **Junior** — Recognize bash syntax; run prepared scripts.
- **Mid** — Apply basic bash for ad-hoc tasks; debug script failures.
- **🎯 Senior (TARGET)** — Engineer the team's script template + anti-patterns reference; review shell PRs for safety; decide when shell is the right tool vs when to graduate to Python.
- **Staff** — Architect a shared scripting library + linting (shellcheck enforcement) across teams.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.2.3: Define text-processing & one-liner conventions

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/text-processing-cookbook.md` documenting 10 canonical one-liners using grep, sed, awk, cut, sort, uniq, jq, and xargs — solving real Lab problems (parsing logs, transforming CSV, filtering JSON streams). Document the team's "when to use grep vs awk vs jq" decision rule.

**Skill progression by level:**
- **Junior** — Recognize the tool names; use basic `grep`.
- **Mid** — Apply 3-4 of the tools for ad-hoc data manipulation.
- **🎯 Senior (TARGET)** — Author the team cookbook; mentor mid-level engineers on one-liner composition; review PRs that have ad-hoc scripts for the more readable alternative.
- **Staff** — *(out of natural progression for this sub-skill)*
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.2.4: Own Python environment & dependency management

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/python-envs.md` comparing venv, poetry, uv, conda, and pyenv/asdf — with the team's choice (likely uv + pyproject.toml) and rationale. Document lock-file discipline (`uv.lock` committed; never `pip install --upgrade` in CI without lock-bump). Apply uv across all Lab Python projects with versioned `pyproject.toml` + `uv.lock`.

**Skill progression by level:**
- **Junior** — Recognize that Python needs virtual environments.
- **Mid** — Apply venv or poetry; install packages from requirements.txt.
- **🎯 Senior (TARGET)** — Define the team's Python env standard (uv + pyproject.toml + lock); migrate existing projects; review PRs for lock-file hygiene.
- **Staff** — Architect monorepo Python tooling (uv workspaces, Pants) across teams.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.2.5: Master Git internals & advanced workflows

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/git-internals.md` covering the object model (blob, tree, commit, tag), refs and packfiles, HEAD and the index — explaining *why* rebase rewrites hashes. Author `docs/runbooks/git-recovery.md` with recipes for common scenarios: interactive rebase to clean history, cherry-pick across branches, bisect to find a regression, reflog to recover dropped commits, worktrees for parallel work. Mentor at least one mid-level engineer through a recovery scenario.

**Skill progression by level:**
- **Junior** — Recognize commit, branch, merge concepts.
- **Mid** — Apply rebase, cherry-pick, basic conflict resolution.
- **🎯 Senior (TARGET)** — Master Git's data model; ship the team's recovery runbook; mentor others through "I lost my commits" scenarios.
- **Staff** — Architect monorepo strategy (submodules vs subtrees vs separate repos) at the platform level.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.2.6: Define branching strategy & Git hooks for the team

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/branching-strategy.md` comparing trunk-based, GitHub-flow, and gitflow — with the team's choice (likely trunk-based for data teams) and rationale. Engineer the team's Git hooks via pre-commit (ruff + mypy + sqlfluff + gitleaks for secret detection) versioned at `.pre-commit-config.yaml`. Engineer a custom `prepare-commit-msg` hook that injects ticket ID from branch name (e.g., `IDP-123-...` → "[IDP-123]"). Document the conventional-commits convention.

**Skill progression by level:**
- **Junior** — Recognize branching strategies by name.
- **Mid** — Apply the team's branching strategy correctly.
- **🎯 Senior (TARGET)** — Define the strategy + ship the hooks + commitlint configuration; review PRs for conventional-commits and hook compliance.
- **Staff** — Architect cross-repo Git automation (semantic-release, changelog generation) at the platform level.
- **Principal** — Govern org-wide source-control policy.

---

## Story 1.3 — Apply Distributed Systems Theory in Practice

> **What "Senior at this Skill" means.** A Senior on this Story can reason about distributed-systems failure modes without needing to consult papers each time. They know that the Two Generals problem means timeouts are inevitable, that exactly-once is an illusion without idempotency, and that consensus has theoretical limits. They've translated this theory into the team's retry, circuit-breaker, idempotency, and sharding practices.

### Sub-skill 1.3.1: Understand distributed-systems impossibility results

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/distributed-systems-impossibility.md` covering the Two Generals problem (consensus over lossy channels), Byzantine Generals (consensus with malicious actors), and FLP (no deterministic consensus under asynchronous failure) — with practical implications: why every retry must have a timeout, why no system can guarantee zero-loss without redundancy, why we tolerate inconsistency in exchange for availability. Cite 3 famous postmortems (S3 us-east 2017, GitHub MySQL 2018, AWS Aurora 2019) showing the theory in action.

**Skill progression by level:**
- **Junior** — Recognize that distributed systems have unique failure modes.
- **Mid** — Apply timeouts and retries as default in any RPC code.
- **🎯 Senior (TARGET)** — Understand the impossibility results well enough to explain them to a mid-level engineer; use them to inform architecture decisions; review designs for naive assumptions ("retry forever", "exactly-once delivery").
- **Staff** — Architect failure-mode taxonomies and cross-team incident-learning loops.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.3.2: Define consensus & replication discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/consensus-replication.md` covering consensus algorithms (Paxos / Raft / ZAB — which systems use which: etcd→Raft, ZooKeeper→ZAB, Kafka KRaft→Raft), replication models (leader-follower sync/async, multi-leader, leaderless Dynamo-style), quorum (R + W > N derivation and Cassandra/DynamoDB tuning), and logical clocks (Lamport, vector clocks, HLC) with the systems exhibiting each. Document when replication choice is load-bearing for the team's stack.

**Skill progression by level:**
- **Junior** — Recognize the names of replication models.
- **Mid** — Apply quorum reasoning to a Cassandra-style system; debug split-brain incidents.
- **🎯 Senior (TARGET)** — Define the team's replication discipline; explain consensus algorithms in mentoring conversations; choose replication strategy per use case.
- **Staff** — Architect cross-region replication topology and disaster-recovery plans.
- **Principal** — Govern org-wide replication and DR policy at multi-region scale.

---

### Sub-skill 1.3.3: Define distributed-transaction & saga patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/distributed-transactions.md` covering 2PC, 3PC, sagas (orchestration vs choreography), outbox pattern, and CRDTs (G-Counter, OR-Set, LWW-Register, with real cases at Figma, Riak). Document why 2PC is rarely used in modern microservices and when sagas + outbox is the right pattern instead. Apply outbox-pattern in 1 Lab pipeline as a reference.

**Skill progression by level:**
- **Junior** — Recognize that distributed transactions are different from local ACID.
- **Mid** — Apply a saga or outbox pattern under guidance.
- **🎯 Senior (TARGET)** — Define the team's distributed-transaction pattern per use case; ship the outbox-pattern reference; review designs for missing transaction boundaries.
- **Staff** — Architect platform-level transactional infrastructure (e.g., Debezium + outbox at scale).
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.3.4: Own retry, circuit-breaker & idempotency discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/retry-circuit-breaker.md` covering retry idioms (linear / exponential backoff with jitter), DLQ patterns, circuit-breaker state machine (Closed → Open → Half-Open), bulkhead isolation, idempotency-key strategies (TTL'd dedup store), and concurrency-vs-parallelism (GIL, Amdahl, optimistic vs pessimistic locking). Engineer reusable `lab/utils/circuit_breaker.py` with tests and use it in 2 Lab pipelines. Engineer idempotency-key handling in one ingestion pipeline.

**Skill progression by level:**
- **Junior** — Recognize retry as a concept; apply a basic library retry decorator.
- **Mid** — Apply exponential backoff + jitter; understand when retries cause storms.
- **🎯 Senior (TARGET)** — Own the team's resilience pattern library; engineer the circuit-breaker module; review designs for missing idempotency keys.
- **Staff** — Architect cross-service resilience patterns (service mesh, platform-wide DLQ).
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.3.5: Define sharding, membership & time discipline

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/sharding-membership.md` covering sharding strategies (range, hash, consistent hashing — when each works), membership protocols (gossip/SWIM in Cassandra/Consul, heartbeat), distributed locks (Redlock, etcd leases — and the Kleppmann × antirez debate), and distributed time (clock skew, NTP, monotonic vs wall clocks, with 3 historical bugs caused by clock skew including CockroachDB anti-affinity). Document when distributed locks are the wrong answer and what to use instead.

**Skill progression by level:**
- **Junior** — Recognize sharding as a scaling tool.
- **Mid** — Apply consistent hashing or range partitioning under guidance.
- **🎯 Senior (TARGET)** — Define the team's sharding + locking discipline; spot misuse of distributed locks in design; mentor mid-level engineers through clock-skew bugs.
- **Staff** — Architect cross-region sharding topology + consistency contracts.
- **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 1.4 — Adopt Polyglot Programming Literacy

> **What "Senior at this Skill" means.** A Senior here isn't fluent in 5 languages — they're *literate* enough in Scala/Java/Go/Rust to read code, understand idioms, contribute small changes, and choose the right language for a new project. The senior knows when PySpark stops scaling and Scala Spark is required, when a Go-based K8s operator is faster to ship than a Python equivalent, when Rust extensions via PyO3 unlock 10× speedups.

### Sub-skill 1.4.1: Acquire Scala & Java literacy for Spark/Flink stacks

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/scala-java-for-de.md` covering 10 Scala idioms relevant to Spark (case classes, traits, implicits, the Spark Scala API patterns) and Java essentials (collections, streams, JVM GC tuning + heap sizing for Spark/Flink workloads). Engineer 1 Lab Spark job in Scala alongside its PySpark equivalent — benchmark and document where Scala wins (cold start, type safety, performance on tight loops).

**Skill progression by level:**
- **Junior** — Recognize Scala/Java exist as JVM languages.
- **Mid** — Apply PySpark; read JVM stack traces.
- **🎯 Senior (TARGET)** — Read Scala/Java code fluently; ship 1 Scala Spark job + benchmark; tune JVM heap for Spark; review JVM-stack designs.
- **Staff** — Architect Scala-vs-PySpark conventions across the team.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.4.2: Acquire Go literacy for K8s tooling & observability

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/go-for-de.md` covering 5 Go idioms relevant to DE tooling (goroutines + channels, error handling, building K8s operators, OpenTelemetry collector extensions). Engineer 1 Go-based K8s sidecar in the Lab (e.g., log shipper or custom metrics exporter) with Dockerfile and manifest.

**Skill progression by level:**
- **Junior** — Recognize Go as the language of K8s tooling.
- **Mid** — Apply a Go CLI or tool; modify a small Go program.
- **🎯 Senior (TARGET)** — Read Go code fluently; ship 1 Go-based K8s sidecar; choose Go vs Python for small tools.
- **Staff** — Architect Go-based platform tooling (operators, controllers) used across teams.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.4.3: Acquire Rust literacy for high-performance extensions

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/rust-for-de.md` covering Rust fundamentals (ownership, borrowing, lifetimes, traits, async/await with tokio), and the case for Rust extensions in data engineering — when Python performance is a bottleneck and PyO3 + maturin unlocks 10×+ speedups. Engineer 1 Rust extension via PyO3 in the Lab (e.g., JSON-lines parser) with benchmark vs pure Python.

**Skill progression by level:**
- **Junior** — Recognize Rust as a systems language.
- **Mid** — Read Rust code at a basic level; recognize ownership semantics.
- **🎯 Senior (TARGET)** — Read and write small Rust; ship 1 PyO3 extension; choose Rust vs Cython vs Numba.
- **Staff** — Architect Rust-based platform components (high-throughput proxies, parsers).
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.4.4: Define the team's polyglot trade-off decision matrix

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/polyglot-decisions.md` documenting the team's decision matrix — when each language wins (Scala for Spark > N TB/day, Go for K8s tooling and sidecars, Rust for hot-path performance, Python for everything else). Include 5 real scenarios with the language chosen and why. Document the FFI and interop patterns (JNI for JVM ↔ Python, PyO3 for Rust ↔ Python).

**Skill progression by level:**
- **Junior** — Recognize that different languages have different strengths.
- **Mid** — Apply the existing team conventions.
- **🎯 Senior (TARGET)** — Define the team's decision matrix + interop patterns; lead language-choice discussions in design reviews.
- **Staff** — Architect cross-language conventions and shared CI tooling.
- **Principal** — Govern org-wide language-strategy policy.

---

## Story 1.5 — Apply Data Structures & Algorithms in Production

> **What "Senior at this Skill" means.** A Senior on this Story doesn't grind LeetCode — they recognize the DSA *inside the systems they use every day*. They know B-trees power Postgres indexes; LSM trees power Cassandra and RocksDB; hash tables power joins; Bloom filters power dedup pruning; HyperLogLog powers approximate distinct counts; consistent hashing powers sharding. They've measured these abstractions delivering real cost-deltas in the Lab.

### Sub-skill 1.5.1: Understand storage-engine data structures (B-trees & LSM trees)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/storage-engines.md` covering the two dominant storage-engine families: B-trees (read-optimized, update-in-place — used by Postgres, MySQL InnoDB) and LSM trees (write-optimized, append + compact — used by RocksDB, Cassandra, ClickHouse). Document the trade-offs (write amplification vs read amplification, compaction cost, lookup latency) and which workloads each fits. Reference 1 specific Lab use case where the choice matters.

**Skill progression by level:**
- **Junior** — Recognize that databases have storage engines.
- **Mid** — Apply Postgres index choice (B-tree vs hash vs GIN) appropriately.
- **🎯 Senior (TARGET)** — Explain the two engine families; recognize which engine powers each system in the stack; choose database systems informed by storage-engine fit.
- **Staff** — Architect storage-engine choice at platform level (when to introduce a new engine).
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.5.2: Understand join, dedup & probabilistic structures

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/join-dedup-data-structures.md` covering hash tables in joins (hash join, hash aggregation, spill-to-disk), Bloom filters and Cuckoo filters (probabilistic membership for dedup and join pruning), and skip lists (the data structure behind Redis sorted sets). Apply a Bloom filter in the Lab dedup logic and benchmark vs exact dedup with a relative-cost report.

**Skill progression by level:**
- **Junior** — Recognize hash tables and Bloom filters by name.
- **Mid** — Apply a Bloom filter library; understand the false-positive trade-off.
- **🎯 Senior (TARGET)** — Engineer a Bloom-filter-backed dedup in the Lab; choose between exact dedup and probabilistic by cost-delta; explain probabilistic-membership trade-offs.
- **Staff** — Architect dedup infrastructure across pipelines using shared filter state.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.5.3: Understand approximation algorithms (HyperLogLog, t-digest, MinHash + LSH)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/approximation-algorithms.md` covering HyperLogLog (approximate distinct count — BigQuery `APPROX_COUNT_DISTINCT`, Snowflake `APPROX_COUNT_DISTINCT`), t-digest (quantiles), MinHash + LSH for similarity search at scale. Apply HyperLogLog in the Lab analytics layer with accuracy comparison vs `COUNT(DISTINCT)` — quantify the accuracy/cost trade-off.

**Skill progression by level:**
- **Junior** — Recognize that approximate algorithms exist.
- **Mid** — Apply `APPROX_COUNT_DISTINCT` in a query.
- **🎯 Senior (TARGET)** — Engineer HLL/t-digest/MinHash in production-grade analytics; quantify accuracy-vs-cost trade-offs; choose approximation vs exact per use case.
- **Staff** — Architect cross-pipeline use of approximate-aggregation libraries.
- **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 1.5.4: Understand distributed-systems data structures (consistent hashing, tries, heaps)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/distributed-data-structures.md` covering consistent hashing for sharding and load balancing (vs naive modulo hashing), priority queues / heaps for back-pressure and scheduling, tries for autocomplete and IP routing, and DAG traversal + topological sort (the algorithms inside dbt/Airflow lineage). Reference how each structure shows up in systems the team uses.

**Skill progression by level:**
- **Junior** — Recognize the data structures by name.
- **Mid** — Apply a priority queue under guidance.
- **🎯 Senior (TARGET)** — Recognize consistent hashing, topological-sort, and tries inside the systems the team uses; reference them in architecture discussions.
- **Staff** — Architect data-structure-aware infrastructure choices (e.g., when to introduce a Trie-backed lookup service).
- **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 5 Story-level 🎯 milestones have been reached** — which requires all ~25 sub-skill 🎯 Senior levels to be reached. The mastery evidence is the body of canonical notes (`docs/notes/*.md`), runbooks (`docs/runbooks/*.md`), and Lab artifacts (Bloom filter dedup, HLL analytics, Scala Spark job, Go sidecar, Rust extension) that the team consults and forks.

## How to Use This File

1. **For Jira import**: same convention as Story 4.1 pilot and Epic 2 pilot — each `### Sub-skill N.M.K:` section is one Jira issue. Group issues under Story-level Jira epics; group Stories under the Epic-1 Jira epic.
   - **Issue summary naming**: do *not* prefix Jira summaries with `Epic <N>`, `Story <N.M>`, or `Sub-skill <N.M.K>` / `Sub-task <N.M.K>` — that hierarchy is already conveyed by the Jira issue type and parent link, so the numeric prefix is redundant and clutters board views. Use only the descriptive title from the section heading (e.g., `Fundamentals and Theory`, `Owning the Team's Data-Systems Theory Foundations`, `Defining the team's batch-vs-streaming-vs-micro-batch decision framework`).
   - **Label convention** (applied at creation time, used for JQL filtering and reporting):
     - **Issue-type role labels**:
       - Epics → `skills-set`
       - Stories → `skill`
       - Sub-skills → `sub-skill`
     - **Skill-class label** (applied to Epics — picks the broad category the skills-set belongs to):
       - `hard-skill` — technical / theoretical skills measurable by an artifact (e.g., Epic 1 "Fundamentals and Theory", Epic 9 "Streaming").
       - `soft-skill` — communication, mentoring, leadership, stakeholder management.

       Exactly one of these is required on every Epic.
     - **Target-level label** (applied to every Epic, Story, and Sub-task — reflects the `**Target:**` field from this document):
       - One of `target-junior`, `target-mid`, `target-senior`, `target-staff`, `target-principal`.
       - For Epic 1, all issues are `target-senior`.

     Do *not* add per-Epic, per-Story, or per-Sub-skill numeric scoping labels (`epic-1`, `story-1.1`, `sub-skill-1.1.1`, `sub-task-1.1.1`, etc.). The hierarchy is already conveyed by the Jira issue type and parent link — those scopes are recoverable with `parent = IDP-X` in JQL, so the numeric labels are redundant and pollute the project's label index.
2. **For self-assessment**: track progress against each level in Jira (mark the corresponding sub-task Done when the level is reached). The 🎯 Senior level is the calibration target.
3. **For mentoring**: theoretical sub-skills (most of Epic 1) translate to whiteboard conversations rather than PRs — the mentor checks "can the mid-level engineer explain this concept clearly?", not just "did they ship the artifact?".
