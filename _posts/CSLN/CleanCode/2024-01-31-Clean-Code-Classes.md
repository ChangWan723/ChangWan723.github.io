---
title: "Clean Code: Classes"
date: 2024-01-31 18:16:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/class.jpg
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Class Organization](#class-organization)
  * [Classes Should Be Small!](#classes-should-be-small)
    * [Class Size](#class-size)
    * [The Single Responsibility Principle](#the-single-responsibility-principle)
    * [Cohesion](#cohesion)
  * [How to Deal With Change?](#how-to-deal-with-change)
    * [Organizing for Change](#organizing-for-change)
    * [Isolating from Change](#isolating-from-change)
<!-- TOC -->

---

## Class Organization

Classes should be organized for readability and ease of understanding. A well-organized class tells a clear story about the application, with a top-down narrative approach:

1. **Public Static Constants**: If any, should be at the top.
2. **Private Static Variables**: Followed by private static variables.
3. **Private Instance Variables**: Clustered together without sprawling through the class. (There is seldom a good reason to have a **public variable**)
4. **Public Functions**: Public functions come next. Each public function should be followed by the private functions it calls.

This organization ensures that the class's most important aspects, its public interface, are presented upfront and are not buried within the class's implementation details.

## Classes Should Be Small!

> The first rule of classes is that they should be small. The second rule of classes is that they should be smaller than that.

### Class Size

- "Smaller is better" when it comes to classes. **The more focused a class is, the easier it is to understand and maintain.** 
- Classes should be small not just in terms of **lines of code** but more importantly, in terms of **responsibilities**. 

>  In fact, **naming** is probably the first way of helping determine class size. **If we cannot derive a concise name for a class, then it’s likely too large.** The more ambiguous the class name, the more likely it has too many responsibilities.

### The Single Responsibility Principle

- The [Single Responsibility Principle (SRP)](/posts/SRP/) asserts that a class should have one, and only one, reason to change.

> At the same time, many developers fear that a large number of small, single-purpose classes makes it more difficult to understand the bigger picture. They are concerned that they must navigate from class to class in order to figure out how a larger piece of work gets accomplished.
> 
> However, a system with many small classes has no more moving parts than a system with a few large classes. There is just as much to learn in the system with a few large classes. So the question is: **Do you want your tools organized into toolboxes with many small drawers each containing well-defined and well-labeled components? Or do you want a few drawers that you just toss everything into?**

### Cohesion

Cohesion refers to how closely related and focused the responsibilities of a class are. High cohesion within a class means that the class's methods and variables are cohesively grouped around a central purpose. As classes grow, they tend to accumulate more variables and methods, leading to decreased cohesion. **To maintain high cohesion, classes should be split whenever they start taking on multiple responsibilities.**

> **When classes lose cohesion, split them!**


## How to Deal With Change?

Classes should be designed with the understanding that **software is inherently evolutionary**. Clean classes are those that can adapt to new requirements and changes in the domain without significant rewrites or refactoring.

### Organizing for Change

Classes should be open for extension but closed for modification ([Open-Closed Principle](/posts/OCP/)). **A well-designed class anticipates the likelihood of change and is structured in a way that allows for these changes without the need for modification of the class's code.**

### Isolating from Change

A clean class should minimize the impact of change by reducing how much a change in one class forces changes in other classes. This can be achieved through the use of interfaces and abstract classes, allowing classes to communicate and collaborate **without being tightly coupled to each other's specific implementations** ([Dependency Inversion Principle](/posts/DIP/)).


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
