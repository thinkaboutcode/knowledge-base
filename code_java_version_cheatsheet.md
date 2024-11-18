# Overview of Recent Java Versions

## Java 21 (September 2023 - LTS)
- **Pattern Matching for Switch**: Extends pattern matching to switch expressions, improving code readability.
- **Record Patterns**: Simplifies destructuring of records and other data types, reducing boilerplate.
- **Virtual Threads**: Introduces lightweight threads, improving scalability and concurrency (Project Loom).
- **Foreign Function & Memory API (Third Preview)**: Enhances native code interaction, providing more control over memory management.
- **Sequenced Collections**: New interfaces and collections that guarantee element ordering.

### Pattern Matching for Switch
```java
public class PatternMatchingSwitchExample {

    public static void main(String[] args) {
        printObjectDetails("Hello, Java!");
        printObjectDetails(42);
        printObjectDetails(3.14);
        printObjectDetails(new int[]{1, 2, 3});
        printObjectDetails(null);
    }

    public static void printObjectDetails(Object obj) {
        switch (obj) {
            case String s -> 
                System.out.println("It's a String with length: " + s.length());
            case Integer i -> 
                System.out.println("It's an Integer with value: " + i);
            case Double d -> 
                System.out.println("It's a Double with value: " + d);
            case int[] arr -> 
                System.out.println("It's an int array with length: " + arr.length);
            case null -> 
                System.out.println("It's null!");
            default -> 
                System.out.println("Unknown type: " + obj);
        }
    }
}
```

### Record Pattern in Java

The **record pattern** is a feature introduced in **Java 21** as part of the Project Amber initiative. It enhances pattern matching by allowing developers to match and destructure **record types**. Records, introduced in Java 14 as a preview feature and finalized in Java 16, are a special kind of class in Java designed to be simple data carriers, automatically generating methods like `equals()`, `hashCode()`, and `toString()`.

#### Key Concepts of Record Pattern

#### 1. Simplified Syntax for Matching Records
- A **record** in Java is a class that holds a fixed set of fields. With the **record pattern**, Java enables you to destructure those fields easily within the context of **pattern matching**.
- It simplifies code that traditionally uses **`instanceof`** and **type casting** to work with the fields of a record.

#### 2. Pattern Matching for Record Classes
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

#### Virtual Threads
[Check this for more info](code_java_virtual_threads_cheatsheet.md) 

#### Sequenced Collections

Sequenced collections provide a more consistent way to handle collections that have an order, such as `List`, `Deque`, and `Set`. They allow you to access both the sequence (order of elements) and provide a consistent interface for operations like accessing elements by their index or iterating through the collection.

In particular, sequenced collections introduce a new interface called `Sequenced` with methods like `first()`, `last()`, and `next()`, which can be used to access the first and last elements of a collection, among other things.

#### Key Points:
- **`List`** and **`Deque`** are examples of sequenced collections in Java 20.
- **`first()`**: Returns the first element in the collection.
- **`last()`**: Returns the last element in the collection.
- **`forEach()`**: Standard method to iterate over all elements.

#### Benefits of Sequenced Collections:
1. **Consistency**: Provides consistent methods like `first()` and `last()` for accessing elements, regardless of the collection type.
2. **Simplification**: Reduces the need to write custom code for common operations on ordered collections.
3. **Extensibility**: Can be used with any collection that maintains an order (e.g., `List`, `Deque`, `Set`).

Sequenced collections streamline handling ordered collections by providing a unified API for sequence-related operations.

```java
import java.util.*;

public class SequencedCollectionExample {
  public static void main(String[] args) {
    // Create a List (Sequenced collection)
    List<String> fruits = List.of("Apple", "Banana", "Cherry", "Date");

    // Accessing the first and last elements using sequenced collection methods
    System.out.println("First fruit: " + fruits.first());
    System.out.println("Last fruit: " + fruits.last());

    // Iterating through the sequenced collection
    System.out.println("All fruits:");
    fruits.forEach(System.out::println);

    // Create a Deque (also a Sequenced collection)
    Deque<String> vegetables = new ArrayDeque<>(List.of("Carrot", "Broccoli", "Spinach"));

    // Accessing the first and last elements of the Deque
    System.out.println("First vegetable: " + vegetables.first());
    System.out.println("Last vegetable: " + vegetables.last());

    // Adding and removing from the Deque
    vegetables.addFirst("Cucumber");
    vegetables.addLast("Potato");
    System.out.println("Updated vegetables:");
    vegetables.forEach(System.out::println);
  }
}
```



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

