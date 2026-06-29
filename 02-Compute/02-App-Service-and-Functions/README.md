# Azure App Service and Azure Functions

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure App Service and Azure Functions, including architecture, hosting models, scaling, monitoring, security, and Microsoft's recommended best practices for modern Platform as a Service (PaaS) workloads.

---

## Overview

Azure App Service and Azure Functions are Azure's primary **Platform as a Service (PaaS)** compute services.

They allow organizations to deploy applications without managing virtual machines, operating systems, or the underlying infrastructure. Microsoft is responsible for platform maintenance, patching, scaling infrastructure, and high availability.

This section explains when to use each service, how App Service Plans work, how Azure Functions execute serverless workloads, and the operational best practices required for production environments.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure App Service architecture.
- Understand Azure Functions architecture.
- Configure App Service Plans.
- Differentiate hosting models.
- Understand scaling behavior.
- Deploy secure and highly available applications.
- Apply Microsoft's recommended operational best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Azure App Service, Azure Functions, App Service Plans, hosting models, scaling, and enterprise deployment scenarios. |
| **02 - Best Practices** | Security, monitoring, autoscaling, cost optimization, hosting recommendations, and operational best practices. |

---

## Compute Architecture

```text
                 Azure Compute
                      │
        ┌─────────────┴─────────────┐
        │                           │
        ▼                           ▼
 Azure App Service          Azure Functions
        │                           │
        ▼                           ▼
 App Service Plan         Hosting Plan
        │                           │
        ▼                           ▼
 Web Apps / APIs        Event-driven Functions
```

---

## Skills Covered

This section includes:

- Azure App Service
- Azure Functions
- App Service Plans
- Hosting Plans
- Autoscaling
- Always On
- Cold Start
- Application Insights
- Azure Monitor
- Microsoft Entra Authentication
- Azure Key Vault
- PaaS Best Practices

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Deploy Azure App Service.
- Configure App Service Plans.
- Deploy Azure Functions.
- Configure autoscaling.
- Monitor application performance.
- Secure PaaS workloads.
- Optimize application hosting costs.

---

## Key Takeaways

- Azure App Service hosts web applications, REST APIs, and backend services without requiring Virtual Machine management.
- Azure Functions provides serverless, event-driven compute that automatically scales based on demand.
- App Service Plans define the compute resources shared by one or more App Services.
- Selecting the appropriate hosting model improves scalability, performance, availability, and cost efficiency.
- Monitoring, security, and autoscaling are essential components of production-ready PaaS deployments.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure App Service documentation | https://learn.microsoft.com/azure/app-service/ |
| Azure Functions documentation | https://learn.microsoft.com/azure/azure-functions/ |
| App Service plans | https://learn.microsoft.com/azure/app-service/overview-hosting-plans |
| Azure Functions hosting options | https://learn.microsoft.com/azure/azure-functions/functions-scale |
| Application Insights | https://learn.microsoft.com/azure/azure-monitor/app/app-insights-overview |
| Azure Monitor documentation | https://learn.microsoft.com/azure/azure-monitor/ |
| Azure Key Vault documentation | https://learn.microsoft.com/azure/key-vault/general/ |
| Microsoft Learn – Host a web application with Azure App Service | https://learn.microsoft.com/training/modules/host-a-web-app-with-azure-app-service/ |
| Microsoft Learn – Create serverless applications with Azure Functions | https://learn.microsoft.com/training/modules/create-serverless-applications/ |
