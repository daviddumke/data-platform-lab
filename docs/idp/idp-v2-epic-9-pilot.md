# IDP v2 — Epic 9 Pilot · Streaming and Event-Driven Architectures

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's streaming-vs-batch decisions — the streaming fundamentals (Kafka, watermarks, stateful processing), the engine choice (Flink vs Spark Streaming vs Beam), streaming-SQL adoption (Materialize, ksqlDB), stateful-workflow patterns (Temporal), and broker selection (Kafka vs Pulsar vs NATS vs RabbitMQ). They've shipped at least one streaming POC end-to-end and the published ADR explaining the team's choice.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 9.1 — Understand Streaming Fundamentals

> **What "Senior at this Skill" means.** A Senior here can derive (not just recite) Akidau's Dataflow model — event time vs processing time, watermarks, windowing, late data — and know which delivery semantics (at-most, at-least, exactly-once) the team's stack actually delivers.

### Sub-skill 9.1.1: Understand Kafka fundamentals (topics, partitions, consumer groups, offsets)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/kafka-fundamentals.md` covering topics, partitions, consumer groups, offsets, ISR (in-sync replicas), retention policies, and Kafka's delivery semantics (the at-least-once default + exactly-once via transactions). Document Pub/Sub vs Kinesis vs Kafka comparison.

**Skill progression by level:**
- [ ] **Junior → Mid** — Recognize topic/partition/offset model; produce + consume a basic Kafka stream.
- [ ] **Mid** — Apply consumer groups + offset commits correctly.
- [ ] **🎯 Senior (TARGET)** — Mentor mid-level engineers on the model; explain consumer-group rebalancing failure modes; review Kafka-related PRs for correctness.
- [ ] **Staff** — Architect Kafka cluster topology + multi-cluster patterns.
- [ ] **Principal** — Govern org-wide event-streaming infrastructure strategy.

---

### Sub-skill 9.1.2: Understand event time, processing time & watermarks (Dataflow model)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/dataflow-model.md` summarizing Akidau's "Streaming 101/102" — event time vs processing time vs ingestion time, watermarks (heuristic + perfect), late data handling, and the per-key state model. Provide 1 worked example: a Lab Flink/ksqlDB pipeline with explicit watermark + late-data policy.

**Skill progression by level:**
- [ ] **Junior** — Recognize event time vs processing time as concepts.
- [ ] **Mid** — Apply windowing with a default watermark.
- [ ] **🎯 Senior (TARGET)** — Define the team's watermark + late-data policy per pipeline; review streaming PRs for time-semantics correctness.
- [ ] **Staff** — Architect cross-pipeline time-semantics conventions.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.1.3: Understand stateful processing + windowing patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/stateful-streaming.md` covering Flink state backends (RocksDB, heap), Spark Structured Streaming state stores, window types (tumbling, hopping, sliding, session), and the per-key state model. Provide 1 worked example of each window type in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize windowing as a concept.
- [ ] **Mid** — Apply tumbling or hopping windows.
- [ ] **🎯 Senior (TARGET)** — Engineer all 4 window types in the Lab; document state-backend trade-offs; review streaming PRs for state-management correctness.
- [ ] **Staff** — Architect state-backend choice + tuning at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 9.2 — Build an End-to-End Streaming POC

> **What "Senior at this Skill" means.** A Senior here has shipped a complete streaming pipeline end-to-end in the Lab — producer → broker → processor → sink — proving the team's streaming stack works at production grade.

### Sub-skill 9.2.1: Engineer a producer → Kafka → consumer POC

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer in the Lab a complete producer (Python service) → Kafka topic → consumer (Python service) flow via Docker Compose. Demonstrate consumer-group rebalancing, offset management, and graceful shutdown. Document in `docs/notes/kafka-poc.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize the producer/consumer model.
- [ ] **Mid** — Apply a basic producer/consumer with a library.
- [ ] **🎯 Senior (TARGET)** — Engineer the canonical POC with rebalancing + graceful shutdown; mentor mid-level engineers; review streaming PRs.
- [ ] **Staff** — Architect Kafka client conventions at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.2.2: Engineer Kafka → Flink → Iceberg streaming sink (with windowing)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer in the Lab a Kafka → Flink (with windowed aggregation) → Iceberg sink pipeline. Demonstrate watermarks, late-data handling, and exactly-once-via-transactions to the sink. Document in `docs/notes/flink-iceberg-poc.md`.

