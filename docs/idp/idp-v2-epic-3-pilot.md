# IDP v2 — Epic 3 Pilot · Storage Layer

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills owns the team's storage discipline — they decide layering (Bronze/Silver/Gold), partitioning + clustering strategy, table-format choice (Iceberg / Delta / Hudi), columnar format + compaction, NoSQL/NewSQL adoption, real-time OLAP vs warehouse, specialized stores (vector / search / time-series / graph), and the migration story for legacy Hadoop. They've published the team's reference notes and shipped Lab implementations that demonstrate each choice in production-grade code.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered.

---

## Story 3.1 — Architect the Storage Layering

> **What "Senior at this Skill" means.** A Senior here decides how the team's storage stack is layered (Bronze/Silver/Gold or raw/refined/aggregated), what transformations happen between layers, and what retention + tiering applies at each. They published the team's reference and configured the actual lifecycle policies.

### Sub-skill 3.1.1: Design the team's layered architecture (Bronze/Silver/Gold)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/medallion-vs-raw-refined.md` comparing Medallion (Bronze/Silver/Gold) and raw/refined/aggregated layering — with each layer's responsibilities (Bronze = immutable raw + minimal validation; Silver = deduped + conformed; Gold = business-facing marts) and the transformations between them. Apply the 3-layer model in the Lab via dbt + Iceberg with explicit `models/{staging,intermediate,marts}/` separation and document the team's "what belongs in which layer" decision tree.

**Skill progression by level:**
- [ ] **Junior** — Recognize the 3 layers and their names.
- [ ] **Mid** — Apply staging/intermediate/marts conventionally in dbt.
- [ ] **🎯 Senior (TARGET)** — Design the team's layer responsibilities + transformation contracts; review modeling PRs against layer fit; mentor mid-level engineers on the boundary cases ("does this belong in Silver or Gold?").
- [ ] **Staff** — Architect cross-domain Medallion at platform scale with shared layer-promotion infrastructure.
- [ ] **Principal** — Govern org-wide data-layer policy and SLA per layer.

---

### Sub-skill 3.1.2: Define retention & storage-tiering policy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/retention-tiering.md` with the team's matrix: layer × data-class × retention × tier (e.g., Bronze raw events → 90d hot + 2y warm + 5y archive; Gold marts → indefinite hot). Document S3/GCS lifecycle rules in Terraform applied to the Lab, with cost-delta measured over a 30-day window. Tie retention decisions explicitly to LGPD/GDPR right-to-erasure obligations.

**Skill progression by level:**
- [ ] **Junior** — Recognize that storage costs vary by tier (S3 Standard / IA / Glacier).
- [ ] **Mid** — Apply a lifecycle rule under guidance.
- [ ] **🎯 Senior (TARGET)** — Define the team's retention + tier matrix; ship it as Terraform; review storage decisions for cost vs compliance fit.
- [ ] **Staff** — Architect retention + tiering automation across the platform (auto-archival, cost-attribution dashboards).
- [ ] **Principal** — Govern org-wide retention policy + regulatory mapping.

---

## Story 3.2 — Engineer Partitioning & Clustering

> **What "Senior at this Skill" means.** A Senior here ensures every table the team ships is partitioned and clustered correctly — and can prove it via partition-pruning audits showing real cost-delta. They reject high-cardinality partition keys in PR review and explain why.

### Sub-skill 3.2.1: Define the team's partitioning strategy framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/partitioning.md` covering partitioning by time, hash, range, and Iceberg hidden partitioning — with anti-patterns (high cardinality, partition-per-tenant for thousands of tenants, daily partitions when monthly suffices). Apply correct partition strategy to 5 Lab tables and document the rationale per table.

