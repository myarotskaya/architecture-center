---
layout: LandingPage
---

# Azure Data Architecture Guide

This guide presents a structured approach for designing data-centric solutions on Microsoft Azure. It is based on proven practices derived from customer engagements and is intended as an entry point for all data-related topics in Azure. 

## Introduction

The cloud is changing the way applications are designed, including how data is processed and stored. Instead of a single general-purpose database that handles all of a solution's data, the _polyglot persistence_ approach is to use multiple, specialized databases and datastores — each is optimized to provide specific capabilities needed by the solution. The perspective on data in the solution changes as a result. It is no longer the case that there are multiple layers of business logic and a single data layer. Instead modern, polyglot persistence solutions are designed around the notion of a data pipeline which describe how data flows through a solution, where it is processed, where it is stored, and how it is consumed by the next component in the pipeline. 

Owing to the fundamental importance of the data pipeline throughout modern data architectures, this guide demonstrates all data pipelines as variants of the following canonical data pipeline:  

![Overview Data Pipeline](./images/overall-data-pipeline.png)
TODO: This image needs an update with the lighter blue and the gray arrows.

## How this guide is structured

This guide covers the big picture concepts in [common data architectures](./common-architectures/index.md) and leads you to the pipeline patterns used by each architecture. The pipeline patterns are used to describe how the various processing and storage components fit together when handling the data. Finally, the technology choices will help you narrow the list of candidate Azure services--that are appropriate to your pipeline pattern--down to those services that are most appropriate to your specific requirements.

![Overview of the structure of the guide](./images/overview-flowchart.png)

Here are the common architectures covered in this guide:

- [Relational data](./common-architectures/relational-data.md)
- [Non-relational data](./common-architectures/non-relational-data.md)
- [Big data](./common-architectures/big-data.md)
- [Data pipeline](./common-architectures/data-pipeline.md)
- [Advanced analytics](./common-architectures/advanced-analytics.md)
- [Interactive data exploration](./common-architectures/interactive-data-exploration.md)



