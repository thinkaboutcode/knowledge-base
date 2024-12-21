# Overview of Data Tools

## Table of Contents
1. [Apache NiFi](#1-apache-nifi)
    - [Example: Simple Data Flow in NiFi](#example-simple-data-flow-in-nifi)
2. [Apache Drill](#2-apache-drill)
    - [Example: Querying a JSON File in Drill](#example-querying-a-json-file-in-drill)
3. [Apache Pulsar](#3-apache-pulsar)
    - [Example: Producing and Consuming Messages in Pulsar](#example-producing-and-consuming-messages-in-pulsar)
        - [Producer Example](#producer-example)
        - [Consumer Example](#consumer-example)
4. [Dremio](#4-dremio)
    - [Example: Creating a Virtual Dataset in Dremio](#example-creating-a-virtual-dataset-in-dremio)

---

# Overview of Data Tools

## 1. Apache NiFi
- **Purpose**: Apache NiFi is a data integration and workflow automation tool designed to automate the flow of data between systems.
- **Features**:
    - **Data Flow Management**: Automates the movement of data between different sources and destinations, supporting various data formats and protocols.
    - **Real-Time Processing**: Processes and routes data in real-time for near-instantaneous decision-making.
    - **Extensibility**: Includes a wide range of processors for different data tasks; users can build custom processors.
    - **Security**: Strong security features like fine-grained access control, data encryption, and SSL/TLS support.
- **Use Cases**: Data ingestion from IoT devices, streaming data pipelines, and ETL processes.

### Example: Simple Data Flow in NiFi
You can create a simple flow that fetches data from an HTTP endpoint and writes it to a file. Here’s a conceptual setup:

1. **GetHTTP** processor to fetch data:
    - **Properties**:
        - URL: `https://api.example.com/data`

2. **PutFile** processor to save the data:
    - **Properties**:
        - Directory: `/data/output`
        - Filename: `data.json`

Here’s a sample NiFi flow in JSON format:
```json
{
  "processors": [
    {
      "id": "GetHTTP",
      "type": "org.apache.nifi.processors.standard.GetHTTP",
      "properties": {
        "url": "https://api.example.com/data"
      }
    },
    {
      "id": "PutFile",
      "type": "org.apache.nifi.processors.standard.PutFile",
      "properties": {
        "Directory": "/data/output",
        "File Name": "data.json"
      }
    }
  ],
  "connections": [
    {
      "source": "GetHTTP",
      "destination": "PutFile"
    }
  ]
}
```

## 2. Apache Drill
- **Purpose**: Apache Drill is an open-source SQL query engine for big data exploration, designed to query large datasets from various sources.
- **Features**:
    - **Schema-Free**: Queries data without defining a schema beforehand.
    - **Support for Multiple Formats**: Supports a variety of data formats, including JSON, Parquet, CSV, etc.
    - **SQL Compatibility**: Uses standard SQL for querying, making it accessible for SQL developers.
    - **Scalability**: Handles queries on datasets from kilobytes to petabytes.
- **Use Cases**: Ad hoc querying of semi-structured data, data exploration, and combining data from different sources for analysis.

### Example: Querying a JSON File in Drill
Assuming you have a JSON file containing user data stored in HDFS, you can run a query like this:

```sql
SELECT name, age
FROM dfs.`/path/to/user_data.json`
WHERE age > 25
ORDER BY age DESC;
```

## 3. Apache Pulsar
- **Purpose**: Apache Pulsar is a distributed messaging and streaming platform designed for high-throughput, low-latency messaging.
- **Features**:
    - **Multi-Tenancy**: Supports multi-tenancy out of the box, ideal for larger organizations or SaaS providers.
    - **Geo-Replication**: Strong support for cross-region replication for global data distribution.
    - **Unified Messaging**: Supports both queuing and streaming use cases in a single system.
    - **Scalability and Performance**: Designed to scale horizontally and handle millions of messages per second with low latency.
- **Use Cases**: Real-time data processing, message queuing, event streaming, and data pipeline orchestration.

### Example: Producing and Consuming Messages in Pulsar

Here’s a simple Java example to produce and consume messages in Apache Pulsar.

#### Producer Example
This example demonstrates how to create a producer that sends messages to a topic:

```java
import org.apache.pulsar.client.api.*;

public class ProducerExample {
    public static void main(String[] args) throws PulsarClientException {
        // Create a Pulsar client
        PulsarClient client = PulsarClient.builder()
                .serviceUrl("pulsar://localhost:6650")
                .build();

        // Create a producer for the topic "my-topic"
        Producer<byte[]> producer = client.newProducer()
                .topic("my-topic")
                .create();

        // Send a message
        producer.send("Hello Pulsar!".getBytes());

        // Clean up
        producer.close();
        client.close();
    }
}
```

#### Consumer Example
```java
import org.apache.pulsar.client.api.*;

public class ConsumerExample {
    public static void main(String[] args) throws PulsarClientException {
        // Create a Pulsar client
        PulsarClient client = PulsarClient.builder()
                .serviceUrl("pulsar://localhost:6650")
                .build();

        // Create a consumer for the topic "my-topic"
        Consumer<byte[]> consumer = client.newConsumer()
                .topic("my-topic")
                .subscriptionName("my-subscription")
                .subscribe();

        while (true) {
            // Wait for a message
            Message<byte[]> msg = consumer.receive();
            System.out.printf("Received message: %s%n", new String(msg.getData()));

            // Acknowledge the message
            consumer.acknowledge(msg);
        }
    }
}
```
In these examples:

The Producer connects to Pulsar and sends a message "Hello Pulsar!" to the specified topic.
The Consumer listens for messages from the topic and prints them out, acknowledging each message after processing.

## 4. Dremio
- **Purpose**: Dremio is a data-as-a-service platform that enables users to explore and query data directly from various data sources with high performance.
- **Features**:
    - **Data Virtualization**: Access data from multiple sources without moving or duplicating it.
    - **Apache Arrow**: Leverages the Apache Arrow in-memory format for fast and efficient data processing.
    - **Self-Service**: Allows users to create virtual datasets and run queries easily.
    - **Acceleration Engine**: Offers a data reflection mechanism to cache intermediate results for faster query performance.
- **Use Cases**: Interactive analytics on large datasets, data lake query acceleration, and simplifying data preparation for BI tools.

### Example: Creating a Virtual Dataset in Dremio
After connecting to your data sources in Dremio, you can create a virtual dataset using SQL. Below is an example SQL query that aggregates user orders:

```sql
SELECT
    user_id,
    COUNT(*) AS order_count
FROM
    orders
GROUP BY
    user_id
ORDER BY
    order_count DESC;
```
