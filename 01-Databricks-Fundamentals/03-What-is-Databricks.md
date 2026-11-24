# What Is Databricks?

## 1. How Databricks Started

Databricks originated from the team behind **Apache Spark**.

**Apache Spark** is a distributed data processing framework that processes large datasets across multiple machines, primarily using in-memory computation.

Although Spark is powerful, managing it independently introduces challenges:

- Setting up and managing Spark clusters
- Scaling computing resources
- Optimizing infrastructure costs
- Maintaining the underlying infrastructure

**Databricks was initially created as a managed platform for Apache Spark**, simplifying cluster management, infrastructure provisioning, and scaling.

## 2. What Is Databricks Today?

Databricks has evolved from a managed Spark platform into a **unified data and AI platform**.

It provides capabilities for multiple data-related workloads within a single environment.

| Capability | Purpose |
|---|---|
| Data Engineering | Build and manage data pipelines |
| Data Analytics | Analyze datasets and generate insights |
| Data Warehousing | Run SQL workloads using SQL warehouses |
| Machine Learning | Develop and manage ML models using tools such as MLflow |
| AI and Applications | Build AI applications and chatbots |
| Dashboards | Visualize data and create reports |
| Real-Time Analytics | Process and analyze streaming data |
| Databricks Jobs | Schedule and orchestrate workflows |
| AI Functions | Perform AI-powered operations such as extracting information from documents |

**Key concept:** Databricks is no longer just a platform for running Apache Spark. It supports end-to-end data engineering, analytics, and AI workloads.

## 3. Databricks Is Multi-Cloud

Databricks is available on three major cloud platforms:

- **Microsoft Azure** — Azure Databricks
- **Amazon Web Services (AWS)** — Databricks on AWS
- **Google Cloud Platform (GCP)** — Databricks on Google Cloud

In this DP-750 course, we focus on **Azure Databricks**.

## 4. Separation of Compute and Storage

A major architectural concept in Databricks is the separation of **compute** and **storage**.

**Storage layer:** Stores the actual datasets, typically in cloud storage such as Azure Data Lake Storage Gen2 (ADLS Gen2).

**Compute layer:** Uses Databricks processing resources to read, transform, and analyze the data.

In our Azure environment:

- **ADLS Gen2** → Stores data
- **Azure Databricks** → Processes data

This separation allows compute resources to scale independently of storage, improving flexibility and cost management.

## 5. Databricks for Data Engineers

Databricks supports several professional roles, including data engineers, data analysts, data scientists, and machine learning engineers.

For the **DP-750 Data Engineer Associate** learning path, the main focus is:

- Data ingestion and transformation
- Apache Spark and PySpark
- Delta Lake and Lakehouse architecture
- Data pipelines and orchestration
- Databricks SQL
- Data governance, security, and optimization

## DP-750 Key Takeaways

- **Apache Spark** is a distributed data processing engine.
- **Databricks** started as a managed Apache Spark platform.
- Today, Databricks is a unified data and AI platform.
- Databricks supports Azure, AWS, and GCP.
- Compute and storage can scale independently.
- Azure Databricks commonly processes data stored in ADLS Gen2.
- Databricks Jobs provides workflow scheduling and orchestration.

**Remember: Apache Spark is the processing engine; Databricks is the platform that manages Spark and provides additional data engineering, analytics, and AI capabilities.**