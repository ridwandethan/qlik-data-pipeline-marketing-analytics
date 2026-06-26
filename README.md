# 📊 Advanced Qlik Sense Data Pipeline for Multi-Source Marketing Analytics

This repository contains an end-to-end data integration and transformation pipeline designed in **Qlik Scripting Language (.qvs)**. The pipeline architecture is engineered specifically for high-volume health-tech subscription metrics—focusing on raw ingestion performance, complex JSON flattening, data governance, and strategic business logic.

---

## 📺 Live Interactive Project Walkthrough
> **Recruiter Note:** Since enterprise Qlik Sense Cloud instances are secured behind private tenant firewalls, I have recorded a **live interactive product demo** showcasing the script execution, the associative data model viewer, and how the metrics drive business decisions.
>
> 📥 **[WATCH THE LIVE INTERACTIVE VIDEO DEMO HERE](https://loom.com)** *(Replace this with your 2-3 min Loom or YouTube video link)*

---

## 🚀 Architectural Design (3-Layer QVD Framework)
To meet Nutrameg's standard for a highly scalable data stack, the pipeline decouples data stages to minimize source system overhead:
1. **Extract Layer:** High-frequency data ingestion from PostgreSQL (Production Orders) and Google BigQuery (GA4 Clickstream) converted instantly into optimized, native `.qvd` files.
2. **Transform Layer:** Handles asynchronous structural data cleaning, advanced string manipulation, and standardizing messy data coming from third-party Marketing APIs (Meta & Google Ads).
3. **Presentation Layer:** Establishes a completely clean, optimized associative data model optimized for the Qlik In-Memory engine.

---

## 🛠️ Key Data Engineering Challenges Solved (Included in `.qvs` file)

### 1. Hardest Part: JSON Flattening & Dynamic Mapping
Marketing APIs output highly nested, messy string structures. This architecture bypasses slow row-by-row relational parsers by utilizing optimized hash-lookups in memory:
* **`MAPPING LOAD` + `ApplyMap`:** Dynamically standardizes unstructured geographical data (e.g., converting 'ID', 'Indo', 'IDN' to a unified 'Indonesia').
* **`TextBetween`:** Flattens nested JSON payloads directly inside the Qlik RAM cache for maximum script velocity.

### 2. Performance Tracking: Real-Time Incremental Load
To handle massive e-commerce orders without bottlenecking the production PostgreSQL database, the script implements an optimized **Insert & Update (Upsert)** incremental loading scheme using historical `.qvd` deltas and `NOT Exists()` deduplication checks.

### 3. Data Governance: Preventing Synthetic Keys
When blending production DB schemas with GA4 events, conflicting column namings like `id` or `status` are isolated safely using the **`QUALIFY`** and **`UNQUALIFY`** states, ensuring a perfect **Star Schema** data model free from circular references.

---

## 📈 Executive Decision-Making Metrics Delivered
This pipeline feeds key executive layers with ready-to-use business dimensions:
* **Customer Lifetime Value (LTV) Segmentation:** Automatically calculates dynamic aggregation and segments users (`VIP Subscription Tier`, `Loyal Health Subscriber`, `Standard Tier`) right at the memory-load stage to drive automated retention marketing campaigns.

---
## 💻 Tech Stack Leveraged
* **BI Tooling:** Qlik Sense Cloud (SaaS Architecture)
* **Data Sources:** PostgreSQL, Google BigQuery, Google Analytics 4 (GA4), Meta Ads API
* **Language:** Qlik Data Scripting Language (QVS)
