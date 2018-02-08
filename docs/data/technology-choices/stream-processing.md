---
title: Choosing a stream processing technology
description: 
author: zoinerTejada
ms:date: 02/09/2018
---

# Choosing a stream processing technology

Real-time processing components consume events or messages from either queue or file based storage, with the goal of inspecting, querying, filtering, and aggregating events. Then forwarding the outcome to another message queue, file store, or database. In some cases, they may invoke REST methods that trigger an application function like sending out an alert or updating a real-time visualization. The key requirement of such processing engines is that they are capable of applying their computation to endless streams of data and produce results with minimal latency, in a near real-time fashion.

## What are your options when choosing a technology for real-time processing?
In Azure, all of the following data stores will meet the core requirements supporting real-time processing:
- [Azure Stream Analytics](/azure/stream-analytics/)
- [HDInsight with Spark Streaming](/azure/hdinsight/spark/apache-spark-streaming-overview)
- [HDInsight with Storm](/azure/hdinsight/storm/apache-storm-overview)
- [Azure Functions](/azure/azure-functions/functions-overview)
- [Azure App Service WebJobs](/azure/app-service/web-sites-create-web-jobs)

## Key Selection Criteria

For real-time processing scenarios, begin choosing the appropriate service for your needs by answering these questions:

- Do you want to author stream processing logic declaratively or imperatively?

- Do you need built-in support for temporal processing or windowing?

- Does your data arrive in formats besides Avro, JSON, or CSV? If yes, consider options support any format using custom code.

- Do you need to scale your processing beyond 1 GB/s? If yes, consider the options that scale with the cluster size. 

## Capability matrix

The following tables summarize the key differences in capabilities. 

### General capabilities
| | Azure Stream Analytics | HDInsight with Spark Streaming | HDInsight with Storm | Azure Functions | Azure App Service WebJobs |
| --- | --- | --- | --- | --- | --- | 
| Programmability | Stream analytics query language, JavaScript | Scala, Python, Java | Java, C# | C#, F#, Node.js | C#, Node.js, PHP, Java, Python |
| Programming paradigm | Declarative | Mixture of declarative and imperative | Imperative | Imperative | Imperative |    
| Pricing model | By streaming units | By cluster hour | By cluster hour | Per function execution and resource consumption | Per app service plan hour |  

### Integration capabilities
| | Azure Stream Analytics | HDInsight with Spark Streaming | HDInsight with Storm | Azure Functions | Azure App Service WebJobs |
| --- | --- | --- | --- | --- | --- | 
| Inputs | [Stream Analytics inputs](/azure/stream-analytics/stream-analytics-define-inputs)  | Event Hubs, IoT Hub, Kafka, HDFS  | Event Hubs, IoT Hub, Storage Blobs, Azure Data Lake Store  | [Supported bindings](/azure/azure-functions/functions-triggers-bindings#supported-bindings) | Service Bus, Storage Queues, Storage Blobs, Event Hubs, WebHooks, Cosmos DB, Files |
| Sinks |  [Stream Analytics outputs](/azure/stream-analytics/stream-analytics-define-outputs) | HDFS | Event Hubs, Service Bus, Kafka | [Supported bindings](/azure/azure-functions/functions-triggers-bindings#supported-bindings) | Service Bus, Storage Queues, Storage Blobs, Event Hubs, WebHooks, Cosmos DB, Files | 

### Processing capabilities
| | Azure Stream Analytics | HDInsight with Spark Streaming | HDInsight with Storm | Azure Functions | Azure App Service WebJobs |
| --- | --- | --- | --- | --- | --- | 
| Built-in temporal/windowing support | Yes | Yes | Yes | No | No |
| Input data formats | Avro, JSON or CSV, UTF-8 encoded | Any format using custom code | Any format using custom code | Any format using custom code | Any format using custom code |
| Scalability | Up to 1 GB/second | Bounded by cluster size | Bounded by cluster size | Up to 200 function app instances processing in parallel | Bounded by app service plan capacity | 
| Late arrival and out of order event handling support | Yes | Yes | Yes | No | No |


See also:

- [Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics](/azure/stream-analytics/stream-analytics-comparison-storm)
