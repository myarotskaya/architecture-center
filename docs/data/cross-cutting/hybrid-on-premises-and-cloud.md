---
title: Extending on-premises data solutions to the cloud
description: 
author: zoinerTejada
ms:date: 01/17/2018
---

# Extending on-premises data solutions to the cloud

When organizations move workloads and data to the cloud, often their on-premises datacenters still play an important role. For many organizations, integrating these two to create a "hybrid cloud" is essential.

Hybrid cloud uses compute or storage resources on your on-premises network and in the cloud. You can use hybrid cloud as a path to migrate your business and its IT needs to the cloud or integrate cloud platforms and services with your existing on-premises infrastructure as part of your overall IT strategy.

This article examines the best practices for managing data in a hybrid cloud environment &mdash; how to create a consistent data platform that spans on-premises and cloud-based workloads. This consistency lets you use the same tools and skills throughout your environment.

### Network shares

In a hybrid cloud architecture, it is common for an organization to keep newer files on-premises while archiving older files to the cloud. The benefits of doing this are twofold. On one hand, it keeps the newest or most commonly accessed files within your network to reduce bandwidth usage and file access times. On the other hand, this approach helps you manage unexpected local storage growth. This is sometimes called file tiering, where there is seamless access to both sets of files, on-premises and cloud-hosted.

Organizations may also wish to move their network shares entirely to the cloud. This would be desirable, for example, if the applications that access them are also located in the cloud. This procedure can be done using [data orchestration](../technology-choices/pipeline-orchestration-data-movement.md) tools.

### On-premises data stores

On-premises data stores include databases, lists, and files. There may be several reasons to keep these local. You may choose to leverage your existing on-premises investments as you migrate workloads and applications to the cloud. Or there may be regulations or policies that do not permit moving specific data or workloads to the cloud. Data sovereignty, privacy, or security concerns may favor on-premises placement. 

Some of the important considerations in placing application data in a public cloud include:

* **Cost**. The cost of storage in Azure can be significantly lower than the cost of maintaining storage with similar characteristics in an on-premises datacenter. Of course, many companies will have existing investments in high-end SANs, so these cost advantages may not reach full fruition until existing hardware ages out.
* **Elastic scale**. Planning for and managing data capacity growth in an on-premises environment can be challenging, particularly when data growth is difficult to predict. These applications can take advantage of the capacity-on-demand and virtually unlimited storage available in the cloud. This consideration is less relevant for applications that consist of relatively static sized datasets.
* **Disaster recovery**. Data stored in Azure can be automatically replicated within an Azure region and across geographic regions. Similar levels of protection can be provided in on-premises infrastructures through data replication technologies where multiple datacenters are available. In hybrid environments, these same technologies can be used to replicate between on-premises and cloud-based data stores.

### Extending data stores to the cloud

There are several options for extending on-premises data stores to the cloud. One option is to have on-premises and cloud replicas. This can help you achieve a high level of fault tolerance, but may require making changes to your applications to connect to the appropriate data store in the event of a failover.

Another option is to move a portion of the data to cloud storage, while keeping the more current or more highly accessed data on-premises. This method can provide a more cost-effective option for long-term storage, as well as improve data access response times by reducing your operational data set.

In situations where you desire to keep all of your data on-premises, yet harness the compute power and accessibility of the cloud, consider using a hybrid application. To do this, you would host your application in the cloud and connect it to your on-premises data store over a secure connection.

## When to use a hybrid solution

There are several strong cases for hybrid cloud, such as meeting industry regulations for how and where data can be stored. When connectivity and latency issues have a performance impact on your ability to transfer data between your on-premises data stores and the cloud, you may opt to maintain select data to work with locally. A hybrid approach to cloud could make sense for using existing on-premises technology as an asset in digital transformation as opposed to treating them as purely legacy investments. Once you realize that cloud doesn't have to be an all or nothing prospect, there are many ways to harness the power of the cloud while maximizing your current investments.

Consider using a hybrid solution in the following scenarios:

* As a transition strategy during a longer-term migration to a fully cloud native solution.
* When regulations or policies do not permit moving specific data or workloads to the cloud.
* For disaster recovery and fault tolerance, by replicating data and services between on-premises and cloud environments.
* To reduce latency between your on-premises data center and remote locations, by hosting part of your architecture in Azure.

## Challenges

* Making security, management, your data platform, and development consistent between on-premises and cloud, avoiding duplication of work and wasting valuable resources. Synchronizing differences between environments can be painful and costly.

* Creating a reliable, low latency and secure data connection between your on-premises and cloud environments.

