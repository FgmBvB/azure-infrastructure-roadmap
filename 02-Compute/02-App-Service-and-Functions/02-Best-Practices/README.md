# Azure App Service and Azure Functions Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for deploying, securing, scaling, monitoring, and optimizing Azure App Service and Azure Functions.

---

## Overview

Azure App Service and Azure Functions eliminate much of the operational overhead associated with managing infrastructure.

To maximize availability, security, performance, and cost efficiency, Microsoft recommends following cloud-native design principles and using Azure-native management services.

---

## Application Lifecycle

```text
Plan
 │
 ▼
Deploy
 │
 ▼
Secure
 │
 ▼
Scale
 │
 ▼
Monitor
 │
 ▼
Optimize
```

---

> [!TIP]
> **Key Concepts**
>
> - Select the appropriate hosting model.
> - Use automatic scaling whenever possible.
> - Monitor application health continuously.
> - Secure applications using Microsoft Entra ID.
> - Separate workloads with different performance requirements.

---

## Choosing the Right Service

Microsoft recommends selecting the compute service based on the workload.

| Workload | Recommended Service |
|----------|---------------------|
| Web applications | Azure App Service |
| REST APIs | Azure App Service |
| Background processing | Azure Functions |
| Event-driven automation | Azure Functions |
| Scheduled jobs | Azure Functions |

---

## App Service Plans

For App Service deployments:

- Select the appropriate pricing tier.
- Separate production and development workloads.
- Place high-demand applications in dedicated App Service Plans.
- Enable autoscaling where supported.
- Enable **Always On** for production applications.

Applications sharing the same App Service Plan also share the same compute resources.

---

## Scaling

To improve performance and availability:

- Configure autoscaling based on CPU, memory, or HTTP requests.
- Scale out before scaling up whenever appropriate.
- Monitor scaling rules regularly.
- Test application behavior under load.

---

## Security

Microsoft recommends:

- Enable Microsoft Entra ID authentication whenever possible.
- Use HTTPS only.
- Store secrets in Azure Key Vault.
- Apply the principle of least privilege.
- Restrict access using Networking features where supported.
- Keep application runtimes updated.

---

## Monitoring

Monitor applications using:

- Azure Monitor
- Application Insights
- Log Analytics
- Activity Log
- Metrics
- Alerts

Collecting telemetry helps identify performance bottlenecks and application failures.

---

## Cost Optimization

To reduce Azure costs:

- Right-size App Service Plans.
- Use Consumption Plans for event-driven workloads.
- Avoid oversized Premium tiers.
- Consolidate small applications only when resource usage allows.
- Review Azure Advisor recommendations.

---

## Azure Functions

Microsoft recommends:

- Use Functions for short-lived event-driven workloads.
- Select the appropriate hosting plan.
- Enable **Always On** when using Dedicated hosting.
- Use Durable Functions for long-running workflows.
- Design functions to be stateless whenever possible.

---

## Enterprise Scenario

A retail company hosts its public website using Azure App Service.

Customer uploads trigger Azure Functions that automatically resize images, generate thumbnails, and store metadata.

Application Insights monitors performance, while Azure Monitor generates alerts for failed requests and abnormal response times.

Separate App Service Plans isolate production workloads from internal business applications.

---

## Best Practices Checklist

- Choose the appropriate Azure compute service.
- Right-size App Service Plans.
- Enable autoscaling.
- Enable Always On for production App Services.
- Secure applications with Microsoft Entra ID.
- Store secrets in Azure Key Vault.
- Enable Application Insights.
- Monitor application health continuously.
- Use Durable Functions for long-running workflows.
- Review Azure Advisor recommendations regularly.

---

## Common Pitfalls

- Hosting unrelated production workloads in the same App Service Plan.
- Ignoring Cold Start behavior in Consumption Plans.
- Using Azure Functions for continuously running applications.
- Deploying production applications without monitoring.
- Hardcoding secrets inside application code.
- Oversizing App Service Plans without monitoring utilization.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - App Service Plans
> - Always On
> - Autoscaling
> - Azure Functions hosting plans
> - Cold Start
> - Application Insights
> - Security best practices
> - Cost optimization

---

## Key Takeaways

- Azure App Service is optimized for hosting web applications and APIs.
- Azure Functions provides scalable serverless execution for event-driven workloads.
- App Service Plans determine compute resources and scaling capabilities.
- Monitoring, autoscaling, and security should be configured from the beginning of every deployment.
- Choosing the appropriate hosting model improves performance, availability, and operational efficiency.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure App Service documentation | https://learn.microsoft.com/azure/app-service/ |
| App Service plans | https://learn.microsoft.com/azure/app-service/overview-hosting-plans |
| Azure Functions documentation | https://learn.microsoft.com/azure/azure-functions/ |
| Azure Functions hosting options | https://learn.microsoft.com/azure/azure-functions/functions-scale |
| Application Insights | https://learn.microsoft.com/azure/azure-monitor/app/app-insights-overview |
| Azure Monitor documentation | https://learn.microsoft.com/azure/azure-monitor/ |
| Azure Key Vault documentation | https://learn.microsoft.com/azure/key-vault/general/ |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Microsoft Learn – Host a web application with Azure App Service | https://learn.microsoft.com/training/modules/host-a-web-app-with-azure-app-service/ |
| Microsoft Learn – Create serverless applications with Azure Functions | https://learn.microsoft.com/training/modules/create-serverless-applications/ |
