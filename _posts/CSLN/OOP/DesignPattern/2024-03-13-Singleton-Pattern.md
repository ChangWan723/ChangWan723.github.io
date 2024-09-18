---
title: Why I Don't Recommend Using the Singleton Pattern?
date: 2024-03-13 18:36:00 UTC
categories: [(CS) Learning Note, OOP]
tags: [software engineering, OOP, Design Patterns]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Singleton Pattern?](#what-is-singleton-pattern)
    * [The Effect of the Singleton Pattern](#the-effect-of-the-singleton-pattern)
  * [How to Implement a Singleton?](#how-to-implement-a-singleton)
    * [Eager Initialization](#eager-initialization)
    * [Lazy Initialization](#lazy-initialization)
    * [Static Block Initialization](#static-block-initialization)
    * [Double-Checked Locking](#double-checked-locking)
    * [Static Inner Class](#static-inner-class)
    * [Enum Singleton](#enum-singleton)
  * [Why I Don't Recommend Using the Singleton Pattern](#why-i-dont-recommend-using-the-singleton-pattern)
    * [Compromised OOP Feature Support](#compromised-oop-feature-support)
    * [Obscured Class Dependencies](#obscured-class-dependencies)
    * [Impediments to Extensibility](#impediments-to-extensibility)
    * [Challenges in Code Testability](#challenges-in-code-testability)
    * [Lack of Support for Parameterized Constructors](#lack-of-support-for-parameterized-constructors)
  * [What are the Alternatives to the Singleton Pattern?](#what-are-the-alternatives-to-the-singleton-pattern)
    * [Dependency Injection (DI)](#dependency-injection-di)
    * [Factory Pattern](#factory-pattern)
    * [Monostate Pattern](#monostate-pattern)
<!-- TOC -->

---

## What is Singleton Pattern?

The Singleton Pattern is a creational design pattern that restricts the instantiation of a class to one "single" instance. This is particularly useful when exactly one object is needed to coordinate actions across the system, such as in logging, driver objects, caching, thread pools, and configuration settings.

### The Effect of the Singleton Pattern

- **Controlled Access:** Singleton provides controlled access to the sole instance, preventing unauthorized changes.
- **Lazy Initialization:** It’s efficient in resource management, as it can delay the instance creation until it is needed.
- **Global State:** Singleton can store a global state that's accessible across the application.

## How to Implement a Singleton?

### Eager Initialization

Eager initialization involves creating the Singleton instance at the time of class loading. It's straightforward but has the drawback of not being lazy.

```java
public class EagerInitializedSingleton {
    private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();

    private EagerInitializedSingleton() {}

    public static EagerInitializedSingleton getInstance() {
        return instance;
    }
}
```

**Advantages:**
- Easy to implement.
- Thread-safe.

**Disadvantages:**
- Instance is created even if it might not be used in the application, which could lead to resource wastage.

### Lazy Initialization

This method delays the creation of the instance until it is needed for the first time.

```java
public class LazyInitializedSingleton {
    private static LazyInitializedSingleton instance;

    private LazyInitializedSingleton() {}

    public static LazyInitializedSingleton getInstance() {
        if (instance == null) {
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```

**Advantages:**
- Saves resources by delaying the creation.

**Disadvantages:**
- Not thread-safe without additional synchronization logic.

### Static Block Initialization

Similar to eager initialization but with the option for error handling during instance creation.

```java
public class StaticBlockSingleton {
    private static StaticBlockSingleton instance;

    static {
        try {
            instance = new StaticBlockSingleton();
        } catch (Exception e) {
            throw new RuntimeException("Exception occurred in creating singleton instance");
        }
    }

    private StaticBlockSingleton() {}

    public static StaticBlockSingleton getInstance() {
        return instance;
    }
}
```

**Advantages:**
- Provides error handling options.
- Like eager initialization: 
  - Easy to implement. 
  - Thread-safe.

**Disadvantages:**
- Like eager initialization, it might lead to resource wastage if the instance isn’t used.

### Double-Checked Locking

This approach minimizes the performance overhead of synchronization while maintaining laziness and thread safety.

```java
public class DoubleCheckedLockingSingleton {
    private static volatile DoubleCheckedLockingSingleton instance;

    private DoubleCheckedLockingSingleton() {}

    public static DoubleCheckedLockingSingleton getInstance() {
        if (instance == null) {
            synchronized (DoubleCheckedLockingSingleton.class) {
                if (instance == null) {
                    instance = new DoubleCheckedLockingSingleton();
                }
            }
        }
        return instance;
    }
}
```

> - **Why use the keyword `volatile`?**
>   - **`volatile` ensures ordering of instructions**.
>     - `volatile` can **prevent instruction reordering optimisations.** This ensures that no memory address is assigned to the `instance` before the initialisation of the object is complete.
>   - **`volatile` ensures visibility of changes in a multi-threaded environment.**
>     - When a variable is declared `volatile`, **any write operations to the variable are immediately synchronised back into main memory;** at the same time, any read operations to the variable are read from main memory, not from the thread's private cache
> - **Why use class-level lock `DoubleCheckedLockingSingleton.class`?**
>   - Because **instances of the singleton are static** (i.e., class level), it is a natural choice to use the class-level lock (global locking).
> - **Why do we need double null checking?**
>   - **First check: improves performance** by avoiding entering the synchronisation block for every call after the singleton has already been created.
>   - **Second check: ensure thread safety.** Because even if it passes the first null check, there is no guarantee that instance will be null due to the lack of locking.
{: .prompt-tip }

**Advantages:**
- Thread-safe and lazy initialization without significant performance impact.

**Disadvantages:**
- More complex implementation.

### Static Inner Class

Utilizes a static inner class to hold the instance, taking advantage of the JVM’s class loading mechanism to ensure thread safety and laziness.

```java
public class StaticInnerClassSingleton {
    private StaticInnerClassSingleton() {}

    private static class SingletonHolder {
        private static final StaticInnerClassSingleton INSTANCE = new StaticInnerClassSingleton();
    }

    // INSTANCE is created only when someone calls the getInstance() method.
    public static StaticInnerClassSingleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

**Advantages:**
- Lazy initialization and thread-safe without synchronization overhead.
- This way has almost no drawbacks and is the most recommended way.


### Enum Singleton

The enum approach guarantees the singleton property through Java's enum type.

```java
public enum EnumSingleton {
    INSTANCE;

    public void doSomething(String param) {
        // Some functionality here
    }
}
```

**Advantages:**
- Easy to implement, provides serialization machinery for free, and is thread-safe.

**Disadvantages:**
- Not as flexible as a class-based singleton (e.g., in terms of inheritance).

## Why I Don't Recommend Using the Singleton Pattern

### Compromised OOP Feature Support

- **Singleton pattern essentially violates the essence of Abstraction in OOP.**
  - Using the singleton pattern means that whatever the `class` is, it must be instantiated.
  - In that case, all uses of the singleton pattern would **have to rely on concrete implementations** (rather than abstract interfaces). This is not conducive to code scalability.
- Besides that, **singleton patter is not friendly to Inheritance and Polymorphic features in OOP.**
  - Theoretically, a singleton class can also be inherited and polymorphic. But this would look very strange and would lead to less readable code.


### Obscured Class Dependencies

- **One of the key principles of maintainable code is explicitness**, especially regarding dependencies between classes.  
  - Dependencies between classes declared through constructors, parameter passing, instance variables, etc. are easily recognised by looking at the definition of the function or the class structure.
  - **But Singleton instances, often accessed directly through static methods, obscure these dependencies.**
  - It obscures the system's architecture, complicating understanding and modification.

### Impediments to Extensibility

- **A singleton class can only have one instance.**
  - If at some point in the future we need to create two instances or more instances (it could happen), it will require a relatively large change to the code.
  - In contrast, the factory pattern has good extensibility.

### Challenges in Code Testability

- In unit testing, it is difficult to replace static singleton cases with `mock`. 
  - **It is therefore difficult to isolate the unit under test** (e.g., the database link), thus complicating the test.
- The singleton pattern may have global variables (state), which may be modified.
  - **This can cause different unit tests to interact with each other,** which is contrary to the principles of unit testing.

> - **Global variables are a procedural oriented style of programming and have various drawbacks in OOP.** 
>   - In the POP paradigm, a program is viewed as a series of procedures or function calls. These procedures operate on global variables or data passed through function parameters. Global variables are more common in this paradigm because they provide a simple mechanism for different procedures to share data.
>   - OOP treats a program as a collection of objects. One of the basic principles of OOP is encapsulation, which tends to encapsulate data and operations associated with it inside an object in order to hide the concrete implementation of the object and to reduce direct external access to the data. Global variables violate the principle of encapsulation because they are globally accessible, rather than being confined inside the object. This reduces the object's ability to control its own state.
{: .prompt-tip }


### Lack of Support for Parameterized Constructors

- **The Singleton pattern does not naturally accommodate constructors with parameters**, as the instance is typically created through a static method without parameters. 
  - This limitation restricts the flexibility in configuring the singleton instance, compelling developers to resort to additional methods or mechanisms to provide the necessary configuration, which can complicate the code.

## What are the Alternatives to the Singleton Pattern?

Given these drawbacks, it's worth considering alternatives that offer similar benefits without the accompanying disadvantages:

### Dependency Injection (DI)

DI frameworks, such as Spring (for Java) or Autofac (for .NET), manage object creation and dependencies. By configuring a class as a singleton within the DI container, you gain the benefits of a single instance without the Singleton pattern's drawbacks, enhancing testability and reducing coupling.

### Factory Pattern

The Factory pattern can control object creation more flexibly, allowing for parameters, varying implementations, and more straightforward subclassing. When combined with configuration or DI, it can effectively replace singletons in many scenarios.

### Monostate Pattern

The Monostate pattern achieves singleton-like behavior through static member variables while allowing multiple instances of a class. This approach can offer a compromise, retaining instance-level method calls and constructor use while ensuring shared state.

> Despite the drawbacks of the singleton pattern, it's a bit extreme to treat it as an anti-pattern and advocate eliminating its use in projects.
> 
> **If the singleton class has no need for extensions and does not depend on external systems, then there is no problem in designing it as a singleton class. For some global information, sometimes it is really simple and convenient to use it directly as a singleton class.**
{: .prompt-tip }


---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Design Patterns_. Geek Time. 