* Replicating your data and modifying your applications and tools to use the correct data stores within each environment.

## Azure Stack

For the most complete hybrid cloud solution option available today, consider using [Microsoft Azure Stack](/azure/azure-stack/). Azure Stack is a hybrid cloud platform that lets you provide Azure services from your datacenter. This helps maintain consistency between on-premises and Azure, by using identical tools and requiring no code changes. 

The following are some use cases for Azure and Azure Stack:

* **Edge and disconnected solutions**. Address latency and connectivity requirements by processing data locally in Azure Stack and then aggregating in Azure for further analytics, with common application logic across both. 
* **Cloud applications that meet varied regulations**. Develop and deploy applications in Azure, with the flexibility to deploy the same applications on-premises on Azure Stack to meet regulatory or policy requirements.
* **Cloud application model on-premises**: Use Azure to update and extend existing applications or build new ones. Use a consistent DevOps processes across Azure in the cloud and Azure Stack on-premises.

### SQL Server data stores

If you are running SQL Server on-premises, you can use Microsoft Azure Blob Storage service for backup and restore. For more information, see [SQL Server Backup and Restore with Microsoft Azure Blob Storage Service](/sql/relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service). This capability gives you limitless off-site storage, and the ability to share the same backups between your on-premises SQL Server and SQL Server running in a virtual machine in Azure. 

[Azure SQL Database](/azure/sql-database/) is a managed relational database-as-a service. Because Azure SQL Database uses the Microsoft SQL Server Engine, applications can access data in the same way with both technologies. Azure SQL Database can also be combined with SQL Server in useful ways. For example, the [SQL Server Stretch Database](/sql/sql-server/stretch-database/stretch-database) feature lets an application access what looks like a single table in a SQL Server database while some or all rows of that table might be stored in Azure SQL Database. This technology automatically moves data that's not accessed for a defined period of time to the cloud. Applications reading this data are unaware that any of it has been moved to the cloud.

Maintaining data stores on-premises and in the cloud can be challenging when you desire to keep the data synchronized. You can address this with [SQL Data Sync](/azure/sql-database/sql-database-sync-data), a service built on Azure SQL Database that lets you synchronize the data you select, bi-directionally across multiple Azure SQL databases and SQL Server instances. While Data Sync makes it easy to keep your data up-to-date across these various data stores, it should not be used for disaster recovery or for migrating from on-premises SQL Sever to Azure SQL Database.

For disaster recovery and business continuity, you can use [AlwaysOn Availability Groups](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) to replicate data across two or more instances of SQL Server, some of which can be running on Azure virtual machines in another geographic region.

### Network shares and file-based data stores

[Azure StorSimple](/azure/storsimple/) offers the most complete integrated storage solution for managing storage tasks between your on-premesis devices and Azure cloud storage. StorSimple is an efficient, cost-effective, and easily manageable storage area network (SAN) solution that eliminates many of the issues and expenses associated with enterprise storage and data protection. It uses the proprietary StorSimple 8000 series device, integrates with cloud services, and provides a set of management tools for a seamless view of all enterprise storage, including cloud storage.

Another way to use on-premises network shares alongside cloud-based file storage is with [Azure Files](/azure/storage/files/storage-files-introduction). Azure Files offers fully managed file shares that you can access with the standard [Server Message Block](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx?f=255&MSPPError=-2147217396) (SMB) protocol (sometimes referred to as CIFS). You can mount Azure Files as a file share on your local computer, or use them with existing applications that access local or network share files.

To synchronize file shares in Azure Files with your on-premises Windows Servers, use [Azure File Sync](/azure/storage/files/storage-sync-files-planning). One major benefit of Azure File Sync is the ability to tier files between your on-premises file server and Azure Files. This lets you keep only the newest and most recently accessed files locally. 

For more information, see [Deciding when to use Azure Blob storage, Azure Files, or Azure Disks](/azure/storage/common/storage-decide-blobs-files-disks).

## Hybrid networking

This article focused on hybrid data solutions, but another consideration is how to extend your on-premised network to Azure. For more information about this aspect of hybrid solutions, see the following topics:

- [Choose a solution for connecting an on-premises network to Azure](../../reference-architectures/hybrid-networking/considerations.md)

- [Hybrid network reference architectures](../../architecture/reference-architectures/hybrid-networking/index.md)

## Technology choices

- [Pipeline orchestration, control flow, and data movement](../technology-choices/pipeline-orchestration-data-movement.md)
- [Analytical Data Stores](../technology-choices/analytical-data-stores.md)
- [Data transfer](../technology-choices/data-transfer.md)
- [Data Storage](../technology-choices/data-storage.md)