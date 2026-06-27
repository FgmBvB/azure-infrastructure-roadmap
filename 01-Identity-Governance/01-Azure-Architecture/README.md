# Azure Architecture

> [!NOTE]
> This document is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It is continuously updated as I gain new knowledge and hands-on experience.

---

## Azure Platform Overview

```text
                    Microsoft Azure
                          │
     ┌────────────┬────────────┬────────────┐
     │            │            │            │
 Compute     Networking    Storage    Security
```

---

> [!TIP]
> **Key Concepts**
>
> - Azure is Microsoft's public cloud platform.
> - Microsoft manages the physical infrastructure.
> - Customers deploy and manage cloud resources.
> - Resources can be provisioned on demand.
> - Azure follows a shared responsibility model.

---

## Overview

Microsoft Azure is Microsoft's public cloud platform, providing a wide range of cloud services including compute, networking, storage, databases, security, monitoring, and artificial intelligence.

Instead of purchasing, maintaining, and replacing physical hardware, organizations can deploy and manage IT resources on Microsoft's global infrastructure using a pay-as-you-go model.

Azure enables businesses to build scalable, highly available, and secure environments while reducing the operational complexity of managing traditional on-premises infrastructure.

---

## Purpose

Traditional on-premises infrastructure requires organizations to purchase, maintain, and eventually replace physical hardware. This approach involves significant capital investment, ongoing maintenance, and limited scalability.

Microsoft Azure was created to provide a cloud platform where organizations can deploy and manage IT resources without owning the underlying infrastructure.

By using Azure, businesses can quickly provision services, scale resources on demand, improve availability, and reduce the operational burden of maintaining physical datacenters.

---

## Architecture

Azure is built on Microsoft's global infrastructure, consisting of datacenters distributed across multiple geographic regions.

Customers can deploy cloud resources such as virtual machines, storage accounts, databases, networking components, and many other services through the Azure Portal, Azure CLI, PowerShell, REST APIs, or Infrastructure as Code (IaC) tools.

Microsoft manages the underlying physical infrastructure while customers are responsible for configuring and managing their cloud resources according to the shared responsibility model.

---

## Enterprise Scenario

A company currently hosts its infrastructure in an on-premises datacenter.

As the business grows, the organization requires additional compute, storage, and networking resources. Purchasing new hardware increases costs and operational complexity.

By adopting Microsoft Azure, the company can provision resources on demand, improve business continuity, simplify infrastructure management, and scale services according to business needs.

---

## Shared Responsibility Model

Microsoft is responsible for managing the physical infrastructure, including datacenters, networking, hardware, and the Azure platform.

Customers are responsible for configuring and securing their cloud resources, identities, applications, operating systems, and data, depending on the cloud service model (IaaS, PaaS, or SaaS).

Understanding the shared responsibility model is fundamental for designing secure Azure environments.

---

## Best Practices

- Design the cloud architecture before deploying resources.
- Apply the principle of least privilege.
- Design for scalability and high availability.
- Monitor resource utilization and costs from the beginning.
- Automate deployments whenever possible.

---

## Common Pitfalls

- Treating Azure as only a virtualization platform.
- Deploying resources without proper planning.
- Ignoring cost management.
- Assigning excessive permissions.
- Designing workloads without considering resilience.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure architecture fundamentals.
> - Global Azure infrastructure.
> - Shared responsibility model.
> - Cloud deployment methods.
> - Core Azure services.

---

## Key Takeaways

- Azure is Microsoft's public cloud platform.
- Microsoft manages the physical infrastructure.
- Customers manage their cloud resources.
- Resources can be deployed on demand.
- Azure enables scalable, resilient, and globally distributed solutions.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Azure Documentation](https://learn.microsoft.com/azure/) | Azure platform overview |
| [Azure Fundamentals – Describe Azure Architecture and Services](https://learn.microsoft.com/training/paths/azure-fundamentals-describe-azure-architecture-services/) | Azure architecture fundamentals |
| [Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/azure/well-architected/) | Architecture best practices |
