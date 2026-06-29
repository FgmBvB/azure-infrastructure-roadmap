# Azure Containers Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure's container compute services, explains their architecture, deployment models, scaling capabilities, and helps identify the appropriate service for different workloads.

---

## Overview

Containers package an application together with its runtime, libraries, and dependencies into a lightweight, portable unit that can run consistently across different environments.

Azure provides several managed container services designed for different operational requirements, ranging from simple container execution to fully orchestrated Kubernetes clusters.

Understanding when to use each service is an important objective of the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Understand container technology.
- Differentiate Azure Container Instances (ACI), Azure Kubernetes Service (AKS), and Virtual Machine Scale Sets (VMSS).
- Understand container orchestration.
- Select the appropriate Azure compute service.
- Identify common enterprise deployment scenarios.

---

## Azure Container Services

```text
                   Azure Containers
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
Azure Container      Azure Kubernetes   Virtual Machine
Instances (ACI)      Service (AKS)      Scale Sets (VMSS)
        │                 │                 │
        ▼                 ▼                 ▼
 Single Containers   Container Cluster   VM-based Scaling
```

---

## Containers

A container packages:

- Application code
- Runtime
- Libraries
- Dependencies
- Configuration

Unlike Virtual Machines, containers share the host operating system kernel, making them lightweight and fast to start.

---

## Azure Container Instances (ACI)

Azure Container Instances provide the fastest way to run containers in Azure.

Characteristics:

- No infrastructure management
- No Kubernetes cluster required
- Fast deployment
- Per-second billing
- Supports Linux and Windows containers

Typical workloads include:

- Batch processing
- Scheduled jobs
- Development environments
- Automation tasks

---

## Azure Kubernetes Service (AKS)

Azure Kubernetes Service (AKS) is Azure's managed Kubernetes platform.

Microsoft manages the Kubernetes control plane while customers manage:

- Node pools
- Applications
- Networking
- Storage
- Scaling policies

AKS is designed for large-scale containerized applications.

---

## Virtual Machine Scale Sets (VMSS)

Virtual Machine Scale Sets allow administrators to deploy and manage large groups of identical Virtual Machines.

Although VMSS is not a container service itself, it provides the underlying compute platform used by Azure Kubernetes Service worker nodes.

VMSS supports:

- Automatic scaling
- Load balancing
- High availability
- Rolling upgrades

---

## Service Comparison

| Service | Best For |
|----------|----------|
| **Azure Container Instances** | Single containers and short-lived workloads |
| **Azure Kubernetes Service** | Large-scale orchestrated container applications |
| **Virtual Machine Scale Sets** | Automatically scaling groups of Virtual Machines |

---

## Scaling

Azure container services provide different scaling models.

| Service | Scaling |
|----------|----------|
| **ACI** | Manual deployment of container instances |
| **AKS** | Automatic or manual scaling of node pools and workloads |
| **VMSS** | Automatic scaling based on metrics or schedules |

---

## Enterprise Scenario

A software company hosts its production microservices on Azure Kubernetes Service.

Background image-processing jobs execute in Azure Container Instances when demand increases.

The AKS worker nodes run on Virtual Machine Scale Sets, allowing automatic scaling during periods of high traffic.

---

## Best Practices

- Use Azure Container Instances for simple container workloads.
- Use AKS for production container orchestration.
- Design containers to be stateless whenever possible.
- Store container images in Azure Container Registry.
- Monitor container workloads using Azure Monitor.
- Keep container images updated and secure.

---

## Common Pitfalls

- Deploying complex production applications in ACI.
- Choosing AKS for very small workloads.
- Treating containers as Virtual Machines.
- Storing persistent application data inside containers.
- Ignoring monitoring and image updates.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Containers
> - Azure Container Instances (ACI)
> - Azure Kubernetes Service (AKS)
> - Virtual Machine Scale Sets (VMSS)
> - Container orchestration
> - Scaling
> - Common deployment scenarios

---

## Key Takeaways

- Containers provide lightweight and portable application deployment.
- Azure Container Instances offer simple, serverless container execution.
- Azure Kubernetes Service provides managed Kubernetes orchestration.
- Virtual Machine Scale Sets deliver scalable infrastructure and underpin AKS worker nodes.
- Choosing the appropriate Azure compute service improves scalability, availability, and operational efficiency.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Container Instances documentation | https://learn.microsoft.com/azure/container-instances/ |
| Azure Kubernetes Service documentation | https://learn.microsoft.com/azure/aks/ |
| Virtual Machine Scale Sets documentation | https://learn.microsoft.com/azure/virtual-machine-scale-sets/ |
| Azure Container Registry documentation | https://learn.microsoft.com/azure/container-registry/ |
| Azure Monitor for containers | https://learn.microsoft.com/azure/azure-monitor/containers/ |
| Microsoft Learn – Run container images in Azure Container Instances | https://learn.microsoft.com/training/modules/run-docker-with-azure-container-instances/ |
| Microsoft Learn – Introduction to Azure Kubernetes Service | https://learn.microsoft.com/training/modules/intro-to-azure-kubernetes-service/ |
