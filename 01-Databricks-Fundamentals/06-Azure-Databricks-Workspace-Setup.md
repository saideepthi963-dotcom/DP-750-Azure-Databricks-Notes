# Azure Databricks Workspace Setup

## 1. Azure Resources and Resource Groups

### Azure Resource

A resource is an individual service or manageable component deployed in Azure.

Examples:

- Azure Databricks
- Azure Data Factory
- Azure Storage Account
- Virtual Machines
- Azure Databricks Access Connector

### Azure Resource Group

A resource group is a logical container used to organize and manage related Azure resources.

Resources belonging to the same project can be grouped together for easier management.

```mermaid
flowchart TD
    A["Azure Subscription"] --> B["Resource Group"]
    B --> C["Azure Databricks"]
    B --> D["Storage Account"]
    B --> E["Access Connector"]
    B --> F["Azure Data Factory"]

    style A fill:#0078D4,color:#fff
    style B fill:#D6EAF8,color:#000
```

## 2. Microsoft Entra ID

Microsoft Entra ID, formerly Azure Active Directory, is Microsoft's cloud-based identity and access management service.

It helps manage:

- Users and groups
- Authentication
- Application identities
- Service principals

Entra ID provides identities, while Azure RBAC controls what those identities can access within Azure resources.

## 3. Creating an Azure Resource Group

1. Sign in to the Azure Portal.
2. Search for **Resource groups**.
3. Select **Create**.
4. Select the appropriate subscription.
5. Enter a resource group name.
6. Select a region.
7. Select **Review + create**.
8. Select **Create**.

Example configuration used in the course:

| Setting | Value |
|---|---|
| Resource group | azure-databricks |
| Region | Canada Central |

For production workloads, select regions based on service availability, latency, compliance, and business requirements.

## 4. Creating an Azure Databricks Workspace

Navigate to the resource group and select **Create**.

Search for **Azure Databricks** in Azure Marketplace and select the official service.

### Workspace Configuration

| Setting | Description |
|---|---|
| Subscription | Azure subscription used for deployment and billing |
| Resource group | Container for the Databricks workspace |
| Workspace name | Name of the Databricks workspace |
| Region | Azure region where the workspace is deployed |
| Pricing tier | Trial or Premium, depending on eligibility |
| Workspace type | Serverless or Hybrid |
| Managed resource group | Resource group managed by Azure Databricks |

## 5. Pricing Tier

The instructor demonstrates two pricing options.

### Trial

- Provides a 14-day Premium trial for eligible users.
- Useful for learning and experimentation.
- Can be upgraded after the trial.

### Premium

- Paid pricing tier.
- Provides Premium workspace capabilities.
- Charges depend on resource consumption and workload configuration.

**Cost caution:** A Databricks trial does not necessarily eliminate all Azure infrastructure or storage charges. Monitor Azure costs and stop unused compute.

## 6. Workspace Types

Azure Databricks provides different workspace deployment options.

### Serverless Workspace

- Uses Databricks-managed serverless compute.
- Includes Databricks-managed default storage.
- Requires less infrastructure configuration.

### Hybrid Workspace

- Supports classic compute in the customer's Azure environment.
- Supports serverless compute for eligible workloads.
- Supports customer-managed Azure storage.
- Provides greater flexibility for compute configuration.

The instructor selects **Hybrid** because the course covers both classic and serverless compute.

```mermaid
flowchart TD
    A["Azure Databricks Workspace"] --> B["Serverless Workspace"]
    A --> C["Hybrid Workspace"]

    B --> D["Serverless Compute"]
    B --> E["Default Storage"]

    C --> F["Classic Compute"]
    C --> G["Serverless Compute"]
    C --> H["Azure Storage"]

    style A fill:#FF3621,color:#fff
    style B fill:#D5F5E3,color:#000
    style C fill:#D6EAF8,color:#000
```

## 7. Managed Resource Group

When deploying a hybrid Azure Databricks workspace, Azure Databricks creates a managed resource group for infrastructure resources that it manages.

For example, when a classic compute cluster is created, its underlying Azure VMs and associated infrastructure can be provisioned in the managed resource group.

### Main vs. Managed Resource Group

| Main Resource Group | Managed Resource Group |
|---|---|
| Managed by the customer | Managed by Azure Databricks |
| Contains the workspace resource and other project resources | Contains Databricks-managed infrastructure |
| Used for project resource management | Used for supporting workspace infrastructure |
| Customer manages resources | Avoid manually modifying managed resources |

### Recommended Naming Convention

```text
azure-databricks
azure-databricks-managed
```

Using related names makes it easier to identify which managed resource group belongs to a particular project.

### Resource Group Architecture

```mermaid
flowchart TD
    A["Azure Subscription"] --> B["Main Resource Group"]
    A --> C["Managed Resource Group"]

    B --> D["Azure Databricks Workspace"]
    B --> E["ADLS Gen2 Storage"]

    D -.->|Manages infrastructure| C

    C --> F["Driver VM"]
    C --> G["Worker VMs"]
    C --> H["Supporting Infrastructure"]

    style B fill:#D6EAF8,color:#000
    style C fill:#D5F5E3,color:#000
    style D fill:#FF3621,color:#fff
```

**Important:** Do not manually modify or delete resources inside the managed resource group unless explicitly supported by Databricks.

## 8. Launching the Databricks Workspace

After configuring the workspace:

1. Select **Review + create**.
2. Complete configuration validation.
3. Select **Create**.
4. Wait for deployment to complete.
5. Navigate to the main resource group.
6. Open the Azure Databricks resource.
7. Select **Launch Workspace**.

The Azure Databricks web application opens, providing access to notebooks, compute, pipelines, jobs, and other workspace features.

The web application belongs to the **Control Plane**, while workload execution happens in the **Compute Plane**.

## DP-750 Key Takeaways

- An Azure resource is an individual deployed service or component.
- A resource group logically organizes related Azure resources.
- Microsoft Entra ID manages identities and authentication.
- Hybrid workspaces support classic and serverless compute.
- Serverless workspaces simplify infrastructure configuration.
- The managed resource group contains infrastructure managed by Azure Databricks.
- Avoid manually modifying the managed resource group.
- Launch Workspace opens the Databricks Control Plane interface.

**Remember: Main Resource Group = Project Resources | Managed Resource Group = Databricks-managed Infrastructure.**