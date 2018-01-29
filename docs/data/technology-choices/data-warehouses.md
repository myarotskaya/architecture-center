---
title: Choosing a data warehouse
description: 
author: zoinerTejada
ms:date: 01/17/2018
---

# Choosing a data warehouse

A data warehouse is a central, organizational, relational repository of integrated data from one or more disparate sources. (For more information, see [Data warehousing and data marts](../scenarios/data-warehouse.md).) This topic compares the main options for data warehouses in Azure.

## What are your options when choosing a data warehouse?

There are several options for implementing a data warehouse in Azure, depending on your needs. The following lists are broken into two categories, [symmetric multiprocessing](https://en.wikipedia.org/wiki/Symmetric_multiprocessing) (SMP) and [massively parallel processing](https://en.wikipedia.org/wiki/Massively_parallel) (MPP). 

SMP:

- [Azure SQL Database](/azure/sql-database/)
- [SQL Server in a virtual machine](/sql/sql-server/sql-server-technical-documentation)

MPP:

- [Azure Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)
- [Apache Hive on HDInsight](/azure/hdinsight/hadoop/hdinsight-use-hive)
- [Interactive Query (Hive LLAP) on HDInsight](/azure/hdinsight/interactive-query/apache-interactive-query-get-started)

As a general rule, SMP-based warehouses are best suited for small to medium data sets (up to 4-100 TB), while MPP is often used for big data. The delineation between small/medium and big data partly has to do with your organization's definition and supporting infrastructure. (See [Choosing an OLTP data store](oltp-data-stores.md#scalability-capabilities).) 

Beyond data sizes, the type of workload pattern you plan to support is likely to be a greater determining factor. For example, complex queries may be too slow for an SMP solution, and require an MPP solution instead. MPP-based systems are likely to impose a performance penalty with small data sizes, due to the way jobs are distributed and consolidated across nodes. If your data sizes are already exceeding 1 TB and are expected to continually grow, you may want to consider selecting an MPP solution. However, if your data sizes are less than this, but your workloads are exceeding the available resources of your SMP solution, then MPP may be your best option as well.

The data accessed or stored by your data warehouse could come from a number of data sources, including a data lake, such as [Azure Data Lake Store](/azure/data-lake-store/). For a video session that compares the different strengths of MPP services that can use Azure Data Lake, see [Azure Data Lake and Azure Data Warehouse: Applying Modern Practices to Your App](https://azure.microsoft.com/resources/videos/build-2016-azure-data-lake-and-azure-data-warehouse-applying-modern-practices-to-your-app/).

SMP systems are characterized by a single instance of a relational database management system sharing all resources (CPU/Memory/Disk&mdash;that is, shared everything). MPP solutions, on the other hand, require a different skillset, due to variances in querying, modeling, partitioning of data, and other factors unique to parallel processing. You can scale up an SMP system by adding processors with more CPU cores or faster CPU cores, add more memory, and use a faster I/O subsystem. For an MPP system, you can scale out by adding more compute nodes (which have their own CPU, memory and I/O subsystems). There are physical limitations to scaling up a server, at which point scaling out is more desirable, depending on the workload.

When deciding which SMP solution to use, see [A closer look at Azure SQL Database and SQL Server on Azure VMs](/azure/sql-database/sql-database-paas-vs-sql-server-iaas#a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms). 

Azure SQL Data Warehouse can also be used for small and medium datasets, where the workload is compute and memory intensive. Read more about SQL Data Warehouse patterns and common scenarios:

- [SQL Data Warehouse Patterns and Anti-Patterns](https://blogs.msdn.microsoft.com/sqlcat/2017/09/05/azure-sql-data-warehouse-workload-patterns-and-anti-patterns/)
- [SQL Data Warehouse Loading Patterns and Strategies](https://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/)
- [Migrating Data to Azure SQL Data Warehouse](https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/)
- [Common ISV Application Patterns Using Azure SQL Data Warehouse](https://blogs.msdn.microsoft.com/sqlcat/2017/09/05/common-isv-application-patterns-using-azure-sql-data-warehouse/)

## Key selection criteria

For data warehouse scenarios, choose the appropriate system for your needs by answering these questions:

- Do you want a managed service rather than managing your own servers?
    - If yes, then narrow your options to those that are managed services.
- Are you working with extremely large data sets or highly complex, long-running queries? This is sometimes referred to as a big data workload.
    - If yes, narrow your options to those under MPP capabilities. Some things to consider when reviewing your options for this question, is whether the data source is structured or unstructured. For unstructured, it may need to be processed in a big data environment like Spark on HDInsight or Azure Databricks, Hive LLAP on HDInsight, or perhaps Azure Data Lake Analytics, all of which can serve as ELT (Extract, Load, Transform) and ETL (Extract, Transform, Load) engines. They can output the processed data into structured data, making it easier to load into SQL Data Warehouse or one of the other options. For structured data, SQL Data Warehouse now has a new performance tier called Optimized for Compute. This is provided for compute-intensive workloads requiring ultra-high performance.
- Do you want to separate your historical data from your current, operational data?
    - If so, select one of the options where [orchestration](pipeline-orchestration-data-movement.md) is required, as these are standalone warehouses optimized for heavy read access and best suited for acting as a separate historical data store.
- Do you need the ability to integrate data from several sources, beyond your OLTP data store?
    - If so, consider options that easily integrate multiple data sources. Along with this consolidation, do you have a multi-tenancy requirement? If so, remove SQL Data Warehouse from your choices, as it is not ideal for this requirement as outlined in the [SQL Data Warehouse Patterns and Anti-Patterns](https://blogs.msdn.microsoft.com/sqlcat/2017/09/05/azure-sql-data-warehouse-workload-patterns-and-anti-patterns/) article.
- Do you prefer to use a relational data store?
    - If so, narrow your options to those with a relational data store, but also note that it is possible to use a tool like PolyBase to query non-relational data stores if needed. If you do decide to use PolyBase, consider running a few performance tests to validate whether it will work fast enough against your unstructured data sets for your workload.
- Do you have real-time reporting requirements?
    - If you require rapid query response times on high volumes of singleton inserts, narrow your options to those that can support real-time reporting.
- Do you need to support a large number of concurrent users and connections?
    - The ability to support a number of concurrent users/connections depends on several factors. When using Azure SQL, refer to the [documented resource limits](/azure/sql-database/sql-database-resource-limits) based on your service tier. SQL Server hosted on a virtual machine will rely on the size of the virtual machine and supporting services (type of storage, and so on.) to determine the limit, but [generally supports](/sql/database-engine/configure-windows/configure-the-user-connections-server-configuration-option) up to a maximum of 32,767 user connections. SQL Data Warehouse, however, supports a [maximum of 32 concurrent queries](/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency) across 1,024 concurrent connections, though the number of concurrent queries it supports will increase in the future. Consider using complementary services, such as [Azure Analysis Services](/azure/analysis-services/analysis-services-overview), to overcome such limitations if you do select SQL Data Warehouse.
- What sort of workload do you have?
    - In general, MPP-based warehouse solutions are best suited for analytical, batch-oriented workloads. If your workloads are transactional by nature, with many small read/write operations or multiple row-by-row operations, consider using one of the SMP options. One exception to this guideline is when using stream processing on an HDInsight cluster, such as Spark Streaming, and storing the data within a Hive table.

## Capability Matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

### General capabilities

| | Azure SQL Database | SQL Server in a virtual machine | Azure SQL Database managed instance | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- | -- |
| Is managed service | Yes | No | Yes | Yes | Yes&mdash;with manual configuration/scaling | Yes&mdash;with manual configuration/scaling |
| Requires data orchestration (holds copy of data/historical data) | No | No | No | Yes | Yes | Yes |
| Easily integrate multiple data sources | No | No | No | Yes | Yes | Yes |
| Supports pausing compute | No | No | No | Yes | No \*** | No \*** |
| Relational data store | Yes | Yes | Yes | Yes | No | No |
| Real-time reporting | Yes | Yes | Yes | No | No | Yes |
| Flexible backup restore points | Yes | Yes | Yes | No * | Yes ** | Yes ** |
| SMP/MPP | SMP | SMP | SMP | MPP | MPP | MPP |

\* With SQL Data Warehouse, you can restore a database to any available restore point within the last seven days. Snapshots start every four to eight hours and are available for seven days. When a snapshot is older than seven days, it expires and its restore point is no longer available.

\** Recommend using an [external Hive metastore](/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters#use-hiveoozie-metastore) that can be backed up and restored as needed. Standard backup and restore options that apply to Blob Storage or Data Lake Store can be used for the data, or third party HDInsight backup and restore solutions, such as [Imanis Data](https://azure.microsoft.com/blog/imanis-data-cloud-migration-backup-for-your-big-data-applications-on-azure-hdinsight/) can be used for greater flexibility and ease of use.

\*** HDInsight clusters can be deleted when not needed, then re-created when they are. If you want to do this as a way to reduce cost, you will want to attach an external data store to your cluster so your data is retained when you delete your cluster. You can use Azure Data Factory to automate your cluster's lifecycle by creating an on-demand HDInsight cluster to process your workload, then delete it once the processing is complete.

### Scalability capabilities

| | Azure SQL Database | SQL Server in a virtual machine | Azure SQL Database managed instance | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- | -- |
| Redundant regional servers for high availability  | Yes | Yes | Yes | Yes | No | No |
| Supports query scale out (distributed queries)  | No | No | No | Yes | Yes | Yes |
| Dynamic scalability (scale up)  | Yes | No | Yes | Yes * | No | No |
| Supports in-memory caching of data | Yes | Yes | Yes | No | Yes |

\* SQL Data Warehouse allows you to scale up or down compute by [adjusting the number of data warehouse units (DWUs)](/azure/sql-data-warehouse/sql-data-warehouse-manage-compute-overview).

### Security capabilities

| | Azure SQL Database | SQL Server in a virtual machine | Azure SQL Database managed instance | SQL Data Warehouse | Apache Hive on HDInsight | Hive LLAP on HDInsight |
| --- | --- | --- | --- | --- | --- | -- |
| Authentication  | SQL / Azure Active Directory | SQL / Azure Active Directory / Active Directory | SQL / Azure Active Directory | SQL / Azure Active Directory | local / Azure Active Directory * | local / Azure Active Directory * |
| Authorization  | Yes | Yes | Yes | Yes | Yes * | Yes * |
| Auditing  | Yes | Yes | Yes | Yes | Yes * | Yes * |
| Data encryption at rest | Yes ** | Yes ** | Yes ** | Yes ** | Yes * | Yes * |
| Row-level security | Yes | Yes | Yes | No | Yes * | Yes * |
| Supports firewalls | Yes | Yes | Yes | Yes | Yes \*** | Yes \*** |
| Dynamic data masking | Yes | Yes | Yes | No | Yes * | Yes * |

\* Requires using a [domain-joined HDInsight cluster](/azure/hdinsight/domain-joined/apache-domain-joined-introduction).

\** Requires using Transparent Data Encryption (TDE) to encrypt and decrypt your data at rest.

\*** Supported when [used within an Azure Virtual Network](/azure/hdinsight/hdinsight-extend-hadoop-virtual-network).

Read more about securing your data warehouse:

* [Securing your SQL Database](/azure/sql-database/sql-database-security-overview#connection-security)
* [Secure a database in SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-overview-manage-security)
* [Extend Azure HDInsight using an Azure Virtual Network](/azure/hdinsight/hdinsight-extend-hadoop-virtual-network)
* [Enterprise-level Hadoop security with domain-joined HDInsight clusters](/azure/hdinsight/domain-joined/apache-domain-joined-introduction)

