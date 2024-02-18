---
title: "Clean Code: Systems"
date: 2024-02-02 16:58:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/systems.png
---

In essence, building clean systems is about crafting a harmonious ecosystem where code not only meets current requirements but is also poised gracefully to evolve with future demands. As we imbue our systems with these clean code principles, we lay down a robust foundation for software.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Separating Constructing a System from Using It](#separating-constructing-a-system-from-using-it)
    * [The Challenge of Startup](#the-challenge-of-startup)
      * [Example: Lazy Initialization](#example-lazy-initialization)
    * [How to Solve the Problems?](#how-to-solve-the-problems)
      * [Example](#example)
  * [Separation of Concerns](#separation-of-concerns)
    * [Aspect-Oriented Programming (AOP) as a Solution](#aspect-oriented-programming-aop-as-a-solution)
      * [AOP Concepts](#aop-concepts)
    * [AOP in Practice](#aop-in-practice)
  * [Delaying Decisions](#delaying-decisions)
  * [Use Standards Wisely, When They Add Demonstrable Value](#use-standards-wisely-when-they-add-demonstrable-value)
  * [Systems Need Domain-Specific Languages](#systems-need-domain-specific-languages)
    * [Benefits](#benefits)
<!-- TOC -->

---

## Separating Constructing a System from Using It

**Principle**: Systems should clearly separate the startup process (when the application objects are constructed and the dependencies are "wired" together) from the runtime logic that takes over after startup.

**Application**: Utilize techniques like Dependency Injection (DI) and factories to decouple system construction from business logic. For instance, frameworks like Spring in Java offer comprehensive DI mechanisms to manage this separation cleanly.

### The Challenge of Startup

A system's startup phase is critical yet often convoluted. It involves instantiating objects, establishing dependencies, and setting up resources. This process can become a tangled web that's hard to decipher and maintain.

#### Example: Lazy Initialization

**Example of Startup (Lazy Initialization):**

```java
public class ServiceHolder {
    private static Service service;

    public static Service getService() {
        if (service == null) {
            service = new ExpensiveServiceImplementation(); // This is lazy initialization
        }
        return service;
    }
}

class ExpensiveServiceImplementation {
    public ExpensiveServiceImplementation() {
        // Constructor logic that might be expensive in terms of resources or time
    }

    // Service methods...
}
```

**Lazy Initialization** is a design pattern used to delay the creation of an object, the calculation of a value, or some other expensive process until the first time it is needed.

- **Advantage:** This approach has several benefits such as reducing computational overhead and ensuring resources are utilized only when necessary, thus potentially increasing the program's efficiency, especially during startup.
   - The `service` object is initialised only when `getService()` is called for the first time. 
     - This is lazy because if the `service` object is never requested, it is never created, thus saving resources. The `ExpensiveServiceImplementation` is a hypothetical class that implements the Service interface and might have an expensive construction process.
   - It also ensures that `null` is never returned.

- **Disadvantage:** For instance, there is a hard-coded dependency on a specific service implementation, which might not be suitable in all cases and may also violate the Single Responsibility Principle because the method is doing more than one thing (the code mixes construction logic with normal runtime processing). 
  - `ServiceHolder` is **directly dependent** on `ExpensiveServiceImplementation`. 
    - This makes it difficult to change the service implementation without modifying the `ServiceHolder` class, which can be problematic for testing and when different contexts require different Service implementations. 
    - By directly referencing `ExpensiveServiceImplementation`, `ServiceHolder` must know about the details of creating and initialising this specific implementation. For example, if the constructor of `ExpensiveServiceImplementation` changes to require new parameters, you would have to modify `ServiceHolder` to supply these parameters. 
  - It also **mixes the object creation logic with the usage logic**, which might be better separated.

### How to Solve the Problems?

- The key is to **decouple system construction from its runtime logic**. We can use a few design patterns and principles:
   1. **Dependency Injection**: Rather than hard-coding a specific service implementation, we can inject the service dependency. This allows for greater flexibility and easier testing. 
   2. **Use of Factories**: By using a factory pattern, we can encapsulate the creation logic of the service, making the code more modular.
   3. **Interface Segregation**: Ensure that our service interfaces are specific to client needs so that we don't force clients to depend on methods they do not use. 
   4. **Separation of Concerns**: Keeping the service creation and service usage separate.

#### Example

```java 
public class ServiceHolder {
    private static Service service;
    private static ServiceFactory serviceFactory;

    public static void setServiceFactory(ServiceFactory factory) {
        serviceFactory = factory;
    }

    public static Service getService() {
        if (serviceFactory == null) {
          throw new IllegalStateException("ServiceFactory not initialized.");
        }
   
        if (service == null) {
            service = serviceFactory.createService(); // Creation is now delegated to a factory.
        }
        return service;
    }
}

interface ServiceFactory {
    Service createService();
}

class ExpensiveServiceImplementationFactory implements ServiceFactory {
    public Service createService() {
        return new ExpensiveServiceImplementation();
    }
}

class ExpensiveServiceImplementation {
    public ExpensiveServiceImplementation() {
        // Constructor logic that might be expensive in terms of resources or time
    }

    // Service methods...
}

```

In this refactored code:
  - We introduce a `ServiceFactory` interface that defines a method for creating a `Service`. The interface has the following advantages: 
     1. **Program to an Interface, Not an Implementation**: By programming to an interface, you can change the concrete implementation of the factory without changing the code that uses it. This makes your code more flexible and easier to maintain.
    2. **Decoupling**: The interface decouples the creation of the object from its use. This means that the `ServiceHolder` doesn't need to know any details about how to create the `Service` instance. It only needs to know that it can ask `serviceFactory` to create the service.
    3. **Testability**: With an interface, it becomes easier to inject mock or stub factories for testing purposes. You can create a test implementation of the `ServiceFactory` that creates a lightweight or controlled version of the `Service` for testing.
    4. **Flexibility and Scalability**: If in the future you need to create different kinds of services, you can implement different factories that conform to the `ServiceFactory` interface without changing the client code. This follows the Open/Closed Principle (OCP), where software entities should be open for extension, but closed for modification.
    5. **Consistent API**: The interface provides a consistent API for service creation. No matter what kind of service you need to create, the method call remains the same (createService()). This is easier to document and use.
  - We provide a concrete implementation of the factory (`ExpensiveServiceImplementationFactory`) that knows how to instantiate the `ExpensiveServiceImplementation`.
  - The `ServiceHolder` no longer directly creates an instance of `ExpensiveServiceImplementation`. Instead, it asks the `ServiceFactory` to create it, which is set via `setServiceFactory()`. This allows us to change the service implementation without modifying the `ServiceHolder`.
     - You might say that there are still class (`ExpensiveServiceImplementationFactory`) that depend directly on the creation of the service. This is true, of course, because we always need to the service, which is inevitable. But **this approach succeeds in separating service creation from service use**, which is the problem we're trying to solve.
  - **This approach retains the advantages of lazy initialisation and addresses its disadvantages.**

## Separation of Concerns

Separation of concerns is an age-old principle in software engineering that advocates for segregating a computer program into distinct sections, such that each section addresses a separate concern. However, certain cross-cutting concerns like logging, security, and transaction management often defy this separation, scattering across various modules and tangling the code.

### Aspect-Oriented Programming (AOP) as a Solution

**Aspect-Oriented Programming (AOP)** is a programming paradigm that aims to increase modularity by **allowing the separation of cross-cutting concerns from business logic**. 
  - Cross-cutting concerns are aspects of a program that affect multiple modules, such as logging, security, transaction management, and error handling. 
  - AOP introduces the concept of "**aspects**", which encapsulate behaviors that cut across multiple classes, such as logging, error handling, or security. 
  - AOP addresses these concerns by modularising them into distinct aspects, thereby simplifying the core business logic and enhancing code readability and maintainability.

#### AOP Concepts

- **Aspect**: A module that encapsulates a cross-cutting concern.
- **Join Point**: Specific points in the program execution where an aspect can be applied, such as method calls or field assignments.
- **Advice**: The action taken by an aspect at a particular join point, such as executing code before or after a method call.
- **Pointcut**: Expressions that define which join points an advice should be applied to.
- **Weaving**: The process of applying aspects to target objects to create advised objects, which can happen at compile time, load time, or runtime.

### AOP in Practice

Consider a logging aspect in a web application. Instead of scattering logging statements throughout the codebase, an AOP approach would define a logging aspect that automatically applies logging before and after the execution of selected methods, based on defined pointcuts.

---

There is a simple Java service where we want to add logging functionality to method executions without polluting the business logic with logging code.

```java 
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Pointcut;

@Aspect
public class LoggingAspect {

    @Pointcut("execution(* com.example.service.*.*(..))") // Pointcut expression
    public void serviceMethods() {}

    @Before("serviceMethods()") // Advice that runs before the methods matched by the pointcut
    public void logMethodCall(JoinPoint joinPoint) {
        String methodName = joinPoint.getSignature().getName();
        System.out.println("Executing method: " + methodName);
    }
}
```

- `@Aspect`: This annotation marks the `LoggingAspect` class as an **aspect**.
  - With Spring AOP, simply annotating the aspect class with `@Aspect` and ensuring it's scanned by Spring's component scanner is enough to apply the aspect to the beans.
- `@Pointcut("execution(* com.example.service.*.*(..))")`: This annotation defines a **pointcut** with an expression that specifies which methods will be intercepted. This **pointcut** matches all methods in all classes within the `com.example.service` package. This specific expression means:
    - `execution`: Indicates triggering during the method execution.
    - `*`: Means any return type.
    - `com.example.service.*`: Refers to any class in the com.example.service package.
    - `.*`: Refers to any method within the class.
    - `(..)`: Means any number and type of method arguments.
- `public void serviceMethods() {}`: The `serviceMethods()` method is empty, as it serves only as a marker for the positioning of the **pointcut**. It does not need to contain any logic itself, as it is just a named point marked by `@Pointcut`. This named point is used to be referenced in other notifications (e.g. `@Before`, `@After`, `@Around`, `@AfterReturning`, `@AfterThrowing`, etc.) so that those notifications know which methods they need to be applied to.
- `@Before("serviceMethods()")`: This annotation represents a before **advice**, which will execute before the methods specified by the pointcut `serviceMethods()`.
- `public void logMethodCall(JoinPoint joinPoint)`: This is the **advice** method that will be called before the execution of the method matched by the **pointcut**.
  - The `JoinPoint` parameter provides access to the method being advised, such as the method name, arguments, etc.
  - Now, every time a method in the `com.example.service` package is executed, the `logMethodCall` advice is invoked, logging the method's execution without the service methods being aware of the logging logic.

## Delaying Decisions

**Principle**: Hold making decisions about certain aspects of the system until the last responsible moment. This approach keeps the system flexible and open to change. Systems evolve, and early decisions can lock you into specific technologies or designs that might become obsolete or unsuitable. Delaying decisions keeps your options open for as long as possible.

**Application**: Use plugins, factories, or strategy patterns to encapsulate decisions that are likely to change. For example, deferring the choice of a database or specific business logic algorithm until runtime can significantly enhance the system's adaptability.


## Use Standards Wisely, When They Add Demonstrable Value

**Principle**: Standards should be adopted for their benefits in interoperability, not for their own sake. Blindly following standards without evaluating their impact on the system can lead to complexity and rigidity.

**Application**: Evaluate standards based on the tangible value they bring to your system. For example, using REST for web services offers wide compatibility and simplicity, but it might not always be the best choice if RPC or GraphQL suits your system's needs better.

## Systems Need Domain-Specific Languages

**Domain-Specific Languages (DSLs)** are specialised computer languages focused on a particular aspect of a software application or system. Unlike general-purpose languages(GPL) like Python, Java, or C#, which are designed to be versatile and applicable across various domains, DSLs are tailored to a specific domain or concern, **offering constructs and abstractions that directly map to domain concepts.**
  - DSL is not very general, it is designed for a specific domain, but it is sufficient to represent problems in that domain and to construct solutions to them. For example, HTML is a typical example of DSL. HTML is a language used in web applications, and its inability to perform numerical operations does not prevent it from being widely used in this context.
  - The GPL, on the other hand, is not domain-specific; the designers of the language could not have known what domains the language would be used in, much less what problems the users intended to solve. So the GPL is designed to solve any kind of problem, fit any kind of business, and meet any kind of need. Java, for example, is GPL, and it can run on PCs or mobile devices and be embedded in applications in a variety of industries such as banking, finance, insurance, manufacturing, and so on.

**Principle**: Creating a domain-specific language (DSL) can significantly simplify complex configurations or interactions within a system.

**Application**: Implement DSLs to express domain concepts more clearly. This could be as simple as a configuration DSL using YAML or JSON, or more complex, like a full-fledged scripting language embedded within the system.

### Benefits

- **Increased Productivity**: DSLs can make developers more productive by reducing boilerplate and making complex configurations more readable.
- **Improved Communication**: DSLs can bridge the gap between developers and domain experts, leading to software that better aligns with business needs.


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