### Sealed Classes
```java
// File: Shape.java
public sealed class Shape permits Circle, Rectangle, Triangle {
    // Common properties or methods for all shapes
    public abstract double area();
}

// File: Circle.java
public final class Circle extends Shape {
    private final double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

// File: Rectangle.java
public final class Rectangle extends Shape {
    private final double width;
    private final double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

// File: Triangle.java
public final class Triangle extends Shape {
    private final double base;
    private final double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double area() {
        return 0.5 * base * height;
    }
}
```

### Pattern Matching with instanceof
```java
public class InstanceOfPatternMatchingExample {
    public static void main(String[] args) {
        Object obj = "Hello, Pattern Matching!";

        // Traditional instanceof with explicit casting
        if (obj instanceof String) {
            String str = (String) obj; // Explicit casting
            System.out.println("String length: " + str.length());
        }

        // Modern instanceof with pattern matching
        if (obj instanceof String str) { // Pattern matching
            System.out.println("String length: " + str.length());
        }

        // Another example with different types
        printObjectDetails(42);          // Integer
        printObjectDetails(3.14);        // Double
        printObjectDetails("Pattern!");  // String
    }

    public static void printObjectDetails(Object obj) {
        if (obj instanceof Integer i) {
            System.out.println("Integer value: " + i);
        } else if (obj instanceof Double d) {
            System.out.println("Double value: " + d);
        } else if (obj instanceof String s) {
            System.out.println("String value: " + s);
        } else {
            System.out.println("Unknown type: " + obj);
        }
    }
}
```

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

### Java Records vs. Lombok

Java's **records**, introduced in **Java 16**, share some functionality with the **Lombok** library, especially for creating data classes. Lombok has been popular for reducing boilerplate in Java with annotations, but records bring an alternative with differences in design and scope. Here’s a comparison:

#### Similarities Between Records and Lombok

- **Boilerplate Reduction**: Both records and Lombok reduce repetitive code in Java by eliminating the need to manually write getters, `equals()`, `hashCode()`, and `toString()` methods.
- **Immutability Support**: Records are inherently immutable, and Lombok can create immutable classes with annotations like `@Value`.
- **Data-Oriented Classes**: Both are used primarily for classes that act as **data holders** rather than objects with complex behavior.

#### Key Differences Between Records and Lombok

#### 1. Built-In vs. External Library
- **Records** are a core part of Java starting from **Java 16**, with no external dependencies required.
- **Lombok** is a third-party library, which requires adding a dependency and may have compatibility issues across IDEs and Java versions.

#### 2. Immutable by Default vs. Configurable Immutability
- **Records** enforce immutability by design: fields are `final` and cannot change after construction.
- **Lombok** allows both **mutable** and **immutable** classes. With annotations like `@Data`, Lombok can generate setters for mutable fields, while `@Value` makes immutable classes.

#### 3. Customization of Fields and Methods
- **Lombok** provides greater flexibility with features like:
  - `@Builder` for complex object construction.
  - `@ToString`, `@EqualsAndHashCode`, and `@Getter/@Setter` for fine-tuned control over specific methods.
  - Optional parameters, validation, and default values using `@Builder.Default`.
- **Records** have more limitations. The primary constructor and `toString`, `equals`, and `hashCode` methods are automatically generated and cannot be customized with additional annotations. However, other methods can be added, and **compact constructors** allow data validation or transformation on creation.

#### 4. Subclassing and Finality
- **Records** are implicitly `final` and cannot be subclassed, which supports immutability and predictability.
- **Lombok** classes are not necessarily `final` and can be subclassed, which is useful when inheritance is required.

