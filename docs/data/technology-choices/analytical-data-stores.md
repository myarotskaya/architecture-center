---
title: Choosing an analytical data store
description: 
author: zoinerTejada
ms:date: 02/09/2018
---

# Choosing an analytical data store

In the [big data](../concepts/big-data.md) architecture, we reviewed the overall layout and uses of both the lambda and kappa architectures. Both of these pipelines require an analytical data store that serves processed data in a structured format that can be queried using analytical tools. The analytical data stores that support querying of both hot path data and cold path data by client applications and BI tools are collectively referred to as the serving layer, or data serving storage.

The serving layer deals with processed data from both the hot path and cold path. This can be further subdivided into a speed serving layer that stores a subset of incrementally processed hot path data not yet processed by the batch techniques of the cold path, and a batch serving layer that contains the batch-processed output of the cold path. Because of this, the serving layer requires strong support for random reads with low latency. In addition, data serving storage for the speed layer should also support random writes, since any preparation work needed to create a batch, and batch load data into this store would typically introduce undesired delays. On the other hand, data serving storage for the batch layer does not need to support random writes, but batch writes instead.

There is no single best data management choice for all data storage tasks. Different data management solutions are optimized for different tasks. Most real-world cloud apps and big data processes have a variety of data storage requirements and are often served best by a combination of multiple data storage solutions.

## What are your options when choosing data serving storage?
There are several options for data serving storage in Azure, depending on your needs:

- [SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)
- [Azure SQL Database](/azure/sql-database/)
- [SQL Server in Azure VM](/sql/sql-server/sql-server-technical-documentation)
- [HBase/Phoenix on HDInsight](/azure/hdinsight/hbase/apache-hbase-overview)
- [Hive LLAP on HDInsight](/azure/hdinsight/interactive-query/apache-interactive-query-get-started)
- [Azure Analysis Services](/azure/analysis-services/analysis-services-overview)
- [Azure Cosmos DB](/azure/cosmos-db/)

These options provide various database models that are optimized for different types of tasks:

