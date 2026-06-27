# Regions and Availability

## Overview

Microsoft Azure is organized into geographic locations known as **Azure Regions**. Each region consists of one or more datacenters connected through Microsoft's high-performance global network.

Regions allow organizations to deploy resources close to their users, helping reduce latency, meet regulatory requirements, and improve service availability.

Some Azure regions include **Availability Zones**, which provide additional resilience by distributing resources across physically separate datacenters within the same region.

## Why It Exists

Azure Regions exist to provide customers with global coverage, allowing workloads to be deployed closer to users and data.

This architecture improves performance, supports data residency requirements, and increases service availability by distributing infrastructure across multiple geographic locations.

Availability Zones further improve resilience by protecting applications against failures affecting an individual datacenter.

## How It Works

Each Azure Region contains one or more physical datacenters.

Some regions support Availability Zones, where datacenters are separated by independent power, cooling, and networking infrastructure.

Applications can be deployed across multiple zones to increase availability and reduce the impact of hardware or datacenter failures.

Microsoft also connects all regions through its global backbone network, enabling secure, high-speed communication between Azure services worldwide.

## Enterprise Scenario

A multinational company has offices in Europe, North America, and Asia.

To reduce latency and improve the user experience, the company deploys applications in Azure Regions that are geographically close to each office.

Critical workloads are distributed across Availability Zones to maintain service availability in the event of a datacenter failure.

## Best Practices

- Select the Azure Region closest to your users.
- Verify service availability before choosing a region.
- Use Availability Zones for business-critical workloads whenever supported.
- Consider data residency and compliance requirements.
- Design for high availability from the beginning.

## Common Mistakes

- Choosing a region without considering latency.
- Assuming all Azure services are available in every region.
- Ignoring data residency requirements.
- Deploying critical workloads in a single Availability Zone.
- Confusing Azure Regions with Availability Zones.
  
## AZ-104 Exam Notes

For the AZ-104 certification, you should understand:

- Azure Regions
- Availability Zones
- Region selection
- Service availability by region
- High availability concepts

  ## References

- [Azure Global Infrastructure](https://learn.microsoft.com/azure/reliability/regions-list)
- [Azure Availability Zones](https://learn.microsoft.com/azure/reliability/availability-zones-overview)
- [Microsoft Learn - Describe Azure Architecture and Services](https://learn.microsoft.com/training/paths/azure-fundamentals-describe-azure-architecture-services/)

  ## Key Takeaways

- Azure is organized into geographic Regions.
- Regions contain one or more datacenters.
- Some Regions support Availability Zones.
- Availability Zones improve workload resilience.
- Region selection affects latency, compliance, and service availability.
