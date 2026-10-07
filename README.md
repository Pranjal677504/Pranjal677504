<h1 align="center">Pranjal Prajapati</h1>

<p align="center">
  <strong>Data Engineer · Data Platforms · Distributed Systems</strong><br/>
  Designing production-grade data systems for reliability, scale, and real-world impact.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/pranjal-prajapati-cs/">LinkedIn</a>
  ·
  <a href="mailto:pranjalprajapati580@gmail.com">Email</a>
  ·
  <a href="https://leetcode.com/u/PranjalPrajapati/">LeetCode</a>
</p>

---

## Engineering Profile

I build data platforms for the moment something goes wrong: a source that re-sends yesterday's records, a schema that drifts overnight, a job that dies halfway through a rebuild. Pipelines earn trust in those moments, not on the happy path, so I design for them first.

In practice, that means watermarked incremental ingestion with an overlap window for late source corrections, and idempotent merges keyed on source IDs so any run can be replayed safely. Silver and Gold layers rebuild transactionally and roll back on failure, and reconciliation gates stop a bad load before a consumer ever sees it. Every row traces back through run-level lineage to the batch that produced it, and every run leaves metrics and failure history behind. My Chicago pipeline applies all of this to 1.57M+ records on a daily schedule. My Databricks lakehouse carries the same discipline into multi-entity consolidation with Delta Lake, SCD-oriented dimensions, and incremental MERGE.

What I care about most is judgment about the data itself. Real sources are inconsistent in ways no schema declares: records that look duplicated but are legitimate, sentinel values posing as coordinates, timestamps that are artifacts of the source. I profile before I clean, trace anomalies to a root cause, and encode every decision as an executable check, so data quality is a property of the system rather than something I verify by eye.

I'm deepening my work in distributed systems, Apache Spark, cloud data platforms, and system design, aiming at platforms that hold up in operation, not just in a demo.

## Selected Data Engineering Work

### [Chicago Crime Data Pipeline](https://github.com/Pranjal677504/chicago_crimes_data_pipeline)

[![Daily Pipeline](https://github.com/Pranjal677504/chicago_crimes_data_pipeline/actions/workflows/daily_pipeline.yml/badge.svg)](https://github.com/Pranjal677504/chicago_crimes_data_pipeline/actions/workflows/daily_pipeline.yml)

Production-style analytical pipeline processing **1.57M+ records** from the Chicago Data Portal.

- Incremental API ingestion using watermarks and an overlap window for late source corrections
- Idempotent merge design with source-ID deduplication
- Bronze → Silver → Gold modeling in DuckDB / MotherDuck
- Transactional Silver and Gold rebuilds with rollback on failure
- Automated reconciliation and data-quality gates
- Run IDs, batch lineage, row metrics, watermarks, and failure history
- Daily GitHub Actions orchestration and gated dashboard deployment

**Stack:** Python · SQL · DuckDB · MotherDuck · GitHub Actions · GitHub Pages

**Live analytics:** [pranjal677504.github.io/chicago_crimes_data_pipeline](https://pranjal677504.github.io/chicago_crimes_data_pipeline/)

---

### [FMCG Databricks Lakehouse Pipeline](https://github.com/Pranjal677504/fmcg-databricks-lakehouse-pipeline)

Enterprise-style lakehouse consolidation project for integrating parent and subsidiary data into a governed analytical platform.

- Medallion Architecture across Bronze, Silver, and Gold layers
- Databricks + PySpark processing on Delta Lake
- AWS S3 landing-zone integration
- Schema standardization, deduplication, master-data conformance, and integrity checks
- SCD-oriented dimension processing and incremental `MERGE` patterns
- Star-schema / analytical Gold modeling
- Unity Catalog-oriented namespace and governance design
- Workflow dependency modeling for orchestrated execution

**Stack:** Databricks · Apache Spark / PySpark · Delta Lake · AWS S3 · SQL · Python

---

### [Pizza Sales SQL Analytics](https://github.com/Pranjal677504/Pizza-Sales-Analysis)

Relational SQL project focused on schema design, multi-table joins, analytical queries, and business-facing metrics.

- Multi-table relational modeling and joins
- Aggregations and time-based analysis
- Subqueries and derived tables
- Window functions and partitioned ranking
- Revenue, product, and operational analytics

**Stack:** SQL · MySQL

## Data Engineering Focus

| Area | What I work on |
| --- | --- |
| **Ingestion** | Batch and API ingestion, incremental loads, watermarks, late-arriving updates |
| **Transformation** | SQL/Python transformations, Medallion Architecture, reusable processing layers |
| **Modeling** | Bronze/Silver/Gold, dimensional modeling, fact & dimension design, analytical tables |
| **Reliability** | Idempotency, deduplication, reconciliation, quality gates, rollback-safe processing |
| **Operations** | Scheduling, run metadata, logging, lineage, failure handling, recovery procedures |
| **Platforms** | DuckDB, MotherDuck, Databricks, Spark, Delta Lake, AWS-oriented lakehouse workflows |
| **Delivery** | Curated analytics datasets, semantic layers, dashboards, documented operational interfaces |

## Technology

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/SQL-336791?style=flat-square&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/C++-00599C?style=flat-square&logo=c%2B%2B&logoColor=white" />
  <img src="https://img.shields.io/badge/Apache%20Spark-E25A1C?style=flat-square&logo=apachespark&logoColor=white" />
  <img src="https://img.shields.io/badge/Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white" />
  <img src="https://img.shields.io/badge/Delta%20Lake-00ADD8?style=flat-square" />
  <img src="https://img.shields.io/badge/DuckDB-FFF000?style=flat-square&logo=duckdb&logoColor=black" />
  <img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white" />
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white" />
  <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white" />
  <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black" />
</p>

## How I Approach Data Systems

- **Correctness before convenience:** validate assumptions and reconcile data between layers.
- **Safe re-runs:** design pipelines to be idempotent and recoverable.
- **Incremental by default:** avoid unnecessary full reloads when source semantics allow reliable change processing.
- **Observable operations:** record run state, lineage, watermarks, row counts, and failure context.
- **Explicit data quality:** turn expectations into executable checks rather than informal assumptions.
- **Clear boundaries:** separate ingestion, transformation, validation, serving, and operational concerns.
- **Security-conscious delivery:** keep credentials out of code and minimize unnecessary exposure of raw data.
- **Documentation as part of engineering:** architecture, data dictionaries, runbooks, and recovery procedures belong with the system.

## Current Focus

I am currently prioritizing **data engineering, distributed systems, SQL, Spark, cloud architecture, and DSA** while continuing to build deeper end-to-end systems that are reliable enough to operate, not just demonstrate.

---

<p align="center">
  <em>Interested in data platforms, reliable pipelines, distributed systems, and engineering problems where correctness matters.</em>
</p>
