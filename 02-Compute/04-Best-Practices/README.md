# Azure Compute Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for designing, deploying, securing, monitoring, and optimizing Azure compute services, including Virtual Machines, App Service, Azure Functions, Azure Container Instances (ACI), Azure Kubernetes Service (AKS), and Virtual Machine Scale Sets (VMSS).

---

## Overview

Azure offers multiple compute services, each optimized for different workloads.

Selecting the correct compute platform and following Microsoft's operational recommendations improves availability, scalability, security, performance, and cost efficiency.

Rather than choosing a service based on familiarity, administrators should evaluate workload characteristics, operational requirements, and business objectives.

---

## Azure Compute Decision Flow

```text
Need full OS control?
        │
   ┌────┴────┐
   │         │
 Yes        No
   │         │
   ▼         ▼
Virtual     Web App or API?
Machine          │
                 │
          ┌──────┴──────┐
          │             │
         Yes           No
          │             │
          ▼             ▼
   App Service     Event-driven?
                        │
                 ┌──────┴──────┐
                 │             │
                Yes           Large container platform?
                 │                     │
                 ▼                     ▼
         Azure Functions             AKS
```

---

## Choose the Right Compute Service

| Workload | Recommended Service |
|----------|---------------------|
| Legacy applications | Azure Virtual Machines |
| Enterprise web applications | Azure App Service |
| REST APIs | Azure App Service |
| Event-driven automation | Azure Functions |
| Short-lived containers | Azure Container Instances |
| Production container platforms | Azure Kubernetes Service |
| Large VM fleets | Virtual Machine Scale Sets |

Always choose the simplest service capable of meeting the workload requirements.

---

## High Availability

Microsoft recommends:

- Deploy production Virtual Machines across **Availability Zones** whenever supported.
- Use **Availability Sets** only when Availability Zones are unavailable.
- Enable autoscaling for App Service and AKS where appropriate.
- Design applications to tolerate instance failures.
- Use Azure Load Balancer or Application Gateway to distribute traffic.

Avoid single-instance production deployments.

---

## Performance

Optimize compute performance by:

- Selecting the correct VM size.
- Right-sizing App Service Plans.
- Using Premium storage only when required.
- Monitoring CPU, memory, and disk utilization.
- Scaling out before scaling up whenever possible.

Review Azure Advisor recommendations regularly.

---

## Security

Apply Microsoft's Zero Trust principles:

- Enable Microsoft Entra ID authentication whenever supported.
- Restrict administrative access.
- Apply Azure RBAC using least privilege.
- Protect secrets with Azure Key Vault.
- Keep operating systems and runtimes updated.
- Enable Microsoft Defender for Cloud recommendations.
- Protect Virtual Machines using NSGs and Just-in-Time (JIT) VM Access where appropriate.

---

## Storage

For compute workloads:

- Use Managed Disks for Virtual Machines.
- Never store business data on Temporary Disks.
- Store container data in Azure Files or Azure Disks.
- Design containers to remain stateless whenever possible.

Persistent data should always reside outside ephemeral compute resources.

---

## Monitoring

Enable monitoring from the beginning of every deployment.

Recommended services include:

- Azure Monitor
- Application Insights
- VM Insights
- Container Insights
- Activity Log
- Log Analytics
- Azure Advisor

Configure alerts for:

- CPU utilization
- Memory pressure
- Failed deployments
- Application availability
- Resource health

---

## Cost Optimization

Reduce operational costs by:

- Deallocating unused Virtual Machines.
- Choosing the appropriate App Service Plan.
- Using Azure Functions Consumption Plan for intermittent workloads.
- Scaling AKS clusters according to demand.
- Removing unused Managed Disks and Public IP addresses.
- Purchasing Reserved Instances for predictable Virtual Machine workloads.
- Using Azure Spot Virtual Machines for interruptible workloads.

---

## Operational Excellence

Microsoft recommends:

- Automate deployments using Infrastructure as Code (ARM, Bicep, or Terraform).
- Standardize deployments using reusable templates.
- Apply Azure Policy for governance.
- Protect resources with Resource Locks where appropriate.
- Tag resources consistently for governance and cost management.
- Test backup and disaster recovery procedures regularly.

---

## Common Pitfalls

Avoid these common mistakes:

- Choosing Virtual Machines when a PaaS service is sufficient.
- Oversizing compute resources.
- Running production workloads without monitoring.
- Storing persistent data inside containers.
- Leaving stopped Virtual Machines allocated.
- Ignoring autoscaling configuration.
- Deploying production workloads without backup or disaster recovery planning.
- Hardcoding application secrets instead of using Azure Key Vault.

---

## AZ-104 Exam Tips

For the exam, remember these key decision points:

| Scenario | Recommended Azure Service |
|----------|---------------------------|
| Full operating system control | Virtual Machine |
| Web application or REST API | App Service |
| Event-driven automation | Azure Functions |
| Single container | Azure Container Instances |
| Kubernetes orchestration | Azure Kubernetes Service |
| Automatically scaling Virtual Machines | Virtual Machine Scale Sets |

Questions often focus on selecting the **most appropriate compute service**, not simply the one capable of running the workload.

---

## Key Takeaways

- Choose the simplest Azure compute service that satisfies the workload requirements.
- Prefer Platform as a Service (PaaS) over Infrastructure as a Service (IaaS) whenever possible.
- Design compute workloads for high availability, scalability, and resilience.
- Monitor all compute resources continuously.
- Secure compute services using Microsoft Entra ID, Azure RBAC, Key Vault, and Microsoft Defender for Cloud.
- Optimize costs through right-sizing, autoscaling, and lifecycle management.
- Infrastructure as Code and governance services improve consistency and operational efficiency.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Virtual Machines documentation | https://learn.microsoft.com/azure/virtual-machines/ |
| Azure App Service documentation | https://learn.microsoft.com/azure/app-service/ |
| Azure Functions documentation | https://learn.microsoft.com/azure/azure-functions/ |
| Azure Container Instances documentation | https://learn.microsoft.com/azure/container-instances/ |
| Azure Kubernetes Service documentation | https://learn.microsoft.com/azure/aks/ |
| Virtual Machine Scale Sets documentation | https://learn.microsoft.com/azure/virtual-machine-scale-sets/ |
| Azure Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Microsoft Defender for Cloud | https://learn.microsoft.com/azure/defender-for-cloud/ |
| Azure Monitor documentation | https://learn.microsoft.com/azure/azure-monitor/ |
