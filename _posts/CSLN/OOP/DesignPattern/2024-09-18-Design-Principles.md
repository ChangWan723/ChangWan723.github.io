---
title: Why I Think Design Principles Are More Important Than Design Patterns?
date: 2024-09-18 15:36:00 UTC
categories: [(CS) Learning Note, OOP]
tags: [software engineering, OOP, Design Patterns, Design Principles, SOLID]
pin: false
image:
  path: /assets/img/posts/principles.jpg
---

Currently, there are 23 mainstream design patterns, but:
* some patterns are out of fashion today;
* some patterns have been replaced by frameworks;
* some patterns are even anti-patterns;
* some patterns you may often forget.

These patterns are complex and nerdy, and you may often suffer from mastering them. But that doesn't matter, because **Design Principles Are More Important Than Design Patterns.** Once you have mastered the design principles, you can easily understand the design patterns from various domains, and you may even invent your own design patterns.

> **Don't learn design patterns like algorithms & data structures.** Algorithms & data structures are the foundation for understanding many complex problems, but design patterns are not (design principles are).
> 
> **Without design principles, mastering design patterns is just mastering some nerdy and foolish solutions.** 
{: .prompt-warning }

> **Design principles are the soul of design patterns, and design patterns are derived from design principles.** If a design pattern is applied in a way that violates the design principles, then the design pattern is wrong.
{: .prompt-tip }

---

<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Design Principles & Design Patterns](#design-principles--design-patterns)
    * [What Are Design Principles?](#what-are-design-principles)
    * [What Are Design Patterns?](#what-are-design-patterns)
  * [Why Design Principles Are More Important Than Design Patterns](#why-design-principles-are-more-important-than-design-patterns)
    * [Principles Provide the Foundation for Good Design](#principles-provide-the-foundation-for-good-design)
    * [Using Design Patterns Blindly Can Violate Principles](#using-design-patterns-blindly-can-violate-principles)
    * [Principles Encourage Problem Solving from First Principles](#principles-encourage-problem-solving-from-first-principles)
    * [Principles Are Timeless, Patterns Can Evolve.](#principles-are-timeless-patterns-can-evolve)
    * [Principles Apply to Every Layer of Software](#principles-apply-to-every-layer-of-software)
    * [Principles Help Avoid Over-Engineering](#principles-help-avoid-over-engineering)
<!-- TOC -->

---

## Design Principles & Design Patterns

### What Are Design Principles?

Design principles are **foundational guidelines** that help developers create systems that are maintainable, flexible, and extensible. These principles focus on the structure and behavior of code at a **high level**, emphasizing good practices over specific implementations. These principles are conceptual guidelines that can be applied to any problem and any language, making them **universally** applicable across software projects.

---

**The 7 most important design principles:**

- **SOLID Principles**:
  - **S**ingle Responsibility Principle ([SRP](/posts/SRP/))
  - **O**pen/Closed Principle ([OCP](/posts/OCP/))
  - **L**iskov Substitution Principle ([LSP](/posts/LSP/))
  - **I**nterface Segregation Principle ([ISP](/posts/ISP/))
  - **D**ependency Inversion Principle ([DIP](/posts/DIP/))
- **Law of Demeter**: Objects should only talk to their direct friends, not strangers. (Only expose information that needs to be exposed.)
- **Composition/Aggregate Reuse Principle**: Prefer using composition (building objects by combining other objects) over inheritance (extending a class from another)

---

Other design principles:

- **DRY (Don't Repeat Yourself)**: Avoid duplication in code.
- **KISS (Keep It Simple, Stupid)**: Keep code simple and understandable.
- **YAGNI (You Aren't Gonna Need It)**: Only implement what you currently need.
- ...

### What Are Design Patterns?

Design patterns, on the other hand, are **concrete solutions** to specific problems that developers commonly encounter in software design. They provide a **standardized approach** to solving particular issues, such as object creation, structure, or behavior. **While design patterns are more straightforward and easy to understand, they often only work well after you have a solid foundation of design principles.**

Some popular design patterns include:

- **Creational Patterns**: Singleton, Factory, Builder
- **Structural Patterns**: Adapter, Decorator, Proxy
- **Behavioral Patterns**: Observer, Strategy, Command

## Why Design Principles Are More Important Than Design Patterns

### Principles Provide the Foundation for Good Design

**Design principles are the soul of good design, providing the foundation for writing clean, maintainable, and flexible code.** Without SOLID principles, even well-known design patterns can lead to rigid, overly complex systems.

For example, understanding the **Dependency Inversion Principle** can help you identify overly coupled designs, and design code that depends on abstraction. This principle can be applied in various scenarios, regardless of the design pattern you're using. On the other hand, design patterns are more concrete and can only be applied in specific situations. And they are even often overused.

### Using Design Patterns Blindly Can Violate Principles

**Design patterns, while useful, tend to offer a fixed structure for solving a particular problem.** If you rely too heavily on patterns without first understanding the design principles, you may design code that violates a large number of principles.

For example, the **Singleton Pattern** provides a straightforward solution for managing a single instance of a class, but if not applied correctly, it can lead to inflexible and tightly coupled code that violates core design principles.

### Principles Encourage Problem Solving from First Principles

**Design principles encourage developers to think critically about the problems they're trying to solve, rather than just applying a pre-existing solution.** This mindset fosters creativity and innovation, as developers are more likely to come up with solutions tailored to their unique challenges. Design patterns, on the other hand, may sometimes encourage developers to shoehorn a specific pattern into their project, even if it's not the best fit. 

For example, a developer might use the **Builder Pattern** to cover up the problem of a class with too many constructor parameters. Instead of thinking about whether the class has a **single responsibility** and whether the parameters are well designed.

### Principles Are Timeless, Patterns Can Evolve.

Design principles are universal and stand the test of time. They remain applicable no matter how technology or programming languages evolve. On the other hand, design patterns can change or become obsolete as new technologies emerge. 

For example, the **Singleton Pattern**, which was once widely used, is now often considered problematic in many scenarios due to the introduction of dependency injection and test-driven development.

### Principles Apply to Every Layer of Software

Design principles are not limited to object-oriented programming or specific layers of an application. They can be applied to software architecture, database design, API design, and more. Design patterns, on the other hand, are usually focused on solving problems at the object-oriented design level. They are valuable for dealing with class interactions, object creation, and communication between components, but they don't always address higher-level concerns in software architecture.


For example, **Single Responsibility Principles** and **Interface Segregation Principle** can guide you when designing anything from individual classes to high-level system components.

### Principles Help Avoid Over-Engineering

**Over-engineering is a common pitfall in software development, where developers introduce unnecessary complexity into the code.** Focusing on design principles helps developers maintain simplicity and avoid adding layers of abstraction or patterns that aren’t required by the problem at hand.

For example, the **Visitor Pattern**, born for the defect, is often overused and introduces unnecessary complexity.

