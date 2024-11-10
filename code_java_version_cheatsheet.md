# Overview of Recent Java Versions

## Java 21 (September 2023)
- **Pattern Matching for Switch (Preview)**: Extends pattern matching to switch expressions, improving code readability.
- **Record Patterns (Preview)**: Simplifies destructuring of records and other data types, reducing boilerplate.
- **Virtual Threads (Preview)**: Introduces lightweight threads, improving scalability and concurrency (Project Loom).
- **Foreign Function & Memory API (Second Incubator)**: Enhances native code interaction, providing more control over memory management.
- **Sequenced Collections**: New interfaces and collections that guarantee element ordering.

## Java 20 (March 2023)
- **Record Patterns (Preview)**: Allows destructuring of records in a more intuitive way.
- **Pattern Matching for Switch (Preview)**: Expands the flexibility of switch expressions.
- **Scoped Values (Incubator)**: Introduces scoped variables for better data isolation and concurrency handling.
- **Virtual Threads (Preview)**: Previews virtual threads for more scalable and lightweight concurrency (Project Loom).

## Java 19 (September 2022)
- **Record Patterns (Preview)**: Introduces record pattern matching to enhance records.
- **Pattern Matching for Switch (Preview)**: Extends pattern matching to switch expressions for better readability.
- **Foreign Function & Memory API (Incubator)**: Provides API for managing foreign memory and interoperation with native code.
- **Vector API (Incubator)**: Supports performing vector operations (SIMD) for improved platform-independent performance.

## Java 18 (March 2022)
- **Simple Web Server**: Introduces a minimal HTTP server for testing and prototyping.
- **Code Snippets in Javadoc**: Enhances Javadoc to support embedding code examples easily.
- **UTF-8 by Default**: UTF-8 becomes the default charset for file I/O operations.
- **Vector API (Incubator)**: Experimental API for improving performance with vector computations.

## Java 17 (September 2021 - LTS)
- **Sealed Classes**: Allows better control over class hierarchies by restricting which classes can extend or implement them.
- **Pattern Matching for `instanceof`**: Simplifies type checking and casting.
- **Strong Encapsulation of JDK Internals**: Makes internal JDK APIs inaccessible by default for improved security.
- **New macOS Rendering Pipeline**: Uses Apple's Metal API for improved graphics performance on macOS.
- **JEP 411: Deprecate the Security Manager for Removal**: Signals the potential removal of the Security Manager.

## Java 16 (March 2021)
- **JEP 376: ZGC on macOS**: Adds support for ZGC (Z Garbage Collector) on macOS for low-latency garbage collection.
- **JEP 395: Strongly Encapsulate JDK Internals**: Ensures internal JDK APIs are fully encapsulated, increasing security.
- **JEP 396: Strongly Encapsulate JDK Internals**: Further improvements to encapsulation of internal JDK APIs.
