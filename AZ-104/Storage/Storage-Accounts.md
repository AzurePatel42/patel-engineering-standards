# Azure Storage Accounts

## Overview

An Azure Storage Account is the foundational resource that provides a unique namespace for storing and managing data in Azure. It serves as a secure, scalable, highly available container that hosts Azure Storage services such as Blob Storage, Azure Files, Queue Storage, and Table Storage.

Every object stored in Azure Storage belongs to a Storage Account. Before any application can store or retrieve data, a Storage Account must exist.

---

## Purpose

Azure Storage Accounts provide a unified platform for storing structured and unstructured data while offering enterprise-grade security, durability, scalability, and high availability.

They enable organizations to:

- Store application data
- Host static websites
- Archive backups
- Store logs and diagnostics
- Support analytics workloads
- Provide persistent storage for cloud-native applications

---

## Business Problem

Modern applications require storage systems that are:

- Highly available
- Globally accessible
- Secure
- Cost-effective
- Scalable without downtime

Traditional on-premises storage requires hardware procurement, maintenance, redundancy planning, and disaster recovery strategies.

Azure Storage Accounts eliminate this operational burden by providing managed cloud storage with built-in redundancy, encryption, monitoring, and lifecycle management.

---

# Azure Storage Architecture

```
                Azure Subscription
                        │
                        ▼
               Resource Group
                        │
                        ▼
               Storage Account
                        │
      ┌──────────┬──────────┬──────────┬──────────┐
      ▼          ▼          ▼          ▼
 Blob Storage  Azure Files  Queues    Tables
```

The Storage Account acts as the parent resource for all Azure Storage services.

---

## Storage Account Types

Azure supports several Storage Account types depending on workload requirements.

### General-purpose v2 (Standard)

Recommended for nearly all modern workloads.

Supports:

- Blob Storage
- Azure Files
- Queue Storage
- Table Storage
- Lifecycle Management
- Static Website Hosting

Best choice for production applications.

---

### Premium Block Blob Storage

Optimized for:

- Low latency
- High transaction rates
- Frequently accessed blobs

Use cases:

- Media streaming
- AI workloads
- Large-scale content delivery

---

### Premium FileStorage

Designed for Azure Files workloads requiring:

- SMB
- NFS
- High IOPS
- Low latency

---

### Premium Page Blob

Designed primarily for:

- Azure Virtual Machine managed disks

---

## Performance Tiers

### Standard

Uses HDD-backed infrastructure.

Advantages:

- Lower cost
- Suitable for most applications

---

### Premium

Uses SSD-backed infrastructure.

Advantages:

- Lower latency
- Higher throughput
- Consistent performance

Ideal for mission-critical workloads.

---

## Storage Services

A single Storage Account can host multiple storage services simultaneously.

| Service | Purpose |
|----------|----------|
| Blob Storage | Unstructured objects |
| Azure Files | SMB/NFS file shares |
| Queue Storage | Message queues |
| Table Storage | NoSQL key-value storage |

---

## Naming Rules

Storage Account names:

- Globally unique
- 3–24 characters
- Lowercase letters and numbers only
- No spaces
- No special characters

Example:

```
ppststorageprod01
```

---

## Security

Azure Storage Accounts provide multiple security capabilities.

- Encryption at rest (enabled by default)
- HTTPS-only traffic
- Microsoft Entra ID authentication
- Shared Access Signatures (SAS)
- Access Keys
- Azure RBAC
- Customer-managed keys (CMK)

Always follow the principle of least privilege.

---

## Networking

Storage Accounts can be configured with:

- Public endpoints
- Private Endpoints
- Service Endpoints
- Firewall rules
- Virtual Network restrictions

Production environments should avoid unrestricted public access whenever possible.

---

## Redundancy Options

Azure automatically replicates storage data.

Available options include:

- LRS
- ZRS
- GRS
- RA-GRS
- GZRS
- RA-GZRS

The appropriate option depends on business continuity requirements.

---

## Monitoring

Monitor Storage Accounts using:

- Azure Monitor
- Log Analytics
- Diagnostic Settings
- Metrics
- Alerts

Key metrics include:

- Availability
- Latency
- Transactions
- Capacity
- Egress
- Ingress

---

## Best Practices

- Use General-purpose v2 unless another type is specifically required.
- Enable secure transfer.
- Disable public access when unnecessary.
- Use Microsoft Entra ID instead of storage keys when possible.
- Implement lifecycle management.
- Configure redundancy based on business requirements.
- Monitor capacity and performance.
- Apply resource tags consistently.

---

## PPST Implementation

Within PPST, Azure Storage Accounts provide the storage foundation for cloud-native services.

Potential implementations include:

- Blob Storage for uploaded documents
- Queue Storage for asynchronous task processing
- Azure Files for shared application assets
- Diagnostic logs and backups

Future PPST deployments should externalize storage configuration using environment variables and Managed Identity instead of embedding secrets.

---

## Common Mistakes

- Using Storage Account keys in application code
- Leaving public access enabled
- Choosing incorrect redundancy
- Ignoring lifecycle policies
- Mixing production and development data
- Not enabling monitoring

---

## AZ-104 Exam Notes

Remember:

- General-purpose v2 is the recommended Storage Account type.
- Storage Account names are globally unique.
- Storage Accounts can contain multiple storage services.
- Replication options determine durability and availability.
- Secure transfer should be enabled.
- Microsoft Entra ID authentication is preferred over access keys.

---

## Interview Questions

### What is an Azure Storage Account?

A Storage Account is the top-level Azure resource that provides a secure, scalable namespace for Azure Storage services such as Blob Storage, Azure Files, Queue Storage, and Table Storage.

---

### Why is General-purpose v2 recommended?

Because it supports the full set of Azure Storage capabilities while offering the best balance of functionality, scalability, and cost.

---

### What is the difference between Standard and Premium Storage?

Standard uses HDD-backed storage and is optimized for cost.

Premium uses SSD-backed storage and is optimized for low latency and high performance.

---

### Can one Storage Account contain multiple storage services?

Yes. A single Storage Account can host Blob Storage, Azure Files, Queue Storage, and Table Storage simultaneously.

---

## References

- Microsoft Learn – Azure Storage Accounts
- Microsoft Learn – Azure Storage Redundancy
- Microsoft Learn – Azure Storage Security
- Microsoft Learn – AZ-104: Manage Azure Storage