**Skill progression by level:**
- [ ] **Junior** — *(out of progression — applied work at Senior calibration)*
- [ ] **Mid** — Apply a basic Flink streaming job under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the canonical Flink + Iceberg streaming sink with windowing + exactly-once; document the operational concerns; mentor mid-level engineers.
- [ ] **Staff** — Architect Flink-on-K8s deployment patterns + state-backend infrastructure.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.2.3: Engineer CDC Debezium → Kafka → Iceberg upsert (production-grade)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer the Lab CDC pipeline (Postgres via Debezium → Kafka → Flink/Spark with MERGE → Iceberg upsert). Show comparative queries vs batch ingestion to quantify latency + freshness improvement. Cross-link to Epic 2 Story 2.1's CDC sub-skill.

**Skill progression by level:**
- [ ] **Junior** — *(out of progression — applied work at Senior calibration)*
- [ ] **Mid** — Apply a basic CDC pipeline.
- [ ] **🎯 Senior (TARGET)** — Engineer the production-grade CDC streaming pipeline with measured latency improvement; document operational runbook; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-source CDC at platform scale (shared Kafka Connect cluster, schema-registry integration).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 9.3 — Make the Batch-vs-Streaming Decision

> **What "Senior at this Skill" means.** A Senior here can defend per-pipeline the team's choice of batch vs streaming with concrete trade-offs — not "streaming is modern" reasoning, but cost / latency / operational-complexity analysis tied to the specific use case.

### Sub-skill 9.3.1: Define the batch-vs-streaming decision framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/batch-vs-streaming-decision.md` with the decision flowchart: latency tolerance × cost budget × operational maturity × consumer requirements → batch or streaming. Document the team's default (batch) and the explicit conditions that justify streaming. Apply the framework to 3 hypothetical Lab pipelines.

**Skill progression by level:**
- [ ] **Junior** — Recognize batch vs streaming as different paradigms.
- [ ] **Mid** — Apply existing team conventions to new pipelines.
- [ ] **🎯 Senior (TARGET)** — Define the framework; review proposals against it; push back on "streaming because cool" reasoning.
- [ ] **Staff** — Architect platform-level batch vs streaming portfolio + migration strategy.
- [ ] **Principal** — Govern org-wide streaming-adoption strategy.

---

### Sub-skill 9.3.2: Design Lambda vs Kappa architecture trade-offs

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/lambda-vs-kappa.md` covering Lambda architecture (batch + speed layer with reconciliation) vs Kappa (single streaming layer with re-processing via re-reading the log). Document the cost-delta and operational-complexity trade-offs. Publish a comparative Lab report in `docs/adr/lab-007-batch-vs-stream.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize Lambda and Kappa by name.
- [ ] **Mid** — Apply existing architecture; understand the rough trade-offs.
- [ ] **🎯 Senior (TARGET)** — Define when each wins; publish the ADR; review proposals for architecture-paradigm fit.
- [ ] **Staff** — Architect platform-wide migration paths (Lambda → Kappa where it makes sense).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 9.4 — Evaluate Stream Processing Engines (Flink, Spark Streaming, Beam)

> **What "Senior at this Skill" means.** A Senior here knows the trade-offs between Apache Flink (true streaming, lowest-latency, mature state), Spark Structured Streaming (micro-batch, ecosystem-friendly), and Apache Beam (engine-portable, Dataflow runner). They've shipped at least one job in two engines for comparison.

