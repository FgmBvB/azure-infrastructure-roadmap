# Regions and Availability

> [!NOTE]
> This document is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It is continuously updated as I gain new knowledge and hands-on experience.

---

##  Azure Global Infrastructure

```text
                   Microsoft Azure

                Global Backbone Network
                        │
      ┌─────────────────┼─────────────────┐
      │                 │                 │
 Azure Region A    Azure Region B    Azure Region C
      │
 ┌────┴────┐
 │         │
Zone 1   Zone 2
```

---

> [!TIP]
> **Key Concepts**
>
> - Azure Regions are geographical locations.
> - Each Region contains one or more datacenters.
> - Some Regions support Availability Zones.
> - Availability Zones improve resilience.
> - Region selection affects latency, compliance, and availability.

---

##  Overview

Microsoft Azure is organized into geographic locations known as **Azure Regions**. Each region consists of one or more datacenters connected through Microsoft's high-performance global network.

Regions allow organizations to deploy resources close to their users, helping reduce latency, meet regulatory requirements, and improve service availability.

Some Azure regions include **Availability Zones**, which provide additional resilience by distributing resources across physically separate datacenters within the same region.

---

##  Why It Exists

Azure Regions exist to provide customers with global coverage, allowing workloads to be deployed closer to users and data.

This architecture improves performance, supports data residency requirements, and increases service availability by distributing infrastructure across multiple geographic locations.

Availability Zones further improve resilience by protecting applications against failures affecting an individual datacenter.

---

## How It Works

Each Azure Region contains one or more physical datacenters.

Some regions support Availability Zones, where datacenters are separated by independent power, cooling, and networking infrastructure.

Applications can be deployed across multiple zones to increase availability and reduce the impact of hardware or datacenter failures.

Microsoft operates one of the world's largest private global networks, connecting Azure Regions through its high-capacity backbone infrastructure.

Some Azure Regions are paired with another region within the same geography, known as **Region Pairs**.

Region Pairs support platform updates, disaster recovery strategies, and help improve service resilience by reducing the likelihood of both regions being affected simultaneously.

---

##  Enterprise Scenario

A multinational company has offices in Europe, North America, and Asia.

To reduce latency and improve the user experience, the company deploys applications in Azure Regions that are geographically close to each office.

Critical workloads are distributed across Availability Zones to maintain service availability in the event of a datacenter failure.

---

##  Best Practices

- Select the Azure Region closest to your users.
- Verify service availability before choosing a region.
- Use Availability Zones for business-critical workloads whenever supported.
- Consider data residency and compliance requirements.
- Design for high availability from the beginning.

---

##  Common Mistakes

- Choosing a region without considering latency.
- Assuming all Azure services are available in every region.
- Ignoring data residency requirements.
- Deploying critical workloads in a single Availability Zone.
- Confusing Azure Regions with Availability Zones.

---

##  AZ-104 Exam Notes

For the AZ-104 certification, you should understand:

- Azure Regions
- Availability Zones
- Region selection
- Service availability by region
- High availability concepts

---

##  Key Takeaways

- Azure is organized into geographic Regions.
- Regions contain one or more datacenters.
- Some Regions support Availability Zones.
- Availability Zones improve workload resilience.
- Region selection affects latency, compliance, and service availability.

---

##  References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Regions](https://learn.microsoft.com/azure/reliability/regions-list) | Azure Regions overview and architecture |
| [Azure Availability Zones](https://learn.microsoft.com/azure/reliability/availability-zones-overview) | Availability Zones concepts and resilience |
| [Microsoft Learn – Describe Azure Architecture and Services](https://learn.microsoft.com/training/paths/azure-fundamentals-describe-azure-architecture-services/) | Azure architecture fundamentals |
