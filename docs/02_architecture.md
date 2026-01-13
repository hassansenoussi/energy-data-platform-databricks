# 2. Target Technical Architecture

## 2.1 Architecture Overview
The target architecture is designed to support scalable data ingestion, processing, analytics, and future machine learning use cases in an energy company context.

It follows a modern cloud-native data platform pattern based on:
- object storage for durability and scalability
- distributed data processing
- layered data architecture (Medallion)
- separation of compute and storage

---

## 2.2 High-Level Architecture Components

### Data Sources
The platform integrates multiple data sources:
- Smart meter data (simulated time-series data)
- Customer and contract reference data
- External energy pricing data

Data sources are ingested in batch mode to ensure simplicity, reliability, and cost control.

---

### Cloud Storage Layer
**Azure Data Lake Storage Gen2** is used as the central storage layer.

Reasons for this choice:
- high scalability and durability
- cost-efficient storage
- native integration with Databricks
- support for fine-grained access control

The data lake is organized using a logical folder structure aligned with the Medallion Architecture.

---

### Data Processing Layer
**Databricks (Apache Spark)** is used as the data processing engine.

Key motivations:
- ability to process large-scale time-series data
- support for complex transformations and aggregations
- unified environment for data engineering and data science
- native integration with Delta Lake and MLflow

Spark workloads are designed to be idempotent and reusable.

---

### Storage Format
**Delta Lake** is used as the storage format for curated datasets.

Key benefits:
- ACID transactions on data lake storage
- schema enforcement and evolution
- time travel and versioning
- reliable batch processing

Delta tables serve as the foundation for analytical and machine learning workloads.

---

### Analytics and BI Layer
Business-ready datasets from the Gold layer are consumed by:
- Power BI dashboards
- SQL-based analytical queries

This layer enables fast access to KPIs and operational insights without exposing raw data complexity.

---

### Machine Learning Layer
The platform prepares data for future machine learning use cases such as:
- anomaly detection on energy consumption
- consumption forecasting

**MLflow** is used for:
- experiment tracking
- model versioning
- reproducibility

Machine learning workloads are optional and not mandatory for the core platform functionality.

---

## 2.3 Data Flow and Medallion Architecture

The platform follows the Medallion Architecture pattern:

- **Bronze Layer**  
  Raw data ingestion from source systems with minimal transformation.  
  Purpose: traceability and data lineage.

- **Silver Layer**  
  Cleansed, standardized, and enriched data.  
  Purpose: data quality and consistency.

- **Gold Layer**  
  Aggregated, business-oriented datasets.  
  Purpose: analytics, reporting, and BI.

Each layer is physically separated and logically independent.

---

## 2.4 Compute and Cost Considerations
Compute resources are provisioned using Databricks clusters.

Key cost control principles:
- separation of compute and storage
- use of autoscaling clusters
- termination of idle clusters
- optimization of Spark jobs

Cost optimization is considered a core design requirement.

---

## 2.5 Security and Access Management
Security is enforced at multiple levels:
- role-based access control on Databricks
- restricted access to raw (Bronze) data
- controlled exposure of Gold datasets
- auditability of data access

Sensitive data is protected through masking and anonymization strategies.

---

## 2.6 Design Principles
The architecture is guided by the following principles:
- scalability by design
- simplicity over premature optimization
- clear separation of concerns
- reproducibility and traceability
- cost awareness
