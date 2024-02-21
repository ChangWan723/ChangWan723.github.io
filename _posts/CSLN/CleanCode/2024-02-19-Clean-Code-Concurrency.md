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
    * [Keep Synchronized Sections Small](#keep-synchronized-sections-small)
    * [Be Cautious about Shutting Down Concurrency Code](#be-cautious-about-shutting-down-concurrency-code)
  * [Testing Threaded (Concurrent) Code](#testing-threaded-concurrent-code)
    * [Treat Spurious Failures as Candidate Threading Issues](#treat-spurious-failures-as-candidate-threading-issues)
    * [Get Your Nonthreaded Code Working First](#get-your-nonthreaded-code-working-first)
    * [Make Your Threaded Code Pluggable](#make-your-threaded-code-pluggable)
    * [Run with More Threads Than Processors](#run-with-more-threads-than-processors)
    * [Run on Different Platforms](#run-on-different-platforms)
    * [Instrument Your Code to Try and Force Failures](#instrument-your-code-to-try-and-force-failures)
      * [Hand-coded](#hand-coded)
      * [Automated](#automated)
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

Modern programming languages, libraries, or environments may provide tools to facilitate concurrent  development.

For example, Java offers many improvements for concurrent development over previous versions. 

> When Java was young, Doug Lea wrote the seminal book8 Concurrent Programming in Java. Along with the book he developed several thread-safe collections, which later became part of the JDK in the `java.util.concurrent` package. The collections in that package are safe for multithreaded situations and they perform well. In fact, the `ConcurrentHashMap` implementation performs better than HashMap in nearly all situations. It also allows for simultaneous concurrent reads and writes, and it has methods supporting common composite operations that are otherwise not thread safe.

> Review the classes available to you. In the case of Java, become familiar with `java.util.concurrent`, `java.util.concurrent.atomic`, `java.util.concurrent.locks`.
{: .prompt-tip }

### Keep Synchronized Sections Small

The synchronized keyword in programming introduces a lock, allowing only one thread to execute a block of code at a time. This locking mechanism, while ensuring thread safety, can be costly due to delays and added overhead. Therefore, it's important to use synchronized blocks sparingly and keep them as small as possible to avoid unnecessary performance degradation caused by extensive synchronization.

### Be Cautious about Shutting Down Concurrency Code

Implementing graceful shutdown procedures in systems designed to run indefinitely is challenging due to issues like deadlocks and threads that wait indefinitely for signals.

Problems arise, for example, if a parent thread waits for a deadlocked child thread, causing the system to hang. These scenarios are not uncommon, and significant effort is often required to ensure that concurrent systems can shut down correctly.

> Think about shut-down early and get it working early. It’s going to take longer than you expect. Review existing algorithms because this is probably harder than you think.
{: .prompt-tip }

## Testing Threaded (Concurrent) Code

It's not feasible to prove that code is completely correct, but thorough testing can reduce risks. This complexity escalates when multiple threads interact with shared data. The advice given is to create tests that can uncover potential issues and to run them often under varying configurations and loads.

### Treat Spurious Failures as Candidate Threading Issues

Threaded code can result in rare but critical failures that are difficult to predict and replicate. These failures may occur infrequently, perhaps once in thousands or millions of executions, making them challenging to diagnose. Developers may dismiss these as flukes or attribute them to external anomalies.

However, it's important to treat these failures seriously and not to disregard them as one-offs. Ignoring such issues can lead to building more code on top of an unstable foundation, compounding potential problems.

> Do not ignore system failures as one-offs.
{: .prompt-tip }

### Get Your Nonthreaded Code Working First

> **Nonthreading Code**: Nonthreading or non-threaded code refers to parts of the program that are designed to run sequentially on a single thread, as opposed to concurrently on multiple threads. It's the code that doesn't have to deal with synchronization issues that come with multi-threaded programming.

This is a fundamental piece of advice that suggests before integrating your code with multi-threading, you should ensure that it works correctly in a single-threaded context. In other words, **make sure that the basic functionality of your code is solid and bug-free before adding the complexity of threads.**

The recommendation is to **address non-threading issues separately from threading issues** to confirm that the code operates as intended without the added complexity of threads.

> Do not try to chase down nonthreading bugs and threading bugs at the same time. Make sure your code works outside of threads.
{: .prompt-tip }

### Make Your Threaded Code Pluggable

Design your threaded code to be adaptable, allowing it to run in various configurations such as with a single thread, multiple threads, or with changing thread counts during execution. Ensure it can interact with both actual components and test doubles, which can mimic different operation speeds.

> Make your threaded code modular and flexible to facilitate testing and debugging in different scenarios.
{: .prompt-tip }

### Run with More Threads Than Processors

Running the system with more threads than processors can **promote task swapping**, revealing issues such as missing critical sections or deadlocks.

### Run on Different Platforms

Testing threaded code on various platforms is crucial since threading behaviors can differ significantly across operating systems, as threading policies vary.

### Instrument Your Code to Try and Force Failures

Flaws in concurrent code can remain hidden because they don't always surface during normal operations or simple tests, potentially revealing themselves sporadically over long periods. These bugs are elusive due to the sheer number of execution paths available, making the chance of triggering a failure quite low.

- It's beneficial for issues to emerge early and frequently, and there are two main approaches to code instrumentation: - Hand-coded 
  - Automated

#### Hand-coded

To better detect the issues, it's recommended to instrument the code to force different execution orderings, using methods like `Object.wait()`, `Object.sleep()`, `Object.yield()`, and adjusting `Object.priority()`.

For example, The inserted call to `yield()` will change the execution pathways taken by the code and
possibly cause the code to fail where it did not fail before:

```java 
public synchronized String nextUrlOrNull() {
    if (hasNext()) {
       String url = urlGenerator.next();
       Thread.yield(); // inserted for testing.
       updateHasNext();
       return url;
    }
    return null;
}
```

However, this manual approach has several drawbacks:
- It requires identifying the right places for insertion.
- Determining the appropriate calls to use is not always clear.
- Such code can slow down production environments if left in inadvertently.
- It's a haphazard method that may not systematically uncover issues.


#### Automated

Automated tools such as Aspect-Oriented Frameworks, CGLIB, or ASM can be used to instrument code for concurrency testing. With the tools, the method could be designed to randomly induce sleeping, yielding, or doing nothing when executed, altering the thread execution order. By integrating such randomness, it's possible to expose flaws that might not surface under normal conditions. The overarching goal is to "jiggle" the execution of threads to uncover potential concurrency problems.

> Use jiggling strategies to ferret out errors.
{: .prompt-tip }


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
