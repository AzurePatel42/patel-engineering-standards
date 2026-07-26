# Azure Table Storage

## Overview

Azure Table Storage is a fully managed NoSQL key-value store designed for storing large volumes of structured, non-relational data.

Unlike SQL databases, Table Storage does not use schemas, joins, foreign keys, or relationships.

It is optimized for massive scalability, low cost, and fast key-based lookups.

---

# Why Table Storage Exists

Traditional SQL databases work well for relational data.

Example:

```
Customers
Orders
Products
Invoices
```

These require:

- Relationships
- Foreign Keys
- Joins
- ACID Transactions

However, many cloud applications simply need to store large amounts of structured data without relationships.

Examples:

- Device telemetry
- User preferences
- Application logs
- Metadata
- Configuration
- Session data

Azure Table Storage was built for these scenarios.

---

# Table Storage Architecture

```
Storage Account

        │

        ▼

Table

        │

        ▼

Entities (Rows)
```

Unlike SQL databases:

```
Database
    │
    ▼
Table
    │
    ▼
Row
```

Azure Table Storage uses:

```
Storage Account
        │
        ▼
Table
        │
        ▼
Entity
```

---

# Core Components

## Storage Account

Owns one or more tables.

---

## Table

A collection of entities.

Example:

```
Users

Logs

Telemetry

Settings
```

---

## Entity

Equivalent to a database row.

Example:

```json
{
    "PartitionKey": "Customer",
    "RowKey": "1001",
    "Name": "Mahesh Patel",
    "City": "Dallas",
    "Status": "Active"
}
```

---

# Partition Key

The Partition Key determines how Azure distributes data across storage partitions.

Example:

```
PartitionKey

Customer

Employee

Supplier
```

Entities with the same PartitionKey are stored together.

Benefits:

- Faster queries
- Better scalability
- Load balancing

---

# Row Key

The Row Key uniquely identifies an entity within a partition.

Example:

```
PartitionKey    RowKey

Customer        1001

Customer        1002

Customer        1003
```

The combination of:

```
PartitionKey + RowKey
```

forms the primary key.

---

# Querying Data

Fast lookup:

```
PartitionKey = Customer

RowKey = 1001
```

Slow lookup:

```
Find everyone named John
```

Table Storage is optimized for key-based access, not complex searching.

---

# Characteristics

- NoSQL
- Schema-less
- Highly scalable
- Low latency
- Massive capacity
- Low cost
- Automatic partitioning

---

# Advantages

- Extremely scalable
- Fast key lookups
- Cost effective
- Fully managed
- Simple API
- Handles billions of entities

---

# Limitations

- No joins
- No foreign keys
- Limited querying
- No stored procedures
- No relational constraints
- No complex transactions across partitions

---

# Table Storage vs PostgreSQL

| Azure Table Storage | PostgreSQL |
|----------------------|------------|
| NoSQL | Relational |
| Schema-less | Schema-based |
| No joins | Joins supported |
| Key-value lookups | Rich SQL queries |
| Massive scale | Strong relational features |
| Cheap | More expensive |
| Simple queries | Complex queries |

Choose PostgreSQL when relationships matter.

Choose Table Storage when scalability and simple lookups matter.

---

# Table Storage vs Cosmos DB Table API

| Table Storage | Cosmos DB |
|--------------|-----------|
| Lower cost | Higher cost |
| Storage Account | Cosmos DB Account |
| Basic performance | Global distribution |
| Regional | Multi-region |
| Basic SLA | Enterprise SLA |

Table Storage is suitable for many applications.

Cosmos DB is designed for globally distributed applications.

---

# Common Use Cases

- Application logs
- IoT telemetry
- User profiles
- Session state
- Product catalog metadata
- Device inventory
- Configuration data
- Audit logs

---

# PPST Integration

Current PPST primarily uses PostgreSQL.

```
Inventory API
        │
        ▼
PostgreSQL
```

Future opportunities for Table Storage include:

```
PPST

        │

        ├── User Sessions

        ├── Audit Logs

        ├── Worker Metadata

        ├── Job Status

        └── Configuration Cache
```

Business data continues to belong in PostgreSQL.

---

# Azure Portal Walkthrough

1. Open Azure Portal

2. Select Storage Account

3. Navigate to Tables

4. Create Table

Example:

```
applicationlogs
```

5. Add Entities

6. Query Entities

---

# Azure CLI

Create Table

```bash
az storage table create \
    --account-name <storage-account> \
    --name applicationlogs
```

List Tables

```bash
az storage table list \
    --account-name <storage-account>
```

---

# Best Practices

- Design good Partition Keys
- Keep entities small
- Query by PartitionKey
- Avoid table scans
- Store related entities together
- Use RowKey for unique identification
- Design for horizontal scaling

---

# AZ-104 Exam Tips

Choose Table Storage when:

- Massive structured data
- NoSQL workloads
- Key-value lookups
- Low-cost storage
- Large-scale cloud applications

Do NOT choose Table Storage when:

- Complex SQL queries
- Relationships
- Joins
- Foreign Keys
- Transactions across many tables

Those scenarios require Azure SQL Database or PostgreSQL.

---

# Interview Questions

## What is Azure Table Storage?

A managed NoSQL key-value store for structured, non-relational data.

---

## What is the primary key?

PartitionKey + RowKey.

---

## Why is PartitionKey important?

It determines how Azure distributes and scales data.

---

## When would you choose Table Storage over SQL?

When relationships are unnecessary and scalability, simplicity, and low cost are the priorities.

---

# PPST Engineering Notes

Azure Table Storage is not a replacement for PostgreSQL.

Recommended architecture:

```
Blob Storage
        │
        ▼
Documents

Queue Storage
        │
        ▼
Tasks

PostgreSQL
        │
        ▼
Business Data

Table Storage
        │
        ▼
Logs
Metadata
Configuration

Redis
        │
        ▼
Cache
```

Each storage technology has a distinct responsibility.

---

# Summary

Azure Table Storage is a scalable, schema-less NoSQL database designed for key-value workloads.

It excels at storing massive amounts of structured data with fast key-based access while remaining inexpensive and highly available.

For PPST, Table Storage is best suited for metadata, logs, configuration, and operational data, while PostgreSQL remains the primary datastore for transactional business data.