**Skill progression by level:**
- [ ] **Junior** — Recognize partitioning as a query-optimization tool.
- [ ] **Mid** — Apply time-partitioning on fact tables.
- [ ] **🎯 Senior (TARGET)** — Define the team's partition-strategy framework + anti-pattern catalogue; review PRs that introduce high-cardinality keys; mentor mid-level engineers on partition-key choice.
- [ ] **Staff** — Architect cross-warehouse partition conventions + automated partition-evolution tooling.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.2.2: Engineer clustering, z-ordering & bucketing

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/clustering-zordering.md` comparing BigQuery clustering, Delta z-ordering, Iceberg bucketing, and Hive bucketing — with the trade-offs (write cost vs query speed) and use cases. Engineer clustering + z-ordering in 3 Lab tables with measured query-cost reduction.

**Skill progression by level:**
- [ ] **Junior** — Recognize clustering as an addition to partitioning.
- [ ] **Mid** — Apply BigQuery clustering on warehouse-specific tables.
- [ ] **🎯 Senior (TARGET)** — Engineer correct clustering + z-ordering per warehouse; ship Lab tables with measured cost reduction; review PRs for clustering correctness.
- [ ] **Staff** — Architect platform-level clustering recommendations (analyze + suggest from query patterns).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.2.3: Own partition-pruning audit methodology

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/runbooks/partition-pruning-audit.md` with the team's methodology — how to find tables not pruning, the EXPLAIN/`bytes_billed` signals to check, common fix patterns. Apply the audit on 5 Lab queries with before/after evidence in `docs/audit/pruning-2026Q2.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize that partitions can fail to prune.
- [ ] **Mid** — Read a query plan and see whether pruning happened.
- [ ] **🎯 Senior (TARGET)** — Own the audit methodology; ship 5 worked Lab audits with cost-delta; mentor mid-level engineers through their first audit.
- [ ] **Staff** — Architect continuous partition-pruning regression detection (scheduled audits + alerting).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 3.3 — Evaluate & Operate Table Formats

> **What "Senior at this Skill" means.** A Senior here can justify the team's choice of Iceberg vs Delta vs Hudi vs raw Parquet — not by trend-following, but by trade-off analysis grounded in the team's workload. They operate the chosen format day-to-day: snapshots, compaction, VACUUM, time-travel.

### Sub-skill 3.3.1: Master Apache Iceberg internals & operations

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/iceberg-internals.md` covering Iceberg's manifest list, snapshot model, branches/tags, compaction, hidden partitioning, and the catalog implementations (Hive, REST, Nessie). Apply Iceberg as the default Lab table format with documented migration from Parquet and an ADR `docs/adr/lab-001-iceberg.md`.

**Skill progression by level:**
- [ ] **Junior** — Recognize Iceberg as a table format.
- [ ] **Mid** — Apply Iceberg in dbt or Spark with default config.
- [ ] **🎯 Senior (TARGET)** — Master Iceberg internals + operations; ship Lab as Iceberg-default with documented migration; review Iceberg-related PRs for compaction and snapshot hygiene.
- [ ] **Staff** — Architect cross-engine Iceberg catalogs (REST + Nessie) + governance at platform scale.
- [ ] **Principal** — Govern org-wide table-format strategy and migration roadmap.

---

### Sub-skill 3.3.2: Evaluate Delta Lake and Hudi as alternatives

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/delta-vs-hudi-vs-iceberg.md` covering Delta Lake (transaction log, OPTIMIZE, VACUUM, time-travel — Databricks-native ergonomics), Hudi (Copy-on-Write vs Merge-on-Read trade-offs), and the cases where each beats Iceberg. Document the team's "if X then Delta; if Y then Hudi" exception cases.

**Skill progression by level:**
- [ ] **Junior** — Recognize Delta and Hudi as alternatives to Iceberg.
- [ ] **Mid** — Apply one of them in a single Lab use case.
- [ ] **🎯 Senior (TARGET)** — Evaluate all 3 formats against the team's workload; document the exception cases; review architecture proposals that involve table-format choice.
- [ ] **Staff** — Architect multi-format support across the platform (e.g., Iceberg + Delta coexisting per use case).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.3.3: Engineer time-travel & snapshot operations

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Engineer time-travel queries on Lab Iceberg tables for 3 use cases (debug a yesterday's-data discrepancy, rollback a bad PR's data load, audit historical pricing). Author `docs/notes/time-travel-patterns.md` documenting the 3 use cases and the operational cost (snapshot retention + storage).

**Skill progression by level:**
- [ ] **Junior** — Recognize that table formats support time-travel.
- [ ] **Mid** — Apply `VERSION AS OF` syntactically.
- [ ] **🎯 Senior (TARGET)** — Engineer 3 production-grade time-travel use cases in the Lab; document the operational trade-offs; mentor mid-level engineers on safe rollback patterns.
- [ ] **Staff** — Architect time-travel as a platform feature (automated rollback workflows, audit-trail integration).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 3.4 — Design Columnar Formats & File-Layout

