---
title: Choosing a data transfer technology
description: 
author: zoinerTejada
ms:date: 02/09/2018
---

# Transferring data to and from Azure

There are several options for transferring data to and from Azure, depending on your needs.

## Physical transfer

Using physical hardware to transfer data to Azure is a great option when your network is too slow or unreliable, getting additional network bandwidth is cost-prohibitive, or when security or organizational policies do not allow outbound connections when dealing with sensitive data. If the amount of time to transfer your data is your primary concern, you may want to perform a calculation and test to check whether physically transporting your data is actually slower than transporting over the network.

### Azure Import/Export service

The [Azure Import/Export service](/azure/storage/common/storage-import-export-service) allows you to securely transfer large amounts of data to Azure Blob Storage or Azure Files by shipping **internal** SATA HDDs or SDDs to an Azure datacenter. This can also be used to transfer data from Azure Storage to hard disk drives and have them shipped to you for loading on-premises.

You can use this service in scenarios such as:

- **Migrating data to the cloud**: Move large amounts of data to Azure quickly and cost effectively.
- **Backup**: Take backups of your on-premises data to store in Azure Storage when transferring over your network is not a viable option.
- **Data recovery**: Recover large amounts of data stored in Azure Storage and have it delivered to your on-premises location.

Back up a series of folders or a list of files to send to the service. You will need to use the [Azure Import/Export tool](/azure/storage/common/storage-import-export-tool-setup) to prepare your hard drive(s) that you'll send to the service.

The [detailed steps for using this service](/azure/storage/common/storage-import-export-service) can be simplified to the following:

* Step 1: Prepare the drive(s) using [WAImportExport tool](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip) and generate journal file(s)
* Step 2: Create an Import Job in Azure
* Step 3: Ship the drive(s) to the Azure Datacenter shipping address provided in Step 2
* Step 4: Update the job created in Step 2 with the tracking number of the shipment

### Azure Data Box

