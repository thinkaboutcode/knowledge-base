# Overview of Recent Java Versions

## Java 21 (September 2023)
- **Pattern Matching for Switch (Preview)**: Extends pattern matching to switch expressions, improving code readability.
- **Record Patterns (Preview)**: Simplifies destructuring of records and other data types, reducing boilerplate.
- **Virtual Threads (Preview)**: Introduces lightweight threads, improving scalability and concurrency (Project Loom).
- **Foreign Function & Memory API (Second Incubator)**: Enhances native code interaction, providing more control over memory management.
- **Sequenced Collections**: New interfaces and collections that guarantee element ordering.

### Record Pattern in Java

The **record pattern** is a feature introduced in **Java 21** as part of the Project Amber initiative. It enhances pattern matching by allowing developers to match and destructure **record types**. Records, introduced in Java 14 as a preview feature and finalized in Java 16, are a special kind of class in Java designed to be simple data carriers, automatically generating methods like `equals()`, `hashCode()`, and `toString()`.

#### Key Concepts of Record Pattern

##### 1. Simplified Syntax for Matching Records
- A **record** in Java is a class that holds a fixed set of fields. With the **record pattern**, Java enables you to destructure those fields easily within the context of **pattern matching**.
- It simplifies code that traditionally uses **`instanceof`** and **type casting** to work with the fields of a record.

##### 2. Pattern Matching for Record Classes
- The **record pattern** allows you to match records and extract their components directly in the pattern.
- This feature eliminates the need for manually accessing the fields of the record.

#### Benefits of Record Pattern

- **Concise Code**: The record pattern allows you to match records and extract their components directly, removing the need for getter methods or field access.
- **Improved Readability**: The ability to destructure records directly in the pattern improves code clarity, especially when working with record classes.
- **Type Safety**: The pattern matching process ensures type safety, ensuring that only the correct type is matched and destructured.

#### Summary

- Introduced in **Java 21**.
- Simplifies working with **record types** by allowing for direct matching and extraction of fields.
- Reduces boilerplate code and enhances readability and type safety.

This feature is part of a broader set of improvements in pattern matching in Java, including **instanceof**, **switch expressions**, and other advanced matching capabilities.


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

### Effect of "Strong Encapsulation of JDK Internals" on Existing Code

The feature **"Strong Encapsulation of JDK Internals"**, introduced in **Java 16** and refined in later versions, has significant implications for existing code, especially those relying on internal JDK APIs. Below is an overview of the effect this change has on legacy and current applications:

#### 1. Inaccessibility of Internal JDK APIs
- **By default, internal JDK APIs** (e.g., classes and methods under `sun.*`, `com.sun.*`, or `jdk.*`) are **no longer accessible** unless explicitly allowed via command-line flags or module configurations.
- Previously, these internal APIs were available for tasks like performance optimization, working around limitations, or leveraging undocumented functionality.
- **Result**: Any code that uses these internal APIs will break or fail to compile since they are no longer part of the public API.

#### 2. Impact on Existing Code
- **Compilation Failures**: Code that imports or uses internal JDK classes will result in **compilation errors** if the modules or packages are not explicitly opened.
- **Runtime Failures**: Even if code compiles (e.g., through reflective access or command-line flags), attempting to access these APIs will result in **runtime errors**, such as `IllegalAccessException`, unless the program is configured to allow access using JVM flags.
- **Reflection-Based Code**: Many frameworks (e.g., Hibernate, Spring, and application servers) and tools may use reflection to access JDK internals. This type of code may break due to **strong encapsulation**, requiring updates to the framework or additional configurations to re-enable access.

#### 3. JVM Flags and Workarounds
- **Command-Line Flags**: Developers can still access these internal APIs by using JVM flags like `--add-opens` or `--add-exports`. For example:
    - `--add-opens java.base/sun.nio.ch=ALL-UNNAMED` to allow access to internal classes in the `sun.nio.ch` package.
    - `--add-exports java.base/com.sun.nio.sctp=ALL-UNNAMED` to export internal JDK packages to unnamed modules.
- **Note**: This workaround **is not recommended for production**, as it negates some of the security and modularity benefits of strong encapsulation.

#### 4. Security and Maintenance Benefits
- **Improved Security**: Strong encapsulation limits the attack surface by preventing access to internal and potentially insecure or outdated JDK classes.
- **Stability and Maintainability**: By hiding internal APIs, future JDK releases can change the implementation of these APIs without breaking public-facing code. This leads to **better stability** across Java versions.
- **Encourages Best Practices**: It encourages developers to use officially supported, public APIs or libraries that are not reliant on undocumented or unsupported internal features.

#### 5. What Can Developers Do?
- **Update Dependencies**: If your application relies on internal JDK APIs, you need to either update the affected code or migrate to official Java APIs or third-party libraries that do not depend on JDK internals.
- **Use Public APIs**: Developers are encouraged to migrate their code to **official, supported Java APIs** or leverage newer solutions available in Java.

#### 6. Example Use Cases Affected
- **Reflection Access**: If your code uses reflection to access JDK internals, this will no longer work unless granted access via JVM flags.
- **Frameworks and Libraries**: Some third-party libraries or frameworks that relied on internal JDK APIs (e.g., `sun.misc.Unsafe`) may break unless updated to avoid reliance on these internals.
- **Custom JVM Optimizations**: If your application directly interfaces with JVM internals for optimizations (e.g., garbage collection tuning or memory buffers), this will require changes.

#### Summary
**Strong Encapsulation of JDK Internals** improves Java’s security and maintainability but introduces challenges for codebases dependent on internal JDK APIs. To maintain compatibility with newer Java versions:

- **Refactor or replace** reliance on internal JDK APIs.
- Use **official APIs** or migrate to third-party libraries that do not depend on JDK internals.
- If necessary, use JVM flags temporarily for compatibility, but this is not recommended for production environments due to security risks.

This change encourages developers to move towards **modular and secure approaches**, adhering to public, supported Java APIs.


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
