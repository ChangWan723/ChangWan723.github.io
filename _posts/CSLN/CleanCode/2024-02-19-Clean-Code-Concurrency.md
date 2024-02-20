---
title: "Clean Code: Concurrency "
date: 2024-02-19 22:56:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/concurrency.png
---

> **Writing clean concurrent programs is hard — very hard.** It is much easier to write code that executes in a single thread. It is also easy to write multithreaded code that looks fine on the surface but is broken at a deeper level. Such code works fine until the system is placed under stress.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction of Concurrency](#introduction-of-concurrency)
    * [Why Concurrency?](#why-concurrency)
    * [Some Statements about Concurrency](#some-statements-about-concurrency)
  * [Concurrency Defense Principles](#concurrency-defense-principles)
    * [Keep It Simple](#keep-it-simple)
    * [Single Responsibility Principle](#single-responsibility-principle)
    * [Limit the Scope of Data](#limit-the-scope-of-data)
    * [Use Copies of Data](#use-copies-of-data)
    * [Threads Should Be as Independent as Possible](#threads-should-be-as-independent-as-possible)
    * [Use Clear Names](#use-clear-names)
    * [Know Your Library](#know-your-library)
<!-- TOC -->

---

## Introduction of Concurrency

Concurrency is not just a tool for improving performance; it's a fundamental paradigm shift in how we think about structuring and executing our code. In an era where multi-core processors are ubiquitous, understanding concurrency is indispensable. It's about doing multiple things at once, not necessarily making things faster but making applications more responsive and efficient.

### Why Concurrency?

- **Concurrency is a decoupling strategy.** Concurrency can separate the execution of tasks ('what') from the timing ('when'), improving application efficiency and structure.
  - For example, the standard “Servlet” model of Web applications. It allows web applications to process requests asynchronously, where each request is handled independently, facilitating a decoupled system architecture. 
- **Concurrency can improve performance.** Systems with concurrency can meet tight response and throughput constraints, an essential feature for high-demand applications. 
  - The single-thread involves a lot of waiting at Web sockets for I/O to complete.
  - Concurrent processing can address this by allowing multiple data requests to be handled simultaneously, which is especially beneficial as system usage grows.

### Some Statements about Concurrency

- **Concurrency does not always improve performance.**
  - Concurrency can sometimes improve performance, but only when there is a lot of wait time that can be shared between multiple threads or multiple processors.
- **Writing concurrent programs does affect design.**
  - It changes algorithms and significantly impacts system structure due to the decoupling of tasks from timing.
- **Understanding concurrency issues remains crucial in systems using containers like Web or EJB containers to avoid concurrent update issues and deadlocks.**
- **Concurrency introduces overhead in both performance and the complexity of the code.**
- **Implementing concurrency correctly is challenging, even for simple problems.**
- **Bugs in concurrent systems may not be repeatable, leading them to be overlooked as one-offs rather than recognized as true defects.**
- **Effective concurrency often requires a fundamental shift in design strategy.**
- **Concurrency can create a significant uncertainty in the process**
  - The complexity of concurrent programming is further highlighted by considering the number of different execution paths possible in the method due to concurrency issues.

## Concurrency Defense Principles

The principles, while not explicitly designed for concurrency, provide a solid foundation for tackling concurrent programming challenges.

### Keep It Simple

Concurrency introduces complexity, there's no denying it. However, the Clean Code principle of keeping things simple applies even more so here. We should strive to keep our concurrent code as straightforward as possible. This might mean preferring higher-level abstractions provided by modern languages and frameworks, such as `async/await` in JavaScript or the `Stream` API in Java, over more complex and error-prone constructs like raw threads and locks.

### Single Responsibility Principle

> The SRP5 states that a given method/class/component should have a single reason to change. Concurrency design is complex enough to be a reason to change in it’s own right and therefore deserves to be separated from the rest of the code. 

> Keep your concurrency-related code separate from other code.
{: .prompt-tip }

### Limit the Scope of Data

In concurrent programming, shared mutable state is the root of all evil. To write clean concurrent code, we should limit the scope of mutable data as much as possible and use immutable data structures whenever feasible. This approach minimizes the chances of race conditions and makes the code easier to reason about.

> Take data encapsulation to heart; severely limit the access of any data that may be shared.
{: .prompt-tip }

### Use Copies of Data

Avoiding shared data can simplify concurrency by copying objects and treating them as read-only or merging results from these copies in a single thread. While there may be concerns about the overhead from object creation and garbage collection, the benefits of reducing synchronization could outweigh these costs.

### Threads Should Be as Independent as Possible

Design threaded code so that each thread operates independently, processing requests with its own unshared data, like local variables, to minimize synchronization issues.

For instance, HttpServlets in web applications behave as if isolated, using only local variables within doGet and doPost methods, thereby avoiding synchronization problems. However, shared resources, like database connections, can still present challenges for servlet-based applications.

> Attempt to partition data into independent subsets than can be operated on by independent threads.
{: .prompt-tip }

### Use Clear Names

Just as we name variables and functions in a way that expresses their intent, we should make names clear and understandable when using concurrency.

For example, using a `ConcurrentHashMap` in Java clearly signals to the reader that this data structure is intended for use in a concurrent context.

### Know Your Library

Modern programming languages and environments may provide tools to facilitate concurrent  development.

For example, Java offers many improvements for concurrent development over previous versions. 

> When Java was young, Doug Lea wrote the seminal book8 Concurrent Programming in Java. Along with the book he developed several thread-safe collections, which later became part of the JDK in the `java.util.concurrent` package. The collections in that package are safe for multithreaded situations and they perform well. In fact, the `ConcurrentHashMap` implementation performs better than HashMap in nearly all situations. It also allows for simultaneous concurrent reads and writes, and it has methods supporting common composite operations that are otherwise not thread safe.

> Review the classes available to you. In the case of Java, become familiar with `java.util.concurrent`, `java.util.concurrent.atomic`, `java.util.concurrent.locks`.
{: .prompt-tip }


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
