# Azure App Service and Azure Functions Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure App Service and Azure Functions, explains their architecture, hosting models, scaling capabilities, and common deployment scenarios.

---

## Overview

Azure App Service and Azure Functions are Azure Platform as a Service (PaaS) compute offerings.

Unlike Virtual Machines, Microsoft manages the underlying infrastructure, operating system, runtime updates, and platform maintenance, allowing developers and administrators to focus on applications instead of servers.

While both services run applications, they target different workloads:

- **Azure App Service** hosts long-running web applications and APIs.
- **Azure Functions** executes event-driven serverless code.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure App Service.
- Understand Azure Functions.
- Differentiate App Service and Functions.
- Understand App Service Plans.
- Understand scaling options.
- Identify common enterprise scenarios.
- Choose the appropriate Azure compute service.

---

## Azure Compute Services

```text
                 Azure Compute
                      │
      ┌───────────────┼───────────────┐
      │                               │
      ▼                               ▼
 Azure App Service            Azure Functions
      │                               │
      ▼                               ▼
Web Apps / APIs          Event-driven Functions
```

---

## Azure App Service

Azure App Service is a fully managed platform for hosting:

- Web Applications
- REST APIs
- Backend Services

Supported technologies include:

- .NET
- Java
- Node.js
- Python
- PHP
- Ruby

Azure manages:

- Operating system
- Runtime updates
- Load balancing
- Scaling
- Platform maintenance

---

## App Service Plans

Every App Service runs inside an **App Service Plan**.

The App Service Plan defines:

- Compute resources
- Pricing tier
- Scaling limits
- Operating system (Windows or Linux)
- Region

Multiple App Services can share the same App Service Plan.

---

## Azure Functions

Azure Functions is Azure's serverless compute platform.

Functions execute automatically in response to events without requiring administrators to manage servers.

Common triggers include:

- HTTP requests
- Timers
- Azure Storage events
- Service Bus messages
- Event Grid
- Event Hub
- Queue Storage

Azure automatically provisions compute resources as needed.

---

## Hosting Models

| Service | Typical Execution Model |
|----------|-------------------------|
| **App Service** | Long-running applications |
| **Azure Functions** | Short-lived event-driven execution |

Azure Functions supports multiple hosting plans, including Consumption, Premium, and Dedicated.

---

## Scaling

Both services support automatic scaling.

| Service | Scaling |
|----------|----------|
| **App Service** | Manual or automatic scaling depending on the pricing tier |
| **Azure Functions** | Automatic scaling based on incoming events (depending on the hosting plan) |

Scaling occurs without requiring administrators to provision additional Virtual Machines manually.

---

## App Service vs Azure Functions

| Azure App Service | Azure Functions |
|-------------------|-----------------|
| Hosts complete applications | Executes individual functions |
| Long-running workloads | Event-driven execution |
| Always available applications | Runs only when triggered (Consumption plan) |
| Ideal for websites and APIs | Ideal for automation and integrations |

---

## Enterprise Scenario

A company hosts its customer portal using Azure App Service.

When customers upload files, Azure Functions automatically validates the documents, generates thumbnails, and stores metadata in Azure Storage.

The web application remains continuously available, while Azure Functions execute only when required.

---

## Best Practices

- Choose App Service for web applications and REST APIs.
- Choose Azure Functions for event-driven automation.
- Select the appropriate App Service Plan.
- Enable automatic scaling where appropriate.
- Monitor application performance with Azure Monitor and Application Insights.
- Secure applications using Microsoft Entra ID authentication whenever possible.

---

## Common Pitfalls

- Choosing Azure Functions for long-running applications.
- Using oversized App Service Plans.
- Ignoring automatic scaling configuration.
- Deploying production workloads without monitoring.
- Confusing App Service with Virtual Machines.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure App Service
> - App Service Plans
> - Azure Functions
> - Hosting models
> - Scaling
> - Triggers
> - App Service vs Functions

---

## Key Takeaways

- Azure App Service and Azure Functions are managed PaaS compute services.
- App Service is designed for web applications and APIs.
- Azure Functions provides serverless, event-driven compute.
- App Service Plans determine the compute resources available to App Service.
- Selecting the appropriate service improves scalability, operational efficiency, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure App Service documentation | https://learn.microsoft.com/azure/app-service/ |
| Azure Functions documentation | https://learn.microsoft.com/azure/azure-functions/ |
| App Service plans | https://learn.microsoft.com/azure/app-service/overview-hosting-plans |
| Azure Functions hosting options | https://learn.microsoft.com/azure/azure-functions/functions-scale |
| Application Insights | https://learn.microsoft.com/azure/azure-monitor/app/app-insights-overview |
| Microsoft Learn – Host a web application with Azure App Service | https://learn.microsoft.com/training/modules/host-a-web-app-with-azure-app-service/ |
| Microsoft Learn – Create serverless applications with Azure Functions | https://learn.microsoft.com/training/modules/create-serverless-applications/ |
