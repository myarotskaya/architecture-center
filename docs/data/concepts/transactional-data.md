---
title: Transactional data
description: 
author: zoinerTejada
ms:date: 01/17/2018
---

# Transactional data

Transactional data is information an organization collects that tracks the interactions related to what the organization does. These interactions are typically business transactions such as payments received from customers or payments made to suppliers, products moving through inventory, orders taken or services delivered. Transactional events, which represent the transactions themselves, not reference tables, typically contain a time dimension, some numerical values, and references to other data.

Transactional data stores that support strong consistency can leverage transactions using various locking strategies, such as pessimistic locking, to ensure all data are strongly consistent within the context of the enterprise, for all users and processes.

The most common deployment architecture that utilizes transactional data is the data store tier in a 3-tier architecture. A 3-tier architecture typically consists of a presentation tier, business logic tier, and data store tier. A related deployment architecture is the [N-tier](/azure/architecture/guide/architecture-styles/n-tier) architecture, which may have multiple middle-tiers handling business logic.

![Example of a 3-tier application](./images/three-tier-application.png)

## Typical traits of transactional data

Transactional data tends to have the following traits:

| Requirement | Description |
| --- | --- |
| Normalization | Highly normalized |
| Schema | Schema on write, strongly enforced|
| Consistency | Strong consistency, ACID guarantees |
| Integrity | High integrity |
| Uses transactions | Yes |
| Locking strategy | Pessimistic or Optimistic|
| Updateable | Yes |
| Appendable | Yes |
| Workload | Heavy writes, moderate reads |
| Indexing | Primary and secondary indexes |
| Datum size | Small to medium sized |
| Model | Relational |
| Data shape | Tabular |
| Query flexibility | Highly flexible |
| Scale | Small (MBs) to Large (a few TBs) | 