---
title: Common Commands in JDK
date: 2024-01-25 20:30:00 UTC
categories: [(CS) Learning Note, Java]
tags: [software engineering, Java, JVM]
pin: false
---

Java Development Kit (JDK) offers commands that are essential for Java development, each serving a specific purpose. Understanding these commands and their parameters is crucial for any Java developer.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [`javac` (Java compiler)](#javac-java-compiler)
  * [`java` (Java launcher)](#java-java-launcher)
  * [`jar` (Creat and manage JAR files)](#jar-creat-and-manage-jar-files)
  * [`javap` (Java Class File Disassembler)](#javap-java-class-file-disassembler)
  * [`javadoc` (Generates HTML documentation)](#javadoc-generates-html-documentation)
  * [`jconsole` (Monitoring tool)](#jconsole-monitoring-tool)
  * [`jps` (Java Virtual Machine Process Status Tool)](#jps-java-virtual-machine-process-status-tool)
  * [`jstat` (JVM Statistics Monitoring Tool)](#jstat-jvm-statistics-monitoring-tool)
  * [`jinfo` (Configuration Info for Java)](#jinfo-configuration-info-for-java)
  * [`jmap` (Memory Map for Java)](#jmap-memory-map-for-java)
  * [`jhat` (JVM Heap Analysis Tool)](#jhat-jvm-heap-analysis-tool)
  * [`jstack` (Stack Trace for Java)](#jstack-stack-trace-for-java)
<!-- TOC -->

---

## `javac` (Java compiler)

**Purpose**: `javac` is the Java compiler command. It's used to compile Java source files into bytecode (.class files).

**Some Parameters**:
- `-classpath` or `-cp`: Set the classpath.
- `-d`: Specify the destination directory for generated class files.

**Example**:

Compile a Java file named `Example.java`:
```bash
javac Example.java
```

Compile multiple Java files in a specific directory:
```bash
javac -d ./bin ./src/*.java
```

## `java` (Java launcher)

**Purpose**: The `java` command is used to launch a Java application. It starts the Java runtime environment, loads the specified class, and calls its `main` method.

**Some Parameters**:
- `-classpath` or `-cp`: Set the classpath.
- `-Dproperty=value`: Set a system property.
- `-Xmx`: Maximum size of the memory allocation pool.
- `-Xms`: Initial size of the memory allocation pool.

**Example**:

Run a class named `Example`:
```bash
java -cp ./bin Example
```

Run with increased heap size:
```bash
java -Xmx512m -Xms256m -cp ./bin Example
```

## `jar` (Creat and manage JAR files)

**Purpose**: Used for creating and managing JAR (Java Archive) files, which bundle multiple Java class files and associated metadata into a single file.

**Some Parameters**:
- `c`: Creates a new JAR file.
- `f`: Specifies the JAR file name.
- `v`: Generates verbose output.
- `x`: Extracts files from a JAR file.

**Example**:

Create a JAR file:
```bash
jar cfv example.jar -C ./bin .
```

Extract a JAR file:
```bash
jar xvf example.jar
```

## `javap` (Java Class File Disassembler)

**Purpose**: Disassembles class files.

**Some Parameters**:
- `-c`: Disassembles the bytecode.
- `<classfile>`: The name of the class file to disassemble.

**Example**:
```bash
javap -c MyClass.class
```

**Expected Response**:
```
Compiled from "MyClass.java"
public class MyClass extends java.lang.Object{
public MyClass();
Code:
0: aload_0
1: invokespecial #1                  // Method java/lang/Object."<init>":()V
4: return

    public void myMethod();
    Code:
       0: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
       3: ldc           #3                  // String Hello, World!
       5: invokevirtual #4                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
       8: return
}
```
Displays disassembled bytecode of the `MyClass` class file.

## `javadoc` (Generates HTML documentation)

**Purpose**: Generates HTML documentation from Java source code with special documentation comments.

**Some Parameters**:
- `-d`: Destination directory for output.
- `-sourcepath`: Source files path.

**Example**:

Generate documentation for all Java files in a directory:

```bash
javadoc -d ./docs -sourcepath ./src
```

## `jconsole` (Monitoring tool)

**Purpose**: `jconsole` is a monitoring tool that provides information about the performance and resource consumption of running Java applications.

**Example**:

Launch JConsole:
```bash
jconsole
```


## `jps` (Java Virtual Machine Process Status Tool)

**Purpose**: JVM Process Status Tool, displays all HotSpot virtual machine processes on a given system.

**Example**:
```bash
jps -l
```

**Expected Response**:
```
2234 sun.tools.jps.Jps
4691 my.java.Application
```
Lists running Java processes with their process ids and the main class name.

## `jstat` (JVM Statistics Monitoring Tool)

**Purpose**: Monitors JVM statistics. Tools used to monitor the virtual machine a variety of operational status information. Including class loading, memory, rubbish collection, JIT compilation and other operational data.

**Some Parameters**:

- `-gc`: Monitors garbage collection statistics.
- `<vmid>`: The process id of the JVM.
- `<interval>`: The time between data samples in milliseconds.
- `<count>`: The number of samples to take before terminating.

**Example**:
```bash
jstat -gc 4691 250 4
```

**Expected Response**:
```
S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT   
46080.0 46080.0 0.0    0.0    184320.0  11614.4  368640.0   32252.8  4480.0 4345.7 512.0  498.2      5    0.305   2      0.273    0.578
```
Displays garbage collection statistics for the JVM with process id 4691. 

1. S0C: capacity of the first survivor in the young generation (KB)
2. S1C: capacity of the second survivor in the young generation (KB)
3. S0U: currently used space of the first survivor in the young generation (KB)
4. S1U: currently used space of the second survivor in the young generation (KB)
5. EC: capacity of Eden in the young generation (KB)
6. EU: currently used space of Eden in the young generation (KB)
7. OC: Capacity of the Old generation (KB)
8. OU: Currently used space in Old generation (KB)
9. PC: Capacity of Perm (Persistent Generation) (KB)
10. PU: Perm Used Space (KB)
11. YGC: number of gc's in the young generation from application startup to sampling
12. YGCT: time from application startup to gc in the young generation at the time of sampling (s)
13. FGC: number of gc in old generation (full gc) from application startup to sampling time
14. FGCT: time(s) spent in gc from application startup to gc in old generation (full gc) at sample time
15. GCT: total time(s) used for gc from application startup to sampling time


## `jinfo` (Configuration Info for Java)

**Purpose**: Shows configuration info for a Java process.

**Some Parameters**:
- `<vmid>`: The process id of the JVM.

**Example**:
```bash
jinfo 4691
```

**Expected Response**:
```
Attaching to process ID 4691, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 25.131-b11
Java System Properties:

java.runtime.name = Java(TM) SE Runtime Environment
java.vm.version = 25.131-b11
java.vm.vendor = Oracle Corporation
```
Lists configuration information for the JVM with process id 4691.

## `jmap` (Memory Map for Java)

**Purpose**: Prints memory-related information of a Java process.

**Some Parameters**:
- `-heap`: Prints heap summary information.
- `<vmid>`: The process id of the JVM.

**Example**:
```bash
jmap -heap 4691
```

**Expected Response**:
```
Attaching to process ID 4691, please wait...
Debugger attached successfully.

Heap Configuration:
MinHeapFreeRatio = 40
MaxHeapFreeRatio = 70
MaxHeapSize      = 2097152000 (2000.0MB)
NewSize          = 1310720 (1.25MB)
MaxNewSize       = 17592186044415 MB
OldSize          = 5439488 (5.1875MB)
NewRatio         = 2
SurvivorRatio    = 8
MetaspaceSize    = 21807104 (20.796875MB)
CompressedClassSpaceSize = 1073741824 (1024.0MB)
MaxMetaspaceSize = 17592186044415 MB
G1HeapRegionSize = 0 (0.0MB)
```
Displays heap configuration and utilization for the JVM process.

## `jhat` (JVM Heap Analysis Tool)

**Purpose**: Analyzes heap dump files.It is used in conjunction with jmap to analyse the heapdump(.hprof) generated by jmap.

**Some Parameters**:
- `<heapdumpfile>`: The filename of the heap dump.

**Example**:
```bash
jhat -J-Xmx4G heapdump.hprof
```

**Expected Response**:
```
Reading from heapdump.hprof...
Dump file created Thu Jan 07 10:32:18 PST 2021
Snapshot read, resolving...
Resolving 9876543 objects...
Chasing references, expect 12345 dots....................................
Snapshot resolved.
Started HTTP server on port 7000
Server is ready.
```
Analyzes the heap dump file and starts a web server for analysis.

## `jstack` (Stack Trace for Java)

**Purpose**: Prints stack traces of Java threads. jstack is used to generate a snapshot of the threads in the java virtual machine at the current moment. A thread snapshot is a collection of method stacks for each thread currently executing within the java virtual machine. The main purpose of generating thread snapshots is to locate the reasons for threads to appear a long time to stop , such as thread deadlocks, dead loops, requests for external resources resulting in a long time to wait and so on.

**Some Parameters**:
- `<vmid>`: The process id of the JVM.

**Example**:
```bash
jstack 4691
```

**Expected Response**:
```
Full thread dump Java HotSpot(TM) 64-Bit Server VM (25.131-b11 mixed mode):

"Attach Listener" #14 daemon prio=9 os_prio=0 tid=0x00007f13c4001000 nid=0x1234 waiting on condition [0x0000000000000000]
java.lang.Thread.State: RUNNABLE

"Finalizer" #3 daemon prio=8 os_prio=0 tid=0x00007f13c000a800 nid=0x1107 in Object.wait() [0x00007f13b4ffe000]
java.lang.Thread.State: WAITING (on object monitor)
```
Provides a snapshot of all threads' stack traces in the JVM.
