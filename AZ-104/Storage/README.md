# Azure Storage

## Overview

Azure Storage is Microsoft's scalable, durable, and highly available cloud storage platform.

It provides multiple storage services for structured data, unstructured data, files, messaging, and disks.

Azure Storage is designed to support enterprise applications with high durability, security, and scalability.

---

# Engineering Objectives

Azure Storage should provide:

- High availability
- Durability
- Scalability
- Security
- Cost efficiency
- Disaster recovery

---

# Azure Storage Services

Azure Storage consists of several services.

| Service | Purpose |
|----------|---------|
| Blob Storage | Store unstructured data such as documents, images, videos, and backups |
| Azure Files | Managed file shares using SMB |
| Queue Storage | Message queues for asynchronous communication |
| Table Storage | NoSQL key-value storage |
| Managed Disks | Persistent disks for Azure Virtual Machines |

---

# Blob Storage

Blob Storage is the primary object storage service in Azure.

Common use cases:

- Documents
- Images
- PDFs
- Videos
- Application uploads
- AI training datasets
- Backup files

Example:

```
Storage Account
        │
        ▼
Container
        │
        ├── invoice.pdf
        ├── image.jpg
        └── report.docx
```

---

# Storage Accounts

Every Azure Storage resource belongs to a Storage Account.

A Storage Account provides:

- Authentication
- Authorization
- Encryption
- Monitoring
- Replication
- Networking

Example naming convention:

```
stppstdev001
stppstprod001
```

---

# Storage Containers

Blob Storage organizes objects into containers.

Example:

```
uploads
documents
images
backups
logs
```

Containers help organize application data.

---

# Redundancy Options

Azure provides multiple replication strategies.

| Replication | Description |
|-------------|-------------|
| LRS | Locally Redundant Storage |
| ZRS | Zone-Redundant Storage |
| GRS | Geo-Redundant Storage |
| GZRS | Geo-Zone-Redundant Storage |

Choose the replication strategy based on business continuity requirements.

---

# Security

Azure Storage supports:

- Microsoft Entra ID authentication
- Managed Identity
- RBAC
- Shared Access Signatures (SAS)
- Storage Account Keys
- Private Endpoints
- Encryption at Rest
- Encryption in Transit

Engineering preference:

```
Managed Identity
        ↓
RBAC
        ↓
Private Endpoint
```

Avoid embedding Storage Account Keys inside applications whenever possible.

---

# Networking

Storage Accounts should be protected using:

- Private Endpoints
- Firewall Rules
- Virtual Networks
- Network Security Groups

Public access should be minimized whenever possible.

---

# Lifecycle Management

Azure Storage supports lifecycle rules.

Example:

```
30 Days
↓

Move to Cool Tier

↓

90 Days

↓

Archive Tier

↓

365 Days

↓

Delete
```

Lifecycle policies help reduce storage costs.

---

# Monitoring

Monitor Storage Accounts using:

- Azure Monitor
- Metrics
- Diagnostic Logs
- Alerts
- Azure Activity Logs

Monitor:

- Capacity
- Transactions
- Availability
- Latency
- Errors

---

# Engineering Best Practices

- Use Managed Identity
- Enable RBAC
- Prefer Private Endpoints
- Encrypt data
- Enable soft delete
- Configure lifecycle policies
- Monitor storage usage
- Use appropriate redundancy
- Separate production and development storage accounts

---

# PPST Storage Standard

Every PPST-based service should:

- Store uploaded files in Azure Blob Storage
- Authenticate using Managed Identity
- Use Azure RBAC
- Avoid embedded storage keys
- Enable encryption
- Use lifecycle management
- Protect Storage Accounts with Private Endpoints when applicable

---

# Engineering Checklist

- Storage Account created
- Naming standard followed
- Blob Containers created
- Managed Identity configured
- RBAC assigned
- Encryption enabled
- Lifecycle policy configured
- Monitoring enabled
- Backup strategy documented