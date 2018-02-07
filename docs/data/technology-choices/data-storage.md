---
title: Choosing a data storage technology
description: 
author: zoinerTejada
ms:date: 02/09/2018
---

# Choosing a big data storage technology 

## What are your options when choosing data storage in Azure?

There are several options for ingesting data into Azure, depending on your needs:

**File storage**

- [Azure Storage blobs](/azure/storage/blobs/storage-blobs-introduction)
- [Azure Data Lake Store](/azure/data-lake-store/)

**NoSQL databases**

- [Azure Cosmos DB](/azure/cosmos-db/)
- [HBase on HDInsight](http://hbase.apache.org/)

## Azure Storage blobs

Azure Storage is a Microsoft-managed cloud service that provides storage that is highly available, secure, durable, scalable, and redundant. Microsoft takes care of maintenance and handles critical problems for you. Azure Storage is the most ubiquitous storage solution Azure provides, due to the number of services and tools that can be used with it.

There are various Azure Storage services you can use to store data. The most flexible service option for storing blobs from a number of data sources is [Blob storage](/azure/storage/blobs/storage-blobs-introduction). Blobs are basically files like those that you store on your computer (or tablet, mobile device, and so on). They can be pictures, Microsoft Excel files, HTML files, virtual hard disks (VHDs), big data such as logs, database backups&mdash;pretty much anything. Blobs are stored in containers, which are similar to folders. A container provides a grouping of a set of blobs. All blobs must be in a container. An account can contain an unlimited number of containers. A container can store an unlimited number of blobs.

Azure Storage is an excellent choice for big data and analytics solutions, given its flexibility, high availability, and low cost, compared to other options, such as Azure Data Lake Store. Its option of [three storage tiers](/azure/storage/blobs/storage-blob-storage-tiers) allow you to store your data most cost-effectively, depending on how you use it. These include the hot storage tier for frequently accessed data, cool storage tier for less frequently accessed data, and the archive storage tier for rarely accessed data.

After storing files in Blob storage, you can access them from anywhere in the world using URLs, the REST interface, or one of the Azure SDK storage client libraries. Storage client libraries are available for multiple languages, including Node.js, Java, PHP, Ruby, Python, and .NET.

There are three types of blobs&mdash;block blobs, page blobs (used for VHD files), and append blobs.

- **Block blobs** are used to hold ordinary files up to about 4.7 TB. This is the type most commonly used for any form of analytics. 
- **Page blobs** are used to hold random access files up to 8 TB in size. These are used for the VHD files that back virtual machines.
- **Append blobs** are made up of blocks like the block blobs, but are optimized for append operations. These are used for things like logging information to the same blob from multiple virtual machines.

Azure Blob storage can be accessed from Hadoop (available through HDInsight). HDInsight can use a blob container in Azure Storage as the default file system for the cluster. Through a Hadoop distributed file system (HDFS) interface provided by a WASB driver, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs. Azure Blob storage can also be accessed via Azure SQL Data Warehouse using its PolyBase feature.

Other options that make Azure Storage a good choice are:

- [Multiple concurrency strategies](/azure/storage/common/storage-concurrency?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
- [Flexible disaster recovery and high availability options](/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json), like Geo-redundant storage (GRS) and Read-access geo-redundant storage (RA-GRS)
- [Encryption at rest](/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) to help protect and safeguard your data
- [Role-Based Access Control (RBAC)](/azure/storage/common/storage-security-guide?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#management-plane-security) to control access using Azure Active Directory users and groups

## Azure Data Lake Store

[Azure Data Lake Store](/azure/data-lake-store/) is an enterprise-wide hyper-scale repository for big data analytic workloads. Data Lake enables you to capture data of any size, type, and ingestion speed in one single [secure](/azure/data-lake-store/data-lake-store-overview#DataLakeStoreSecurity) location for operational and exploratory analytics.

Data Lake Store does not impose any limits on account sizes, file sizes, or the amount of data that can be stored in a data lake. Data is stored durably by making multiple copies and there is no limit on the duration of time that the data can be stored in the Data Lake. In addition to making multiple copies of files to guard against any unexpected failures, Data lake spreads parts of a file over a number of individual storage servers. This improves the read throughput when reading the file in parallel for performing data analytics.

As an alternative to Azure Storage, Data Lake Store can be accessed from Hadoop (available through HDInsight) using the WebHDFS-compatible REST APIs. You may consider using this as an alternative to Azure Storage when your individual or combined file sizes exceed that which is supported by Azure Storage. However, there are [performance tuning guidelines](/azure/data-lake-store/data-lake-store-performance-tuning-guidance#optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight) you should follow when using Data Lake Store as your primary storage for an HDInsight cluster, with specific guidelines for [Spark](/azure/data-lake-store/data-lake-store-performance-tuning-spark), [Hive](/azure/data-lake-store/data-lake-store-performance-tuning-hive), [MapReduce](/azure/data-lake-store/data-lake-store-performance-tuning-mapreduce), and [Storm](/azure/data-lake-store/data-lake-store-performance-tuning-storm). Also, be sure to check Data Lake Store's [regional availability](https://azure.microsoft.com/regions/#services), because it is not available in as many regions as Azure Storage, and it needs to be located in the same region as your HDInsight cluster.

Coupled with Azure Data Lake Analytics, Data Lake Store is specifically designed to enable analytics on the stored data and is tuned for performance for data analytics scenarios. Data Lake Store can also be accessed via Azure SQL Data Warehouse using its PolyBase feature.

## Azure Cosmos DB

[Azure Cosmos DB](/azure/cosmos-db/) is Microsoft’s globally distributed multi-model database. Azure Cosmos DB was built from the ground up with global distribution and horizontal scale at its core. It offers turnkey global distribution across any number of Azure regions by transparently scaling and replicating your data wherever your users are. Elastically scale throughput and storage worldwide, and pay only for the throughput and storage you need. Azure Cosmos DB guarantees single-digit-millisecond latencies at the 99th percentile anywhere in the world, offers multiple well-defined consistency models to fine-tune performance, and guarantees high availability with multi-homing capabilities.

Azure Cosmos DB is schema-agnostic. It automatically indexes all the data without requiring you to deal with schema and index management. It’s also multi-model, natively supporting document, key-value, graph, and column-family data models. With Azure Cosmos DB, you can access your data using APIs of your choice, as DocumentDB SQL (document), MongoDB (document), Azure Table Storage (key-value), and Gremlin (graph) are all natively supported.

Azure Cosmos DB features:

- [Turnkey global distribution](/azure/cosmos-db/distribute-data-globally)
- [Elastic scaling of throughput and storage](/azure/cosmos-db/partition-data) worldwide
- Single-digit millisecond latencies at the 99th percentile
- [Five well-defined consistency levels](/azure/cosmos-db/consistency-levels)
- Guaranteed high availability

## HBase on HDInsight

[Apache HBase](http://hbase.apache.org/) is an open-source, NoSQL database that is built on Hadoop and modeled after Google BigTable. HBase provides random access and strong consistency for large amounts of unstructured and semi-structured data in a schemaless database organized by column families.

Data is stored in the rows of a table, and data within a row is grouped by column family. HBase is a schemaless database in the sense that neither the columns nor the type of data stored in them need to be defined before using them. The open-source code scales linearly to handle petabytes of data on thousands of nodes. It can rely on data redundancy, batch processing, and other features that are provided by distributed applications in the Hadoop ecosystem.

The [HDInsight implementation](/azure/hdinsight/hbase/apache-hbase-overview) leverages the scale-out architecture of HBase to provide automatic sharding of tables, strong consistency for reads and writes, and automatic failover. Performance is enhanced by in-memory caching for reads and high-throughput streaming for writes. In most cases, you'll want to [create the HBase cluster inside a virtual network](/azure/hdinsight/hbase/apache-hbase-provision-vnet) so other HDInsight clusters and applications can directly access the tables.

## Key selection criteria

For data ingest scenarios, choose the appropriate system for your needs by answering these questions:

- Do you need managed, high speed, cloud-based storage for any type of text or binary data?
    - If yes, then select one of the file storage options.
- Do you need file storage that is optimized for parallel analytics workloads and high throughput/IOPS?
    - If yes, then narrow your file storage options to those that are tuned to analytics workload performance.
- Do you need to store your unstructured or semi-structured data in a schemaless database that provides high-speed read access and consistency to your data?
    - If so, select one of the NoSQL options. Compare options for indexing, available database models, and regional availability. Depending on the type of data you need to store and how you want to work with it, the selection of primary database models may be the biggest determining factor.
- Can you use the service in your region?
    - Check the [regional availability for each Azure service](https://azure.microsoft.com/regions/#services) to find out. If the service you want to use is not in your region, or nearby, then that could automatically disqualify it from your options. This is especially true in situations when data sovereignty is a high priority.

## Capability matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

### File storage capabilities

|  | Azure Data Lake Store | Azure Blob Storage containers |
| --- | --- | --- |
| Purpose | Optimized storage for big data analytics workloads |General purpose object store for a wide variety of storage scenarios |
| Use cases | Batch, streaming analytics, and machine learning data such as log files, IoT data, click streams, large datasets | Any type of text or binary data, such as application back end, backup data, media storage for streaming, and general purpose data |
| Key concepts | Data Lake Store account contains folders, which in turn contains data stored as files | Storage account has containers, which in turn has data in the form of blobs |
| Structure | Hierarchical file system | Object store with flat namespace |
| API | REST API over HTTPS | REST API over HTTP/HTTPS |
| Server-side API | Proprietary [WebHDFS-compatible REST API](https://msdn.microsoft.com/library/azure/mt693424.aspx) | [Azure Blob Storage REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx) |
| Hadoop file system client | Yes |Yes |
| Data operations&mdash;authentication | Based on [Azure Active Directory Identities](/azure/active-directory/active-directory-authentication-scenarios) | Based on shared secrets [Account Access Keys](/azure/storage/common/storage-create-storage-account#manage-your-storage-account) and [Shared Access Signature Keys](/azure/storage/common/storage-dotnet-shared-access-signature-part-1), and [Role-Based Access Control (RBAC)](/azure/security/security-storage-overview) |
| Data operations&mdash;authentication protocol | OAuth 2.0. Calls must contain a valid JWT (JSON web token) issued by Azure Active Directory | Hash-based message authentication code (HMAC). Calls must contain a Base64-encoded SHA-256 hash over a part of the HTTP request. |
| Data operations&mdash;authorization | POSIX access control lists (ACLs). ACLs based on Azure Active Directory identities can be set file and folder level. | For account-level authorization use [Account Access Keys](/azure/storage/common/storage-create-storage-account#manage-your-storage-account)<br>For account, container, or blob authorization use [Shared Access Signature Keys](/azure/storage/common/storage-dotnet-shared-access-signature-part-1) |
| Data Operations&mdash;Auditing | Available.  |Available |
| Encryption data at rest | <ul><li>Transparent, server side</li> <ul><li>With service-managed keys</li><li>With customer-managed keys in Azure KeyVault</li></ul></ul> | <ul><li>Transparent, server side</li> <ul><li>With service-managed keys</li><li>With customer-managed keys in Azure KeyVault (coming soon)</li></ul><li>Client-side encryption</li></ul> |
| Management operations (for example, account create) | [Role-based access control](/azure/active-directory/role-based-access-control-what-is) (RBAC) provided by Azure for account management | [Role-based access control](/azure/active-directory/role-based-access-control-what-is) (RBAC) provided by Azure for account management |
| Developer SDKs | .NET, Java, Python, Node.js | .Net, Java, Python, Node.js, C++, Ruby |
| Analytics workload performance | Optimized performance for parallel analytics workloads, High Throughput and IOPS | Not optimized for analytics workloads |
| Size limits | No limits on account sizes, file sizes or number of files | Specific limits documented [here](/azure/azure-subscription-service-limits#storage-limits) |
| Geo-redundancy | Locally-redundant (multiple copies of data in one Azure region) | Locally redundant (LRS), globally redundant (GRS), read-access globally redundant (RA-GRS). See [here](/azure/storage/common/storage-redundancy) for more information |
| Service state | Generally available | Generally available |
| Regional availability | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) |
| Price | See [Pricing](https://azure.microsoft.com/pricing/details/data-lake-store/) | See [Pricing](https://azure.microsoft.com/pricing/details/storage/) |

### NoSQL database capabilities

| | Azure Cosmos DB | HBase on HDInsight |
| --- | --- | --- |
| Primary database model | Document store, graph DBMS, key-value store, wide column store | Wide column store |
| Data types | Yes (JSON data types) | No |
| Secondary indexes | Yes | No |
| SQL language support | Yes | Yes (using the [Phoenix](http://phoenix.apache.org/) JDBC driver) |
| Available APIs |[DocumentDB](/azure/cosmos-db/documentdb-introduction), [MongoDB](/azure/cosmos-db/mongodb-introduction), [Graph](/azure/cosmos-db/graph-introduction) (Gremlin), RESTful HTTP, [Table](/azure/cosmos-db/table-introduction), [Cassandra](/azure/cosmos-db/cassandra-introduction) (preview) | Java, RESTful HTTP, Thrift |
| Consistency | Strong, bounded-staleness, session, consistent prefix, eventual | Strong |
| Native Azure Functions integration | [Yes](/azure/cosmos-db/serverless-computing-database) | No |
| Regional availability | See [here](https://azure.microsoft.com/regions/#services) | See [here](https://azure.microsoft.com/regions/#services) |
| Automatic global distribution | [Yes](/azure/cosmos-db/distribute-data-globally), while maintaining all 5 consistency models | No [HBase cluster replication can be configured](/azure/hdinsight/hbase/apache-hbase-replication) across regions with eventual consistency |
| Pricing model | Elastically scalable request units (RUs) charged per-second as needed, elastically scalable storage | Per-minute pricing for HDInsight cluster (horizontal scaling of nodes), storage |