> **What "Senior at this Skill" means.** A Senior here understands what's inside a Parquet file (row groups, column chunks, page indexes, statistics) well enough to debug a slow scan, choose between Parquet/ORC/Avro per use case, and engineer compaction that hits the 128 MB–1 GB sweet spot.

### Sub-skill 3.4.1: Understand Parquet/ORC/Avro internals & selection criteria

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/columnar-formats.md` covering Parquet's physical structure (row groups, column chunks, pages, statistics, page index), ORC's stripe-based structure, and Avro's row-based serialization. Document when each format wins: Parquet for analytics-heavy reads, ORC for Hive-ecosystem compatibility, Avro for streaming + schema evolution.

**Skill progression by level:**
- [ ] **Junior** — Recognize Parquet/ORC/Avro names.
- [ ] **Mid** — Apply Parquet by default; choose Avro for streaming.
- [ ] **🎯 Senior (TARGET)** — Understand each format's internals well enough to debug a slow scan or unexpected file size; review PRs that introduce a new format.
- [ ] **Staff** — Architect cross-format conversion + storage migration at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.4.2: Engineer file-size + compaction strategy

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/file-size-compaction.md` covering the small-files problem, target file size sweet spots (128 MB–1 GB), and compaction strategies (Iceberg `rewrite_data_files`, Delta `OPTIMIZE`, Hive INSERT OVERWRITE). Engineer a Lab compaction DAG that runs on schedule, with metrics showing file-count reduction and query-speed improvement.

**Skill progression by level:**
- [ ] **Junior** — Recognize that many small files hurt performance.
- [ ] **Mid** — Apply manual compaction occasionally.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's automated compaction; document target file sizes; review PRs that produce small-file pollution.
- [ ] **Staff** — Architect platform-level compaction tooling across many tables.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.4.3: Engineer predicate pushdown & statistics tuning

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/predicate-pushdown.md` covering how min/max statistics, dictionary encoding, and Bloom filters at the Parquet level enable predicate pushdown. Document the team's column-encoding-strategy decision tree (when to use dictionary, when delta, when RLE).

**Skill progression by level:**
- [ ] **Junior** — Recognize "predicate pushdown" as a concept.
- [ ] **Mid** — Apply predicate filters and observe scan reduction.
- [ ] **🎯 Senior (TARGET)** — Engineer encoding choices for pushdown; review PRs for pushdown-killers (e.g., function applied to predicate).
- [ ] **Staff** — Architect platform-wide encoding standards + analyzer tooling.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 3.5 — Select NoSQL, Key-Value & NewSQL

> **What "Senior at this Skill" means.** A Senior here knows the document / wide-column / key-value / NewSQL landscape well enough to recommend the right storage per workload — and integrates them as ingestion sources or serving caches in the Lab.

### Sub-skill 3.5.1: Own document-DB literacy (MongoDB, Couchbase)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/document-dbs.md` covering MongoDB's document model, indexes (compound, multikey, text), aggregation pipeline, and change streams + Couchbase's similar features. Apply Mongo as a Lab source with ingestion via change streams (resume tokens, oplog retention).

**Skill progression by level:**
- [ ] **Junior** — Recognize document model vs relational.
- [ ] **Mid** — Apply Mongo queries; design a basic schema.
- [ ] **🎯 Senior (TARGET)** — Own the team's Mongo ingestion pattern + schema conventions; mentor on document-vs-relational choice.
- [ ] **Staff** — Architect document-DB integration at platform scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.5.2: Own wide-column DB literacy (Cassandra, DynamoDB, HBase)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/wide-column-dbs.md` covering Cassandra's partition + clustering key model, tunable consistency (ONE/QUORUM/ALL), DynamoDB's single-table design pattern + GSI/LSI, Apache HBase's HFile model. Provide 1 worked single-table design example for a Lab use case.

**Skill progression by level:**
- [ ] **Junior** — Recognize wide-column as a category.
- [ ] **Mid** — Read a Cassandra schema; apply DynamoDB queries.
- [ ] **🎯 Senior (TARGET)** — Design wide-column schemas for given access patterns; review proposals that use Cassandra/Dynamo.
- [ ] **Staff** — Architect cross-region wide-column deployments.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.5.3: Own key-value & cache literacy (Redis)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/redis-patterns.md` covering Redis data structures (strings, hashes, sorted sets, streams), persistence options (RDB vs AOF), eviction policies, and the cache-aside / write-through / write-behind patterns. Apply Redis as a feature-store cache in the Lab (microservice reading features by user key) with measured latency.

