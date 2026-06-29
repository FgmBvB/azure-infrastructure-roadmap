# Azure Containers Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for deploying, securing, monitoring, and optimizing Azure container workloads using Azure Container Instances (ACI), Azure Kubernetes Service (AKS), and Virtual Machine Scale Sets (VMSS).

---

## Overview

Azure provides multiple container services designed for different operational requirements.

Selecting the appropriate service and following Microsoft's operational recommendations improves scalability, reliability, security, and cost efficiency.

Containerized workloads should be designed to be lightweight, portable, and resilient to infrastructure changes.

---

## Container Deployment Lifecycle

```text
Design
   │
   ▼
Containerize
   │
   ▼
Deploy
   │
   ▼
Scale
   │
   ▼
Monitor
   │
   ▼
Maintain
```

---

> [!TIP]
> **Key Concepts**
>
> - Choose the appropriate container service.
> - Keep containers stateless whenever possible.
> - Store persistent data outside containers.
> - Monitor workloads continuously.
> - Keep container images updated.

---

## Choosing the Right Service

Microsoft recommends selecting the Azure container service according to workload complexity.

| Workload | Recommended Service |
|----------|---------------------|
| Single container workloads | Azure Container Instances (ACI) |
| Container orchestration | Azure Kubernetes Service (AKS) |
| Scalable VM infrastructure | Virtual Machine Scale Sets (VMSS) |

Avoid deploying Kubernetes clusters for workloads that only require a few standalone containers.

---

## Container Design

Applications should be designed following cloud-native principles.

Recommendations include:

- Keep containers lightweight.
- Run a single primary application per container.
- Design applications to be stateless.
- Externalize configuration whenever possible.
- Use immutable container images.

---

## Persistent Storage

Containers should not store business-critical data locally.

Instead, use external storage such as:

- Azure Files
- Azure Disks
- Azure NetApp Files

Persistent storage allows workloads to survive container recreation, scaling operations, or node replacement.

---

## Security

Microsoft recommends:

- Store container images in Azure Container Registry (ACR).
- Scan images for vulnerabilities.
- Keep base images updated.
- Apply the principle of least privilege.
- Use Microsoft Entra ID where supported.
- Avoid embedding secrets inside container images.
- Store secrets in Azure Key Vault or Kubernetes Secrets (AKS).

---

## Scaling

To improve availability and performance:

- Use AKS autoscaling for production workloads.
- Scale applications horizontally whenever possible.
- Configure appropriate resource requests and limits.
- Monitor utilization before increasing cluster size.

Avoid overprovisioning compute resources.

---

## Monitoring

Monitor container workloads using:

- Azure Monitor
- Container Insights
- Log Analytics
- Application Insights
- Azure Advisor

Monitoring should include:

- CPU utilization
- Memory usage
- Container restarts
- Application availability
- Resource consumption

---

## Cost Optimization

To reduce Azure costs:

- Use ACI only for temporary or burst workloads.
- Scale AKS clusters according to demand.
- Remove unused container images.
- Delete unused container instances.
- Review Azure Advisor recommendations regularly.

---

## Enterprise Scenario

A software company runs production microservices on AKS.

Application images are stored in Azure Container Registry.

Persistent application data is stored in Azure Files, while Azure Monitor and Container Insights continuously collect performance metrics.

Background processing tasks execute in Azure Container Instances to avoid maintaining additional infrastructure.

---

## Best Practices Checklist

- Select the appropriate Azure container service.
- Design containers to be stateless.
- Store persistent data outside containers.
- Use Azure Container Registry.
- Enable monitoring from deployment.
- Configure autoscaling where appropriate.
- Keep container images updated.
- Protect secrets using Azure Key Vault.
- Review Azure Advisor recommendations.

---

## Common Pitfalls

- Using AKS for very small workloads.
- Deploying stateful applications without persistent storage.
- Embedding secrets inside container images.
- Ignoring image updates and vulnerability scanning.
- Overprovisioning Kubernetes clusters.
- Treating containers like Virtual Machines.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Container Instances (ACI)
> - Azure Kubernetes Service (AKS)
> - Virtual Machine Scale Sets (VMSS)
> - Container Groups
> - Persistent Storage
> - Azure Container Registry
> - Autoscaling
> - Container monitoring
> - Security best practices

---

## Key Takeaways

- Azure provides multiple container services optimized for different workloads.
- Stateless application design simplifies scaling and recovery.
- Persistent data should always be stored outside containers.
- Monitoring, autoscaling, and image management are essential for production environments.
- Choosing the appropriate Azure container platform improves operational efficiency, availability, and cost optimization.

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
```
