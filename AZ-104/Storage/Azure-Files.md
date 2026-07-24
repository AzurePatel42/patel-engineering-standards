# Azure Files

## Objective

Understand Azure Files, its architecture, use cases, authentication methods, and how it differs from Blob Storage.

---

# What is Azure Files?

Azure Files is a fully managed file share service in Azure that provides shared storage using the SMB (Server Message Block) and NFS protocols.

Unlike Blob Storage, Azure Files behaves like a traditional network file share.

Example:

Employee Laptop
        │
SMB Share
        │
Azure Files

---

# Why Azure Files?

Many applications expect a shared file system.

Instead of managing your own Windows File Server, Azure provides one as a managed service.

Common uses:

- Shared documents
- Lift-and-shift applications
- Home directories
- Configuration files
- Application shared storage

---

# Azure Files Architecture

Azure Storage Account
        │
File Share
        │
Folders
        │
Files

Example:

Storage Account

↓

engineering-share

↓

Projects

↓

PPST

↓

README.md

---

# Supported Protocols

- SMB 3.x
- NFS 4.1 (Premium)

SMB is the most common protocol.

---

# Authentication

Azure Files supports:

- Storage Account Keys
- Shared Access Signatures (SAS)
- Microsoft Entra ID
- Azure AD DS
- On-premises Active Directory

---

# Azure Files vs Blob Storage

| Feature | Azure Files | Blob Storage |
|----------|-------------|--------------|
| File System | ✅ | ❌ |
| SMB Support | ✅ | ❌ |
| HTTP Access | Limited | ✅ |
| Images | ❌ | ✅ |
| Videos | ❌ | ✅ |
| PDFs | ✅ | ✅ |
| Mount as Drive | ✅ | ❌ |
| AI Dataset Storage | Limited | ✅ |

---

# Performance Tiers

Standard

- HDD
- Lower cost

Premium

- SSD
- Low latency
- High IOPS

---

# Security

- Encryption at Rest
- Encryption in Transit
- Private Endpoints
- RBAC
- Microsoft Entra ID
- Azure Backup

---

# PPST Integration

Example 1

Application Logs

↓

Azure Files

↓

Mounted by Containers

--------------------

Example 2

Shared Configuration

↓

Azure Files

↓

Multiple Services

--------------------

Example 3

Temporary Uploads

↓

Azure Files

↓

Processing Service

↓

Blob Storage

---

# Best Practices

- Use Blob Storage for object storage.
- Use Azure Files for shared file systems.
- Prefer Microsoft Entra ID authentication.
- Use Private Endpoints in production.
- Enable backups for critical shares.

---

# Blob Storage vs Azure Files

Choose Blob Storage when:

- Images
- Videos
- PDFs
- AI datasets
- Object storage

Choose Azure Files when:

- Shared folders
- Network drives
- Legacy applications
- Lift-and-shift migrations

---

# AZ-104 Exam Tips

Remember:

Blob = Object Storage

Azure Files = Network File Share

Managed Disk = VM Disk

Queue = Messaging

Table = NoSQL

Microsoft frequently tests choosing the correct storage service for a scenario.

---

# Key Takeaways

✔ Azure Files is a managed file share.

✔ Supports SMB and NFS.

✔ Can be mounted like a network drive.

✔ Ideal for shared application storage.

✔ Not a replacement for Blob Storage.