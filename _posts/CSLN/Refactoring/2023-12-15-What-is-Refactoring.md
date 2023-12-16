---
title: What is Refactoring?
date: 2023-12-15 23:45:00 UTC
categories: [(CS) Learning Note, Refactoring]
tags: [software engineering, Refactoring, code]
pin: false
---

Refactoring isn't just about cleaning up code; it's a vital process for maintaining the health, efficiency, and sustainability of a software system. 

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Refactoring?](#what-is-refactoring)
    * [Big Refactoring and Small Refactoring](#big-refactoring-and-small-refactoring)
    * [Key Elements of Refactoring](#key-elements-of-refactoring)
  * [Why Refactor?](#why-refactor)
  * [When Refactor?](#when-refactor)
  * [How Refactor?](#how-refactor)
<!-- TOC -->

---

## What is Refactoring?

> Refactoring is the process of changing a software system in such a way that it does not alter the
external behavior of the code yet improves its internal structure.

Refactoring is the process of **restructuring existing code without changing its external behaviour.** It's about improving the internal structure of software to make it easier to understand, cheaper to modify, and more reliable.

**Refactoring code is generally much harder than just writing code.** Refactoring requires you to be able to see the **Bad Smells** that exist in the code, and to be able to use theoretical knowledge of **design ideas, principles, patterns, programming specifications**, etc., to solve these problems in a rational and skillful way.

### Big Refactoring and Small Refactoring

- **Small Refactoring**
    - **Definition**: Small refactoring involves making minor, incremental changes to the codebase. These changes are usually simple and localized, affecting a small part of the code, such as a single function or class.
    - **Characteristics**:
        - Quick to implement and less risky.
        - Does not require extensive planning or restructuring.
        - Examples include renaming variables for clarity, simplifying complex conditional statements, or breaking down large methods into smaller, more manageable ones.
        - Can be done continuously and often forms part of regular development activities.
        - Helps in maintaining the readability and maintainability of the code without altering its functionality.
    - **Examples**:
        - Renaming variables or methods for clarity.
        - Simplifying complex conditional statements
        - Breaking down large methods into smaller
        - Remove duplicate code
      
- **Big Refactoring**
    - **Definition**: Big refactoring, in contrast, involves significant changes to the codebase. It’s a more comprehensive approach that may involve altering the software's architecture, design patterns, or overall structure.
    - **Characteristics**:
        - Requires careful planning and consideration, as it can have a broader impact on the system.
        - Often carried out in response to accumulated technical debt, or when preparing the codebase for new features or scalability.
        - Carries higher risk and often requires thorough testing to ensure that functionality is not broken.
        - Typically done less frequently than small refactoring, often as part of a dedicated project or development phase.
    - **Examples**: 
        - Redesigning a software module.
        - Integrating a new architecture pattern.
        - Transitioning to a different technology stack.

### Key Elements of Refactoring

1. **Improving Code Structure**: Refactoring aims at simplifying the design of the code, making it more readable and less complex.
2. **No Functional Changes**: The functionality of the code remains unchanged; refactoring doesn't fix bugs or add new features.
3. **Continuous Process**: It's a regular maintenance activity, not a one-time event.

## Why Refactor?

1. **refactoring code is inevitable**
    - Good code or architecture is not completely designed from the beginning, just as good products are iterated. Most real projects always have some features that need to be changed. **Code and architecture always need to be changed as the project evolves, so refactoring code is inevitable.**

2. **Refactoring prevents code from rotting beyond repair.** 
   - The project is evolving and the code is constantly piling up. **If no one is responsible for the quality of the code, the code will always evolve in the direction of worse and worse.** After a certain amount of chaos, quantitative change leads to qualitative change, and the maintenance cost of the project is already higher than the cost of redeveloping a new set of code, and no one can refactor it again.

3. **Refactoring is an effective way to avoid over-design.** 
    - We cannot predict all future requirements and changes. In the process of maintaining the code, **we can refactor the code when we really encounter problems, which can effectively avoid investing too much time in over-design** in the early stage.

4. **Refactoring can reduce Technical Debt**
   - Technical debt happens when you take shortcuts in writing your code so that you achieve your goal faster, but at the cost of uglier, harder to maintain code. It's called technical debt because it's like taking out a loan. **Sometimes we have to go into technical debt because of delivery pressures or deadlines. We can use refactoring to reduce these technical debts at the right time later.** 

5. **Optimising Performance**
   - **Sometimes, refactoring can lead to more efficient code**, although performance optimisation isn’t its primary goal.

> **Refactoring ability is also an essential measure of an engineer's code ability**. 
> 
> The so-called "**junior engineers maintain the code, senior engineers design the code, expert engineers refactor the code**", this sentence means that: 
>   - Junior engineers fix bugs, modify and add functional code in the existing code framework.
>   - Senior engineers design code structure and build the code framework from scratch. 
>   - Expert engineers are responsible for the code quality, and need to find the problems existing in the code, refactor the code, and **always ensure that the code quality is in a controllable state**.
>
> (Of course, the junior, senior and expert here are only a relative concept, not a definite rank).
{: .prompt-tip }


## When Refactor?

Do we refactor when the code is so bad that it's unbearable? **Of course not.** The worse the code, the more difficult it is to reduce technical debt. So it's unrealistic to hope that intensive refactoring will solve all the problems after the code sucks beyond tolerance. We have to explore a **sustainable approach**.

So the strategy we should adopt is **Continuous Refactoring**:
  - When you don't have anything to do, you can take a look at the code in your project that is not well written and can be optimised, and **refactor it proactively**. 
  - We need to make `Continuous Refactoring` a development habit, just like `Unit Testing` and `Code Review` as part of development, which will be beneficial to the project and to ourselves.

> - **As a developer, the Continuous Refactoring awareness is more important than the refactoring ability**.
>     - As technology is updating, requirements are changing, and people are moving around, the quality of the code will always be decreasing, and **the code will never be perfect, so refactoring needs to be done continuously**. You need to be aware of continuous refactoring to avoid code rot.
> - **As a company, it is important to develop a good culture of Continuous Refactoring** and have a good view of code quality.
>     - It's more important for a company to encourage employees to refactor rotten code than to chastise them for writing bad code. Leadership must understand and support the importance of refactoring. They should allocate time and resources for refactoring tasks and refactoring knowledge sharing.
{: .prompt-tip }


## How Refactor?

Refactoring involves a series of small, controlled steps:

1. **Identify Code Smells**: These are indicators of problems in the code, like duplications, large classes, or long methods.
2. **Choose the Right Refactoring Techniques**: Apply specific refactoring techniques like extracting methods, simplifying conditional expressions, or renaming variables.
3. **Ensure Behavior Preservation**: Use tests to ensure that the refactored code still behaves as expected.
4. **Repeat**: Refactoring is an iterative process. It’s done in small steps, and each step is tested.

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Design Patterns_. Geek Time.
