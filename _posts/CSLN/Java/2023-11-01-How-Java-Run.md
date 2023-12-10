---
title: How does Java code runs?
date: 2023-11-01 23:04:00 UTC
categories: [(CS) Learning Note, Java]
tags: [software engineering, Java, JVM]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Journey of Java Code: From Compilation to Execution](#journey-of-java-code-from-compilation-to-execution)
    * [Writing the Code](#writing-the-code)
    * [Compilation to Java bytecode](#compilation-to-java-bytecode)
    * [Loading](#loading)
    * [Linking](#linking)
    * [Initialization](#initialization)
    * [Compilation to Machine Code](#compilation-to-machine-code)
    * [Execution](#execution)
  * [Why execute Java in the JVM?](#why-execute-java-in-the-jvm)
<!-- TOC -->

---

## Journey of Java Code: From Compilation to Execution

### Writing the Code

The first step is writing the Java code. This is the stage where we, as developers, define the classes, methods, and logic to solve a particular problem or accomplish a specific task.

```java
public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello, World!");
  }
}
```

### Compilation to Java bytecode

Once the code is written, the next step is to compile it. The Java compiler, `javac`, transforms the human-readable `.java` file into a `.class` file containing Java bytecode.

```sh
javac HelloWorld.java
```

Java bytecode is a set of instructions that is independent of the underlying hardware. This is what makes Java platform independent.

### Loading

The compiled bytecode is then loaded into the Java Virtual Machine (JVM) by the class loader. The class loader is responsible for finding and loading the class files.

The loaded Java class is stored in the Method Area. The JVM will execute the code in the Method Area during runtime.

### Linking

Before the class can be used, it must be linked. Linking involves three steps:

1. **Verification:** The bytecode is verified to ensure that it adheres to Java's safety rules and doesn't contain any illegal instructions.
2. **Preparation:** Memory is allocated for the class variables and default values are assigned.
3. **Resolution:** Symbolic references in the bytecode are replaced with direct references.

### Initialization

After linking, the class is initialized. This involves executing any static initializers and initializing static variables. The JVM ensures that this process is thread-safe and that the class is fully initialized before it is used.

### Compilation to Machine Code

The verified bytecode is then compiled into native machine code. This step is necessary because the CPU can only understand and execute machine code specific to the hardware architecture. The native machine code is then stored in the JVM's code cache for reuse.

> In HotSpot, the compilation process has two forms: 
> 1. **Interpreted execution**, i.e., compiling bytecode into machine code and executing it line by line; 
> 2. **Just-In-Time compilation (JIT)**, i.e., compiling all bytecode contained in a method into machine code and then executing it.
> 
> The advantage of the former is that it **doesn't have to wait for compilation**, while the advantage of the latter is that it actually **runs faster**.
> 
> HotSpot uses hybrid mode by default, which combines the advantages of both: it will first use interpreted execution, and then the hot code, which is repeatedly executed, is compiled in JIT compiler in the unit of methods.
{: .prompt-tip }


### Execution

Finally, the native machine code is executed by the CPU, and the output is displayed to the user.

```sh
Hello, World!
```
During runtime, whenever a Java method is called, the JVM generates a stack frame in the current thread's Java method stack to hold local variables and bytecode operands. The size of this stack frame is calculated in advance, and the JVM does not require the stack frame to be continuously distributed in memory space.

When exiting the currently executing method, no matter if it returns normally or abnormally, the JVM pops the current stack frame of the current thread and discards it.

![](https://i.postimg.cc/wB6QsPgb/jvm3.png){: .w-100 .shadow .rounded-10 }



## Why execute Java in the JVM?

- Java, as a **high-level programming language**, has a very complex syntax and a high level of abstraction. Therefore, it is not practical to run such complex programmes directly on hardware. So, before running the Java programme, we need to do some transformations on it.
- Java can run on different platforms in the JVM. This is often referred to as **"write once, run everywhere (WORA)"**.
- Another advantage of the JVM is that it brings a **Managed Runtime**. This managed environment takes over the responsibility of dealing with long and error-prone parts of the code. The most widely known of these is automatic memory management and garbage collection(GC).
