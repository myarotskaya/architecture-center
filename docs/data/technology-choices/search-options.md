---
title: Choosing a search data store
description: 
author: zoinerTejada
ms:date: 02/09/2018
---

# Choosing a search data store

## What are your options when choosing a search data store?
In Azure, all of the following data stores will meet the core requirements for search against free-form text data by providing a search index:
- [Azure Search](/azure/search/search-what-is-azure-search)
- [ElasticSearch](https://azuremarketplace.microsoft.com/marketplace/apps/elastic.elasticsearch?tab=Overview)
- [HDInsight with Solr](/azure/hdinsight/hdinsight-hadoop-solr-install-linux)
- [SQL Server or Azure SQL Database with full text search](/sql/relational-databases/search/full-text-search)

## How do you choose?
Each data store brings with it a unique set of capabilities, giving you the option to select the one that most closely meets your requirements. 

## Key selection criteria

For search scenarios, begin choosing the appropriate search data store for your needs by answering these questions:
- Do you want a managed service or do you prefer to setup and manage the cluster of virtual machines running the search data store?
    - If yes, then narrow your options to those that are managed services.
- Can you specify your index schema upfront?
    - If yes, then narrow your options to those that are schema on write.
- Do you need an index only for full-text search, or do you also need rapid aggregation of numeric data and other analytics?
    - If you need functionality beyond full-text search, then examine the options that support analytics beyond full text search.
- Do you need a search index for log analytics scenarios, that provides support for log collection, aggregation as well as visualizations on indexed data?
    - If yes, then you should consider the options that are part of a log analytics stack.
- Do you need support for semantic search such as identifying documents related to a given document or extracting the key phrases in a document?
    - If yes, consider the options that support semantic search.
- Do you need to index data in files on disk formats like plain text, PDF, Word, PowerPoint, and Excel?
    - If yes, consider the options that provide document indexers.
- Does your database have specific security needs?
    - If yes, examine the options that provide capabilities like transparent data encryption, authentication with Azure Active Directory and IP-based or virtual network&ndash;based access controls.

## Capability matrix

The following tables summarize the key differences in capabilities between each.

### General capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- | 
| Is managed service | Yes | No | Yes | Yes (for SQL DB and SQL Server managed instances) |  
| REST API | Yes | Yes | Yes | No |
| Programmability | .NET | Java | Java | T-SQL | 
| Document indexers for common file types (PDF, DOCX, TXT, and so on) | Yes | No | Yes | No |

### Manageability capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- |
| Index schema definition | Schema fixed during creation | Updateable schema | Updateable schema | Updateable schema |
| Supports scale out  | Yes | Yes | Yes | No |

### Analytic workload capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- | 
| Supports analytics beyond full text search | No | Yes | Yes | Yes |
| Part of a log analytics stack | No | Yes (ELK) |  No | No |
| Supports semantic search | Yes (find similar documents only) | Yes | Yes | Yes | 

### Security capabilities
| | Azure Search | ElasticSearch | HDInsight with Solr | SQL Server or SQL DB with full text search | 
| --- | --- | --- | --- | --- | 
| Row-level security | Partial (requires application query to filter by group id) | Partial (requires application query to filter by group id) | Yes | Yes | 
| Transparent data encryption | No | No | No | Yes |  
| Restrict access to specific IP addresses | No | Yes | Yes | Yes |   
| Restrict access to allow virtual network access only | No | Yes | Yes | Yes |  
| Active Directory authentication (integrated authentication) | No | No | No | Yes | 