**Skill progression by level:**
- [ ] **Junior** — Recognize Redis as a cache.
- [ ] **Mid** — Apply Redis SET/GET; understand TTL.
- [ ] **🎯 Senior (TARGET)** — Engineer Redis as a feature-store cache; document the patterns + persistence trade-offs; review PRs for cache-invalidation bugs.
- [ ] **Staff** — Architect Redis-as-a-service across teams (HA, sharding, monitoring).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.5.4: Evaluate NewSQL for distributed OLTP at scale

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/newsql.md` covering CockroachDB, Spanner, TiDB, YugabyteDB — their consensus models (Raft-based), horizontal scaling, and the cases where they beat Postgres for OLTP-at-scale. Apply CockroachDB in the Lab and benchmark vs Postgres for an OLTP workload, documenting the cost/complexity trade-off.

**Skill progression by level:**
- [ ] **Junior** — Recognize NewSQL as a category between traditional SQL and NoSQL.
- [ ] **Mid** — Apply CockroachDB or Spanner for a simple use case.
- [ ] **🎯 Senior (TARGET)** — Evaluate NewSQL adoption against the team's actual scale; document the trade-offs; review proposals.
- [ ] **Staff** — Architect NewSQL adoption as a platform decision with migration path.
- [ ] **Principal** — Govern OLTP-platform strategy at the org level.

---

### Sub-skill 3.5.5: Define polyglot persistence decision framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/polyglot-persistence.md` with the team's decision flowchart: workload (OLTP / OLAP / search / time-series / cache / graph) → recommended storage. Document the cost of polyglot (operational overhead, learning curve, integration complexity) and when monoculture beats polyculture.

**Skill progression by level:**
- [ ] **Junior** — Recognize that different storage suits different workloads.
- [ ] **Mid** — Apply the existing team conventions.
- [ ] **🎯 Senior (TARGET)** — Define the decision flowchart; review storage-choice proposals against it; push back on unnecessary polyglot adoption.
- [ ] **Staff** — Architect cross-team polyglot governance (which storage is "supported" vs "experimental").
- [ ] **Principal** — Govern org-wide storage portfolio + retirement policy.

---

## Story 3.6 — Architect Real-Time OLAP Solutions

> **What "Senior at this Skill" means.** A Senior here can decide between ClickHouse / Pinot / Druid / StarRocks vs BigQuery/Snowflake for real-time analytics workloads — and has shipped a Lab benchmark that proves the trade-offs.

### Sub-skill 3.6.1: Master ClickHouse internals & operations

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/clickhouse.md` covering the MergeTree engine family (Replicated, Distributed, Replacing, Aggregating), materialized views, and operational concerns (parts management, mutations, ZooKeeper coordination). Apply ClickHouse in the Lab with a benchmark vs DuckDB and Postgres on the same dataset, documenting the cost/latency/throughput trade-offs.

**Skill progression by level:**
- [ ] **Junior** — Recognize ClickHouse as a fast OLAP engine.
- [ ] **Mid** — Apply basic ClickHouse queries; understand MergeTree at a high level.
- [ ] **🎯 Senior (TARGET)** — Engineer a Lab ClickHouse stack with benchmarks; review proposals for ClickHouse adoption against actual workload fit.
- [ ] **Staff** — Architect ClickHouse as a platform service (clustering, replication, backup).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.6.2: Evaluate Pinot, Druid & StarRocks alternatives

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/real-time-olap-alternatives.md` covering Apache Pinot (real-time + offline tables, segments, broker/server/controller), Apache Druid (segments, lookups, native Kappa architecture), and StarRocks/Apache Doris (emerging open-source alternatives). Document when each beats ClickHouse and when none of them beats a warehouse.

