# IDP v2 — Epic 19 Pilot · AWS for Data Engineering (DEA-C01)

> **What "Senior at this Set of skills" means.** A Senior on this Set of skills can architect a production AWS data platform across ingestion, storage, processing, orchestration, security, and cost — aligned to the **AWS Certified Data Engineer Associate (DEA-C01)** exam. They've shipped ≥2 services per Story in the Lab and passed the exam.
>
> **Bibliography.** *AWS Certified Data Engineer Associate Study Guide* (Sybex/Wiley) · *Data Engineering with AWS* 2nd ed. (Eagar) · AWS Well-Architected — Data Analytics Lens · AWS Skill Builder DEA-C01 plan · re:Invent talks (DAT/ANT/BIG tracks).
>
> **Exam objectives.** Ingestion & Transformation 34% · Data Store Management 26% · Operations & Support 22% · Security & Governance 18%.
>
> **Mastery rule.** A Skill is mastered at Senior when all its 🎯 sub-skill levels have been reached. This Set of Skills is mastered when all its skills are mastered AND DEA-C01 passed.

---

## Story 19.1 — Operate AWS Ingestion Services

### Sub-skill 19.1.1: Select between Kinesis Data Streams, Firehose, and MSK for streaming ingestion

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-streaming-ingest.md` covering Kinesis Data Streams (shards, retention, KCL/KPL, on-demand mode), Kinesis Data Firehose (delivery streams, buffering, S3/Redshift/OpenSearch sinks, format conversion), and Amazon MSK (managed Kafka + MSK Connect + MSK Serverless) with selection criteria. Engineer Kinesis Data Streams + KCL in the Lab via LocalStack with a consumer in Python, and engineer MSK + MSK Connect in a Compose stack.

**Skill progression by level:**
- [ ] **Junior** — Recognize Kinesis and Kafka by name.
- [ ] **Mid** — Apply existing Kinesis / MSK producers and consumers.
- [ ] **🎯 Senior (TARGET)** — Select between Streams, Firehose, MSK per workload; engineer Lab proofs; mentor mid-level engineers on shard counts and on-demand vs provisioned.
- [ ] **Staff** — Architect cross-team streaming ingestion strategy.
- [ ] **Principal** — Govern org-wide streaming platform policy.

---

### Sub-skill 19.1.2: Engineer DMS CDC + Glue Crawlers for batch and CDC ingestion

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-batch-cdc-ingest.md` covering AWS DMS (full load + CDC, source/target endpoints, replication validation), AWS AppFlow for SaaS sources, AWS DataSync for bulk transfer, Glue Crawlers + Glue Data Catalog for schema discovery, and Snowball for offline transfer. Engineer DMS CDC from Postgres → S3 in the Lab with Compose + replication task config.

**Skill progression by level:**
- [ ] **Junior** — Recognize DMS and Glue as ingestion tools.
- [ ] **Mid** — Apply existing DMS tasks.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab DMS CDC + Glue Catalog setup; mentor mid-level engineers on replication validation.
- [ ] **Staff** — Architect cross-team CDC + cataloging strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 19.2 — Operate AWS Storage Services

### Sub-skill 19.2.1: Engineer S3 + Lake Formation as the data-lake foundation

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-data-lake.md` covering S3 storage classes (Standard, IA, Glacier tiers, Intelligent-Tiering) with lifecycle policies, S3 edge features (Object Lambda, Select, Multipart, strong consistency), and Lake Formation (governance, fine-grained access, row/column security, tag-based ACL — vs Glue Catalog only). Engineer S3 + Glue Catalog + Athena queries in the Lab via LocalStack and Lake Formation tag-based ACL via Terraform.

**Skill progression by level:**
- [ ] **Junior** — Recognize S3 and Glue Catalog.
- [ ] **Mid** — Apply existing S3 buckets and Glue tables.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab data-lake foundation; mentor mid-level engineers on storage classes and Lake Formation tag-based ACL.
- [ ] **Staff** — Architect cross-team data-lake governance.
- [ ] **Principal** — Govern org-wide data-lake policy.

---

### Sub-skill 19.2.2: Engineer Redshift (provisioned + Serverless) with dist/sort optimization

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-redshift.md` covering RA3 nodes + Spectrum + Workload Management + Concurrency Scaling + AQUA, Redshift Serverless economics vs provisioned, and dist style + sort key design. Engineer a Redshift cluster + dist/sort optimization in the Lab with EXPLAIN-validated queries.