#### 5. Compatibility and Ecosystem
- **Records**, being a core language feature, are fully supported across Java tooling, IDEs, and frameworks.
- **Lombok** support varies by IDE and build tool, though it has improved over the years.

#### When to Use Records vs. Lombok

- **Use Records** when:
  - You want a **concise, immutable data class** without external dependencies.
  - You’re working on a project where **immutability** is essential and using Java 16 or newer.
  - You don’t need the additional customization features that Lombok offers.

- **Use Lombok** when:
  - You need **customization** beyond what records provide, such as mutable fields, builder patterns, or optional methods like setters.
  - You’re working with a codebase that already uses Lombok or needs to support a **Java version older than Java 16**.
  - You need finer control over specific methods or fields.

#### Summary

Java **records** offer a built-in solution for creating immutable data classes in Java but lack the advanced features and flexibility provided by **Lombok**. For developers who need simplicity and immutability and are on Java 16+, records are a powerful tool. However, for projects requiring more customization or backward compatibility, **Lombok** remains a valuable alternative.


## Java 15 (September 2020)
- **Sealed Classes (Preview)**: Introduces sealed classes to restrict the inheritance of classes.
- **Hidden Classes**: Supports hidden classes that can be used by frameworks for better runtime performance.
- **ZGC (Z Garbage Collector)**: Experimental low-latency garbage collector to handle large heaps efficiently.

## Java 14 (March 2020)
- **JEP 358: Helpful NullPointerException**: Improves `NullPointerException` messages by providing more context about the error.
- **JEP 359: Records (Preview)**: Introduces records, a new kind of type to model immutable data.
- **JEP 370: Foreign-Memory Access API (Incubator)**: Introduces a new API for safely accessing memory outside of the Java heap.

### Helpful NullPointerException (Java 14)

Introduced in **Java 14**, the **Helpful NullPointerException** provides more detailed information when a `NullPointerException` occurs. It helps developers quickly identify which variable or expression caused the `null` dereference, making debugging easier and faster.

#### Key Features:
- **Detailed Error Messages**: The exception message includes the name of the variable or expression that was `null`.
- **Improved Debugging**: Instead of just saying `NullPointerException`, it specifies which object or method was null, providing context to locate the issue quickly.
- **Enabled by Default**: This feature is enabled by default in Java 14 and later.
- **Can Be Disabled**: It can be turned off with the JVM flag `-XX:-ShowCodeDetailsInExceptionMessages`.

#### Benefits:
- **Faster Debugging**: Developers can easily spot which variable caused the exception.
- **Better Developer Experience**: Makes stack traces more informative and reduces debugging time.

In summary, **Helpful NullPointerException** in Java 14 enhances error messages to make `NullPointerExceptions` easier to debug by showing exactly which part of the code was `null`.


## Java 13 (September 2019)
- **JEP 355: Text Blocks**: Introduces text blocks for multi-line string literals, improving readability and reducing escape sequences.
- **JEP 351: ZGC (Z Garbage Collector)**: Improved ZGC for better performance and scalability.
- **JEP 350: Dynamic CDS Archives**: Introduces a dynamic class-data-sharing feature to improve startup performance.

### Text Blocks for Multi-Line String Literals (Java 13+)

Introduced in **Java 13** as a **preview feature** and made permanent in **Java 15**, **text blocks** provide an easier and more readable way to work with **multi-line string literals**. They eliminate the need for cumbersome concatenation and escape sequences, making the code cleaner and more readable.

#### Key Features of Text Blocks:
- **Multi-line Strings**: Text blocks allow you to define strings that span multiple lines without the need for explicit line breaks or concatenation.
- **Automatic Formatting**: Whitespace and line breaks are preserved as part of the string, making the code more intuitive.
- **Escape Sequences**: You no longer need to escape special characters like newline `\n`, tab `\t`, or quotes `\"` within the text block.
- **Consistent Indentation**: The text block automatically strips out unnecessary leading indentation, making the code look well-structured.

#### Syntax:
Text blocks are enclosed in triple quotes (`"""`), and the string content inside can span multiple lines.

#### Example:
```java
String json = """
               {
                 "name": "John",
                 "age": 30,
                 "city": "New York"
               }
               """;
```

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
