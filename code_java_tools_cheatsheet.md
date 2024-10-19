# Java Frameworks Cheat Sheet

## 1. **Spring Framework**
A comprehensive framework for building Java applications, especially popular for web, enterprise, and microservices development.

- **Core Features:**
    - Dependency Injection (DI)
    - Aspect-Oriented Programming (AOP)
    - Spring MVC for web applications
    - Spring Boot for rapid application development
    - Spring Cloud for microservices
- **Key Dependencies:**
    - `spring-core`
    - `spring-boot-starter`
    - `spring-web`
- **Use Cases:**
    - RESTful APIs, Microservices, Enterprise apps
- **Website:** [https://spring.io/](https://spring.io/)

## 2. **Hibernate**
A leading Object-Relational Mapping (ORM) framework, integrating Java applications with relational databases.

- **Core Features:**
    - Maps Java objects to database tables
    - Lazy loading, caching
    - HQL (Hibernate Query Language)
    - Automatic schema generation
- **Key Dependencies:**
    - `hibernate-core`
    - `hibernate-entitymanager`
- **Use Cases:**
    - Data persistence and database operations in enterprise applications
- **Website:** [https://hibernate.org/](https://hibernate.org/)

## 3. **Micronaut**
A modern, lightweight JVM framework optimized for microservices, serverless computing, and low-overhead applications.

- **Core Features:**
    - Dependency Injection (DI) without reflection
    - Fast startup times and low memory footprint
    - Built-in HTTP server/client
    - Reactive programming support
    - GraalVM native image support
- **Key Dependencies:**
    - `micronaut-core`
    - `micronaut-http-client`
- **Use Cases:**
    - Microservices, serverless applications, cloud-native apps
- **Website:** [https://micronaut.io/](https://micronaut.io/)

## 4. **Quarkus**
A Kubernetes-native Java framework designed for building cloud-native and microservice applications, optimized for GraalVM and HotSpot.

- **Core Features:**
    - Native image support with GraalVM
    - Fast startup time and low memory usage
    - Seamless integration with frameworks like Hibernate, RESTEasy, and Vert.x
    - Reactive programming support
- **Key Dependencies:**
    - `quarkus-core`
    - `quarkus-hibernate-orm`
    - `quarkus-resteasy`
- **Use Cases:**
    - Cloud-native applications, Microservices, Containerized environments
- **Website:** [https://quarkus.io/](https://quarkus.io/)

## 5. **Jakarta EE**
The successor to Java EE, offering a robust framework for developing enterprise applications, now managed by the Eclipse Foundation.

- **Core Features:**
    - Includes APIs for REST (JAX-RS), Persistence (JPA), Dependency Injection (CDI), and more
    - Simplifies development of large-scale, distributed, and transactional applications
    - Compatible with modern cloud environments
- **Key Dependencies:**
    - `javax.enterprise`
    - `jakarta.persistence`
    - `jakarta.ws.rs`
- **Use Cases:**
    - Large-scale enterprise systems, transactional applications
- **Website:** [https://jakarta.ee/](https://jakarta.ee/)

## 6. **Dropwizard**
A lightweight, open-source Java framework for developing RESTful web services, known for its minimal configuration and out-of-the-box features.

- **Core Features:**
    - Built-in support for RESTful APIs
    - Uses Jetty, Jersey, and Jackson for web handling
    - Production-ready monitoring, metrics, and health checks
    - Integrated with Hibernate for ORM
- **Key Dependencies:**
    - `dropwizard-core`
    - `dropwizard-jersey`
- **Use Cases:**
    - Building microservices and REST APIs quickly
- **Website:** [https://www.dropwizard.io/](https://www.dropwizard.io/)

## 7. **Vert.x**
A lightweight, event-driven, reactive framework for building scalable, high-performance applications, supporting polyglot programming.

- **Core Features:**
    - Non-blocking I/O and event-driven architecture
    - Built-in support for reactive programming
    - Polyglot support (Java, Kotlin, Groovy, JavaScript, etc.)
    - Verticles for modular, concurrent programming
- **Key Dependencies:**
    - `vertx-core`
    - `vertx-web`
- **Use Cases:**
    - High-concurrency web applications, microservices, and real-time systems
- **Website:** [https://vertx.io/](https://vertx.io/)

## 8. **Grails**
A Groovy-based web application framework built on top of Spring Boot, designed for rapid development.

- **Core Features:**
    - Convention over configuration
    - GORM (ORM for Groovy)
    - Built-in testing and scaffolding tools for CRUD apps
    - Plugin architecture for extending functionality
- **Key Dependencies:**
    - `grails-core`
    - `gorm`
- **Use Cases:**
    - Rapid web application development, CRUD systems
- **Website:** [https://grails.org/](https://grails.org/)

## 9. **JHipster**
A development platform for generating, developing, and deploying Spring Boot and Angular/React applications using microservices architecture.

- **Core Features:**
    - Full-stack generation (Java backend + JS frontend)
    - Microservice and monolithic architectures
    - Pre-configured for Spring Boot and modern JavaScript frameworks
    - Supports OAuth2, JWT, and database options like SQL, NoSQL
- **Key Dependencies:**
    - `spring-boot`
    - `jhipster-dependencies`
- **Use Cases:**
    - Full-stack web applications, microservices, rapid prototyping
- **Website:** [https://www.jhipster.tech/](https://www.jhipster.tech/)

## 10. **Vaadin**
A modern Java framework for building rich, dynamic web applications with a focus on a server-driven architecture and UI components.

- **Core Features:**
    - Server-side Java UI components
    - Two-way data binding
    - HTML5, WebSocket, and modern web standards support
    - Integration with Spring and other backends
- **Key Dependencies:**
    - `vaadin-core`
- **Use Cases:**
    - Business web applications, dashboard interfaces
- **Website:** [https://vaadin.com/](https://vaadin.com/)

---

**Tips for Choosing the Right Framework:**
- **Spring Boot** and **Hibernate** are still the go-to for enterprise and large-scale applications.
- **Micronaut** and **Quarkus** are gaining traction for microservices and cloud-native apps.
- **Jakarta EE** is ideal for traditional, large enterprise systems.
- **Vert.x** and **Dropwizard** are preferred for high-concurrency, lightweight, and RESTful APIs.

# Java Libraries Cheat Sheet

## 1. **Jackson**
A widely used library for JSON processing (parsing and generating JSON from Java objects).

- **Core Features:**
    - Serialize/Deserialize Java objects to/from JSON
    - Streaming and tree models
    - Annotations for custom serialization
- **Key Modules:**
    - `jackson-databind` (ObjectMapper)
    - `jackson-core` (Streaming API)
    - `jackson-annotations`
- **Use Cases:**
    - JSON APIs, RESTful services, data serialization
- **Website:** [https://github.com/FasterXML/jackson](https://github.com/FasterXML/jackson)

## 2. **Gson**
A simple and lightweight library to convert Java objects into JSON and vice versa, developed by Google.

- **Core Features:**
    - Serialize/Deserialize Java objects to/from JSON
    - Supports complex types (collections, generics)
    - Custom serialization logic via TypeAdapter
- **Key Dependencies:**
    - `gson`
- **Use Cases:**
    - JSON processing for web apps, microservices
- **Website:** [https://github.com/google/gson](https://github.com/google/gson)

## 3. **Apache Commons**
A collection of reusable Java components that simplify many common programming tasks.

- **Core Features:**
    - String manipulation (Commons Lang)
    - IO operations (Commons IO)
    - Collection utilities (Commons Collections)
    - Object pooling, email handling, etc.
- **Key Dependencies:**
    - `commons-lang3`
    - `commons-io`
    - `commons-collections4`
- **Use Cases:**
    - General-purpose utilities for various Java projects
- **Website:** [https://commons.apache.org/](https://commons.apache.org/)

## 4. **Log4j/Logback/SLF4J**
Logging libraries to track events during application execution.

- **Core Features:**
    - Configurable log levels (INFO, DEBUG, ERROR)
    - Logging to different outputs (file, console, etc.)
    - SLF4J as a facade, allowing switching between Log4j and Logback
- **Key Dependencies:**
    - `log4j-core` (Log4j)
    - `logback-classic` (Logback)
    - `slf4j-api` (SLF4J)
- **Use Cases:**
    - Debugging and logging for enterprise apps and microservices
- **Websites:**
    - [Log4j](https://logging.apache.org/log4j/2.x/)
    - [Logback](https://logback.qos.ch/)
    - [SLF4J](http://www.slf4j.org/)

## 5. **JUnit**
A popular testing framework for unit testing in Java, widely used in TDD (Test-Driven Development).

- **Core Features:**
    - Test annotation-based testing (e.g., `@Test`)
    - Assertions for expected results
    - Fixtures (`@Before`, `@After`) for test setup/teardown
- **Key Dependencies:**
    - `junit-jupiter-api` (JUnit 5)
    - `junit-vintage-engine` (for backward compatibility)
- **Use Cases:**
    - Unit testing, TDD practices
- **Website:** [https://junit.org/junit5/](https://junit.org/junit5/)

## 6. **Mockito**
A widely used mocking framework for Java testing, which allows creating mock objects for unit tests.

- **Core Features:**
    - Mocking objects and methods
    - Verification of method invocations
    - Stubbing return values for methods
- **Key Dependencies:**
    - `mockito-core`
    - `mockito-junit-jupiter`
- **Use Cases:**
    - Testing interactions between classes, mock dependencies
- **Website:** [https://site.mockito.org/](https://site.mockito.org/)

## 7. **Apache HttpClient**
A robust HTTP client library to handle HTTP requests and responses.

- **Core Features:**
    - Support for GET, POST, PUT, DELETE requests
    - SSL/TLS, cookies, authentication
    - Connection pooling for high-performance applications
- **Key Dependencies:**
    - `httpclient`
    - `httpcore`
- **Use Cases:**
    - Interacting with REST APIs, microservices communication
- **Website:** [https://hc.apache.org/](https://hc.apache.org/)

## 8. **Guava**
A set of core libraries from Google offering utilities for collections, caching, strings, and concurrency.

- **Core Features:**
    - Enhanced collections (ImmutableList, Multimap)
    - String utilities (e.g., splitting, joining)
    - In-memory caching
    - Functional programming support (Functions, Predicates)
- **Key Dependencies:**
    - `guava`
- **Use Cases:**
    - Simplifying coding with utilities, caching, functional programming
- **Website:** [https://github.com/google/guava](https://github.com/google/guava)

## 9. **MapStruct**
A code generator that greatly simplifies the implementation of mappings between Java bean types based on a simple interface definition.

- **Core Features:**
    - Automatic object mapping
    - Custom mapping logic via annotations
    - Supports nested mappings and collections
- **Key Dependencies:**
    - `mapstruct`
- **Use Cases:**
    - DTO to entity mapping, object transformations
- **Website:** [https://mapstruct.org/](https://mapstruct.org/)

## 10. **Lombok**
A Java library that reduces boilerplate code by providing annotations to auto-generate getters, setters, constructors, and more.

- **Core Features:**
    - `@Getter`, `@Setter` for auto-generating getter/setter methods
    - `@Builder` for fluent object construction
    - `@Data` for automatic creation of getters, setters, equals, hashcode, and toString
- **Key Dependencies:**
    - `lombok`
- **Use Cases:**
    - Reducing boilerplate code, simplifying data objects
- **Website:** [https://projectlombok.org/](https://projectlombok.org/)

## 11. **Hibernate Validator**
An implementation of JSR-380 (Bean Validation) that allows for annotation-based validation on Java objects.

- **Core Features:**
    - Standard bean validation annotations (`@NotNull`, `@Size`, `@Email`, etc.)
    - Custom constraint creation
    - Validation of fields, method parameters, and return values
- **Key Dependencies:**
    - `hibernate-validator`
- **Use Cases:**
    - Data validation in web forms, DTO validation in APIs
- **Website:** [https://hibernate.org/validator/](https://hibernate.org/validator/)

## 12. **Apache Kafka**
A distributed streaming platform for building real-time data pipelines and streaming applications.

- **Core Features:**
    - Publish-subscribe messaging
    - High-throughput, fault-tolerant streaming
    - Log-based storage for event-driven architectures
- **Key Dependencies:**
    - `kafka-clients`
- **Use Cases:**
    - Event streaming, real-time analytics, microservices messaging
- **Website:** [https://kafka.apache.org/](https://kafka.apache.org/)

## 13. **Apache POI**
A library for reading and writing Microsoft Office documents, such as Excel, Word, and PowerPoint files.

- **Core Features:**
    - Read/write Excel files (`.xls`, `.xlsx`)
    - Read/write Word (`.docx`) and PowerPoint (`.pptx`) files
    - Supports formulas, styling, and data formats in spreadsheets
- **Key Dependencies:**
    - `poi`
    - `poi-ooxml`
- **Use Cases:**
    - Office file processing, generating reports
- **Website:** [https://poi.apache.org/](https://poi.apache.org/)

## 14. **Flyway**
A database migration tool for versioning and automating schema changes.

- **Core Features:**
    - Version control of database migrations
    - SQL-based and Java-based migrations
    - Supports a variety of databases (Postgres, MySQL, Oracle, etc.)
- **Key Dependencies:**
    - `flyway-core`
- **Use Cases:**
    - Database version control, automating schema changes
- **Website:** [https://flywaydb.org/](https://flywaydb.org/)

## 15. **Quartz Scheduler**
A powerful and flexible library for job scheduling in Java applications.

- **Core Features:**
    - Schedule jobs using cron expressions
    - Trigger jobs at specific intervals
    - Persistent job store and clustering for distributed scheduling
- **Key Dependencies:**
    - `quartz`
- **Use Cases:**
    - Task scheduling, background jobs, cron-like scheduling in apps
- **Website:** [http://www.quartz-scheduler.org/](http://www.quartz-scheduler.org/)

---

**General Tips for Choosing Libraries:**
- Use **Jackson** or **Gson** for JSON serialization.
- Leverage **SLF4J** with **Logback** for flexible logging solutions.
- For unit testing, combine **JUnit** with **Mockito** for mocking dependencies.
- **Apache Commons** and **Guava** are great for general utility functions.
- **Hibernate Validator** and **Map

# Spring Cloud Cheat Sheet

Spring Cloud provides tools for developers to build cloud-native applications. It integrates with Spring Boot to provide a suite of frameworks for microservices architecture, making it easier to manage distributed systems.

## 1. **Spring Cloud Config**
Centralized configuration management for distributed systems.

- **Core Features:**
    - Externalized configuration via a central server
    - Supports various backends (Git, SVN, File System, etc.)
    - Dynamic configuration updates without application restarts
- **Key Annotations:**
    - `@EnableConfigServer`
    - `@RefreshScope`
- **Use Cases:**
    - Central management of application properties, dynamic configuration updates
- **Website:** [Spring Cloud Config](https://spring.io/projects/spring-cloud-config)

## 2. **Spring Cloud Netflix**
A set of tools and components from Netflix for building microservices.

### Key Components:
- **Eureka**
    - **Description:** Service discovery server for registering and discovering microservices.
    - **Key Annotations:** `@EnableEurekaServer`, `@EnableEurekaClient`
    - **Use Cases:** Dynamic service registration and discovery.
    - **Website:** [Eureka](https://spring.io/projects/spring-cloud-netflix)

- **Ribbon**
    - **Description:** Client-side load balancer to distribute requests across multiple service instances.
    - **Use Cases:** Load balancing between microservices.
    - **Website:** [Ribbon](https://spring.io/projects/spring-cloud-netflix)

- **Hystrix**
    - **Description:** Circuit breaker for handling failures in a distributed system, providing fallback options.
    - **Key Annotations:** `@HystrixCommand`
    - **Use Cases:** Resilience in microservices, preventing cascading failures.
    - **Website:** [Hystrix](https://spring.io/projects/spring-cloud-netflix)

- **Zuul**
    - **Description:** API gateway that provides dynamic routing, monitoring, and security.
    - **Key Annotations:** `@EnableZuulProxy`
    - **Use Cases:** Route requests to microservices, handle cross-cutting concerns.
    - **Website:** [Zuul](https://spring.io/projects/spring-cloud-netflix)

## 3. **Spring Cloud Gateway**
An API gateway built on Spring Framework, providing routing and filtering capabilities.

- **Core Features:**
    - Built on Spring WebFlux for reactive programming
    - Routing, load balancing, and request filtering
    - Integration with Spring Security for authentication
- **Key Annotations:**
    - `@EnableGateway`
- **Use Cases:**
    - API management, routing requests, rate limiting
- **Website:** [Spring Cloud Gateway](https://spring.io/projects/spring-cloud-gateway)

## 4. **Spring Cloud Sleuth**
Distributed tracing solution that provides unique identifiers for requests across microservices.

- **Core Features:**
    - Automatically adds tracing information to logs
    - Integration with Zipkin or other tracing systems
- **Key Dependencies:**
    - `spring-cloud-starter-sleuth`
- **Use Cases:**
    - Performance monitoring, debugging in microservices architecture
- **Website:** [Spring Cloud Sleuth](https://spring.io/projects/spring-cloud-sleuth)

## 5. **Spring Cloud Bus**
Links nodes of a distributed system with a lightweight message broker, propagating state changes and configuration updates.

- **Core Features:**
    - Propagates configuration changes across services
    - Integrates with Spring Cloud Config and Spring Cloud Stream
- **Key Dependencies:**
    - `spring-cloud-starter-bus-amqp` (for RabbitMQ)
    - `spring-cloud-starter-bus-kafka` (for Kafka)
- **Use Cases:**
    - Broadcasting configuration changes, event propagation
- **Website:** [Spring Cloud Bus](https://spring.io/projects/spring-cloud-bus)

## 6. **Spring Cloud Stream**
A framework for building message-driven microservices using messaging systems like RabbitMQ and Kafka.

- **Core Features:**
    - Declarative programming model for messaging
    - Supports multiple messaging middleware
    - Built-in binder for RabbitMQ and Kafka
- **Key Annotations:**
    - `@EnableBinding`
    - `@StreamListener`
- **Use Cases:**
    - Event-driven microservices, stream processing
- **Website:** [Spring Cloud Stream](https://spring.io/projects/spring-cloud-stream)

## 7. **Spring Cloud Function**
A framework that promotes the development of functions (instead of services) and can be used with various programming models.

- **Core Features:**
    - Function as a service model (FaaS)
    - Support for reactive programming
    - Integration with various messaging systems
- **Key Annotations:**
    - `@FunctionName`
    - `@Bean`
- **Use Cases:**
    - Building serverless applications, microservices as functions
- **Website:** [Spring Cloud Function](https://spring.io/projects/spring-cloud-function)

## 8. **Spring Cloud Kubernetes**
Integrates Spring Cloud with Kubernetes, enabling service discovery, configuration, and load balancing in a Kubernetes environment.

- **Core Features:**
    - Service discovery with Kubernetes
    - Configuration management using ConfigMaps and Secrets
    - Load balancing across Pods
- **Key Dependencies:**
    - `spring-cloud-starter-kubernetes`
- **Use Cases:**
    - Cloud-native applications on Kubernetes, configuration management
- **Website:** [Spring Cloud Kubernetes](https://spring.io/projects/spring-cloud-kubernetes)

---

**General Tips for Using Spring Cloud:**
- Leverage **Spring Cloud Config** for centralized configuration management.
- Use **Spring Cloud Gateway** or **Zuul** as an API gateway for routing and filtering.
- Implement **Eureka** for service discovery and **Ribbon** for client-side load balancing.
- Utilize **Hystrix** for circuit-breaking patterns to improve resilience.
- Integrate **Sleuth** for tracing requests across services, especially in debugging and performance monitoring.

For more detailed documentation and examples, visit the [Spring Cloud Documentation](https://spring.io/projects/spring-cloud).
