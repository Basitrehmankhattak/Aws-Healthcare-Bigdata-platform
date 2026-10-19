# AWS Medallion Healthcare Big Data & MLOps Platform

![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazon-aws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

An event-driven, cloud-native data architecture engineered on AWS to ingest, transform, and analyze real-time IoT healthcare telemetry data within an isolated, enterprise-grade VPC.

---

##  System Architecture

```mermaid
graph LR
    A[IoT Telemetry / Devices] -->|Event-Driven Ingestion| B[(AWS S3: Bronze Raw)]
    B --> C[AWS Step Functions Workflow]
    C -->|Trigger ETL Jobs| D[AWS Glue Clean & Model]
    D --> E[(AWS S3: Silver / Gold)]
    E --> F[Amazon Athena Query Engine]
    E --> G[Amazon SageMaker ML Models]
    F --> H[Amazon QuickSight Dashboards]
