---
title: Azure Data Architecture Guide
description: 
author: zoinerTejada
ms:date: 01/17/2018
layout: LandingPage
---

# Azure Data Architecture Guide

This guide presents a structured approach for designing data-centric solutions on Microsoft Azure. It is based on proven practices derived from customer engagements.

## Introduction

The cloud is changing the way applications are designed, including how data is processed and stored. Instead of a single general-purpose database that handles all of a solution's data, the _polyglot persistence_ approach is to use multiple, specialized databases and data stores &mdash; each optimized to provide specific capabilities. The perspective on data in the solution changes as a result. There are no longer multiple layers of business logic that read and write to a single data layer. Instead, polyglot persistence solutions are designed around a *data pipeline* that describes how data flows through a solution, where it is processed, where it is stored, and how it is consumed by the next component in the pipeline. 

## How this guide is structured

This guide is structure around a basic pivot: The distinction between *relational* or *structured* data and *non-relational* or *unstructured* data. 

![](./images/guide-steps.svg)

Relational data is generally stored in a traditional RDBMS or a data warehouse. It has a pre-defined schema ("schema on write") with a set of constraints to maintain referential integrity. Most relational databases use Structured Query Language (SQL) for querying. Solutions that use relational databases include online transaction processing (OLTP) and online analytical processing (OLAP).

Non-relational data is any data that does not use the [relational model](https://en.wikipedia.org/wiki/Relational_model) found in traditional RDBMS systems. This may include key-value data, JSON data, graph data, time series data, and other data types. The term *NoSQL* refers collectively to databases that are designed to hold various types of non-relational data. (The term is not entirely accurate, because many non-relational data stores support SQL compatible queries.) Non-relational data and NoSQL databases often come up in discussions of *big data* solutions. A big data architecture is designed to handle the ingestion, processing, and analysis of data that is too large or complex for traditional database systems. 

Within each of these two main pivots, the Data Architecture Guide contains the following sections:

- **Concepts.** Overview articles that introduce the main concepts you need to understand when working with this type of data.
- **Scenarios.** A representative set of data scenarios, including a discussion of the relevant Azure services and the appropriate architecture for the scenario.
- **Technology choices.** Detailed comparions of various data technologies available on Azure, including open source options. Within each category, we describe the key selection criteria and a capability matrix, to help you choose the right technology for your scenario.

This guide is not intended to teach you data science or database theory &mdash; entire books have been written on those subjects. Instead, the goal is to help you select the right data architecture or data pipeline for your scenario, and then select the Azure services and technologies that best fit your requirements. If you already have an architecture in mind, you can skip directly to the technology choices.

## Traditional RDBMS

### Concepts

- [Relational data](./concepts/relational-data.md) 
- [Transactional data](./concepts/transactional-data.md) 
- [Semantic modeling](./concepts/semantic-modeling.md) 

### Scenarios

- [Online analytical processing (OLAP)](./scenarios/online-analytical-processing.md)
- [Online transaction processing (OLTP)](./scenarios/online-transaction-processing.md) 
- [Data warehousing and data marts](./scenarios/data-warehousing.md)
- [ETL](./scenarios/etl.md) 

## Big data and NoSQL

### Concepts

- [Non-relational data](./concepts/non-relational-data.md)
- [Big data architectures](./concepts/big-data.md)
- [Advanced analytics](./concepts/advanced-analytics.md) 
- [Machine learning at scale](./concepts/machine-learning-at-scale.md)
- [Processing CSV and JSON files](./concepts/csv-and-json.md)

### Scenarios

- [Batch processing](./scenarios/batch-processing.md)
- [Interactive data exploration](./scenarios/interactive-data-exploration.md)
- [Natural language processing](./scenarios/natural-language-processing.md)
- [Real time processing](./scenarios/real-time-processing.md)
- [Search](./scenarios/search.md)
- [Time series solutions](./scenarios/time-series.md)

## Cross-cutting concerns

- [Data transfer](./technology-choices/data-transfer.md) 
- [Extending on-premises data solutions to the cloud](./cross-cutting/hybrid-on-premises-and-cloud.md) 
- [Monitoring data solutions](./cross-cutting/monitoring-data-solutions.md) 
- [Securing data solutions](./cross-cutting/secure-solutions.md) 
