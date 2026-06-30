# Azure DNS

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure DNS, name resolution inside Virtual Networks, Azure Private DNS, Azure DNS Zones, custom DNS servers, and DNS integration with Azure networking services.

---

# Overview

The **Domain Name System (DNS)** translates human-readable domain names into IP addresses.

Azure provides built-in DNS services for internal name resolution and offers managed public and private DNS services for enterprise environments.

Proper DNS configuration is essential for communication between Azure resources, hybrid networks, and Internet-facing applications.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure DNS.
- Differentiate Public and Private DNS Zones.
- Understand Azure-provided DNS.
- Configure Custom DNS Servers.
- Understand Private DNS Zone linking.
- Choose the appropriate DNS solution for different scenarios.

---

# Azure DNS Architecture

```text
                    Azure DNS
                        │
        ┌───────────────┴───────────────┐
        │                               │
        ▼                               ▼
 Public DNS Zones               Private DNS Zones
        │                               │
 Internet Clients           Virtual Networks
                                        │
                                 Azure Resources
```

---

# Azure-Provided DNS

Every Virtual Network automatically receives Azure-provided DNS.

Characteristics:

- No configuration required.
- Automatically resolves Azure hostnames.
- Available only inside the Virtual Network.
- Supports name resolution between Azure resources.

The Azure DNS virtual server is always reachable using:

```text
168.63.129.16
```

This virtual IP address is provided by Azure and is available in every region.

---

## Azure DNS Virtual IP

Azure provides the virtual IP address:

```text
168.63.129.16
```

This address is a special Azure platform virtual IP used for multiple infrastructure services, including:

- Azure-provided DNS
- Load Balancer health probes
- Virtual Machine Agent communication
- Platform monitoring services

Characteristics:

- Available in every Azure region.
- Accessible only from within Azure Virtual Networks.
- Not reachable from on-premises networks through VPN or ExpressRoute.

> [!IMPORTANT]
> Do not block **168.63.129.16** with Network Security Groups, Azure Firewall, or guest operating system firewalls unless explicitly required and fully understood, as doing so can disrupt Azure platform functionality.

---

# Public DNS Zones

Azure DNS Public Zones host Internet-accessible DNS records.

Common record types include:

| Record | Purpose |
|---------|---------|
| A | Maps hostname to IPv4 address |
| AAAA | Maps hostname to IPv6 address |
| CNAME | Alias to another hostname |
| MX | Mail routing |
| TXT | Verification and security |
| NS | Name server delegation |
| SOA | Zone authority information |
| PTR | Reverse DNS lookup |

Example:

```text
www.contoso.com

↓

52.168.x.x
```

---

# Private DNS Zones

Private DNS Zones provide internal name resolution for Azure Virtual Networks.

Characteristics:

- Accessible only from linked VNets.
- Not published to the Internet.
- Automatically resolve private endpoints.
- Support hybrid environments.

Example:

```text
database.contoso.local

↓

10.0.2.4
```

---

# Virtual Network Links

Private DNS Zones become available through **Virtual Network Links**.

Two types exist:

| Link Type | Description |
|-----------|-------------|
| Registration | Azure automatically registers VM hostnames |
| Resolution | DNS queries only |

Registration links can be configured for only one VNet per zone.

Resolution links support multiple VNets.

---

## Private DNS Auto-Registration

Azure Private DNS can automatically create and remove DNS records for Virtual Machines.

Important considerations:

- A Virtual Network can be linked to multiple Private DNS Zones for name resolution.
- Only one Private DNS Zone can enable **auto-registration** for a given Virtual Network.
- DNS records are automatically updated when supported Virtual Machines are created or deleted.

This simplifies internal name resolution without requiring manual DNS administration.

> [!TIP]
> Use auto-registration for Virtual Machine hostnames and standard Azure workloads. Additional DNS records can always be managed manually when required.

---

# Azure Private DNS

Azure Private DNS simplifies internal name resolution.

Benefits include:

- No DNS server maintenance.
- High availability.
- Automatic replication.
- Native integration with Azure networking.
- Supports Private Endpoints.

Private DNS is commonly used with:

- Private Endpoints
- Azure SQL Database
- Azure Storage
- Azure Key Vault
- Azure App Service

---

# Custom DNS Servers

Organizations may use their own DNS servers.

Common scenarios:

- Active Directory Domain Services
- Hybrid environments
- Existing enterprise DNS infrastructure
- Custom forwarding rules

Custom DNS servers can run:

- On Azure Virtual Machines.
- On-premises.
- In another cloud environment.

---

## DNS Configuration Precedence

Azure resolves DNS configuration using the following precedence:

1. DNS settings configured on the Network Interface (NIC).
2. DNS settings configured on the Virtual Network.
3. Azure-provided DNS.

If no custom configuration exists, Azure automatically uses the Azure-provided DNS service.

---

### Applying DNS Changes

Changing the DNS server configuration of a Virtual Network does not immediately update existing Virtual Machines.

The new DNS settings are obtained through DHCP.

To apply the new configuration, administrators should:

- Restart the Virtual Machine, or
- Renew the DHCP lease from within the guest operating system.

Until the DHCP configuration is refreshed, Virtual Machines continue using their previous DNS server settings.

> [!IMPORTANT]
> Plan DNS migrations carefully to avoid temporary name resolution issues during infrastructure changes.

# DNS Resolution Flow

```text
Application

      │

      ▼

DNS Query

      │

      ▼

Azure DNS
or
Custom DNS Server

      │

      ▼

Resolved IP Address
```

---

# Enterprise Scenario

A company deploys Active Directory Domain Services on Azure Virtual Machines.

All Virtual Networks are configured to use the domain controllers as custom DNS servers.

Private DNS Zones are used for Azure Private Endpoints, allowing internal resources to resolve Azure services without exposing traffic to the Internet.

---

# Best Practices

- Use Azure-provided DNS for simple environments.
- Use Private DNS Zones with Private Endpoints.
- Configure redundant Custom DNS Servers.
- Link Private DNS Zones only where required.
- Avoid exposing internal names publicly.
- Document DNS architecture.

---

# Common Pitfalls

- Forgetting to configure Custom DNS after deploying Active Directory.
- Assuming Private DNS Zones are accessible from the Internet.
- Not linking VNets to Private DNS Zones.
- Mixing internal and public namespaces incorrectly.
- Using a single DNS server without redundancy.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure-provided DNS
> - Azure DNS Zones
> - Public DNS
> - Private DNS
> - Virtual Network Links
> - Registration vs Resolution
> - Custom DNS
> - Name resolution

---

# Key Takeaways

- Azure provides built-in DNS services for every Virtual Network.
- Public DNS Zones publish records to the Internet.
- Private DNS Zones provide secure internal name resolution.
- Custom DNS integrates Azure with enterprise environments.
- Proper DNS design is essential for scalable, secure, and reliable Azure networking.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure DNS documentation | https://learn.microsoft.com/azure/dns/ |
| Azure DNS overview | https://learn.microsoft.com/azure/dns/dns-overview |
| Azure Private DNS | https://learn.microsoft.com/azure/dns/private-dns-overview |
| Name resolution for Azure resources | https://learn.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances |
| Azure Private Endpoints DNS | https://learn.microsoft.com/azure/private-link/private-endpoint-dns |
| Microsoft Learn – Host your domain on Azure DNS | https://learn.microsoft.com/training/modules/host-domain-azure-dns/ |
