# Azure Managed Disks

## Overview

Azure Managed Disks are persistent block-level storage volumes used by Azure Virtual Machines (VMs).

Unlike Blob Storage, which stores files and objects, Managed Disks function like physical hard drives or SSDs attached to a server.

Azure automatically manages the storage infrastructure, replication, availability, and scalability, allowing engineers to focus on applications instead of storage management.

---

# Why Managed Disks Exist

Every Virtual Machine requires storage for:

- Operating System
- Applications
- Configuration
- Logs
- Databases
- Temporary files

Traditional infrastructure required administrators to manage physical disks manually.

Azure Managed Disks eliminate that complexity.

---

# Architecture

```
Azure Subscription

        │

        ▼

Resource Group

        │

        ▼

Virtual Machine

        │

 ┌──────┴──────┐

 ▼             ▼

OS Disk    Data Disk(s)

        │

        ▼

Azure Managed Disks
```

---

# Types of Managed Disks

Azure provides several disk options.

## Standard HDD

- Magnetic storage
- Lowest cost
- Highest latency
- Development environments
- Backup workloads
- Rarely accessed data

Best For:

- Test environments
- Archive workloads

---

## Standard SSD

- Solid State Drive
- Better performance
- Lower latency
- Cost effective

Best For:

- Web servers
- Small production workloads
- Development VMs

---

## Premium SSD

Enterprise SSD storage designed for production applications.

Features:

- High IOPS
- Low latency
- Predictable performance

Best For:

- SQL Server
- PostgreSQL
- Enterprise applications
- High-traffic APIs

---

## Premium SSD v2

Improved version of Premium SSD.

Advantages:

- Adjustable IOPS
- Adjustable throughput
- Better price-performance

Suitable for modern production workloads.

---

## Ultra Disk

Highest-performance disk offering.

Features:

- Extremely low latency
- Very high IOPS
- Massive throughput

Used for:

- SAP HANA
- Oracle
- Enterprise databases
- Financial systems

---

# Disk Comparison

| Disk Type | Cost | Performance | Typical Use |
|------------|------|-------------|-------------|
| Standard HDD | Lowest | Low | Dev/Test |
| Standard SSD | Low | Medium | Small Production |
| Premium SSD | Medium | High | Production |
| Premium SSD v2 | Medium | Very High | Enterprise Production |
| Ultra Disk | Highest | Maximum | Mission Critical |

---

# Disk Types

Azure VMs typically use:

### OS Disk

Contains:

- Windows
- Linux
- Boot files
- Installed software

Every VM requires one OS disk.

---

### Data Disk

Stores:

- Databases
- Documents
- Application files
- User data

A VM can attach multiple data disks.

---

### Temporary Disk

Provides temporary local storage.

Characteristics:

- Fast
- Not persistent
- Data may be lost during maintenance or VM redeployment

Do NOT store important business data here.

---

# Managed Disk Features

Azure automatically provides:

- Encryption at rest
- High availability
- Durability
- Snapshots
- Incremental backups
- Monitoring
- Scaling

---

# Snapshots

Snapshots capture a point-in-time copy of a disk.

Example:

```
VM

↓

OS Disk

↓

Snapshot
```

Useful for:

- Backup
- Recovery
- Testing
- Migration

---

# Availability

Managed Disks can be used with:

- Availability Sets
- Availability Zones
- Azure Backup
- Azure Site Recovery

This improves resilience and disaster recovery.

---

# Security

Azure Managed Disks support:

- Server-side encryption
- Customer-managed keys
- Azure Key Vault integration
- Microsoft Entra ID
- RBAC

---

# Performance Metrics

Important concepts:

IOPS

Input/Output Operations Per Second.

Higher IOPS = More database operations.

---

Throughput

Amount of data transferred per second.

Measured in MB/s.

---

Latency

Time required to complete an operation.

Lower latency means faster application response.

---

# Azure Portal Walkthrough

1. Open Azure Portal

2. Create Virtual Machine

3. Select Disk tab

4. Choose disk type

Example:

```
Premium SSD
```

5. Add additional Data Disks

6. Review performance

---

# Azure CLI

Create Managed Disk

```bash
az disk create \
    --resource-group myResourceGroup \
    --name MyDisk \
    --size-gb 128 \
    --sku Premium_LRS
```

List Disks

```bash
az disk list \
    --resource-group myResourceGroup
```

Attach Disk

```bash
az vm disk attach \
    --resource-group myResourceGroup \
    --vm-name MyVM \
    --name MyDisk
```

---

# PPST Integration

Current deployment:

```
Docker

↓

Local PostgreSQL
```

Future Azure deployment:

```
Azure VM

↓

Premium SSD

↓

PostgreSQL

↓

PPST Services
```

Eventually PPST will migrate to Azure Database for PostgreSQL, where Microsoft manages the underlying storage.

---

# Best Practices

- Choose the correct disk type
- Separate OS and Data disks
- Use Premium SSD for production databases
- Monitor disk performance
- Use snapshots before major upgrades
- Encrypt sensitive workloads
- Right-size storage capacity

---

# AZ-104 Exam Tips

Know which disk fits each workload.

Choose:

Standard HDD

- Lowest cost
- Development
- Backup

Standard SSD

- General purpose
- Moderate workloads

Premium SSD

- Production databases
- Enterprise applications

Ultra Disk

- Mission-critical
- Highest performance

---

# Interview Questions

### What is an Azure Managed Disk?

A fully managed block storage service for Azure Virtual Machines.

---

### Why use Managed Disks?

Azure manages storage infrastructure, availability, replication, and scalability automatically.

---

### Difference between Blob Storage and Managed Disks?

Blob Storage stores objects like PDFs, images, and videos.

Managed Disks provide block storage for operating systems and virtual machines.

---

### What is the difference between an OS Disk and a Data Disk?

The OS Disk contains the operating system and boot files.

The Data Disk stores application and business data.

---

# PPST Engineering Notes

Current PPST primarily uses Docker containers and PostgreSQL.

As the platform grows, workloads may run on:

```
Azure Container Apps

Azure Kubernetes Service

Azure Virtual Machines
```

Managed Disks become important whenever applications or databases require persistent block storage on Azure VMs.

---

# Summary

Azure Managed Disks provide secure, durable, high-performance block storage for Azure Virtual Machines.

Choosing the correct disk type helps balance cost, performance, and reliability.

For PPST, Managed Disks are most relevant when running self-managed databases or services on Azure Virtual Machines, while managed Azure database services abstract much of this storage management.