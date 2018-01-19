---
title: 
description: 
author: zoinerTejada
ms:date: 01/17/2018
---

# Technology choices: Data pipeline orchestration, control flow, and data movement

## What are your options for pipeline orchestration, control flow, and data movement?
In Azure, the following services and tools will meet the core requirements for pipeline orchestration, control flow, and data movement:

- [Azure Data Factory](/azure/data-factory/)
- [Oozie on HDInsight](/azure/hdinsight/hdinsight-use-oozie-linux-mac)
- [SQL Server Integration Services (SSIS)](/sql/integration-services/sql-server-integration-services)

## How do you choose?
These services and tools can be used independently from one another, or at times, used together to create a hybrid solution for your data pipeline needs. For instance, the new Integration Runtime (IR) in Azure Data Factory V2 is capable of natively executing SSIS packages in a managed Azure compute environment. While there is some overlap in functionality between these services, there are a few key differences that will lead you to select one over the other in certain situations.

## Key Selection Criteria

Answer the following questions to help you narrow down your choices, then use the matrices below to select your options for your scenario: <!--I like this intro text, it's different than the ones that talk about the tables first that I typically flag. Maybe use this consistently?-->

- Do you need big data capabilities for moving and transforming your data? Usually this means multi-gigabytes to terabytes of data.
    - If yes, then narrow your options to those that best suited for big data.
- Do you require a managed service that can operate at scale?
    - If so, select one of the cloud-based services that aren't limited by your local processing power.
- Are some of your data sources located on-premises?
    - If yes, look for options that can work with both cloud and on-premises data sources or destinations.
- Is your source data stored in Blob storage on an HDFS filesystem?
    - Look for options that support Hive queries.

## Capability matrix

### General capabilities

| | Azure Data Factory | SQL Server Integration Services (SSIS) | Oozie on HDInsight
| --- | --- | --- | --- |
| Managed | Yes | No | Yes |
| Cloud-based | Yes | No (local) | Yes |
| Prerequisite | Azure Subscription | SQL Server  | Azure Subscription, HDInsight cluster |
| Management tools | Azure Portal, PowerShell, CLI, .NET SDK | SSMS, PowerShell | Bash shell, Oozie REST API, Oozie web UI |
| Pricing | Pay per usage | Licensing / pay for features | No additional charge on top of running the HDInsight cluster |

### Pipeline capabilities

| | Azure Data Factory | SQL Server Integration Services (SSIS) | Oozie on HDInsight
| --- | --- | --- | --- |
| Copy data | Yes | Yes | Yes |
| Custom transformations (C#) | Yes | Yes | Yes (MapReduce, Pig, and Hive jobs) |
| Azure Machine Learning scoring | Yes | Yes (with scripting) | No |
| HDInsight On-Demand | Yes | No | No |
| Azure Batch | Yes | No | No |
| Pig, Hive, MapReduce | Yes | No | Yes |
| Spark | Yes | No | No |
| Execute SSIS Package | Yes | Yes | No |
| Control flow | Yes | Yes | Yes |
| Access on-premises data | Yes | Yes | No |

### Scalability capabilities

| | Azure Data Factory | SQL Server Integration Services (SSIS) | Oozie on HDInsight
| --- | --- | --- | --- |
| Scale up | Yes | No | No |
| Scale out | Yes | No | Yes (by adding worker nodes to cluster) |
| Optimized for big data | Yes | No | Yes |

## Where to go from here
Read next:
[Data Warehouse Pipeline Pattern](../solutions/data-warehousing.md)

See also:

Related pipeline patterns
- Working with transactional data
    - [Online Transaction Processing (OLTP)](../solutions/online-transaction-processing.md)
    - [Online Analytical Processing (OLAP)](../solutions/online-analytical-processing.md)
    - [Data Warehousing](../solutions/data-warehousing.md)

Related technology choices
- Transactional data stores
    - [Online Analytical Processing (OLAP) data stores](../technology-choices/olap-data-stores.md)
    - [Data warehouses](../technology-choices/data-warehouses.md)