**Skill progression by level:**
- [ ] **Junior** — Recognize the names of the alternatives.
- [ ] **Mid** — Apply one of them for a single use case.
- [ ] **🎯 Senior (TARGET)** — Evaluate Pinot/Druid/StarRocks against the team's workload; recommend per use case.
- [ ] **Staff** — Architect real-time-OLAP platform strategy at multi-team scale.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.6.3: Define real-time-OLAP adoption decision criteria

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/real-time-olap-decision.md` with the team's flowchart: query-latency target × concurrency × data-freshness × cost-budget → recommendation. Document the "if you don't need < 1s P99, use BigQuery/Snowflake" default and the cases that justify dedicated real-time OLAP.

**Skill progression by level:**
- [ ] **Junior** — Recognize that real-time OLAP is a separate category from warehouses.
- [ ] **Mid** — Apply the existing team default (warehouse) and recognize when it's the wrong choice.
- [ ] **🎯 Senior (TARGET)** — Define the team's adoption criteria; review proposals that involve dedicated real-time OLAP.
- [ ] **Staff** — Architect real-time-OLAP as a platform offering with shared infra + cost-attribution.
- [ ] **Principal** — Govern org-wide real-time-analytics strategy.

---

## Story 3.7 — Architect Specialized Data Stores

> **What "Senior at this Skill" means.** A Senior here knows when to specialize (vector for semantic search, search engines for full-text, time-series for metrics, graph for traversal) vs when to keep everything in the warehouse. They've shipped at least 2 specialized stores in the Lab as references.

### Sub-skill 3.7.1: Engineer vector DBs for semantic search

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/vector-dbs.md` covering pgvector (Postgres extension), Pinecone, Weaviate, Qdrant, Milvus — with similarity metrics (cosine, dot, L2) and ANN algorithms (HNSW, IVF) and their accuracy/speed trade-offs. Apply pgvector in the Lab for semantic search over a document corpus, measuring recall@k vs latency.

**Skill progression by level:**
- [ ] **Junior** — Recognize that vector DBs exist for embedding search.
- [ ] **Mid** — Apply pgvector or Pinecone for a simple semantic search.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's Lab vector-DB stack with measured recall/latency; choose vector DB per use case; review proposals.
- [ ] **Staff** — Architect vector-DB as a platform service shared across ML/RAG teams.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.7.2: Engineer search engines (Elasticsearch / OpenSearch)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/search-engines.md` covering Elasticsearch / OpenSearch architecture (inverted index, BM25 ranking, faceted search), Meilisearch and Typesense as lightweight alternatives, and the trade-offs (cost, operational complexity, query DSL). Apply OpenSearch in the Lab for log analytics + full-text search with shipped dashboards.

**Skill progression by level:**
- [ ] **Junior** — Recognize search engines as a category.
- [ ] **Mid** — Apply ES queries; ingest logs into ES.
- [ ] **🎯 Senior (TARGET)** — Engineer the team's OpenSearch stack for logs + search; tune ranking and faceting; mentor mid-level engineers.
- [ ] **Staff** — Architect search-as-a-service across products.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.7.3: Engineer time-series DBs (TimescaleDB / InfluxDB)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/time-series-dbs.md` covering TimescaleDB (Postgres extension — hypertables, continuous aggregates, retention policies), InfluxDB, QuestDB, and Prometheus storage. Apply TimescaleDB in the Lab for 1 time-series dataset (e.g., metrics from Lab DAGs) with queries comparing it vs plain Postgres on the same data.

**Skill progression by level:**
- [ ] **Junior** — Recognize that time-series DBs are specialized.
- [ ] **Mid** — Apply TimescaleDB or InfluxDB for a sample workload.
- [ ] **🎯 Senior (TARGET)** — Engineer TimescaleDB in the Lab + benchmark vs Postgres; document when each wins; review proposals for time-series workloads.
- [ ] **Staff** — Architect time-series stack at platform scale (TSDB + downsampling + retention).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.7.4: Understand graph databases & Cypher

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/graph-dbs.md` covering Neo4j, Amazon Neptune, ArangoDB and the Cypher query language. Document use cases where graph DBs win (multi-hop traversal, recommendation, fraud detection) and where they don't (analytics roll-ups, OLAP).

**Skill progression by level:**
- [ ] **Junior** — Recognize graph databases as a category.
- [ ] **Mid** — Apply a basic Cypher query.
- [ ] **🎯 Senior (TARGET)** — Understand when graph DBs are the right fit; read Cypher fluently; review proposals.
- [ ] **Staff** — Architect graph-DB adoption with platform-level operations.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.7.5: Define specialized-store adoption decision framework

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/specialized-store-decision.md` with the team's decision flowchart: workload type → recommended specialized store (or "keep it in the warehouse"). Document the cost of specialization (op overhead, learning curve, integration) and the team's threshold for adoption.