### Sub-skill 9.4.1: Master Apache Flink fundamentals (DataStream API, Table API, SQL)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/flink-fundamentals.md` covering the 3 Flink APIs (DataStream low-level, Table high-level, Flink SQL declarative), state backends, checkpointing semantics, and Flink on Kubernetes deployment. Cross-link to sub-skill 9.2.2.

**Skill progression by level:**
- [ ] **Junior** — Recognize Flink as a stream processor.
- [ ] **Mid** — Apply Flink SQL for basic jobs.
- [ ] **🎯 Senior (TARGET)** — Master Flink's 3 APIs; document the operational concerns; review streaming proposals for Flink fit.
- [ ] **Staff** — Architect Flink at platform scale (multi-tenant, state-backend infrastructure).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.4.2: Evaluate Spark Structured Streaming + Apache Beam alternatives

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/spark-streaming-vs-beam.md` covering Spark Structured Streaming (micro-batch, ecosystem-coherent with Spark batch), Apache Beam (engine-portable abstraction with Dataflow / Flink / Spark runners). Document when each wins vs Flink.

**Skill progression by level:**
- [ ] **Junior** — Recognize Spark Streaming and Beam by name.
- [ ] **Mid** — Apply one of them under guidance.
- [ ] **🎯 Senior (TARGET)** — Evaluate engines for a given workload; recommend per use case; review proposals.
- [ ] **Staff** — Architect engine-portability strategy (e.g., Beam where engine-portability matters).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.4.3: Engineer same-job comparison across engines (proof artifact)

**Target:** `Staff`

**Activity & Artifact (Senior DoD):** Engineer the same job in Flink AND Spark Structured Streaming in the Lab (`compare-stream-engines` branch) with a comparative ADR documenting latency, cost, operational-complexity, and developer-experience trade-offs.

**Skill progression by level:**
- [ ] **Junior** — *(out of progression — applied work at Senior+ calibration)*
- [ ] **Mid** — *(out of progression)*
- [ ] **Senior** — Apply one engine fluently; document the comparison via prior knowledge of the other.
- [ ] **🎯 Staff (TARGET)** — Engineer the same job in both engines; publish the comparative ADR; influence platform engine choice.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 9.5 — Design Streaming SQL & Stateful Workflows

> **What "Senior at this Skill" means.** A Senior here knows when streaming SQL (Materialize, ksqlDB, Flink SQL) beats imperative streaming code, and when stateful long-running workflows (Temporal.io) beat both. They've shipped a Materialize POC and a Temporal workflow.

### Sub-skill 9.5.1: Engineer streaming SQL (Materialize, ksqlDB, RisingWave)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/streaming-sql.md` covering ksqlDB (streaming SQL over Kafka, KStreams + KTables, push queries), Materialize (Postgres-wire-protocol over streaming, incremental view maintenance via differential dataflow), and RisingWave as a modern open-source alternative. Apply Materialize in the Lab with an incremental view over a Kafka stream.

**Skill progression by level:**
- [ ] **Junior** — Recognize streaming SQL as a category.
- [ ] **Mid** — Apply ksqlDB or Materialize basic queries.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab streaming SQL POC; document when streaming SQL beats imperative streaming; review proposals.
- [ ] **Staff** — Architect streaming-SQL at platform scale (multi-tenant Materialize, shared Kafka).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.5.2: Define streaming SQL vs batch incremental dbt decision

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/streaming-sql-vs-incremental-dbt.md` covering the trade-off — streaming SQL gives sub-second freshness at higher cost + operational complexity; batch incremental dbt (Snowflake Dynamic Tables, dbt incremental models) gives minute-to-hour freshness at lower cost. Document the team's "freshness threshold" decision rule.

**Skill progression by level:**
- [ ] **Junior** — Recognize that freshness has cost.
- [ ] **Mid** — Apply incremental dbt; understand its freshness floor.
- [ ] **🎯 Senior (TARGET)** — Define the decision rule; review proposals for streaming-SQL-vs-incremental-dbt fit.
- [ ] **Staff** — Architect cross-pipeline freshness strategy at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.5.3: Engineer Temporal.io for stateful long-running workflows

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/temporal.md` covering Temporal.io architecture (durable workflows, signals, queries, activity replay), use cases where Temporal beats Airflow (long-running stateful work, human-in-the-loop, saga patterns), and the operational model. Engineer a Lab Temporal workflow (e.g., long-running ingestion with saga pattern) + comparison vs equivalent Airflow DAG.

