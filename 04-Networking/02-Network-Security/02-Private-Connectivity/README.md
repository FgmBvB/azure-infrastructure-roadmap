# Azure Private Connectivity

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure private connectivity services, including Service Endpoints, Private Link, Private Endpoints, Private DNS integration, and Microsoft's recommended best practices for securing Azure PaaS services.

---

# Overview

Azure provides multiple mechanisms for securely connecting Virtual Networks to Azure services without exposing workloads unnecessarily to the public Internet.

The two primary technologies are:

- **Service Endpoints**
- **Private Endpoints (Azure Private Link)**

Although both improve security, they operate very differently and are designed for different scenarios.

Understanding these differences is essential for the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Differentiate Service Endpoints and Private Endpoints.
- Understand Azure Private Link.
- Configure Private Endpoints.
- Configure Private DNS Zones.
- Secure Azure PaaS services.
- Select the appropriate private connectivity solution.

---

# Azure Private Connectivity Architecture

```text
                     Azure Virtual Network
                              │
          ┌───────────────────┴───────────────────┐
          │                                       │
          ▼                                       ▼
 Service Endpoint                     Private Endpoint
          │                                       │
          ▼                                       ▼
 Azure Public Endpoint             Private IP Address
          │                                       │
          └──────────── Azure Backbone ───────────┘
                              │
                              ▼
                    Azure PaaS Services
```

---

# Service Endpoints

Service Endpoints extend the identity of a Virtual Network to supported Azure services.

Characteristics:

- Traffic remains on the Microsoft backbone network.
- Azure service still uses its **public endpoint**.
- Simple to configure.
- No additional private IP addresses are required.
- Access can be restricted to selected VNets.

Supported services include:

- Azure Storage
- Azure SQL Database
- Azure Key Vault
- Azure Cosmos DB

---

# Private Link

Azure Private Link is the platform that enables private access to Azure services through Private Endpoints.

Private Link provides:

- Private network connectivity
- Traffic isolation
- Elimination of Internet exposure
- Support for Microsoft services, customer services, and partner services

Private Link is the underlying technology behind Private Endpoints.

---

# Private Endpoints

A Private Endpoint creates a private network interface inside your Virtual Network.

Characteristics:

- Receives a private IP address.
- Connects directly to an Azure service.
- Traffic never traverses the public Internet.
- Integrates with Azure Private DNS.
- Can be protected using NSGs (where supported).

Example:

```text
Virtual Machine

↓

10.0.2.5

↓

Private Endpoint

↓

10.0.3.4

↓

Azure Storage Account
```

---

# Private DNS Integration

Private Endpoints typically require Azure Private DNS Zones.

Example:

```text
mystorage.blob.core.windows.net

↓

10.0.3.4
```

Applications continue using the normal Azure service name while DNS automatically resolves it to the private IP address.

Microsoft provides recommended Private DNS Zones for supported services.

---

# Service Endpoints vs Private Endpoints

| Feature | Service Endpoint | Private Endpoint |
|----------|-----------------|------------------|
| Public Endpoint | Yes | No |
| Private IP | No | Yes |
| Uses Azure Backbone | Yes | Yes |
| Internet Exposure | Public endpoint remains accessible | Private connectivity only (if public access is disabled) |
| DNS Changes Required | No | Usually Yes |
| Recommended for Production | Good | Best Practice |

---

# Enterprise Scenario

A company stores confidential financial documents in Azure Storage.

Instead of allowing access through the public endpoint, administrators deploy:

- Private Endpoint
- Private DNS Zone
- Network Security Groups

The Storage Account disables public network access.

Only resources inside authorized Virtual Networks can access the data.

---

# Best Practices

- Prefer Private Endpoints for production workloads.
- Disable public network access when using Private Endpoints.
- Use Azure Private DNS Zones.
- Restrict Service Endpoints to required VNets.
- Use least privilege networking.
- Monitor Private Endpoint connections.
- Document DNS dependencies.

---

# Common Pitfalls

- Confusing Service Endpoints with Private Endpoints.
- Forgetting to configure Private DNS.
- Leaving public access enabled unnecessarily.
- Assuming Service Endpoints create private IP addresses.
- Deploying Private Endpoints without validating DNS resolution.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Private Link
> - Private Endpoints
> - Service Endpoints
> - Private DNS
> - Azure Backbone
> - Public vs Private connectivity
> - Production networking recommendations

---

# Key Takeaways

- Service Endpoints secure access to Azure services while continuing to use public endpoints.
- Private Endpoints provide true private connectivity by assigning private IP addresses within a Virtual Network.
- Azure Private Link is the platform that enables Private Endpoints.
- Private DNS is a critical component of Private Endpoint deployments.
- Microsoft recommends Private Endpoints for highly secure production environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Private Link overview | https://learn.microsoft.com/azure/private-link/private-link-overview |
| Azure Private Endpoint | https://learn.microsoft.com/azure/private-link/private-endpoint-overview |
| Azure Virtual Network Service Endpoints | https://learn.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview |
| Azure Private DNS | https://learn.microsoft.com/azure/dns/private-dns-overview |
| DNS configuration for Private Endpoints | https://learn.microsoft.com/azure/private-link/private-endpoint-dns |
| Microsoft Learn – Secure Azure services with Private Link | https://learn.microsoft.com/training/modules/secure-azure-services-with-private-link/ |
