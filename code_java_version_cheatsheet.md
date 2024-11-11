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

## Java 15 (September 2020)
- **Sealed Classes (Preview)**: Introduces sealed classes to restrict the inheritance of classes.
- **Hidden Classes**: Supports hidden classes that can be used by frameworks for better runtime performance.
- **ZGC (Z Garbage Collector)**: Experimental low-latency garbage collector to handle large heaps efficiently.

## Java 14 (March 2020)
- **JEP 358: Helpful NullPointerException**: Improves `NullPointerException` messages by providing more context about the error.
- **JEP 359: Records (Preview)**: Introduces records, a new kind of type to model immutable data.
- **JEP 370: Foreign-Memory Access API (Incubator)**: Introduces a new API for safely accessing memory outside of the Java heap.

## Java 13 (September 2019)
- **JEP 355: Text Blocks**: Introduces text blocks for multi-line string literals, improving readability and reducing escape sequences.
- **JEP 351: ZGC (Z Garbage Collector)**: Improved ZGC for better performance and scalability.
- **JEP 350: Dynamic CDS Archives**: Introduces a dynamic class-data-sharing feature to improve startup performance.

## Java 12 (March 2019)
- **JEP 189: Shenandoah GC (Garbage Collector)**: Experimental low-latency garbage collector that reduces GC pause times.
- **JEP 230: Microbenchmarking Support**: Improves the JVM's capabilities for benchmarking code reliably.
- **JEP 325: Switch Expressions (Standard)**: Switch expressions were officially made a standard feature, enhancing the expressiveness and usability of the switch statement.

## Java 11 (September 2018 - LTS)
- **Local-Variable Syntax for Lambda Parameters**: Adds the ability to use `var` in lambda parameters.
- **Epsilon Garbage Collector**: A no-op garbage collector designed for performance testing.
- **JEP 321: HTTP Client**: Introduces a new standard HTTP client for making HTTP requests with better performance and features.

## Java 10 (March 2018)
- **Local-Variable Type Inference**: Introduces the `var` keyword to allow local variable type inference.
- **G1 Garbage Collector Improvements**: Improves the performance of the G1 garbage collector.
- **JEP 286: Switch Expressions (Preview)**: Introduces switch expressions to enhance the switch statement with more flexibility and conciseness.

## Java 9 (September 2017)
- **Java Platform Module System (JPMS)**: Introduces the module system to allow for better modularization of the Java platform.
- **JEP 201: Modular JDK**: Modifies the JDK itself to be modular, enabling developers to use only the parts of the JDK they need.
- **JShell**: A Read-Eval-Print Loop (REPL) introduced for experimenting with Java code interactively.

## Java 8 (March 2014)
- **Lambda Expressions**: Introduces lambdas for functional programming features, allowing cleaner and more concise code.
- **Streams API**: Adds a new Stream API for working with sequences of data in a functional style.
- **Default Methods**: Allows interfaces to have default methods with an implementation.
- **java.time Package**: A new API for handling date and time, replacing the old `Date` and `Calendar` classes.

## Java 7 (July 2011)
- **Try-with-Resources**: Simplifies resource management by automatically closing resources like streams and connections.
- **Binary Literals**: Supports binary literals using the `0b` prefix.
- **The Fork/Join Framework**: Introduces a new framework for parallel programming, improving multi-core processor performance.

## Java 6 (December 2006)
- **Scripting API (JSR 223)**: Introduces support for integrating scripting languages (like JavaScript) within Java applications.
- **Performance Improvements**: Includes enhancements to the Java Virtual Machine (JVM) and garbage collection for better performance.
- **Java Compiler API**: Adds an API for interacting with the Java compiler programmatically.