**Skill progression by level:**
- [ ] **Junior** — Recognize that specialized stores exist.
- [ ] **Mid** — Apply existing team conventions.
- [ ] **🎯 Senior (TARGET)** — Define the team's specialization threshold; review proposals for fit.
- [ ] **Staff** — Architect platform-wide specialized-store portfolio + retirement policy.
- [ ] **Principal** — Govern org-wide storage-specialization strategy.

---

## Story 3.8 — Recognize Hadoop Legacy Ecosystem

> **What "Senior at this Skill" means.** A Senior here walks into a legacy Hadoop refactor project and can read the existing stack (HDFS + Hive Metastore + MapReduce/Spark) well enough to plan its migration to a modern lakehouse. They don't need to be Hadoop experts — they need legacy literacy.

### Sub-skill 3.8.1: Recognize HDFS + MapReduce ecosystem (legacy awareness)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/hadoop-legacy.md` covering HDFS architecture (NameNode, DataNode, blocks, replication factor), the MapReduce paradigm (history, mental model, why Spark superseded it), and Ceph as an alternative object/block storage for on-prem. Document why object storage replaced HDFS for new builds.

**Skill progression by level:**
- [ ] **Junior** — Recognize HDFS and MapReduce as legacy.
- [ ] **Mid** — Apply Hadoop ecosystem commands when needed for legacy work.
- [ ] **🎯 Senior (TARGET)** — Read legacy Hadoop stacks fluently; explain why object storage replaced HDFS; mentor mid-level engineers walking into a Hadoop refactor.
- [ ] **Staff** — Architect legacy-Hadoop migration programs.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.8.2: Engineer Hive Metastore as a Lab catalog

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/hive-metastore.md` covering the Hive Metastore (Thrift API, schema, partition discovery) and its continuing role as a catalog standard used by Spark, Trino, and Iceberg. Document Hive QL (HQL), managed vs external tables, and ACID transactions on Hive 3+. Apply Hive Metastore in the Lab used by Spark + Trino, with queries demonstrating cross-engine catalog interoperability.

**Skill progression by level:**
- [ ] **Junior** — Recognize Hive Metastore as a catalog component.
- [ ] **Mid** — Apply Hive Metastore in a Spark or Trino setup.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Metastore + cross-engine queries; document HQL idioms vs modern SQL; review migration plans that move off Metastore.
- [ ] **Staff** — Architect Metastore replacement / coexistence (Iceberg REST catalog migration).
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 3.8.3: Define Hadoop → modern-lakehouse migration patterns

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/hadoop-migration-patterns.md` with the team's migration strategy: in-place catalog migration to Iceberg, dual-write windows for hot tables, Spark-on-K8s replacing YARN, object storage replacing HDFS, downstream consumer cutover. Reference 2-3 industry case studies and quantify the migration cost.

**Skill progression by level:**
- [ ] **Junior** — Recognize that Hadoop refactor projects exist.
- [ ] **Mid** — Apply a migration step under guidance.
- [ ] **🎯 Senior (TARGET)** — Define the team's migration playbook; lead a hypothetical Hadoop → lakehouse migration on paper for the Lab.
- [ ] **Staff** — Architect real-world Hadoop migration programs across multi-team Hadoop estates.
- [ ] **Principal** — Govern org-wide legacy-retirement strategy.

---

## Epic-Level Mastery Definition

**This Epic is mastered at Senior level when all 8 Story-level 🎯 boxes are ticked** — which requires all ~28 sub-skill 🎯 Senior boxes. Mastery evidence: published notes (`docs/notes/*.md`), runbooks (`docs/runbooks/*.md`), Lab implementations (Iceberg-default, compaction DAG, pgvector semantic search, OpenSearch logs, TimescaleDB metrics, Mongo change streams, Redis cache, CockroachDB benchmark), and at least 1 ADR (`docs/adr/lab-001-iceberg.md`).
