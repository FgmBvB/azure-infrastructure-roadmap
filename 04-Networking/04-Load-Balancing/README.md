# Azure Load Balancing

> [!NOTE]
> This module is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Load Balancer, Azure Application Gateway, traffic distribution, health probes, Web Application Firewall (WAF), session persistence, outbound connectivity, and Microsoft's recommended best practices for designing highly available applications.

---

# Overview

Load balancing is a fundamental component of highly available Azure architectures.

Instead of relying on a single server, Azure distributes client traffic across multiple backend resources, improving:

- Availability
- Scalability
- Fault tolerance
- Performance

Azure provides two complementary load balancing services:

- **Azure Load Balancer** (Layer 4)
- **Azure Application Gateway** (Layer 7)

Although both distribute traffic, they operate at different layers of the OSI model and solve different architectural problems.

Understanding their capabilities, limitations, and deployment scenarios is an important objective of the **AZ-104** certification.

---

# Learning Objectives

After completing this module you should be able to:

- Understand Azure Load Balancer.
- Differentiate Layer 4 and Layer 7 load balancing.
- Understand Public and Internal Load Balancers.
- Configure Backend Pools and Health Probes.
- Understand Session Persistence.
- Understand Azure Application Gateway.
- Understand Web Application Firewall (WAF).
- Compare Azure Load Balancer and Application Gateway.
- Apply Microsoft's recommended load balancing best practices.

---

# Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Azure Load Balancer, Application Gateway, Backend Pools, Health Probes, Load Balancing Rules, NAT Rules, Session Persistence, Standard SKU, WAF, outbound connectivity, and service comparison. |
| **02 - Best Practices** | High availability, Standard SKU recommendations, Health Probe design, outbound Internet access, NAT Gateway, WAF deployment, monitoring, governance, cost optimization, and Microsoft's production best practices. |

---

# Service Comparison

| Service | Primary Purpose |
|----------|-----------------|
| **Azure Load Balancer** | Layer 4 (TCP/UDP) traffic distribution |
| **Azure Application Gateway** | Layer 7 (HTTP/HTTPS) intelligent routing with WAF |

Both services can be combined in enterprise architectures.

---

# Typical Enterprise Architecture

```text
                Internet
                    │
                    ▼
      Azure Application Gateway
           (Layer 7 + WAF)
                    │
                    ▼
        Azure Load Balancer
             (Layer 4)
                    │
                    ▼
      Virtual Machine Scale Set
                    │
                    ▼
             Backend Services
```

Application Gateway performs:

- TLS termination
- URL-based routing
- Host-based routing
- Web Application Firewall inspection

Azure Load Balancer distributes network traffic across backend instances.

---

# Core Technologies Covered

This module includes:

- Azure Load Balancer
- Public Load Balancer
- Internal Load Balancer
- Backend Pools
- Health Probes
- Load Balancing Rules
- Inbound NAT Rules
- Session Persistence
- Load Balancing Algorithms (2-Tuple, 3-Tuple, 5-Tuple)
- Standard Load Balancer
- Azure Application Gateway
- Web Application Firewall (WAF)
- TLS Termination
- URL Path Routing
- Host-based Routing
- Outbound Rules
- Azure NAT Gateway integration
- High Availability
- Availability Zones

---

# Design Principles

Microsoft recommends following these principles when designing load-balanced applications:

- Prefer **Standard SKU** resources.
- Design applications to be stateless whenever possible.
- Use Health Probes to detect backend failures.
- Deploy multiple backend instances.
- Protect public web applications with WAF.
- Separate Layer 4 and Layer 7 responsibilities.
- Use explicit outbound connectivity through Azure NAT Gateway or another supported solution.
- Continuously monitor backend health and application performance.

---

# AZ-104 Exam Focus

This module aligns with the Microsoft AZ-104 objectives related to:

- Configure Azure Load Balancer.
- Configure Azure Application Gateway.
- Configure Backend Pools.
- Configure Health Probes.
- Configure Load Balancing Rules.
- Configure Session Persistence.
- Configure Web Application Firewall.
- Select the appropriate load balancing service.
- Design highly available Azure applications.

---

# Key Takeaways

- Azure Load Balancer distributes TCP and UDP traffic at Layer 4, making it ideal for infrastructure workloads and high-performance networking.
- Azure Application Gateway operates at Layer 7, providing intelligent HTTP/HTTPS routing, TLS termination, and integrated Web Application Firewall protection.
- Proper Health Probe configuration is essential to ensure traffic is sent only to healthy backend instances.
- Modern Azure architectures should use explicit outbound connectivity, such as Azure NAT Gateway, rather than relying on implicit Internet access.
- Choosing the correct load balancing service and following Microsoft's design recommendations results in scalable, secure, and highly available Azure applications.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Load Balancer documentation | https://learn.microsoft.com/azure/load-balancer/load-balancer-overview |
| Azure Load Balancer components | https://learn.microsoft.com/azure/load-balancer/components |
| Azure Application Gateway documentation | https://learn.microsoft.com/azure/application-gateway/overview |
| Azure Web Application Firewall | https://learn.microsoft.com/azure/web-application-firewall/ag/ag-overview |
| Azure Load Balancer health probes | https://learn.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview |
| Azure NAT Gateway documentation | https://learn.microsoft.com/azure/nat-gateway/nat-overview |
| Azure Well-Architected Framework – Load balancing | https://learn.microsoft.com/azure/well-architected/service-guides/load-balancer |
| Microsoft Learn – Improve application scalability with Azure Load Balancer | https://learn.microsoft.com/training/modules/improve-app-scalability-resiliency-with-load-balancer/ |
