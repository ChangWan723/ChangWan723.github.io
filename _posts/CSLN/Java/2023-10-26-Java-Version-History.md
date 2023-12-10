---
title: Java Version History
date: 2023-10-26 17:52:00 UTC
categories: [(CS) Learning Note, Java]
tags: [software engineering, Java]
pin: false
---

Java has evolved substantially since its initial release, introducing numerous features that have changed the landscape of programming. This blog takes a look at some of the significant features introduced in each version of Java.

>The features shown below are only some important features of the release, not all of them.
{: .prompt-warning }

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Java 1.0 (1996)](#java-10-1996)
  * [Java 1.1 (1997)](#java-11-1997)
  * [Java 1.2 (1998)](#java-12-1998)
  * [Java 1.3 (2000)](#java-13-2000)
  * [Java 1.4 (2002)](#java-14-2002)
  * [Java 5 (2004)](#java-5-2004)
  * [Java 6 (2006)](#java-6-2006)
  * [Java 7 (2011)](#java-7-2011)
  * [Java 8 (2014) - LTS](#java-8-2014---lts)
  * [Java 9 (2017)](#java-9-2017)
  * [Java 10 (2018)](#java-10-2018)
  * [Java 11 (2018) - LTS](#java-11-2018---lts)
  * [Java 12 (2019)](#java-12-2019)
  * [Java 13 (2019)](#java-13-2019)
  * [Java 14 (2020)](#java-14-2020)
  * [Java 15 (2020)](#java-15-2020)
  * [Java 16 (2021)](#java-16-2021)
  * [Java 17 (2021) - LTS](#java-17-2021---lts)
  * [Java 18 (2022)](#java-18-2022)
  * [Java 19 (2022)](#java-19-2022)
  * [Java 20 (2023)](#java-20-2023)
  * [Java 21 (2023) - LTS](#java-21-2023---lts)
<!-- TOC -->

---

## Java 1.0 (1996)

The first public release of Java, Java 1.0, laid the foundation for future versions.

- **Java fundamental features**: Based on the Oak (The predecessor of the Java), this version basically only contains some Java fundamental features.
- **Applets**: Allowed for small applications to be run within web browsers.
- **AWT**: Abstract Window Toolkit provided the first GUI components.
- **Garbage Collection**: Automatic memory management.
- **Multithreading**: Support for concurrent execution of threads.

## Java 1.1 (1997)

Java 1.1 brought important enhancements to the language and libraries.

- **Inner Classes**: Classes defined within other classes to logically group them.
- **JavaBeans**: Reusable software components for Java.
- **JDBC**: Java Database Connectivity for database interaction.
- **Reflection**: Inspect classes, methods, and fields at runtime.

## Java 1.2 (1998)

Java 1.2, also known as `J2SE`, was a major release with substantial improvements.

- **Swing**: New set of GUI components.
- **Collections Framework**: Provided a unified architecture for collections.
- **JIT Compiler**: Just-In-Time compiler for performance.
- **RMI (Remote Method Invocation)**: Allowed for methods to be called remotely.
- **[Three Java Platforms](/posts/Java-Platform/)**: Java is divided into Java SE, Java EE and Java ME.

## Java 1.3 (2000)

Java 1.3 continued the evolution of Java, adding significant features for developers.

- **HotSpot JVM**: Introduced the HotSpot JVM for improved performance.
- **Java Naming and Directory Interface (JNDI)**: Offered a directory service API for Java applications to interact with directory services.
- **JavaSound API**: API for handling sound in Java applications.
- **Synthetic Proxy Classes**: Support for proxy classes.

## Java 1.4 (2002)

Java 1.4 focused on enhancing the language's functionality and performance.

- **Assertions**: Introduced a mechanism for debugging.
- **Regular Expressions**: Added support for regular expressions in Java.
- **NIO (New Input/Output)**: Improved file handling and channels, allowing for non-blocking I/O operations.
- **Logging API**: Added an API for logging error messages and debugging information.

## Java 5 (2004)

Java 5, also known as `Java SE`, was a milestone release with numerous new features and enhancements. To signify the importance of this version, Java 1.5 (J2SE 1.5) was renamed Java 5 (Java SE 5).

- **Generics**: Introduced type-safe collections, allowing for compile-time type checking.
- **Annotations**: Metadata for programs. It allows for checking, configuration, documentation and other processing.
- **Enumerations**: Allowed for the definition of a set of constants.
- **Varargs**: Enabled variable-length argument lists for methods.
- **Enhanced for-loop**: Simplified iteration over collections.
- **Autoboxing and Unboxing**: This makes it easier for Java to convert between basic data types and wrapper types, reducing redundant code and improving readability.

## Java 6 (2006)

Java 6 focused on improving the overall performance and debugging capabilities.

- **Scripting API**: Added support for scripting languages.
- **Compiler API**: Provided control over the compilation process in Java programs.
- **Pluggable Annotation Processing API**: Allowed for the processing of annotations at compile time.

## Java 7 (2011)

Java 7 brought significant improvements in language features and performance. At the time of this release, Sun had been acquired by Oracle.

- **Try-with-resources**: Introduced automatic resource management, reducing the risk of resource leaks.
- **Diamond Operator**: Simplified the instantiation of generic types.
- **Fork/Join Framework**: Added support for parallel processing.
- **NIO.2**: Introduced a new file system API.
- **G1 Garbage Collector**: Improved garbage collection with the introduction of the G1 garbage collector.

## Java 8 (2014) - LTS

Java 8 was a transformative release, introducing functional programming concepts to the language. Java 8 is the first LTS version of Java.

> **LTS (Long-Term Support)**
> 
> LTS (Long-Term Support) versions of Java are releases that offer extended support and maintenance over a longer period compared to regular or "feature" releases. The LTS versions are ideal for organizations and enterprises that require a stable and maintainable Java environment for their applications over several years.
{: .prompt-tip }

- **Lambda Expressions**: Allowed for concise expression of instances of single-method interfaces (functional interfaces).
- **Streams API**: Simplified collection processing with a functional approach.
- **Default Methods in Interfaces**: Enabled the addition of default implementations in interfaces.
- **Optional Class**: Provided a container object for handling null values more gracefully.
- **New Date and Time API**: Improved date and time handling with a new API.

## Java 9 (2017)

Java 9 introduced modular programming, changing the way Java applications are structured.

- **JPMS (Java Platform Module System)**: Brought in a module system for Java, allowing for better encapsulation of code.
- **JShell**: Added an interactive Java REPL for experimenting with Java code.
- **Stream API Enhancements**: Introduced more flexible operations for the Stream API.
- **Private Interface Methods**: Allowed for common code to be defined in interfaces.
- **HTTP/2 Client API**: Provided support for the HTTP/2 protocol.

## Java 10 (2018)

Java 10 was a short-term release, focusing on improving developer productivity and performance.

- **Local-variable Type Inference**: Introduced 'var' for implicit typing of local variables.
- **Application Class-Data Sharing**: Improved startup performance by sharing common class metadata between Java Virtual Machines.
- **Garbage-Collector Interface**: Improved garbage collector management with a cleaner abstraction.
- **Root Certificates**: Enhanced security with a set of root certificates included in the JDK.

## Java 11 (2018) - LTS

Java 11, a long-term support release, continued to enhance the language's features. 

- **New String Methods**: Added more methods for handling strings.
- **HTTP Client API**: Standardized the HTTP client introduced in Java 9.
- **Epsilon Garbage Collector**: Introduced a no-op garbage collector for performance testing.
- **Dynamic Class-File Constants**: Allowed for constants that are computed at runtime.

## Java 12 (2019)

Java 12 was another short-term release, with incremental improvements.

- **Switch Expressions (Preview)**: Introduced a new switch expression syntax for more concise code.
- **Shenandoah: A Low-Pause-Time Garbage Collector**: Brought in the Shenandoah garbage collector for reduced pause times.
- **Switch Expressions (Preview)**: Improved switch expressions to simplify coding.

## Java 13 (2019)

Java 13 brought additional features and refinements to the language.

- **Text Blocks (Preview)**: Allowed for multi-line string literals.
- **Reimplement the Legacy Socket API**: Replaced the old socket API for improved performance.
- **Dynamic CDS Archives**: Enhanced the application class-data sharing feature.
- **ZGC: Uncommit Unused Memory**: Improved the Z Garbage Collector to return memory to the operating system.

## Java 14 (2020)

Java 14 continued the trend of incremental improvements, focusing on language features.

- **Pattern Matching for instanceof (Preview)**: Simplified the common pattern of instanceof checks followed by casting.
- **Records (Preview)**: Introduced a new type of class for modeling immutable data in applications.
- **Helpful NullPointerExceptions**: Enhanced the debugging information in NullPointerException messages.
- **Foreign-Memory Access API (Incubator)**: Allowed for access to native memory without relying on JNI.

## Java 15 (2020)

Java 15 brought in additional language features and enhancements.

- **Sealed Classes (Preview)**: Introduced the concept of sealed classes for better control over inheritance.
- **Pattern Matching for instanceof (Second Preview)**: Continued improvements in pattern matching.
- **Records (Standard Feature)**: Promoted records to a standard feature of the language.
- **Eden Hazard**: Improved garbage collection with the introduction of the Eden Hazard collector.

## Java 16 (2021)

Java 16 continued the evolution of Java on language features.

- **Unix-Domain Socket Channels**: Introduced support for Unix-domain socket channels for inter-process communication on the same host.
- **ZGC: Concurrent Thread-Stack Processing**: Enhanced the Z Garbage Collector for better performance.
- **Elastic Metaspace**: Optimized memory footprint of the metaspace area in the Java Virtual Machine.
- **Pattern Matching for instanceof**: Promoted pattern matching for instanceof to a standard feature.


## Java 17 (2021) - LTS

Java 17 continues to make enhancements to language features and updates the random number generator.

- **Sealed Classes**: The feature restricts which other classes or interfaces may extend or implement a sealed component.
- **Enhanced Pseudo-Random Number Generators**: It provides new interfaces and implementations for Pseudo-Random Number Generators (PRNG).
- **New macOS Rendering Pipeline**: The new implementation uses the Apple Metal API.
- Pattern Matching for Switch: It facilitates more readable and safe code when multiple case labels share the same code.

## Java 18 (2022)

Java 18 continues to make enhancements to language features and performance.

- **UTF-8 by Default**: The default charset of the platform is now UTF-8.
- **Code Snippets in Java API Documentation**: The Java API documentation provides code examples that illustrate the use of each feature. Introduced the `@snippet` tag to make it easier to embed example source code in API documentation.
- **Vector API**: Java coders can use the new Vector API to perform vector computations.

## Java 19 (2022)

Java 19 introduced several noteworthy features and enhancements aimed at improving developer productivity.

- **Virtual Threads**: They are aimed at making concurrency easier to manage and more scalable.
- **Foreign Function and Memory API**: It allows Java programs to interact with code and data outside the Java runtime, combining the Foreign Function and Storage APIs from previous incubation.
- **Linux/RISC-V Port**: It extends the JDK to the open-source instruction set architecture Linux/RISC-V.

## Java 20 (2023)

Java 20 continues the incremental enhancements seen in earlier versions, building upon features introduced in Java 19 and prior releases.

- **Scoped Values**: Scoped values are immutable values available for reading for a bounded period of execution by a thread, aiming to provide a simple, immutable, and inheritable data-sharing option, especially in scenarios with a large number of threads.
- **Virtual Threads**: Continuing from Java 19, virtual threads are part of the efforts under Project Loom to simplify concurrency management and enhance scalability.

## Java 21 (2023) - LTS

Java 21 brought forth several enhancements, building upon the features of previous versions.

- **Finalization of Virtual Threads**: Virtual threads, which were introduced in earlier versions as a preview feature, have been finalized in Java 21. This feature aims to simplify concurrency in Java by making it easier to handle many threads concurrently.
- **Pattern Matching for Switch Statements**: Pattern Matching for switch statements has been finalized, which allows developers to perform both type checking and type casting in a single step, simplifying code significantly.