**Skill progression by level:**
- [ ] **Junior** — Recognize Redshift as the AWS warehouse.
- [ ] **Mid** — Apply existing Redshift tables.
- [ ] **🎯 Senior (TARGET)** — Engineer Redshift dist/sort design + Serverless trade-off; mentor mid-level engineers on EXPLAIN reading.
- [ ] **Staff** — Architect cross-team warehouse strategy.
- [ ] **Principal** — Govern org-wide warehouse policy.

---

### Sub-skill 19.2.3: Select between RDS/Aurora, DynamoDB, OpenSearch, Timestream for operational + analytical stores

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-operational-stores.md` covering RDS + Aurora (Serverless v2), DynamoDB (single-table design, GSI/LSI, Streams, Global Tables), OpenSearch Service (analytics on logs/search), and Timestream (time series) — with selection criteria for each. Include a single-table DynamoDB example.

**Skill progression by level:**
- [ ] **Junior** — Recognize RDS and DynamoDB.
- [ ] **Mid** — Apply existing RDS/DynamoDB queries.
- [ ] **🎯 Senior (TARGET)** — Select the right store per workload; mentor mid-level engineers on single-table DynamoDB.
- [ ] **Staff** — Architect cross-team operational store strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 19.3 — Operate AWS Processing Services

### Sub-skill 19.3.1: Engineer Glue + EMR + Athena for batch processing

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-batch-processing.md` covering Glue (Spark jobs, Python shell, Studio, Streaming, dynamic frames), EMR (cluster types, Spot fleets, EMR Serverless, EMR on EKS), Athena (federated queries, workgroups, partition projection, CTAS), Lambda for transforms (cold start, limits), and DataBrew for low-code prep. Engineer a Glue job + Athena query in the Lab via LocalStack + an EMR Serverless Spark job in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize Glue, EMR, Athena.
- [ ] **Mid** — Apply existing Glue/Athena queries.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Glue + EMR Serverless setup; select between Glue / EMR / Athena per workload; mentor mid-level engineers.
- [ ] **Staff** — Architect cross-team processing strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 19.3.2: Engineer Step Functions + Managed Flink for orchestration + stream processing

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-stepfn-flink.md` covering Step Functions (state machine, Standard vs Express, error handling, Map states, distributed map) and Kinesis Data Analytics / Managed Apache Flink (vs self-managed Flink). Engineer Step Functions orchestrating an ingestion pipeline in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize Step Functions.
- [ ] **Mid** — Apply existing state machines.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab Step Functions pipeline; select Standard vs Express; mentor mid-level engineers on Map states.
- [ ] **Staff** — Architect cross-team orchestration + streaming strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Story 19.4 — Operate AWS Orchestration

### Sub-skill 19.4.1: Engineer MWAA + EventBridge + Batch for managed orchestration

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-mwaa-eventbridge.md` covering MWAA (environments, sizing, plugins) vs self-managed Airflow (cross-ref Epic 23), EventBridge (event bus, rules, scheduling, schema registry), and AWS Batch. Engineer an MWAA environment via Terraform + an EventBridge + Lambda pipeline in the Lab.

**Skill progression by level:**
- [ ] **Junior** — Recognize MWAA and EventBridge.
- [ ] **Mid** — Apply existing MWAA DAGs.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab MWAA + EventBridge setup; mentor mid-level engineers on the MWAA-vs-self-managed trade-off.
- [ ] **Staff** — Architect cross-team managed orchestration strategy.
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