[Azure Data Box](https://azure.microsoft.com/services/storage/databox/) is a Microsoft-provided appliance that works much like the Azure Import/Export service, in that it allows you to offline-transfer large data sets to Azure in a secure, human-portable way. Microsoft ships you the proprietary, secure, and tamper-resistant transfer appliance and handles the end-to-end logistics, which you can track through the portal. One benefit the Azure Data Box service has over the Azure Import/Export service, is ease of use. With Azure Data Box, you don't need to purchase several hard drives, prepare them, and transfer files to each one until it reaches capacity.

Azure Data Box is supported by a number of industry-leading Azure partners to make it easier to seamlessly leverage offline transport to the cloud from their products. 

## Command line tools and APIs

These options should be considered when you want scripted and programmatic data movement, to integrate data movement into an existing application, and to automate your data transfer workloads.

### Azure CLI

The [Azure CLI](/azure/hdinsight/hdinsight-upload-data#commandline) is a cross-platform tool that allows you to manage Azure services and upload data to Azure Storage. To use the CLI, [install it](/azure/cli-install-nodejs), [connect it with your Azure subscription](/azure/xplat-cli-connect), then run the `azure` commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.

### AzCopy

Use AzCopy from a [Windows](/azure/storage/common/storage-use-azcopy?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) or [Linux](/azure/storage/common/storage-use-azcopy-linux?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) command-line to easily copy data to and from Azure Blob, File, and Table storage with optimal performance. AzCopy is very widely used for a variety of data transfer options to Azure, due to advantages like concurrency and parallelism, the ability to resume copy operations when interrupted, and greater speed than most other options.

If you would like to programmatically integrate AzCopy functionality into your .NET applications, or with just a simple, cross-platform .NET Core console application, consider using the [Microsoft Azure Storage Data Movement Library](/azure/storage/common/storage-use-data-movement-library). This library is the core data movement framework that powers AzCopy, and allows you to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and more.

### PowerShell

Another command-line option is to use the [`Start-AzureStorageBlobCopy` PowerShell cmdlet](/powershell/module/azure.storage/start-azurestorageblobcopy?view=azurermps-5.0.0), a familiar option for Windows administrators who are used to PowerShell. This cmdlet can be used alongside other cmdlets by using the pipeline operator. 

### AdlCopy

[AdlCopy](/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) enables you to copy data from Azure Storage Blobs into Data Lake Store. It can also be used to copy data between two Azure Data Lake Store accounts. However, it cannot be used to copy data from Data Lake Store to Storage Blobs.

AdlCopy can be used in two different modes:

- **Standalone**, where the tool uses Data Lake Store resources to perform the task. This mode is best used for small transfers on an ad hoc basis.
- **Using a Data Lake Analytics account**, where the units assigned to your Data Lake Analytics account are used to perform the copy operation. You might want to use this option when you are looking to perform the copy tasks in a predictable manner.

### Distcp

If you have an HDInsight cluster with access to Data Lake Store, you can use Hadoop ecosystem tools like [Distcp](/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp) to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.

### Sqoop

[Sqoop](/azure/hdinsight/hadoop/hdinsight-use-sqoop) is an Apache project and part of the Hadoop ecosystem. It comes preinstalled on all HDInsight clusters. It allows data transfer between an HDInsight cluster and relational databases such as SQL, Oracle, MySQL, and so on. Sqoop is a collection of related tools, for example import, export, list-all-tables, and list-databases. To use Sqoop, you specify the tool you want to use and the arguments that control the tool. For more information on Sqoop, please refer to the [Sqoop User Guide](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html).

You only need to use Sqoop when you are trying to import/export data between Hadoop and a relational database. It works with both Azure Storage blobs and Data Lake Store.

### PolyBase

[PolyBase](/sql/relational-databases/polybase/get-started-with-polybase) is a technology that accesses data outside of the database via the T-SQL language. In SQL Server 2016, it allows you to run queries on external data in Hadoop or to import/export data from Azure Blob Storage. Queries are optimized to push computation to Hadoop. In Azure SQL Data Warehouse, you can import/export data from Azure Blob Storage and Azure Data Lake Store. Currently, PolyBase is the fastest method of importing data into SQL Data Warehouse.

View [sample syntax](/sql/relational-databases/polybase/get-started-with-polybase#create-t-sql-objects) for creating T-SQL objects that use PolyBase to import data from Hadoop or Azure Blob Storage.

### Hadoop command line

When you have data that resides on an HDInsight cluster head node, you can use the `hadoop -copyFromLocal` command to copy that data to your cluster's attached storage, such as Azure Storage blob or Azure Data Lake Store. In order to use the Hadoop command, you must first connect to the head node. Once connected, you can upload a file to storage.

## Graphical user interface tools

### Azure Storage Explorer

[Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) is a cross-platform tool that allows you to easily manage the contents of your Azure storage accounts. It allows you to upload, download, and manage blobs, files, queues, tables, and Azure Cosmos DB entities. You can also use it to obtain shared access signature (SAS) keys, and configure cross-origin resource sharing (CORS) rules. Use it with Blob storage to manage blobs and folders, as well as upload and download blobs between your local file system and Blob storage, or between storage accounts.

### Azure portal

Both Blob storage and Data Lake Store provide a web-based interface for exploring files and uploading new files one at a time. This is a good option if you do not want to install any tools or issue commands to quickly explore your files, or to simply upload a handful of new ones.

### Azure Data Factory

[Azure Data Factory](/azure/data-factory/) is a powerful, cloud-based service best suited for regularly transferring files between a number of Azure services, on-premises, or a combination of the two. Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores. It can process and transform the data by using compute services such as Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics, and Azure Machine Learning. In other words, Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows in the cloud for [orchestrating](../technology-choices/pipeline-orchestration-data-movement.md) and automating data movement and data transformation.

If your data store is behind a firewall and you are using v1 of Data Factory, use a [data management gateway](/azure/data-factory/v1/data-factory-data-management-gateway) that's installed in your on-premises environment to move the data instead. If using version 2 of Data Factory, use the new self-hosted [integration runtime](/azure/data-factory/create-self-hosted-integration-runtime) (IR) in place of the data management gateway.

## Data ingestion

Your data sources may need to be ingested into Azure, rather than simply copied from a data storage location. An example of this is ingesting telemetry data from internet of things (IoT) devices. Other examples include clickstream data from web applications, or distributed software. Read the [data ingest](../technology-choices/data-storage.md) technology choices article for more information.


## Key Selection Criteria

For data transfer scenarios, choose the appropriate system for your needs by answering these questions:

- Do you need to transfer very large amounts of data, where doing so over an Internet connection would take too long, be unreliable, or too expensive?
    - If yes, then narrow your options to those that deal with physical media.
- Do you prefer to script your data transfer tasks with the added benefit of reusability and consistency?
    - If so, select one of the command line options, or orchestration if you wish to transfer on a scheduled basis.
- Do you need to transfer a very large amount of data over a network connection?
    - If so, select one of the big data options.
- Do you need to transfer data to/from a relational database?
    - If yes, narrow your options to those that support one or more relational databases, taking note of which options also require a Hadoop cluster, which may or may not fit your needs.

## Capability matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

### Physical media capabilities

| | Azure Import/Export service | Azure Data Box |
| --- | --- | --- |
| Form factor | Internal SATA HDDs or SDDs | Secure, tamper-proof, single hardware appliance |
| Microsoft manages shipping logistics | No | Yes |
| Integrates with partner products | No | Yes |
| Reduces administrative overhead of purchasing, preparing, and copying data to multiple drives | No | Yes |

### Network transfer options

#### Command line capabilities

| | Azure CLI | AzCopy | PowerShell | AdlCopy | Distcp | Sqoop | PolyBase | Hadoop command line |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Compatible platform(s) | Linux, OS X, Windows | Linux, Windows | Windows | Linux, OS X, Windows | Hadoop/HDInsight * | Hadoop/HDInsight * | Windows w/ SQL Server instance, Azure SQL Data Warehouse | Hadoop/HDInsight * |
| Copy to/from relational database | No | No | No | No | No | Yes | Yes | No |
| Copy to Blob storage | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes |
| Copy from Blob storage | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No |
| Copy to Data Lake Store | No | No | Yes | Yes | Yes | Yes | Yes | Yes |
| Copy from Data Lake Store | No | No | Yes | Yes | Yes | Yes | Yes | No |
| Optimized for big data | No | No | No | Yes ** | Yes | Yes | Yes *** | Yes |

\* Can be run from a command line/shell session invoked from Linux, OS X, or Windows.

\** AdlCopy is optimized for transferring big data when used with a Data Lake Analytics account.

\*** PolyBase [performance can be increased](/sql/relational-databases/polybase/polybase-guide#performance) by pushing computation to Hadoop and using [PolyBase  scale-out groups](/sql/relational-databases/polybase/polybase-scale-out-groups) to enable parallel data transfer between SQL Server instances and Hadoop nodes.

#### Graphical user interface capabilities

| | Azure Storage Explorer | Azure portal * | Azure Data Factory |
| --- | --- | --- | --- |
| Copy to/from relational database | No | No | Yes |
| Copy to Blob storage | Yes | No | Yes |
| Copy from Blob storage | Yes | No | Yes |
| Copy to Data Lake Store | No | No | Yes |
| Copy from Data Lake Store | No | No | Yes |
| Upload to Blob storage | Yes | Yes | Yes |
| Upload to Data Lake Store | Yes | Yes | Yes |
| Orchestrate data transfers | No | No | Yes |
| Custom data transformations | No | No | Yes |
| Pricing model | Free | Free | Pay per usage |

\* Azure portal in this case means using the web-based exploration tools for Blob storage and Data Lake Store. This excludes using the portal for other services, such as Azure Data Factory.

