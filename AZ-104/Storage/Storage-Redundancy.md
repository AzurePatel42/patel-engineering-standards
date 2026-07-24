# Azure Storage Redundancy

## Objective

Understand how Azure protects data against hardware failures, datacenter outages, and regional disasters using different redundancy options.

---

# Why Storage Redundancy?

Hardware fails.

Disks fail.

Servers fail.

Entire datacenters can lose power.

Azure automatically creates multiple copies of your data to ensure durability and availability.

---

# Types of Redundancy

Azure supports several redundancy options:

- LRS
- ZRS
- GRS
- RA-GRS
- GZRS
- RA-GZRS

Each provides different levels of protection and cost.

---

# 1. LRS (Locally Redundant Storage)

Stores **3 copies** of your data within a single Azure datacenter.

Example:

Datacenter A

Server 1
    │
Server 2
    │
Server 3

Advantages

- Lowest cost
- Fast replication
- Protects against disk/server failures

Disadvantages

- Does NOT protect against datacenter failure

Use Cases

- Development
- Testing
- Non-critical workloads

---

# 2. ZRS (Zone-Redundant Storage)

Stores data across **three Availability Zones** in the same Azure region.

Example

Region: East US

Zone 1
Zone 2
Zone 3

Advantages

- Survives datacenter failure
- High availability

Disadvantages

- Slightly higher cost

Use Cases

- Production applications
- High availability systems

---

# 3. GRS (Geo-Redundant Storage)

Replicates data to another Azure region.

Example

Primary Region

3 copies

↓

Secondary Region

3 copies

Total Copies = 6

Advantages

- Disaster recovery
- Regional protection

Disadvantages

- Higher cost
- Secondary region is not directly readable

---

# 4. RA-GRS

Read-Access Geo-Redundant Storage.

Same as GRS but allows read access from the secondary region.

Advantages

- Read from secondary during outages
- Better availability

Use Cases

- Reporting
- Business continuity

---

# 5. GZRS

Combines:

- Zone Redundancy
- Geo Replication

Protects against:

- Disk failure
- Server failure
- Datacenter failure
- Regional disaster

One of Azure's highest durability options.

---

# 6. RA-GZRS

Adds read access to the secondary region on top of GZRS.

Provides the highest level of resiliency available for standard Azure Storage.

---

# Comparison

| Type | Copies | Datacenter Failure | Zone Failure | Regional Failure | Read Secondary |
|-------|--------|-------------------|--------------|------------------|----------------|
| LRS | 3 | ❌ | ❌ | ❌ | ❌ |
| ZRS | 3 | ✅ | ✅ | ❌ | ❌ |
| GRS | 6 | ✅ | ❌ | ✅ | ❌ |
| RA-GRS | 6 | ✅ | ❌ | ✅ | ✅ |
| GZRS | 6 | ✅ | ✅ | ✅ | ❌ |
| RA-GZRS | 6 | ✅ | ✅ | ✅ | ✅ |

---

# Choosing the Right Option

Development

LRS

Production

ZRS

Business Critical

GZRS

Global Applications

RA-GZRS

---

# PPST Integration

Inventory API

↓

Blob Storage

↓

GZRS

↓

Protect uploaded files

----------------------------

Data Ingestion Pipeline

↓

Blob Storage

↓

GRS

↓

Disaster Recovery

----------------------------

Retrieval Service

↓

Blob Storage

↓

RA-GRS

↓

Read during regional outage

---

# Best Practices

- Use LRS for development.
- Use ZRS for high availability within a region.
- Use GRS or GZRS for disaster recovery.
- Choose redundancy based on Recovery Time Objective (RTO) and Recovery Point Objective (RPO), not just cost.
- Periodically review redundancy settings as application requirements evolve.

---

# AZ-104 Exam Tips

Remember:

L = Local

Z = Zone

G = Geo

RA = Read Access

Microsoft frequently asks scenario-based questions about selecting the appropriate redundancy option.

---

# Key Takeaways

✔ LRS = Cheapest

✔ ZRS = High Availability

✔ GRS = Disaster Recovery

✔ RA-GRS = Disaster Recovery + Read Access

✔ GZRS = Zone + Geo Protection

✔ RA-GZRS = Maximum Availability