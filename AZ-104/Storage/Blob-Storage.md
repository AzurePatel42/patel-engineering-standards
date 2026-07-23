# Azure Blob Storage

## Overview

Azure Blob Storage is Microsoft's object storage service designed to store massive amounts of unstructured data in the cloud. It is optimized for scalability, durability, security, and global accessibility.

Blob Storage is commonly used for storing images, videos, documents, backups, log files, datasets, application assets, and AI training data.

Blob stands for **Binary Large Object**, meaning it can store virtually any type of file regardless of its format.

---

## Purpose

Azure Blob Storage provides highly scalable and cost-effective object storage for modern cloud applications.

It enables organizations to:

- Store application files
- Host static websites
- Archive backups
- Store AI and machine learning datasets
- Manage media content
- Store application logs
- Support disaster recovery
- Deliver content globally

---

## Business Problem

Traditional file servers are expensive to maintain, difficult to scale, and require significant infrastructure management.

Organizations need storage that can:

- Scale automatically
- Handle billions of objects
- Provide high durability
- Offer global accessibility
- Integrate with cloud-native applications
- Reduce operational costs

Azure Blob Storage addresses these challenges by providing managed object storage with built-in redundancy, security, and lifecycle management.

---

# Azure Blob Storage Architecture

```
Azure Subscription
        │
        ▼
 Resource Group
        │
        ▼
 Storage Account
        │
        ▼
 Blob Service
        │
        ▼
 Container
        │
        ▼
 Blob
```

Hierarchy:

- Storage Account
- Blob Service
- Container
- Blob

---

## Blob Types

Azure supports three blob types.

### Block Blob

The most commonly used blob type.

Optimized for:

- Images
- Videos
- Documents
- Backups
- Static website files
- Application assets

Recommended for most workloads.

---

### Append Blob

Designed for append operations.

Typical use cases:

- Application logs
- Audit logs
- Monitoring data

Data can only be added to the end of the blob.

---

### Page Blob

Designed for random read/write operations.

Primary use:

- Azure Virtual Machine Managed Disks

---

## Containers

Containers organize blobs similarly to folders.

Example:

```
Storage Account
│
├── images
├── videos
├── backups
└── logs
```

Containers help organize application data and simplify access management.

---

## Access Tiers

Blob Storage supports multiple access tiers to optimize storage costs.

### Hot Tier

Best for:

- Frequently accessed data

Characteristics:

- Highest storage cost
- Lowest access cost

Examples:

- Active application files
- Current project documents

---

### Cool Tier

Best for:

- Infrequently accessed data

Characteristics:

- Lower storage cost
- Higher access cost

Examples:

- Monthly reports
- Older project files

---

### Cold Tier

Designed for data accessed very rarely.

Characteristics:

- Lower storage cost than Cool
- Higher retrieval costs
- Suitable for long-term storage

Examples:

- Compliance records
- Historical datasets

---

### Archive Tier

Lowest-cost storage option.

Characteristics:

- Offline storage
- Several hours required for retrieval
- Ideal for long-term retention

Examples:

- Regulatory archives
- Old backups
- Historical records

---

## Security

Azure Blob Storage provides enterprise-grade security.

Features include:

- Encryption at rest
- HTTPS-only access
- Microsoft Entra ID authentication
- Shared Access Signatures (SAS)
- Azure RBAC
- Customer-managed keys
- Immutable storage
- Soft delete
- Versioning

Always apply the principle of least privilege.

---

## Networking

Blob Storage supports:

- Public endpoints
- Private Endpoints
- Service Endpoints
- Storage firewalls
- Virtual Network integration

Production environments should restrict public network access whenever possible.

---

## Data Protection

Azure Blob Storage includes several protection mechanisms.

- Soft Delete
- Blob Versioning
- Point-in-Time Restore
- Snapshots
- Immutable Storage
- Object Replication

These features help recover from accidental deletion or corruption.

---

## Lifecycle Management

Lifecycle Management automatically moves or deletes blobs based on rules.

Typical workflow:

```
Hot
 ↓
Cool
 ↓
Cold
 ↓
Archive
 ↓
Delete
```

Benefits:

- Reduced storage costs
- Automated retention
- Compliance support

---

## Monitoring

Monitor Blob Storage using:

- Azure Monitor
- Diagnostic Logs
- Log Analytics
- Metrics
- Alerts

Important metrics include:

- Capacity
- Availability
- Transactions
- Latency
- Ingress
- Egress

---

## Best Practices

- Use Block Blobs for most applications.
- Organize data using logical containers.
- Enable versioning and soft delete.
- Configure lifecycle management.
- Restrict public access.
- Prefer Microsoft Entra ID over storage keys.
- Monitor storage utilization regularly.
- Choose the appropriate access tier.

---

## PPST Implementation

Blob Storage is a natural fit for several PPST services.

Potential implementations include:

- Data Ingestion Pipeline file uploads
- AI document storage
- RAG knowledge base source files
- Report generation
- Application backups
- Cost Intelligence exports
- Inventory images

Future PPST deployments should authenticate using Managed Identity and configure storage through environment variables.

---

## Common Mistakes

- Storing frequently accessed files in Archive tier
- Leaving containers publicly accessible
- Using account keys in application code
- Ignoring lifecycle policies
- Not enabling soft delete
- Not enabling versioning

---

## AZ-104 Exam Notes

Remember:

- Blob Storage stores unstructured data.
- Block Blob is the default choice.
- Blob Storage supports Hot, Cool, Cold, and Archive tiers.
- Containers organize blobs.
- Blob Storage supports lifecycle management.
- Soft Delete and Versioning improve recoverability.
- Blob Storage resides within a Storage Account.

---

## Interview Questions

### What is Azure Blob Storage?

Azure Blob Storage is Microsoft's scalable object storage service for storing unstructured data such as images, videos, documents, backups, and application assets.

---

### What are the three blob types?

- Block Blob
- Append Blob
- Page Blob

---

### Which blob type is used most often?

Block Blob.

It is optimized for storing documents, images, videos, backups, and most application files.

---

### What is the purpose of access tiers?

Access tiers reduce storage costs by matching storage pricing to how frequently data is accessed.

---

### What is the difference between Blob Storage and Azure Files?

Blob Storage is object storage accessed through REST APIs.

Azure Files provides managed file shares using SMB and NFS protocols.

---

## References

- Microsoft Learn – Azure Blob Storage
- Microsoft Learn – Blob Access Tiers
- Microsoft Learn – Lifecycle Management
- Microsoft Learn – Azure Storage Security
- Microsoft Learn – AZ-104: Manage Blob Storage