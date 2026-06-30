# Azure Load Balancing Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended best practices for designing, securing, monitoring, and operating Azure Load Balancer and Azure Application Gateway in production environments.

---

# Overview

Load balancing is essential for building highly available, scalable, and resilient applications.

Microsoft recommends selecting the appropriate load balancing service based on the application protocol, security requirements, and traffic inspection needs.

A well-designed load balancing architecture minimizes downtime while improving application performance and fault tolerance.

---

# Choose the Right Service

Always select the service that matches the workload.

| Scenario | Recommended Service |
|----------|----------------------|
| TCP/UDP applications | Azure Load Balancer |
| HTTP/HTTPS applications | Azure Application Gateway |
| Web applications requiring WAF | Application Gateway with WAF |
| Internal application tiers | Internal Load Balancer |
| Internet-facing infrastructure | Public Load Balancer or Application Gateway |

Do not use Application Gateway for workloads that only require Layer 4 load balancing.

---

# Use Standard SKU

Microsoft recommends using **Standard SKU** networking resources.

Benefits include:

- Secure by default.
- Availability Zone support.
- Higher scalability.
- Better diagnostics.
- Azure Monitor integration.
- Production-ready architecture.

Avoid using legacy Basic SKUs for new deployments.

---

# Outbound Internet Access

Inbound and outbound connectivity are configured independently.

For modern Azure deployments, backend Virtual Machines should **not** rely on implicit outbound Internet access.

Microsoft recommends one of the following outbound connectivity options:

- Azure NAT Gateway (recommended)
- Public IP addresses
- Azure Firewall
- Standard Load Balancer Outbound Rules

Azure NAT Gateway is the preferred solution because it provides:

- Predictable outbound connectivity
- Scalable SNAT
- Simplified management
- Dedicated outbound public IP addresses

> [!IMPORTANT]
> Modern Azure networking no longer recommends relying on default outbound Internet access for Virtual Machines. Production workloads should use an explicit outbound connectivity solution such as Azure NAT Gateway.

---

# Design for High Availability

Applications should tolerate backend failures.

Recommendations:

- Deploy multiple backend instances.
- Use Availability Zones whenever supported.
- Use Virtual Machine Scale Sets for scalable workloads.
- Configure Health Probes for every backend service.
- Test failover scenarios regularly.

Never rely on a single backend instance.

---

# Configure Health Probes Carefully

Health Probes determine backend availability.

Recommendations:

- Use application-specific probe endpoints.
- Avoid probing static pages that always return success.
- Configure appropriate probe intervals.
- Review unhealthy backend reports regularly.
- Monitor probe failures using Azure Monitor.

Poor probe configuration can remove healthy servers or keep failed servers in production.

---

## Health Probe Behavior

Health Probes continuously determine whether backend instances are available.

Typical behavior:

- Azure periodically sends probe requests to each backend instance.
- If multiple consecutive probes fail, the backend is marked as **Unhealthy**.
- Unhealthy instances immediately stop receiving new connections.
- Once probe responses become successful again, Azure automatically returns the backend to service.

Proper probe configuration should:

- Monitor application availability rather than simple network connectivity.
- Use realistic response endpoints.
- Avoid probe configurations that generate false positives.

> [!TIP]
> A poorly designed Health Probe can remove healthy servers from the backend pool or continue sending traffic to failed applications.

---

# Optimize Session Persistence

Choose session persistence only when required.

Recommendations:

- Use **None** whenever possible.
- Enable Client IP affinity only for stateful applications.
- Avoid unnecessary client affinity.
- Design applications to be stateless whenever possible.

Stateless applications scale more efficiently.

---

# Secure Internet-Facing Applications

For public web applications:

- Deploy Application Gateway with WAF.
- Use HTTPS only.
- Enable TLS termination.
- Redirect HTTP traffic to HTTPS.
- Protect against OWASP Top 10 attacks.
- Keep TLS policies up to date.

Never expose production applications without appropriate protection.

---

## Web Application Firewall Modes

Azure Application Gateway Web Application Firewall (WAF) supports two operating modes.

### Detection Mode

Detection mode inspects requests against the OWASP Core Rule Set (CRS).

Requests are:

- Logged
- Reported
- Allowed to continue

This mode is recommended during initial deployments to identify false positives before enforcing security policies.

---

### Prevention Mode

Prevention mode actively protects applications.

Malicious requests are:

- Blocked
- Logged
- Returned with an HTTP **403 Forbidden** response

Prevention mode is the recommended configuration for production environments after WAF rules have been validated.

