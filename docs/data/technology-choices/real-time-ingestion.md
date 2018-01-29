---
title: Choosing a real-time message ingestion technology
description: 
author: zoinerTejada
ms:date: 01/17/2018
---

# Choosing a real-time message ingestion technology

## What are your options for real-time message ingestion?

- [Azure Event Hubs](/azure/event-hubs/)
- [Azure IoT Hub](/azure/iot-hub/)
- [Kafka on HDInsight](/azure/hdinsight/kafka/apache-kafka-get-started)

## Azure Event Hubs

[Azure Event Hubs](/azure/event-hubs/) is a highly scalable data streaming platform and event ingestion service, capable of receiving and processing millions of events per second. Event Hubs can process and store events, data, or telemetry produced by distributed software and devices. Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters. Event Hubs provides publish-subscribe capabilities with low latency at massive scale, which makes it appropriate for big data scenarios.

## Azure IoT Hub

[Azure IoT Hub](/azure/iot-hub/) is a fully managed service that enables reliable and secure bidirectional communications between millions of IoT devices and a cloud-based back end.

Azure IoT Hub:

* Provides multiple device-to-cloud and cloud-to-device communication options. These options include one-way messaging, file transfer, and request-reply methods.
* Provides built-in declarative message routing to other Azure services.
* Provides a queryable store for device metadata and synchronized state information.
* Enables secure communications and access control using per-device security keys or X.509 certificates.
* Provides extensive monitoring for device connectivity and device identity management events.
* Includes device libraries for the most popular languages and platforms.

IoT Hub is often compared to Event Hubs, and some confusion is common when deciding between the two, due to their similarity. When you are managing an IoT infrastructure, even if the only use case is device-to-cloud telemetry ingress, IoT Hub provides a service that is designed for IoT device connectivity. It continues to expand the value proposition for these scenarios with IoT-specific features. Event Hubs is designed for event ingress at a massive scale, both in the context of inter-datacenter and intra-datacenter scenarios.

> [!NOTE]
> For a comparison of Azure Event Hubs and Azure IoT Hubs, see [Comparison of Azure IoT Hub and Azure Event Hubs](/azure/iot-hub/iot-hub-compare-event-hubs). 

