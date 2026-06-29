# Azure Compute

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure compute services, including Virtual Machines, Azure App Service, Azure Functions, Azure Container Instances (ACI), Azure Kubernetes Service (AKS), and Virtual Machine Scale Sets (VMSS). It also introduces Microsoft's recommended practices for designing, securing, monitoring, and optimizing compute workloads in Azure.

---

## Overview

Azure Compute provides a range of services that allow organizations to run applications in the cloud with different levels of control, scalability, and operational responsibility.

Azure supports both **Infrastructure as a Service (IaaS)** and **Platform as a Service (PaaS)** models:

- **Infrastructure as a Service (IaaS)** provides full control over the operating system and infrastructure through Virtual Machines.
- **Platform as a Service (PaaS)** abstracts the underlying infrastructure, allowing administrators and developers to focus on applications instead of servers.
- **Container services** provide lightweight, portable, and scalable application hosting for cloud-native workloads.

Selecting the appropriate compute service is a fundamental skill for Azure administrators and one of the core objectives of the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure compute services.
- Differentiate IaaS, PaaS, and container-based compute.
- Select the appropriate compute service for different workloads.
- Understand scalability and high availability concepts.
- Apply Microsoft's operational best practices.
- Optimize performance, security, and cost.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Virtual Machines** | Azure Virtual Machines, administration, availability, storage, monitoring, diagnostics, and operational best practices. |
| **02 - App Service and Functions** | Azure App Service, Azure Functions, App Service Plans, hosting models, scaling, monitoring, and best practices. |
| **03 - Containers** | Azure Container Instances (ACI), Azure Kubernetes Service (AKS), Virtual Machine Scale Sets (VMSS), persistent storage, scaling, and container best practices. |
| **04 - Best Practices** | Compute architecture recommendations, security, monitoring, high availability, governance, performance optimization, and cost management. |

---

## Azure Compute Services

```text
                        Azure Compute
                              │
      ┌───────────────────────┼────────────────────────┐
      │                       │                        │
      ▼                       ▼                        ▼
Infrastructure          Platform as a          Container Services
 as a Service           Service (PaaS)
    (IaaS)                     │                        │
      │                        │                        │
      ▼                        ▼                        ▼
Virtual Machines      App Service / Functions     ACI / AKS / VMSS
```

---

## Skills Covered

This section includes:

- Azure Virtual Machines (VMs)
- VM Administration
- Managed Disks
- Availability Sets
- Availability Zones
- Azure App Service
- Azure Functions
- App Service Plans
- Azure Container Instances (ACI)
- Azure Kubernetes Service (AKS)
- Container Groups
- Virtual Machine Scale Sets (VMSS)
- Azure Monitor
- Azure Backup
- Autoscaling
- High Availability
- Cost Optimization
- Compute Security

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Deploy and manage Azure Virtual Machines.
- Configure VM storage and availability.
- Deploy Azure App Service and Azure Functions.
- Understand Azure container services.
- Configure autoscaling.
- Monitor compute resources.
- Apply security and governance best practices.
- Optimize Azure compute costs.

---

## Key Takeaways

- Azure offers multiple compute services designed for different workload requirements.
- Virtual Machines provide maximum control, while App Service and Azure Functions reduce operational overhead through Platform as a Service (PaaS).
- Azure Container Instances and Azure Kubernetes Service support modern containerized applications with different levels of orchestration.
- High availability, monitoring, security, and autoscaling are essential components of production-ready compute environments.
- Choosing the appropriate compute service improves operational efficiency, scalability, reliability, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Compute documentation | https://learn.microsoft.com/azure/ |
| Azure Virtual Machines documentation | https://learn.microsoft.com/azure/virtual-machines/ |
| Azure App Service documentation | https://learn.microsoft.com/azure/app-service/ |
| Azure Functions documentation | https://learn.microsoft.com/azure/azure-functions/ |
| Azure Container Instances documentation | https://learn.microsoft.com/azure/container-instances/ |
| Azure Kubernetes Service documentation | https://learn.microsoft.com/azure/aks/ |
| Virtual Machine Scale Sets documentation | https://learn.microsoft.com/azure/virtual-machine-scale-sets/ |
| Azure Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Microsoft Learn – Azure Administrator (AZ-104) learning path | https://learn.microsoft.com/training/paths/az-104-administrator-prerequisites/ |