> [!IMPORTANT]
> Deploying WAF in Detection mode first helps minimize service disruptions caused by incorrectly blocked legitimate traffic.

---

# Secure Internal Workloads

Backend services should remain private.

Recommendations:

- Use Internal Load Balancers.
- Combine with Network Security Groups.
- Use Private Endpoints where appropriate.
- Restrict management access.
- Minimize Public IP usage.

Internal services should not be directly accessible from the Internet.

---

# Monitor Continuously

Monitor application health and load balancing performance.

Recommended services:

- Azure Monitor
- Application Insights
- Azure Load Balancer metrics
- Application Gateway metrics
- Diagnostic Logs
- Activity Log

Configure alerts for:

- Unhealthy backend instances.
- Health Probe failures.
- High latency.
- Backend availability.
- Configuration changes.

---

# Plan for Scalability

Design architectures that support future growth.

Recommendations:

- Deploy multiple backend instances.
- Use Virtual Machine Scale Sets where appropriate.
- Select appropriate backend pool sizes.
- Leave subnet capacity for Application Gateway autoscaling.
- Review Azure Advisor recommendations.

Scaling should not require redesigning the architecture.

---

# Governance

Maintain consistent operational standards.

Recommendations:

- Standardize naming conventions.
- Apply Tags consistently.
- Protect production resources using Resource Locks.
- Review backend pools regularly.
- Audit frontend IP configurations.
- Document routing architecture.

---

# Cost Optimization

Optimize costs without sacrificing availability.

Recommendations:

- Remove unused frontend Public IP addresses.
- Delete unused backend pools.
- Remove obsolete NAT Rules.
- Use Internal Load Balancers where Internet access is unnecessary.
- Select appropriate SKUs based on workload.
- Review Azure Cost Management regularly.

---

# Enterprise Scenario

A global e-commerce platform deploys:

- Azure Application Gateway with WAF
- Azure Load Balancer
- Virtual Machine Scale Set
- Availability Zones
- Azure Monitor
- Application Insights

Application Gateway performs:

- TLS termination
- URL-based routing
- Web Application Firewall inspection

Azure Load Balancer distributes traffic across multiple backend Virtual Machines.

Health Probes automatically remove failed instances from service.

---

# Best Practices Checklist

- Select the appropriate load balancing service.
- Use Standard SKU resources.
- Configure Health Probes correctly.
- Deploy multiple backend instances.
- Use Availability Zones whenever possible.
- Prefer stateless application design.
- Use Application Gateway for HTTP/HTTPS workloads.
- Enable WAF for Internet-facing web applications.
- Secure backend workloads using Internal Load Balancers.
- Monitor backend health continuously.
- Review load balancing rules regularly.
- Document load balancing architecture.

---

# Common Pitfalls

- Choosing the wrong load balancing service.
- Using legacy Basic SKUs.
- Forgetting Health Probes.
- Deploying only one backend instance.
- Misconfiguring session persistence.
- Exposing backend services directly to the Internet.
- Forgetting WAF for public web applications.
- Ignoring monitoring and diagnostics.
- Using oversized or undersized backend pools.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Load Balancer
> - Azure Application Gateway
> - Public vs Internal Load Balancer
> - Health Probes
> - Backend Pools
> - Session Persistence
> - Standard SKU
> - Application Gateway WAF
> - High availability
> - Load balancing best practices

---

# Key Takeaways

- Azure Load Balancer and Azure Application Gateway serve different purposes and should be selected based on the application layer and traffic requirements.
- Health Probes are critical for maintaining high availability by ensuring traffic is sent only to healthy backend instances.
- Standard SKU resources provide better security, scalability, availability, and monitoring than legacy Basic SKUs.
- Stateless application design, continuous monitoring, and proper security controls improve scalability and operational resilience.
- Following Microsoft's load balancing best practices results in highly available, secure, and production-ready Azure applications.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Load Balancer documentation | https://learn.microsoft.com/azure/load-balancer/load-balancer-overview |
| Azure Load Balancer components | https://learn.microsoft.com/azure/load-balancer/components |
| Azure Application Gateway documentation | https://learn.microsoft.com/azure/application-gateway/overview |
| Azure Web Application Firewall | https://learn.microsoft.com/azure/web-application-firewall/ag/ag-overview |
| Azure Load Balancer health probes | https://learn.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview |
| Azure Well-Architected Framework – Load balancing | https://learn.microsoft.com/azure/well-architected/service-guides/load-balancer |
| Microsoft Learn – Improve application scalability with Azure Load Balancer | https://learn.microsoft.com/training/modules/improve-app-scalability-resiliency-with-load-balancer/ |
