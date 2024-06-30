---
title: Why do We Need Software Architecture?
date: 2024-06-30 19:19:00 UTC
categories: [ (CS) Learning Note, Architecture ]
tags: [ software engineering , architecture]
pin: false
---


Software architecture is a critical aspect of software engineering that defines the structure, components, and interactions of a system. 

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Software Architecture?](#what-is-software-architecture)
  * [Historical Background of Architectural Design](#historical-background-of-architectural-design)
    * [Early Days (Before 1960s)](#early-days-before-1960s)
    * [The First Software Crisis: Emergence of Structured Programming (1960s ~ 1970s)](#the-first-software-crisis-emergence-of-structured-programming-1960s--1970s)
    * [The Second Software Crisis: Emergence of OOP (1980s)](#the-second-software-crisis-emergence-of-oop-1980s)
    * [Popularity of Software Architecture (After 1990s)](#popularity-of-software-architecture-after-1990s)
  * [The Purpose of Architectural Design](#the-purpose-of-architectural-design)
    * [Misconceptions about Architecture Design](#misconceptions-about-architecture-design)
    * [The Real Purpose of Architecture Design](#the-real-purpose-of-architecture-design)
<!-- TOC -->

---

## What is Software Architecture?

Software architecture refers to the top-level structure of a software system, encompassing its components, their relationships, and the principles guiding its design and evolution. It acts as a blueprint for both the system and the project, laying out a framework to follow during the development process.

---

**Software architecture refers to the top-level structure of a software system:**

1. **The architecture needs to be clear about which parts the system contains.** 
   - A `system` is a group of related parts. These parts can be `subsystems`, `modules`, `components` etc. 
      - `Subsystems`: A subsystem is also a group of related parts. From a different perspective, one system may be a subsystem of another bigger system.
      - `Modules`: After splitting the system from a **logical point of view**, the resulting unit is a module.
      - `Components`: After splitting the system from a **physical point of view**, the resulting unit is a "component".
2. **The architecture needs to be clear about the rules (principles) for parts operations and collaboration.**
    - `Frameworks` and `Architectures` can both be used to define these rules (principles).
      - `Frameworks` focus on "specification". For example, _Spring MVC_ is a common framework that needs to meet the specifications of _MVC_. _Spring_ provides a lot of basic functionality to help us achieve these specifications, including annotations (_@Controller_, etc.), _Spring JPA_ and so on.
      - `Architectures` focus on "structure". For example, the _MVC architecture_ is describing a particular system structure.
3. **Architecture refers to the top-level structure of the system.** 
    - Avoid confusing system architecture with subsystem architecture, which leads to architectural hierarchy confusion.

## Historical Background of Architectural Design

The concept of software architecture has evolved over time as the complexity and scale of software systems have grown.

### Early Days (Before 1960s)

In the early days of computing, software was relatively simple, and the focus was primarily on algorithms and data structures. The term "software architecture" was not commonly used.

**Since software systems at this time are very simple, it doesn't cause much of problems for developers not to define the structure of the software.**

### The First Software Crisis: Emergence of Structured Programming (1960s ~ 1970s)

**As time goes by, software has exploded in the scale and complexity, leading to low quality, project delays, cost overruns, and other problems.** 

IBM's System/360 operating system development was a prime example of this crisis, with huge investment in the project but repeated delays. The project director, Fred Brooks, later summarised the experience of this project in _"The Mythical Man-Month"_, which became a classic book on software engineering.

![](https://i.postimg.cc/Pq6zNrHH/sa1.png){: .w-10 .shadow .rounded-10 }
_The Mythical Man-Month_

In response to the software crisis, the concept of **"software engineering"** was introduced at two NATO conferences in 1968 and 1969. But this concept was not a silver bullet; it only partially alleviated the crisis. At the same time, Edgar Dijkstra's 1968 paper "Go To Statement Considered Harmful" triggered the development of **Structured Programming**, which led to the birth of the Pascal language and its rapid popularity.

- **Structured programming emphasises "top-down, step-by-step refinement and modularity", which reduces the complexity of the software and becomes the development trend in the 1970s.**

### The Second Software Crisis: Emergence of OOP (1980s)

**In the 1980s, the second software crisis broke out with the development of hardware and the complexity of business requirements.** Although **Structured Programming** alleviated the first crisis to a certain extent, its shortcomings in software extensibility gradually emerged due to rapidly changing business requirements.

**The main problem of the second software crisis was the complexity of software extension. For this reason, Object-Oriented Programming (OOP) became popular.**

Until now, Object-Oriented is still the dominant development mindset. But Object-Oriented, like software engineering, is also not a silver bullet.

### Popularity of Software Architecture (After 1990s)

Although the concept of software architecture appeared as early as the 1960s, its real popularity began in the 1990s. **This happened not because of a new software crisis, but in response to the design problems of large-scale systems.**

Mary Shaw and David Garlan have done a lot of research on software architecture, as they wrote in a 1994 article, _"An Introduction to Software Architecture"_:

> “When systems are constructed from many components, the organization of the overall system (the software architecture) presents a new set of design problems.”

- **Software architecture solves the problems of heavy coupling, extension difficulties and complex logic in large-scale systems**:
  - Heavy internal coupling of the system, low development efficiency;
  - Heavy system coupling makes modification and expansion difficult;
  - The system logic is complex and prone to problems. It is difficult to identify and fix problems when they occur.

> - The first software crisis in the 1960s led to **Structured Programming**, creating the concept of **Modules**;
> - The second software crisis in the 1980s led to **Object-Oriented Programming**, creating the concept of **Objects**;
> - In the 1990s, **Software Architecture** became popular, creating the concept of **Components**.
{: .prompt-tip }

## The Purpose of Architectural Design

### Misconceptions about Architecture Design

- **For software development, is architecture design a necessity?**
  - **No.** Many of a company's initial products may have no architectural design. Initial products are generally small in scale, and developers may simply discuss it and start coding. This way the product development is faster, and it may run well after launch. **Being too obsessed with architecture design and making some unnecessary investments may lead to missed opportunities for the company.**
- **Does doing architecture design always improve development efficiency?**
  - **No. In fact, sometimes, the simplest designs are the most efficient to develop.** After all, architectural design requires an investment of time and manpower, and the project may be faster if this investment is used to code as early as possible.
- **Does a well-designed architecture always facilitate business growth?**
  - **No.** We should have a reasonable architecture design based on the actual business. Business growth dependent on the actual market. **Designing a large-scale system architecture with knowing that the business will not grow is only a waste of resources.**

> Architecture design is not a silver bullet either. It's used to solve problems, not a task you have to complete.
{: .prompt-tip }

So what is the real purpose of architecture design?

### The Real Purpose of Architecture Design

The main purpose of architecture design is to **solve the problems caused by the complexity of a software system.**
  - This conclusion, while simple, is a **guideline to always keep in mind** during the architectural design process.

> - **Architecture design is not about doing everything**, and it is not necessary for every architecture to be high-performance, high-availability, and high-scalability. **Rather, it's about identifying problems and then solving them responsively.**
> - **Architecture design should be based on reality.** "That's how Google is structured, and that's how we're going to do it too." This is wrong. **Without a corresponding commercial scale, large-scale design is just a burden.**
> - **Choose the most appropriate design, not the most popular one**.
{: .prompt-tip }

<br>

---

**Reference:**

- Li, Yunhua (2018) _Learn Architecture from 0_. Geek Time.
