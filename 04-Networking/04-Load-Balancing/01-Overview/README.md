# Azure Load Balancing Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Load Balancer, Azure Application Gateway, load balancing concepts, health probes, traffic distribution, and Microsoft's recommended architectures for highly available applications.

---

# Overview

Highly available applications require traffic to be distributed across multiple backend resources.

Azure provides two primary load balancing services:

- **Azure Load Balancer (Layer 4)**
- **Azure Application Gateway (Layer 7)**

Although both distribute traffic across multiple servers, they operate at different OSI layers and solve different problems.

Understanding when to use each service is an important objective of the **AZ-104** certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Load Balancer.
- Differentiate Public and Internal Load Balancers.
- Understand Health Probes.
- Configure Load Balancing Rules.
- Understand Azure Application Gateway.
- Differentiate Layer 4 and Layer 7 load balancing.
- Compare Azure Load Balancer and Application Gateway.
- Select the appropriate service for production workloads.

---

# Azure Load Balancing Architecture

```text
                   Internet
                       │
         ┌─────────────┴─────────────┐
         │                           │
         ▼                           ▼
 Azure Load Balancer       Azure Application Gateway
    (Layer 4)                     (Layer 7)
         │                           │
         ▼                           ▼
     Backend Pool               Backend Pool
         │                           │
         ▼                           ▼
      Virtual Machines / App Services
```

---

# Azure Load Balancer

Azure Load Balancer is a fully managed **Layer 4 (Transport Layer)** load balancer.

It distributes traffic based on:

- Source IP
- Destination IP
- Source Port
- Destination Port
- Protocol (TCP/UDP)

It does **not** inspect HTTP headers or URLs.

Typical workloads include:

- Virtual Machines
- Virtual Machine Scale Sets
- Network Virtual Appliances
- High-performance TCP/UDP services

---

# Public vs Internal Load Balancer

## Public Load Balancer

Receives traffic from the Internet.

Example:

```text
Internet

↓

Public IP

↓

Azure Load Balancer

↓

Backend Pool
```

Typical use cases:

- Public websites
- APIs
- Internet-facing services

---

## Internal Load Balancer

Receives traffic only inside private networks.

Example:

```text
Application Tier

↓

Internal Load Balancer

↓

Database Tier
```

Typical use cases:

- Multi-tier applications
- Internal APIs
- Backend services

---

# Backend Pools

Backend Pools contain the resources that receive traffic.

Supported resources include:

- Virtual Machines
- Virtual Machine Scale Sets
- IP addresses
- Network Interfaces

Azure distributes traffic only to healthy backend instances.

---

# Health Probes

Health Probes continuously monitor backend availability.

Supported protocols:

- TCP
- HTTP
- HTTPS

If a backend instance fails the configured probe, Azure automatically removes it from traffic distribution until it becomes healthy again.

Health Probes are fundamental for high availability.

---

# Load Balancing Rules

Load Balancing Rules define how traffic is distributed.

A rule specifies:

- Frontend IP
- Backend Pool
- Health Probe
- Protocol
- Frontend Port
- Backend Port

Example:

```text
Frontend:

443

↓

Backend:

443

↓

HTTPS Servers
```

---

# Inbound NAT Rules

Inbound NAT Rules map a unique frontend port to a specific backend instance.

Example:

```text
Public IP

↓

33891

↓

VM01 (RDP)

Public IP

↓

33892

↓

VM02 (RDP)
```

Useful for administrative access without assigning Public IP addresses to every VM.

---

# Session Persistence

Azure Load Balancer supports optional session persistence.

Available modes include:

- None
- Client IP
- Client IP and Protocol

Session persistence helps maintain user affinity across multiple requests.

---

# High Availability Ports

HA Ports allow Azure Load Balancer to balance all TCP and UDP ports.

Typical use cases:

- Network Virtual Appliances
- Firewalls
- High-performance networking scenarios

---

# Azure Application Gateway

