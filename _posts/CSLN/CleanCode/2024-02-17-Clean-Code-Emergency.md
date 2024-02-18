---
title: "Clean Code: Emergency"
date: 2024-02-17 23:00:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/emergency.jpg
---

**Emergent design** offers a practical approach to achieving clean code, focusing on simplicity, clarity, and maintainability. By adhering to the four simple rules, developers can navigate the complexities of software development with confidence, ensuring that their code remains clean, efficient, and adaptable to change.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Embracing Simplicity in Software Design: A Guide to Emergent Design](#embracing-simplicity-in-software-design-a-guide-to-emergent-design)
  * [The Four Rules of Simple Design](#the-four-rules-of-simple-design)
    * [Simple Design Rule 1: Runs All the Tests](#simple-design-rule-1-runs-all-the-tests)
    * [Simple Design Rule 2-4: Refactoring](#simple-design-rule-2-4-refactoring)
      * [Rule 2: No Duplication](#rule-2-no-duplication)
      * [Rule 3: Expresses Intent Clearly](#rule-3-expresses-intent-clearly)
      * [Rule 4: Minimizes Classes and Methods](#rule-4-minimizes-classes-and-methods)
<!-- TOC -->

---

## Embracing Simplicity in Software Design: A Guide to Emergent Design

**Emergent Design** is a principle that emphasizes **the evolution of software design during the development process** rather than trying to foresee and fix the entire design upfront.

Emergent Design supports the concept that **the best designs emerge from a process of continuous refinement and adaptation**, where the focus is on meeting current requirements in the simplest way possible while keeping the codebase clean and ready for future changes.


## The Four Rules of Simple Design

A design is “simple” if it follows these rules, and **these four rules facilitate the emergence of good design**. The rules are given in order of importance:
   1. **Runs all the tests** 
   2. **Contains no duplication**
   3. **Expresses the intent of the programmer**
   4. **Minimizes the number of classes and methods**

### Simple Design Rule 1: Runs All the Tests

The primary goal of any software system is to function as intended. This rule places the utmost importance on having a comprehensive suite of tests that the system must pass consistently. It's a straightforward concept: if the system isn't testable, its reliability is in question. **A well-tested system naturally leads towards a design that is easier to understand and maintain.**

> Writing tests leads to better designs.
{: .prompt-tip }

Langr highlights an interesting cycle: **the more we focus on making our system testable, the better our design becomes.** Writing tests leads to smaller, more focused classes that adhere to the Single Responsibility Principle (SRP). It also encourages the use of design principles and tools that reduce coupling, enhancing the design's quality.

### Simple Design Rule 2-4: Refactoring

With a comprehensive test suite in place, developers are empowered to refactor confidently. **Refactoring becomes an integral part of the development process, allowing the design to evolve and improve continuously.** This is where the principles of clean code truly come into play, guiding developers towards better names, improved cohesion, reduced coupling, and a more modular structure.

This is also where we **apply the final three rules of simple design**: Eliminate duplication, ensure expressiveness, and minimize the number of classes and methods.

#### Rule 2: No Duplication

**Duplication is the root of all evil in software development**. Avoiding redundant code is crucial for maintaining a clean codebase. It ensures that changes need to be made in only one place, reducing the risk of inconsistencies and bugs.

#### Rule 3: Expresses Intent Clearly

**Code should be self-explanatory.** The intent behind each segment of code should be clear to anyone who reads it, making the software easier to understand and modify. This rule emphasizes the importance of good naming conventions, clear structure, and the use of patterns that convey the programmer's intentions effectively.

- In order to clearly express the intention, we can try the following methods:
  - **Choosing good names.** 
  - **Using standard nomenclature.** 
  - **Keeping your functions and classes small.**
  - **Well-written unit tests.** A primary goal of tests is to act as documentation by example.

#### Rule 4: Minimizes Classes and Methods

In order to keep our functions and classes small, we may create too many small classes and methods. Therefore, this rule suggests that **we also minimise the number of functions and classes**.

> **High class and method counts are sometimes the result of pointless dogmatism.** For example, some coding standards insist on creating an interface for each class. But we can't follow these standards mindlessly in real programming. We should resist this dogmatism and adopt a more pragmatic approach.
{: .prompt-tip }

But remember, this rule is the lowest priority of the four rules of Simple Design. **The precondition for following this rule is that it does not break the other three rules.**

Simplicity is key. The design should be as simple as possible, with no unnecessary classes or methods. This doesn't mean the design should be minimalistic at the cost of functionality but rather that every component should have a clear, justified purpose.

<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