### Sub-skill 19.4.2: Define CloudWatch + X-Ray + Systems Manager observability + secrets

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-observability.md` covering CloudWatch (logs, metrics, alarms, dashboards, Log Insights, Cross-Account Observability), X-Ray distributed tracing, and Systems Manager Parameter Store + Secrets Manager integration. Apply in the Lab as canonical setup for data pipelines.

**Skill progression by level:**
- [ ] **Junior** — Recognize CloudWatch.
- [ ] **Mid** — Apply existing CloudWatch dashboards.
- [ ] **🎯 Senior (TARGET)** — Define the canonical observability + secrets stack; mentor mid-level engineers on Log Insights queries.
- [ ] **Staff** — Architect cross-team observability strategy.
- [ ] **Principal** — Govern org-wide observability policy.

---

## Story 19.5 — Govern AWS Security & Compliance

### Sub-skill 19.5.1: Define IAM + KMS + VPC endpoints + audit (CloudTrail, Config, Macie)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-security.md` covering IAM (policies, roles, conditions, permission boundaries, SCPs, IAM Access Analyzer), KMS (customer-managed keys, envelope encryption, key policies, grants, multi-region keys), Secrets Manager rotation, Macie (PII discovery), VPC endpoints + PrivateLink, CloudTrail + CloudTrail Lake, and AWS Config rules essential for DE. Engineer KMS-encrypted S3 + Lake Formation ACL in the Lab + a Macie scan with PII findings report.

**Skill progression by level:**
- [ ] **Junior** — Recognize IAM and KMS.
- [ ] **Mid** — Apply existing IAM policies.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab KMS + Lake Formation + Macie setup; mentor mid-level engineers on permission boundaries.
- [ ] **Staff** — Architect cross-team security strategy.
- [ ] **Principal** — Govern org-wide AWS security policy.

---

## Story 19.6 — Optimize AWS Costs & Pass DEA-C01

### Sub-skill 19.6.1: Engineer AWS cost optimization (S3 tiering, Redshift reservations, Athena tuning, Spot)

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Author `docs/notes/aws-cost.md` covering S3 Intelligent-Tiering + lifecycle, Redshift Reserved Nodes vs On-Demand vs Serverless economics with break-even calculations, Athena cost optimization (partition projection, columnar formats, CTAS, results cache), Spot Instances for EMR/Batch, AWS Cost Explorer + CUR analysis via Athena, and Savings Plans vs RIs vs Spot criteria. Engineer CUR + Athena queries + dashboard in the Lab (QuickSight or Grafana).

**Skill progression by level:**
- [ ] **Junior** — Recognize AWS pricing tiers.
- [ ] **Mid** — Apply existing tagging strategies.
- [ ] **🎯 Senior (TARGET)** — Engineer the Lab CUR dashboard; document break-even calculations; mentor mid-level engineers on Athena cost tuning.
- [ ] **Staff** — Architect cross-team AWS FinOps strategy.
- [ ] **Principal** — Govern org-wide AWS cost policy.

---

### Sub-skill 19.6.2: Pass the AWS Certified Data Engineer Associate (DEA-C01) exam

**Target:** `Senior`

**Activity & Artifact (Senior DoD):** Complete the AWS Skill Builder DEA-C01 learning plan, take 3 practice exams (≥85% pass mark before sitting), pass the DEA-C01 exam. Publish a `docs/certs/dea-c01.md` retrospective covering preparation timeline, weak areas hit during prep, and key insights from the exam.

**Skill progression by level:**
- [ ] **Junior** — *(out of natural progression for this sub-skill)*
- [ ] **Mid** — Apply AWS services daily.
- [ ] **🎯 Senior (TARGET)** — Pass DEA-C01; publish retrospective; mentor mid-level engineers preparing for the exam.
- [ ] **Staff** — *(out of natural progression for this sub-skill)*
- [ ] **Principal** — *(out of natural progression for this sub-skill)*

---

## Epic-Level Mastery Definition

**This Epic is mastered when all 6 Story-level 🎯 boxes are ticked** — which requires 11 sub-skill 🎯 boxes including the DEA-C01 cert pass. Mastery evidence: Kinesis/MSK/DMS ingestion proofs; S3 + Lake Formation + Redshift dist/sort lab; Glue + EMR Serverless + Step Functions pipeline; MWAA + EventBridge + CloudWatch stack; KMS + Macie + VPC endpoints engineered; CUR cost dashboard with break-even calculations; DEA-C01 cert passed.
