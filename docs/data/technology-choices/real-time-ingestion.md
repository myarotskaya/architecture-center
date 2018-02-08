---
title: Choosing a real-time message ingestion technology
description: 
author: zoinerTejada
ms:date: 02/09/2018
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

- Do you need two-way communication between your IoT devices and Azure? If so, choose IoT Hub.

- Do you need to manage access for individual devices and be able to revoke access to a specific device? If yes, choose IoT Hub.

## Capability matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

| | IoT Hub | Event Hubs | Kafka on HDInsight |
| --- | --- | --- | --- |
| Cloud-to-device communications | Yes | No | No |
| Device-initiated file upload | Yes | No | No |
| Device state information | [Device twins](/azure/iot-hub/iot-hub-devguide-device-twins) | No | No |
| Protocol support | MQTT, AMQP, HTTPS <sup>1</sup> | AMQP, HTTPS | [Kafka Protocol](https://cwiki.apache.org/confluence/display/KAFKA/A+Guide+To+The+Kafka+Protocol) |
| Security | Per-device identity; revocable access control. | Shared access policies; limited revocation through publisher policies. | Authentication using SASL; pluggable authorization; integration with external authentication services supported. |

[1] You can also use [Azure IoT protocol gateway](/azure/iot-hub/iot-hub-protocol-gateway) as a custom gateway to enable protocol adaptation for IoT Hub.

For more information, see [Comparison of Azure IoT Hub and Azure Event Hubs](/azure/iot-hub/iot-hub-compare-event-hubss).