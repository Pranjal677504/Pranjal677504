<h1 align="center">Pranjal Prajapati</h1>

<p align="center">
  <strong>Data Engineer · Lakehouse Platforms · Reliable Data Systems</strong><br/>
  I engineer data platforms that are reliable, resilient, and built for scale.
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/pranjal-prajapati-cs/">LinkedIn</a>
  ·
  <a href="mailto:pranjalprajapati580@gmail.com">Email</a>
  ·
  <a href="https://leetcode.com/u/PranjalPrajapati/">LeetCode</a>
</p>

---

## About

I build data platforms for the moments when things go wrong: when a source republishes records, a schema drifts unexpectedly, or a pipeline fails midway through a rebuild. Reliable systems earn trust in those situations, so I design for correctness, recovery, and observability from the start.

That means watermarked incremental ingestion, overlap windows for late corrections, idempotent merges, transactional Silver and Gold layers, reconciliation gates, and run-level lineage. My Chicago pipeline applies these principles to more than 1.57 million records on a daily schedule, while my Databricks lakehouse extends them to multi-entity consolidation using Delta Lake, incremental `MERGE`, and SCD-oriented dimensions.

What matters most to me is understanding the data itself. Real-world sources contain legitimate duplicates, misleading sentinel values, inconsistent timestamps, and undocumented anomalies. I profile before I clean, investigate root causes, and encode important assumptions as executable checks so that data quality becomes a property of the system rather than a manual process.

I’m continuing to deepen my expertise in distributed systems, Apache Spark, cloud data platforms, and system design, with the goal of building data infrastructure that remains reliable in production—not just impressive in a demo.

## Domain Map

```text
Pranjal Prajapati
│
├── Data Engineering
│   ├── Data Ingestion       incremental loads · watermarks · APIs · batch pipelines · late-arriving data
│   ├── Data Modeling        Medallion architecture · dimensional modeling · star schemas · SCDs
│   ├── Reliability          idempotency · deduplication · reconciliation · transactional processing
│   ├── Data Platforms       Databricks · PySpark · Delta Lake · DuckDB · MotherDuck · AWS S3
│   └── Data Operations      quality gates · lineage · observability · orchestration · CI/CD
│
├── Machine Learning
│   ├── ML Pipelines         preprocessing · feature engineering · training workflows · reproducible experiments
│   ├── Model Development    supervised learning · model selection · validation · evaluation
│   └── Data for ML          dataset construction · leakage prevention · feature quality · experiment-ready data
│
├── Applied AI
│   ├── AI Systems           LLM-enabled workflows · retrieval · structured outputs · evaluation
│   └── AI Data Layer        dataset quality · provenance · lineage · evaluation datasets · feedback loops
│
├── Agentic AI
│   ├── Agent Systems        tool-using agents · multi-step workflows · MCP integrations · scoped execution
│   ├── Agent Safety         permission boundaries · branch isolation · controlled tool access
│   └── Evaluation           benchmarks · adversarial testing · red-teaming · merge and deployment gates
│
└── Systems Engineering
    ├── System Design        distributed systems · service boundaries · fault tolerance · consistency
    ├── Data Architecture    scalable data platforms · storage/compute design · batch & streaming architecture
    └── Problem Solving      DSA · complexity analysis · performance · scalability trade-offs
```

*`hands-on`: shipped and running in my repos · `building` / `deepening`: active work, not yet shipped · `exploring`: next direction.*

---

## Selected Work

### [Chicago Crime Data Pipeline](https://github.com/Pranjal677504/chicago_crimes_data_pipeline)

[![Daily Pipeline](https://github.com/Pranjal677504/chicago_crimes_data_pipeline/actions/workflows/daily_pipeline.yml/badge.svg)](https://github.com/Pranjal677504/chicago_crimes_data_pipeline/actions/workflows/daily_pipeline.yml)

A production-style analytical pipeline over **1.57M+ records** from the Chicago Data Portal, running daily without intervention.

- **Incremental ingestion:** watermarks plus an overlap window, so late source corrections are picked up
- **Idempotent merges:** source-ID deduplication makes every re-run safe
- **Medallion modeling:** Bronze → Silver → Gold in DuckDB / MotherDuck
- **Transactional rebuilds:** Silver and Gold roll back on failure, so consumers never see half-built tables
- **Trust layer:** reconciliation between layers and data-quality gates that block bad data from shipping
- **Observability:** run IDs, batch lineage, row metrics, watermarks, and failure history
- **Delivery:** daily GitHub Actions orchestration with a gated dashboard deployment

**Stack:** Python · SQL · DuckDB · MotherDuck · GitHub Actions · GitHub Pages
**Live analytics:** [pranjal677504.github.io/chicago_crimes_data_pipeline](https://pranjal677504.github.io/chicago_crimes_data_pipeline/)

---

### [FMCG Databricks Lakehouse Pipeline](https://github.com/Pranjal677504/fmcg-databricks-lakehouse-pipeline)

An enterprise-style lakehouse that consolidates parent and subsidiary company data into one governed analytical platform.

- Medallion architecture on **Databricks + PySpark + Delta Lake**, with an AWS S3 landing zone
- Schema standardization, deduplication, master-data conformance, and integrity checks
- SCD-oriented dimension handling and incremental `MERGE` patterns
- Star-schema Gold layer for analytics
- Unity Catalog-oriented namespace and governance design
- Workflow dependency modeling for orchestrated execution

**Stack:** Databricks · Apache Spark / PySpark · Delta Lake · AWS S3 · SQL · Python

---

## Engineering Judgment

Profiling the initial ~1.55M-row load of the Chicago pipeline surfaced the problems that never appear in tutorials. Here is how I handled them, and why.

| What I found | What I did | Why |
| --- | --- | --- |
| `case_number` repeats across records; 40 groups (82 rows, ~0.005%) matched on every business field and differed only by ID | Kept every row | `id` is the true primary key and `case_number` is a legitimate one-to-many grouping key. Nothing in the source marks these as errors, so deduplicating would be a guess |
| Two rows with zeroed coordinates and an identical out-of-city lat/long | Traced both to a single geocode failure and nulled their coordinates by explicit ID | An ID-scoped fix can't accidentally null legitimate future edge cases, which a boundary rule could |
| ~22,440 rows (~1.4%) with no geospatial data | Left as `NULL`, neither imputed nor dropped | Missing is a fact about the source. Only provably invalid values, such as sentinel zeros, get corrected |
| Timestamps landing at exactly midnight | Added a `time_is_estimated` flag | A source artifact is labeled, so downstream analysis can exclude it instead of trusting it |
| `CRIM SEXUAL ASSAULT` and `CRIMINAL SEXUAL ASSAULT` coexisting | Normalized in Silver | Category drift would otherwise split trends in the Gold marts |

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

## How I Think About Data Systems

- **Correctness before convenience.** Reconcile every layer against the one before it.
- **Safe to re-run.** If a job can't be replayed, it isn't finished.
- **Incremental by default.** Full reloads are a fallback, not a design.
- **Expectations become code.** Quality rules are executable checks, not tribal knowledge.
- **Observable by design.** Run state, lineage, row counts, and failure context are recorded, not reconstructed after an incident.
- **Docs ship with the system.** Architecture, data dictionaries, and runbooks live next to the code.

## Currently

Deepening **distributed systems, Apache Spark, cloud data platforms, system design, and DSA**, while building data systems reliable enough to operate, not just demonstrate.

---

<p align="center">
  <em>Interested in reliable pipelines, lakehouse architecture, and engineering problems where correctness matters.</em>
</p>
