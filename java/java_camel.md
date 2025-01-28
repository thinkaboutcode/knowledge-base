# Apache Camel

## Table of Contents
1. [Overview of Apache Camel](#overview-of-apache-camel)
2. [Key Concepts in Apache Camel](#key-concepts-in-apache-camel)
3. [Key Features of Apache Camel](#key-features-of-apache-camel)
4. [Apache Camel Architecture](#apache-camel-architecture)
5. [Examples and Code Snippets](#examples-and-code-snippets)
    - [Example 1: A Simple File Copy Route](#example-1-a-simple-file-copy-route)
    - [Example 2: HTTP Request to Transform and Log Data](#example-2-http-request-to-transform-and-log-data)
    - [Example 3: Content-Based Routing](#example-3-content-based-routing)
    - [Example 4: Kafka Integration](#example-4-kafka-integration)
    - [Example 5: Aggregator Pattern](#example-5-aggregator-pattern)
6. [Running Apache Camel in Spring Boot](#running-apache-camel-in-spring-boot)
7. [Advanced Topics](#advanced-topics)
8. [Summary](#summary)

---

### Overview of Apache Camel

Apache Camel is an open-source integration framework that simplifies the process of integrating different systems, applications, and technologies. It provides a standardized approach to handling messaging, routing, and data transformation using predefined **Enterprise Integration Patterns (EIPs)**.

---

### Key Concepts in Apache Camel

1. **Routes**  
   Camel operates based on the concept of routes, which define how messages flow from a source to a destination.

2. **Components**  
   Apache Camel supports various components (connectors) for interacting with different technologies like HTTP, FTP, JMS, Kafka, databases, and more.

3. **DSL (Domain-Specific Language)**  
   Camel routes can be defined using different DSLs, such as Java, XML, or Spring Boot.

4. **Exchange**  
   The exchange is the container for the message and its metadata as it flows through the route.

5. **Processors**  
   Processors allow you to apply custom logic to messages during the routing process.

6. **Enterprise Integration Patterns (EIPs)**  
   Apache Camel implements many well-known EIPs, such as Content-Based Routing, Splitter, Aggregator, and more.

---

### Key Features of Apache Camel

- **Protocol and Data Format Agnostic**: Supports a wide range of protocols and data formats.
- **Rich Ecosystem**: Includes over 300 components to simplify integration tasks.
- **Integration Made Easy**: Allows declarative routing using a fluent DSL.
- **Error Handling**: Built-in mechanisms for retry, dead-letter queues, and exception handling.
- **Lightweight**: Can be embedded in standalone applications or deployed in containers.

---

### Apache Camel Architecture

The architecture revolves around:
1. **Camel Context**: Central container managing all Camel routes.
2. **Endpoints**: Sources or destinations for messages.
3. **Routes**: Connect endpoints and define the processing pipeline.
4. **Processors**: Perform business logic on messages.

---

### Examples and Code Snippets

#### Example 1: A Simple File Copy Route
This example reads files from a source directory and writes them to a target directory.

**Code: Java DSL**
```java
import org.apache.camel.CamelContext;
import org.apache.camel.builder.RouteBuilder;
import org.apache.camel.impl.DefaultCamelContext;

public class FileCopyExample {
    public static void main(String[] args) throws Exception {
        CamelContext context = new DefaultCamelContext();
        
        context.addRoutes(new RouteBuilder() {
            @Override
            public void configure() {
                from("file:input")
                .to("file:output");
            }
        });
        
        context.start();
        Thread.sleep(5000);
        context.stop();
    }
}
```

---

#### Example 2: HTTP Request to Transform and Log Data
This route retrieves data from an HTTP endpoint, processes it, and logs the result.

**Code: Java DSL**
```java
from("timer:fetchData?period=10000") // Trigger every 10 seconds
    .to("http://api.example.com/data") // Fetch data from the API
    .process(exchange -> {
        String body = exchange.getIn().getBody(String.class);
        exchange.getIn().setBody("Processed: " + body);
    })
    .log("${body}");
```

---

#### Example 3: Content-Based Routing
Route messages to different endpoints based on content.

**Code: Java DSL**
```java
from("file:input")
    .choice()
        .when(simple("${file:ext} == 'xml'"))
            .to("file:output/xml")
        .when(simple("${file:ext} == 'json'"))
            .to("file:output/json")
        .otherwise()
            .to("file:output/others");
```

---

#### Example 4: Kafka Integration
Produce and consume messages with Apache Kafka.

**Producer Code**
```java
from("timer:produce?period=1000")
    .setBody(simple("Message sent at ${date:now:yyyy-MM-dd HH:mm:ss}"))
    .to("kafka:my-topic?brokers=localhost:9092");
```

**Consumer Code**
```java
from("kafka:my-topic?brokers=localhost:9092&groupId=myGroup")
    .log("Received: ${body}")
    .to("file:output/kafka");
```

---

#### Example 5: Aggregator Pattern
Aggregate multiple messages into a single message.

**Code: Java DSL**
```java
from("direct:start")
    .aggregate(constant(true), new GroupedBodyAggregationStrategy())
    .completionSize(3) // Aggregate 3 messages at a time
    .log("Aggregated message: ${body}")
    .to("mock:result");
```

---

### Running Apache Camel in Spring Boot

**Spring Boot Dependency**
```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-spring-boot-starter</artifactId>
    <version>3.x.x</version>
</dependency>
```

**Route Example in Spring Boot**
```java
@Component
public class MyCamelRoute extends RouteBuilder {
    @Override
    public void configure() {
        from("file:input")
            .log("Processing file: ${file:name}")
            .to("file:output");
    }
}
```

---

### Advanced Topics
1. **Error Handling**
   ```java
   onException(Exception.class)
       .log("Error occurred: ${exception.message}")
       .handled(true)
       .to("file:error");
   ```

2. **Custom Processor**
   ```java
   public class MyProcessor implements Processor {
       @Override
       public void process(Exchange exchange) throws Exception {
           String body = exchange.getIn().getBody(String.class);
           exchange.getIn().setBody(body.toUpperCase());
       }
   }

   from("direct:start")
       .process(new MyProcessor())
       .to("log:output");
   ```

3. **Split and Aggregate**
   ```java
   from("file:input?fileName=largefile.txt")
       .split(body().tokenize("\n"))
       .streaming()
       .to("direct:processLine");
   ```

---

### Summary

Apache Camel is a powerful framework for solving complex integration problems in a structured and reusable way. Its DSL and rich library of components simplify the implementation of even the most sophisticated use cases. Whether integrating databases, message queues, REST APIs, or file systems, Apache Camel provides the flexibility and tools to get the job done efficiently.
