# AWS Healthcare Big Data & MLOps Platform

![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazon-aws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

An event-driven, cloud-native healthcare data platform built on AWS to process raw streaming IoT device telemetry and clinical batch records into analytics-ready datasets, interactive QuickSight dashboards, and SageMaker anomaly detection models.

---

##  System Architecture

![AWS Healthcare Big Data Architecture](./images/architecture-diagram.jpg)

### Pipeline Workflow
1. **Ingestion:** Clinical batch CSV/JSON records are validated via **AWS Lambda**, while IoT device telemetry streams directly via **IoT Core / Kinesis Firehose** into Amazon S3 raw storage.
2. **Event Automation:** Uploads trigger `S3 ObjectCreated` events, routed by **Amazon EventBridge** to launch orchestration state machines.
3. **Orchestration & Transformation:** **AWS Step Functions** orchestrates sequential **AWS Glue Crawlers** (for schema discovery in Glue Data Catalog) and **AWS Glue ETL Jobs** (Bronze $\rightarrow$ Silver $\rightarrow$ Gold transformations).
4. **Analytics & BI:** Curated Gold datasets are queried via **Amazon Athena** and visualized through **Amazon QuickSight** dashboards.
5. **MLOps & Anomaly Detection:** Features are consumed by **Amazon SageMaker** to detect patient vital anomalies, writing inference results back to S3.
6. **Security & Governance:** Isolated within a private **Amazon VPC** with cross-region backup replication and centralized **CloudWatch** execution monitoring.

---

##  System Implementation & Visual Proof

### 1. S3 Medallion Data Lake Layout (`health-analytics-demo`)
*Organized into clear Bronze, Silver, Gold, and ML Result partitions with cross-region backups.*
![S3 Data Lake Layout](./images/s3-bucket-structure.png)

---

### 2. AWS Step Functions Execution Graph (`healthcare-etl-orchestration`)
*Automated execution sequence handling schema crawlers, data transformation jobs, and quality checks.*
![Step Functions Execution Workflow](./images/step-functions-workflow.jpg)

---

### 3. SageMaker Anomaly Detection Model
*ML model analyzing Systolic BP and Heart Rate metrics to flag patient anomalies in real time.*
![SageMaker Anomaly Detection Notebook](./images/sagemaker-anomaly-detection.png)

---

### 4. Amazon QuickSight Clinical Dashboard
*Real-time clinical insights visualizing average patient vitals, diagnosis distributions, and alert metrics.*
![QuickSight Clinical Insights Dashboard](./images/quicksight-dashboard.png)

---

##  Technology Stack

| Domain | AWS Services & Technologies |
| :--- | :--- |
| **Data Storage & Lake** | Amazon S3 (Bronze / Silver / Gold Medallion Architecture), Cross-Region Replication (CRR) |
| **Ingestion & Automation**| AWS Lambda, Amazon EventBridge, AWS IoT Core / Kinesis Firehose |
| **ETL & Orchestration** | AWS Step Functions, AWS Glue (Crawlers, Data Catalog, PySpark ETL Jobs) |
| **Analytics & ML** | Amazon Athena, Amazon QuickSight, Amazon SageMaker Notebooks |
| **Networking & Monitoring**| AWS VPC (`10.0.0.0/16`), Amazon CloudWatch |

---

##  Key Results & Architectural Impact

* **Event-Driven Automation:** Replaced manual batch triggers with automated EventBridge-to-Step-Functions orchestration.
* **Storage Optimization:** Converted raw, unorganized IoT JSON files into partitioned, compressed Parquet formats (Silver/Gold) for fast query performance in Athena.
* **End-to-End Governance:** Isolated ingestion and compute components inside a dedicated private VPC with full pipeline traceability via CloudWatch logs.
