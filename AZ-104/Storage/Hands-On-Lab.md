# Azure Storage Hands-On Lab

## Overview

This document provides the hands-on implementation guide for Azure Storage services as part of the AZ-104 certification and the Patel Platform Service Template (PPST) cloud migration roadmap.

The goal is to understand Azure Storage by building real resources in Azure, validating them through the Azure Portal and Azure CLI, documenting the implementation, and relating each service to production backend applications.

---

# Learning Objectives

By completing these labs, you will be able to:

- Create and manage Azure Storage Accounts
- Configure Blob Storage
- Work with Queue Storage
- Create Azure File Shares
- Use Azure Table Storage
- Understand Managed Disks
- Secure Azure Storage
- Monitor Azure Storage resources
- Integrate Azure Storage with PPST services

---

# Prerequisites

- Azure Subscription
- Azure Portal access
- Azure CLI installed
- Git
- GitHub account

Repository:

```
patel-azure-labs
```

Reference Documentation:

```
patel-engineering-standards
```

---

# Storage Architecture

```
Azure Subscription
        │
        ▼
Resource Group
        │
        ▼
Storage Account
        │
        ├───────────────┐
        ▼               ▼
 Blob Storage      Queue Storage
        │               │
        ▼               ▼
 Documents       Background Jobs
        │               │
        └──────┬────────┘
               ▼
       PPST Data Ingestion Pipeline
               │
               ▼
        PostgreSQL + pgvector
```

---

# Lab 01 – Azure Storage Account

## Objective

Create an Azure Storage Account and understand the foundational storage resource.

## Azure Portal Tasks

- Create Resource Group
- Create Storage Account
- Configure Standard_LRS redundancy
- Review networking options
- Review security settings
- Add tags
- Validate deployment

## Azure CLI

```bash
az group create \
  --name rg-ppst-storage-lab \
  --location southcentralus

az storage account create \
  --name stppstlab001 \
  --resource-group rg-ppst-storage-lab \
  --location southcentralus \
  --sku Standard_LRS
```

## Validation Checklist

- [ ] Resource Group created
- [ ] Storage Account created
- [ ] Deployment succeeded
- [ ] Activity Log verified
- [ ] Screenshots captured

---

# Lab 02 – Azure Blob Storage

## Objective

Store application files using Azure Blob Storage.

## Azure Portal Tasks

- Create Blob Container
- Upload Markdown files
- View blob properties
- Generate SAS token
- Test blob access

## Azure CLI

```bash
az storage container create \
  --name documents \
  --account-name stppstlab001 \
  --auth-mode login

az storage blob upload \
  --account-name stppstlab001 \
  --container-name documents \
  --name Blob-Storage.md \
  --file Blob-Storage.md \
  --auth-mode login
```

## Validation Checklist

- [ ] Container created
- [ ] Blob uploaded
- [ ] Blob accessible
- [ ] SAS tested
- [ ] Activity Log verified

---

# Lab 03 – Queue Storage

## Objective

Create Azure Queue Storage for asynchronous messaging.

Topics:

- Create Queue
- Send Message
- Receive Message
- Delete Message

PPST Integration:

Background ingestion jobs.

---

# Lab 04 – Managed Disks

## Objective

Understand Azure VM disk storage.

Topics:

- OS Disk
- Data Disk
- Disk Performance
- Snapshots

---

# Lab 05 – Azure Files

## Objective

Create SMB file shares.

Topics:

- File Share
- Mount Share
- Access Control

---

# Lab 06 – Azure Table Storage

## Objective

Store NoSQL key-value data.

Topics:

- Tables
- Partitions
- Row Keys

---

# Lab 07 – Storage Security

Topics

- SAS Tokens
- RBAC
- Microsoft Entra ID
- HTTPS Only
- Firewalls
- Private Endpoints
- Encryption

---

# Lab 08 – Storage Monitoring

Topics

- Activity Log
- Azure Monitor
- Metrics
- Diagnostic Settings
- Alerts

---

# PPST Integration

Azure Storage services will support future PPST deployments.

Examples include:

Blob Storage

- Document uploads
- PDF storage
- DOCX storage
- Markdown storage

Queue Storage

- Background ingestion
- Worker processing
- Retry mechanism

Azure Files

- Shared application files

Table Storage

- Lightweight metadata

---

# Deliverables

By the end of this sprint, you should have:

- Azure Portal implementation
- Azure CLI implementation
- Screenshots
- GitHub documentation
- Engineering notes
- PPST architecture mapping

---

# Lessons Learned

Document observations after completing each lab.

Example:

- Storage Accounts are the parent resource for all Azure Storage services.
- Blob Containers store unstructured data.
- Queue Storage enables asynchronous processing.
- Azure Activity Log is useful for deployment validation.
- SAS tokens provide time-limited access to blobs.

---

# References

- Azure Portal
- Azure CLI
- Microsoft Learn
- AZ-104 Study Guide
- Patel Engineering Standards
- Patel Azure Labs