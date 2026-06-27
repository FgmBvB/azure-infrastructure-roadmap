# Azure Architecture

## Overview

Microsoft Azure is Microsoft's public cloud platform, providing a wide range of cloud services including compute, networking, storage, databases, security, monitoring and artificial intelligence.

Instead of purchasing, maintaining and replacing physical hardware, organizations can deploy and manage IT resources on Microsoft's global infrastructure using a pay-as-you-go model.

Azure enables businesses to build scalable, highly available and secure environments while reducing the operational complexity of managing traditional on-premises infrastructure.

## Why It Exists

Traditional on-premises infrastructure requires organizations to purchase, maintain and eventually replace physical hardware. This approach involves significant capital investment, ongoing maintenance, and limited scalability.

Microsoft Azure was created to provide a cloud platform where organizations can deploy and manage IT resources without owning the underlying infrastructure.

By using Azure, businesses can quickly provision services, scale resources on demand, improve availability, and reduce the operational burden of maintaining physical datacenters.

## How It Works

Azure is built on a global network of Microsoft datacenters distributed across multiple geographic regions.

Customers can deploy cloud resources such as virtual machines, storage accounts, databases, networking components, and many other services through the Azure Portal, Azure CLI, PowerShell, APIs, or Infrastructure as Code (IaC) tools.

Azure manages the underlying physical infrastructure, allowing customers to focus on deploying and managing their workloads rather than maintaining hardware.

## Enterprise Scenario

A medium-sized company currently hosts its applications, databases, file servers, and backup infrastructure in an on-premises datacenter.

As the business grows, the existing infrastructure becomes increasingly difficult to scale, requires significant hardware investment, and demands continuous maintenance.

By adopting Microsoft Azure, the organization can provision new resources in minutes, expand services when demand increases, improve disaster recovery capabilities, and reduce the operational effort required to maintain physical infrastructure.

This allows the IT team to focus on managing workloads and delivering business value rather than maintaining servers and datacenter facilities.

## Best Practices

- Design your architecture before deploying resources.
- Choose Azure regions that are geographically close to your users.
- Follow the principle of least privilege.
- Monitor resource usage and costs from the beginning.
- Design workloads with high availability and resilience in mind.
- Automate deployments whenever possible.

## Common Mistakes

- Treating Azure as just another virtualization platform.
- Deploying resources without proper planning.
- Ignoring cost management during deployments.
- Assigning excessive permissions to users.
- Designing workloads without considering availability and redundancy.

## AZ-104 Exam Notes

For the AZ-104 certification, you should understand:

- The purpose of Microsoft Azure.
- The benefits of cloud computing.
- Azure global infrastructure.
- Shared responsibility model.
- Basic cloud deployment concepts.

## References

## References

- https://learn.microsoft.com/azure/
- https://learn.microsoft.com/training/paths/azure-fundamentals-describe-azure-architecture-services/
- https://learn.microsoft.com/azure/well-architected/

## Key Takeaways

- Azure is Microsoft's public cloud platform.
- Microsoft owns and manages the physical infrastructure.
- Customers deploy and manage cloud resources on demand.
- Azure enables scalable, resilient, and globally distributed solutions.
- The shared responsibility model defines which security and management responsibilities belong to Microsoft and which belong to the customer.