It is not uncommon to use a combination of IoT Hub and Event Hubs or [Kafka](https://github.com/Azure/toketi-kafka-connect-iothub) in the same solution. IoT Hub handles the device-to-cloud communication, and Event Hubs or Kafka handles later-stage event ingress into real-time processing engines.

## Kafka on HDInsight

[Apache Kafka](https://kafka.apache.org/) is an open-source distributed streaming platform that can be used to build real-time data pipelines and streaming applications. Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams. It is horizontally scalable, fault-tolerant, and extremely fast.

[Kafka on HDInsight](/azure/hdinsight/kafka/apache-kafka-get-started) provides you with a managed, highly scalable, and highly available service in Azure. Both Kafka and Event Hubs can be used as your stream buffering layer in your real-time data pipeline when ingesting events. Use the [Streaming/real-time ingest capabilities](#streamingreal-time-ingest-capabilities) matrix to compare these options.

Some common use cases for Kafka are:

* **Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.
* **Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities. For example, user actions on a web site or within an application.
* **Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.
* **Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.


## Key selection criteria

- Do you need to capture streaming data in real time, from a number of sources (like cloud to cloud, on-premises to cloud, or intra-cloud), but only need high throughput ingestion capabilities without any sort of device management?
    - If yes, narrow your streaming/real-time ingest capability options to those that only enable event ingress. This could potentially save you money when cloud-to-device communications are not needed.
- Do you need two-way communication between your IoT devices and your cloud-based streaming platform?
    - If so, narrow your streaming/real-time ingest capability options to those that provide cloud-to-device communication patterns.
- Does your streaming solution require the ability to manage access for individual devices, and have the ability to revoke access to a specific device?
    - If yes, select the service with a security capability that provides per-device identity and revocable access control.
- Can you use the service in your region?
    - Check the [regional availability for each Azure service](https://azure.microsoft.com/regions/#services) to find out. If the service you want to use is not in your region, or nearby, then that could automatically disqualify it from your options. This is especially true in situations when data sovereignty is a high priority.

## Capability matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

| | IoT Hub | Event Hubs | Kafka on HDInsight |
| --- | --- | --- | --- |
| Communication patterns | Enables [device-to-cloud communications](/azure/iot-hub/iot-hub-devguide-d2c-guidance) (messaging, file uploads, and reported properties) and [cloud-to-device communications](/azure/iot-hub/iot-hub-devguide-c2d-guidance) (direct methods, desired properties, messaging) | Only enables event ingress (usually considered for device-to-cloud scenarios) | Only enables event ingress (usually considered for device-to-cloud scenarios) |
| Device state information | [Device twins](/azure/iot-hub/iot-hub-devguide-device-twins) can store and query device state information | No device state information can be stored | No device state information can be stored |
| Device protocol support |Supports MQTT, MQTT over WebSockets, AMQP, AMQP over WebSockets, and HTTPS. Additionally, IoT Hub works with the [Azure IoT protocol gateway](/azure/iot-hub/iot-hub-protocol-gateway), a customizable protocol gateway implementation to support custom protocols. |Supports AMQP, AMQP over WebSockets, and HTTPS | [Kafka](https://cwiki.apache.org/confluence/display/KAFKA/A+Guide+To+The+Kafka+Protocol) (proprietary binary protocol over TCP) |
| Security |Provides per-device identity and revocable access control. See the [Security section of the IoT Hub developer guide](/azure/iot-hub/iot-hub-devguide-security). | Provides Event Hubs-wide [shared access policies](/azure/event-hubs/event-hubs-authentication-and-security-model-overview), with limited revocation support through [publisher's policies](/azure/event-hubs/event-hubs-features#event-publishers). IoT solutions are often required to implement a custom solution to support per-device credentials and anti-spoofing measures. | Use SSL or SASL to authenticate connections to brokers from clients. Optional encryption of data transferred between brokers and clients via SSL. Authorization is pluggable. Integration with external auth services supported. Read [security documentation](https://kafka.apache.org/documentation/#security). |
| Operations monitoring | Enables IoT solutions to subscribe to a rich set of device identity management and connectivity events such as individual device authentication errors, throttling, and bad format exceptions. These events enable you to quickly identify connectivity problems at the individual device level. | Exposes only aggregate metrics | [Use Log Analytics](/azure/hdinsight/hdinsight-hadoop-oms-log-analytics-tutorial) (part of OMS) to monitor HDInsight clusters. Kafka has a [cluster-specific management solution](/azure/hdinsight/hdinsight-hadoop-oms-log-analytics-management-solutions) for Log Analytics. [Additional tools](/azure/hdinsight/hdinsight-key-scenarios-to-monitor) can be used to monitor the cluster. |
| Scale | Is optimized to support millions of simultaneously connected devices | Meters the connections as per [Azure Event Hubs quotas](/azure/event-hubs/event-hubs-quotas). On the other hand, Event Hubs enables you to specify the partition for each message sent. | Use [Azure Managed Disks](/azure/hdinsight/kafka/apache-kafka-scalability) to increase throughput and scalability. Increase number of cluster nodes to scale horizontally. |
| Device SDKs | Provides [device SDKs](https://github.com/Azure/azure-iot-sdks) for a large variety of platforms and languages, in addition to direct MQTT, AMQP, and HTTPS APIs | Is supported on .NET, Java, and C, in addition to AMQP and HTTPS send interfaces | Java, HTTP REST, [other non-Java clients](https://cwiki.apache.org/confluence/display/KAFKA/Clients) |
| File upload | Enables IoT solutions to upload files from devices to the cloud. Includes a file notification endpoint for workflow integration and an operations monitoring category for debugging support. | Not supported | Not supported |
| Route messages to multiple endpoints | Up to 10 custom endpoints are supported. Rules determine how messages are routed to custom endpoints. For more information, see [Send and receive messages with IoT Hub](/azure/iot-hub/iot-hub-devguide-messaging). | Requires additional code to be written and hosted for message dispatching | Kafka partitions streams across the nodes in the HDInsight cluster. Consumer processes can be associated with individual partitions to provide load balancing when consuming records. |