**Skill progression by level:**
- [ ] **Junior** — Recognize Temporal as a workflow engine.
- [ ] **Mid** — Apply a basic Temporal workflow under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Temporal workflow + comparison; document when Temporal beats Airflow; review proposals.
- [ ] **Staff** — Architect Temporal at platform scale (shared cluster, multi-tenant).
- [ ] **Principal** — Govern org-wide stateful-workflow strategy.

---

## Story 9.6 — Select Messaging Brokers Beyond Kafka

> **What "Senior at this Skill" means.** A Senior here knows when Kafka is the right answer (most cases) and when Pulsar (multi-tenancy + tiered storage), NATS (lightweight, low-latency), or RabbitMQ (classic AMQP routing) is better. They've shipped at least one Pulsar POC for comparison.

### Sub-skill 9.6.1: Evaluate Apache Pulsar as a Kafka alternative

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/pulsar.md` covering Pulsar architecture (multi-tenancy by design, tiered storage with BookKeeper, geo-replication, Pulsar Functions), and the use cases where Pulsar beats Kafka (multi-tenant SaaS, infinite retention via tiered storage, geo-distributed). Apply a Pulsar stack in the Lab + producer/consumer demo with benchmark vs Kafka.

**Skill progression by level:**
- [ ] **Junior** — Recognize Pulsar by name.
- [ ] **Mid** — Apply Pulsar under guidance.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Pulsar POC + benchmark; document when Pulsar beats Kafka; review proposals.
- [ ] **Staff** — Architect Pulsar at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.6.2: Compare NATS, RabbitMQ & legacy brokers (Storm/Samza)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/messaging-alternatives.md` covering NATS (lightweight pub/sub, JetStream for persistence, request/reply), RabbitMQ (AMQP, exchanges + queues + routing patterns), and legacy stream processors (Apache Storm + Samza) that may still appear in older stacks. Document when each beats Kafka.

**Skill progression by level:**
- [ ] **Junior** — Recognize the names.
- [ ] **Mid** — Apply RabbitMQ or NATS under guidance.
- [ ] **🎯 Senior (TARGET)** — Evaluate alternatives; recommend per use case; review proposals.
- [ ] **Staff** — Architect cross-broker strategy at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 9.6.3: Define the team's broker-selection criteria

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/broker-selection.md` with the team's decision matrix: latency target × throughput × ordering guarantees × multi-tenancy × ops cost × retention requirements → recommendation. Document the team's default (Kafka) and the explicit exception cases for Pulsar / NATS / RabbitMQ.

**Skill progression by level:**
- [ ] **Junior** — Recognize that brokers differ.
- [ ] **Mid** — Apply existing team conventions.
- [ ] **🎯 Senior (TARGET)** — Define the selection matrix; review broker-adoption proposals.
- [ ] **Staff** — Architect broker portfolio at platform scale.
- [ ] **Principal** — Govern org-wide messaging-platform strategy.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 6 Story-level 🎯 boxes are ticked** — which requires the ~17 sub-skill 🎯 Senior boxes. Mastery evidence: Kafka fundamentals doc + Dataflow-model notes, Lab POCs (producer→Kafka→consumer, Flink+Iceberg, CDC streaming, Materialize incremental view, Temporal workflow, Pulsar POC), batch-vs-streaming + Lambda-vs-Kappa decision ADR, broker-selection matrix.
