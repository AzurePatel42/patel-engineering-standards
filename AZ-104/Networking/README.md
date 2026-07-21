# Azure Networking

## Overview

Networking is the foundation of every Azure environment.

It determines how resources communicate securely with each other, with users, and with external services.

Every production deployment should begin with a well-designed network architecture.

---

# Engineering Objectives

Azure networking should provide:

- Secure communication
- Network isolation
- Controlled inbound traffic
- Controlled outbound traffic
- High availability
- Scalability

---

# Core Components

Azure networking consists of:

- Virtual Networks (VNets)
- Subnets
- Network Security Groups (NSGs)
- Route Tables
- Public IP Addresses
- Private Endpoints
- Azure DNS
- VPN Gateway
- ExpressRoute
- Load Balancer
- Application Gateway

---

# Virtual Network (VNet)

A Virtual Network provides an isolated private network inside Azure.

```
Internet
      │
      ▼
Azure Virtual Network (VNet)
      │
      ├── Subnet A
      ├── Subnet B
      └── Subnet C
```

Resources inside the same VNet can communicate securely.

---

# Subnets

Subnets divide a VNet into smaller logical networks.

Example:

```
VNet

├── Web
├── API
├── Database
└── Management
```

Subnets improve organization and security.

---

# Network Security Groups (NSGs)

NSGs act as virtual firewalls.

They control:

- Inbound traffic
- Outbound traffic

Example:

```
Internet
      │
Allow HTTPS
      │
     NSG
      │
API Subnet
```

Only required ports should be opened.

---

# Private Endpoints

Private Endpoints allow Azure services to be accessed using private IP addresses.

Example:

Application

↓

Private Endpoint

↓

Azure Storage

Traffic remains inside the Azure network.

---

# Azure DNS

Azure DNS provides name resolution for Azure resources.

Examples:

- Internal DNS
- Public DNS
- Private DNS Zones

---

# Load Balancing

Azure supports multiple load-balancing services.

Examples:

- Azure Load Balancer
- Application Gateway
- Front Door

Choose the service based on Layer 4 or Layer 7 requirements.

---

# Engineering Best Practices

- Minimize public exposure
- Use NSGs
- Prefer Private Endpoints
- Segment workloads with subnets
- Separate production and development
- Use Azure DNS
- Document network topology

---

# PPST Networking Standard

Every PPST deployment should:

- Deploy into a dedicated VNet
- Separate services into subnets where appropriate
- Protect workloads with NSGs
- Prefer Private Endpoints for Azure services
- Minimize public IP exposure

---

# Engineering Checklist

- VNet created
- Subnets designed
- NSGs configured
- Private Endpoints used where possible
- Public access minimized
- DNS configured
- Network documented