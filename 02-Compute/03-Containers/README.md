# Azure Containers

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure container services, including Azure Container Instances (ACI), Azure Kubernetes Service (AKS), Virtual Machine Scale Sets (VMSS), container storage, scaling, monitoring, and Microsoft's recommended operational best practices.

---

## Overview

Azure provides several services for running containerized workloads, each designed for different levels of complexity, scalability, and operational control.

From simple single-container deployments to fully managed Kubernetes clusters, Azure enables organizations to deploy modern cloud-native applications without managing the underlying infrastructure.

This section explains the Azure container ecosystem and helps determine which service is best suited for each workload.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure container services.
- Differentiate Azure Container Instances (ACI), Azure Kubernetes Service (AKS), and Virtual Machine Scale Sets (VMSS).
- Understand Container Groups.
- Understand container orchestration.
- Configure persistent storage for containers.
- Apply Microsoft's recommended operational best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Container fundamentals, Azure Container Instances (ACI), Azure Kubernetes Service (AKS), Virtual Machine Scale Sets (VMSS), Container Groups, persistent storage, and scaling concepts. |
| **02 - Best Practices** | Security, monitoring, autoscaling, persistent storage, Azure Container Registry (ACR), cost optimization, and operational recommendations. |

---

## Azure Container Architecture

```text
                    Azure Containers
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
Azure Container      Azure Kubernetes    Virtual Machine
Instances (ACI)      Service (AKS)       Scale Sets (VMSS)
        │                  │                  │
        ▼                  ▼                  ▼
Container Groups     Kubernetes Pods     Worker Nodes
                           │
                           ▼
                 Azure Container Registry
                           │
                           ▼
                  Azure Files / Azure Disks
```

---

## Skills Covered

This section includes:

- Containers
- Azure Container Instances (ACI)
- Container Groups
- Azure Kubernetes Service (AKS)
- Control Plane
- Worker Nodes
- Virtual Machine Scale Sets (VMSS)
- Azure Container Registry (ACR)
- Persistent Storage
- Azure Files
- Azure Disks
- Autoscaling
- Container Monitoring

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Deploy Azure Container Instances.
- Understand Azure Kubernetes Service architecture.
- Differentiate ACI, AKS, and VM Scale Sets.
- Configure container storage.
- Implement autoscaling.
- Monitor container workloads.
- Apply container deployment best practices.

---

## Key Takeaways

- Azure Container Instances provide fast, serverless execution for individual container workloads.
- Azure Kubernetes Service delivers managed Kubernetes orchestration for production-scale applications.
- Virtual Machine Scale Sets provide the scalable infrastructure used by AKS worker nodes.
- Persistent data should be stored outside containers using Azure storage services.
- Choosing the appropriate Azure container platform improves scalability, resilience, operational efficiency, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Container Instances documentation | https://learn.microsoft.com/azure/container-instances/ |
| Azure Kubernetes Service documentation | https://learn.microsoft.com/azure/aks/ |
| Virtual Machine Scale Sets documentation | https://learn.microsoft.com/azure/virtual-machine-scale-sets/ |
| Azure Container Registry documentation | https://learn.microsoft.com/azure/container-registry/ |
| Azure Monitor for containers | https://learn.microsoft.com/azure/azure-monitor/containers/ |
| Azure Container Storage | https://learn.microsoft.com/azure/storage/container-storage/ |
| Microsoft Learn – Run container images in Azure Container Instances | https://learn.microsoft.com/training/modules/run-docker-with-azure-container-instances/ |
| Microsoft Learn – Introduction to Azure Kubernetes Service | https://learn.microsoft.com/training/modules/intro-to-azure-kubernetes-service/ |