- [Key/value](https://msdn.microsoft.com/library/dn313285.aspx#sec7) databases hold a single serialized object for each key value. They're good for storing large volumes of data where you want to get one item for a given key value and you don't have to query based on other properties of the item.
- [Document](https://msdn.microsoft.com/library/dn313285.aspx#sec8) databases are key/value databases in which the values are *documents*. Document here isn't used in the sense of a Word or Excel document, but means a collection of named fields and values, any of which could be a child document. For example, in an order history table an order document might have order number, order date, and customer fields, and the customer field might have name and address fields. The database encodes field data in a format such as XML, YAML, JSON, or BSON, or it can use plain text. One feature that sets document databases apart from key/value databases is the ability to query on non-key fields and define secondary indexes to make querying more efficient. This ability makes a document database more suitable for applications that need to retrieve data based on criteria more complex than the value of the document key. For example, in a sales order history document database you could query on various fields such as product ID, customer ID, customer name, and so forth.
- [Column-family](https://msdn.microsoft.com/library/dn313285.aspx#sec9) databases are key/value data stores that enable you to structure data storage into collections of related columns called column families. For example, a census database might have one group of columns for a person's name (first, middle, last), one group for the person's address, and one group for the person's profile information (DOB, gender, and so on). The database can then store each column family in a separate partition while keeping all of the data for one person related to the same key. You can then read all profile information without having to read through all of the name and address information as well.
- [Graph](https://msdn.microsoft.com/library/dn313285.aspx#sec10) databases store information as a collection of objects and relationships. The purpose of a graph database is to enable an application to efficiently perform queries that traverse the network of objects and the relationships between them. For example, the objects might be employees in a human resources database, and you might want to facilitate queries such as "find all employees who directly or indirectly work for Scott."

## Key selection criteria

Choose the appropriate system for your needs by answering these questions:

- Do you need serving storage that can serve as a hot path for your data? If yes, narrow your options to those that are optimized for speed serving layer.

- Do you need massively parallel processing (MPP) support, where your queries are automatically distributed amongst several processes or nodes? If yes, select an option that supports query scale out.

- Do you prefer to use a relational data store? If so, narrow your options to those with a relational database model. However, note that some non-relational stores support SQL syntax for querying, and tools such as PolyBase can be used to query non-relational data stores.

## Capability matrix

The following tables summarize the key differences in capabilities.

### General capabilities

| | SQL Database | SQL Data Warehouse | HBase/Phoenix on HDInsight | Hive LLAP on HDInsight | Azure Analysis Services | Azure Cosmos DB |
| --- | --- | --- | --- | --- | --- | --- |
| Is managed service | Yes | Yes | Yes <sup>1</sup> | Yes <sup>1</sup> | Yes | Yes |
| Primary database model | Relational (columnar format when using columnstore indexes) | Relational tables with columnar storage | Wide column store | Hive/In-Memory | Tabular/MOLAP semantic models | Document store, graph, key-value store, wide column store |
| SQL language support | Yes | Yes | Yes (using the [Phoenix](http://phoenix.apache.org/) JDBC driver) | Yes | No | Yes |
| Optimized for speed serving layer | Yes, using memory-optimized tables and hash or nonclustered indexes | No | Yes | Yes | No | Yes |

[1] With manual configuration and scaling
 
### Scalability capabilities

| | SQL Database | SQL Data Warehouse | HBase/Phoenix on HDInsight | Hive LLAP on HDInsight | Azure Analysis Services | Azure Cosmos DB |
| --- | --- | --- | --- | --- | --- | --- |
| Redundant regional servers for high availability  | Yes | Yes | Yes | No | No | Yes | Yes |
| Supports query scale out  | No | Yes | Yes | Yes | Yes | Yes |
| Dynamic scalability (scale up)  | Yes | Yes | No | No | Yes | Yes |
| Supports in-memory caching of data | Yes | Yes | No | Yes | Yes | No |

### Security capabilities

| | SQL Database | SQL Data Warehouse | HBase/Phoenix on HDInsight | Hive LLAP on HDInsight | Azure Analysis Services | Azure Cosmos DB |
| --- | --- | --- | --- | --- | --- | --- |
| Authentication  | SQL / Azure Active Directory (Azure AD) | SQL / Azure AD | local / Azure AD <sup>1</sup> | local / Azure AD <sup>1</sup> | Azure AD | database users / Azure AD via access control (IAM) |
| Authorization  | Yes | Yes | Yes <sup>1</sup> | Yes <sup>1</sup> | Yes | [Yes](/azure/cosmos-db/secure-access-to-data) (hash-based message authentication code (HMAC))
| Auditing  | Yes | Yes | Yes <sup>1</sup> | Yes <sup>1</sup> | Yes (when integrated with [Azure Monitor Resource Diagnostic Logs](/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)) | Yes (through [audit logging/activity logs](/azure/cosmos-db/logging))
| Data encryption at rest | Yes <sup>2</sup> | Yes <sup>2</sup> | Yes <sup>1</sup> | Yes <sup>1</sup> | Yes | Yes |
| Row-level security | Yes | No | Yes <sup>1</sup> | Yes <sup>1</sup> | Yes (through object-level security in model) | No |
| Supports firewalls | Yes | Yes | Yes <sup>3</sup> | Yes <sup>3</sup> | Yes | Yes |
| Dynamic data masking | Yes | No | Yes <sup>1</sup> | Yes * | No | No |

[1] Requires using a [domain-joined HDInsight cluster](/azure/hdinsight/domain-joined/apache-domain-joined-introduction).

[2] Requires using transparent data encryption (TDE) to encrypt and decrypt your data at rest.

[3] When used within an Azure Virtual Network. See [Extend Azure HDInsight using an Azure Virtual Network](/azure/hdinsight/hdinsight-extend-hadoop-virtual-network).
