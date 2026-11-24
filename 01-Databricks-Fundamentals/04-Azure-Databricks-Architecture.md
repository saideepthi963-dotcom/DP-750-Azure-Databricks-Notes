# Azure Databricks Architecture

## 1. Overview

Azure Databricks separates platform management from data processing using different architectural planes.

The main components are:

1. **Control Plane** — Manages the Databricks workspace and user interactions.
2. **Classic Compute Plane** — Runs data processing workloads on compute resources in the customer's Azure environment.
3. **Serverless Compute Plane** — Runs workloads on infrastructure managed by Databricks.

The compute architecture depends on whether we use **classic compute** or **serverless compute**.

## 2. Control Plane

The **Control Plane** is managed by Databricks.

It provides the interface and services used to interact with the Databricks platform.

It includes:

- Databricks web application and workspace interface
- Notebooks and code management
- Workspace configuration and management
- Services for coordinating workloads

**Important:** The control plane manages operations; it is not where Spark data processing normally runs.

## 3. Classic Compute Plane (Without Serverless)

In the classic architecture, Databricks provisions and manages compute resources within the customer's Azure environment.

### Components

- **Databricks Control Plane:** Provides the user interface and management services.
- **Compute Cluster:** Contains the driver and worker VMs that execute processing tasks.
- **Azure Data Lake Storage (ADLS Gen2):** Stores the actual data.

### How It Works

1. A user writes and runs code in a Databricks notebook.
2. The control plane coordinates execution on a compute cluster.
3. The cluster reads data from Azure storage.
4. Apache Spark processes the data.
5. Results become available to the user.

**Key concept:** In classic compute, the VMs run in the customer's Azure environment, while Databricks manages their lifecycle.

## 4. Serverless Compute Plane

With **serverless compute**, Databricks manages the underlying compute infrastructure in a Databricks-managed compute plane.

Users do not need to manually provision or manage clusters for supported serverless workloads.

### How It Works

1. A user submits a workload through Databricks.
2. Databricks allocates serverless computing resources.
3. Serverless compute accesses the required data in Azure storage.
4. The workload executes and returns its results.

**Important:** Serverless does not mean there are no servers. It means Databricks manages the servers and computing resources.

The instructor also introduces default storage associated with the serverless architecture. Databricks-managed storage can be used for supported workloads, while external Azure storage remains an option.

## 5. Classic Compute vs. Serverless Compute

| Feature | Classic Compute | Serverless Compute |
|---|---|---|
| Compute infrastructure | Runs in customer's Azure environment | Runs in Databricks-managed environment |
| Infrastructure management | Databricks provisions and manages VMs; users configure compute | Databricks manages underlying resources |
| Cluster configuration | Users select compute settings | Less infrastructure configuration required |
| Data processing | Spark and supported workloads | Supported serverless workloads |
| Data storage | Can access ADLS Gen2 | Can also access ADLS Gen2 |
| Scaling | Manual or configured autoscaling | Databricks-managed scaling |

Both architectures are supported. Serverless does not completely replace classic compute.

## 6. Compute and Storage Separation

Azure Databricks separates the resources used for processing from the location where data is stored.

**Compute** = CPU, RAM, and processing resources.

**Storage** = Where datasets and table files are persisted.

For example:

- **ADLS Gen2** stores Delta table data.
- **Databricks compute** processes the data.
- **Control plane** manages and coordinates the environment.

This separation enables independent scaling of compute and storage.

## DP-750 Key Takeaways

- The **Control Plane** is managed by Databricks and provides workspace management services.
- The **Classic Compute Plane** runs processing resources in the customer's Azure environment.
- The **Serverless Compute Plane** runs processing resources in a Databricks-managed environment.
- Both classic and serverless compute can access data in Azure storage.
- Serverless reduces the need for manual infrastructure management.
- Compute and storage are logically separated.
- Classic and serverless compute architectures coexist.

**Remember: Control Plane = Manage | Compute Plane = Process | Storage = Store Data.**