Azure Application Gateway is a fully managed **Layer 7 (Application Layer)** load balancer.

Unlike Azure Load Balancer, it understands HTTP and HTTPS traffic.

Capabilities include:

- URL-based routing
- Host-based routing
- Cookie-based session affinity
- SSL/TLS termination
- Web Application Firewall (WAF)
- End-to-end TLS
- HTTP header inspection

---

# Web Application Firewall (WAF)

Application Gateway can include Web Application Firewall (WAF).

WAF protects web applications against attacks such as:

- SQL Injection
- Cross-Site Scripting (XSS)
- HTTP protocol attacks
- OWASP Top 10 vulnerabilities

WAF is recommended for Internet-facing web applications.

---

# Azure Load Balancer vs Application Gateway

| Feature | Azure Load Balancer | Application Gateway |
|----------|--------------------|---------------------|
| OSI Layer | Layer 4 | Layer 7 |
| Protocols | TCP / UDP | HTTP / HTTPS / WebSocket |
| URL Routing | No | Yes |
| Host-based Routing | No | Yes |
| SSL Termination | No | Yes |
| Web Application Firewall | No | Yes |
| Session Affinity | Basic | Cookie-based |
| Primary Use | Network traffic | Web applications |

---

# Enterprise Scenario

A company deploys an e-commerce platform.

Internet users connect through:

```text
Internet

↓

Application Gateway (WAF)

↓

Azure Load Balancer

↓

Virtual Machine Scale Set
```

Application Gateway performs:

- SSL termination
- URL routing
- Web Application Firewall inspection

Azure Load Balancer distributes TCP traffic across the backend Virtual Machines.

---

# Best Practices

- Use Standard SKU Load Balancer.
- Use Health Probes for every backend service.
- Remove unhealthy instances automatically.
- Use Internal Load Balancers for backend tiers.
- Deploy Application Gateway for HTTP/HTTPS workloads.
- Enable WAF for Internet-facing applications.
- Use Availability Zones where supported.
- Monitor backend health continuously.

---

# Common Pitfalls

- Confusing Azure Load Balancer with Application Gateway.
- Forgetting Health Probes.
- Using Public Load Balancers unnecessarily.
- Assuming Layer 4 devices inspect HTTP traffic.
- Forgetting WAF for public web applications.
- Leaving unhealthy backend instances in production.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Load Balancer
> - Public vs Internal Load Balancer
> - Backend Pools
> - Health Probes
> - Load Balancing Rules
> - Inbound NAT Rules
> - Session Persistence
> - Azure Application Gateway
> - Web Application Firewall (WAF)
> - Azure Load Balancer vs Application Gateway

---

# Key Takeaways

- Azure Load Balancer distributes TCP and UDP traffic at Layer 4 and is ideal for infrastructure workloads.
- Azure Application Gateway operates at Layer 7 and provides intelligent routing for web applications.
- Health Probes ensure traffic is sent only to healthy backend resources.
- Application Gateway with WAF protects web applications against common attacks while enabling advanced HTTP routing.
- Choosing the correct load balancing service depends on the application protocol, routing requirements, and security needs.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Load Balancer documentation | https://learn.microsoft.com/azure/load-balancer/load-balancer-overview |
| Azure Load Balancer components | https://learn.microsoft.com/azure/load-balancer/components |
| Azure Application Gateway documentation | https://learn.microsoft.com/azure/application-gateway/overview |
| Azure Web Application Firewall | https://learn.microsoft.com/azure/web-application-firewall/ag/ag-overview |
| Azure Load Balancer FAQ | https://learn.microsoft.com/azure/load-balancer/load-balancer-faqs |
| Azure Well-Architected Framework – Load balancing | https://learn.microsoft.com/azure/well-architected/service-guides/load-balancer |
| Microsoft Learn – Improve application scalability with Azure Load Balancer | https://learn.microsoft.com/training/modules/improve-app-scalability-resiliency-with-load-balancer/ |
