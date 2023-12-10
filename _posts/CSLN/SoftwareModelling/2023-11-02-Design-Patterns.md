---
title: Design Patterns
date: 2023-11-02 16:14:00 UTC
categories: [(CS) Learning Note, Software Modelling and Design]
tags: [software engineering, Design Patterns, OOP]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is the Design Patterns?](#what-is-the-design-patterns)
  * [What is a Pattern?](#what-is-a-pattern)
  * [Different Types of Patterns](#different-types-of-patterns)
    * [Creational patterns](#creational-patterns)
    * [Structural Patterns](#structural-patterns)
    * [Behavioural Patterns](#behavioural-patterns)
  * [Good design principles](#good-design-principles)
  * [Good use of Design Pattern Principles](#good-use-of-design-pattern-principles)
<!-- TOC -->

---

## What is the Design Patterns?

- Describes a problem which frequently occurs in our environment, and then describes the core of the solution to the problem
- Software development is **repetitive**: Quite often, different programmers have to solve the **similar** problems.
- Experienced programmers have compared notes and discovered that they arrived at **common solutions** to the same problems
- Over time, these common solutions have been **systematically documented** as the best known approach to solving a given problem

- A good pattern should
  - Be as general as possible
  - Contain a solution that has been proven to effectively solve the problem in the indicated context.

- In order to benefit you must know:
  - The problem you are facing
  - Know design patterns themselves
  - Key is to **understand** the relationship between classes and how to **allocate responsibilities** to them

- There are currently over 100 documented design patterns. The classic book, “Design Patterns: Elements of Reusable Object-Oriented Software” was written by Gamma, Helm, Johnson, and Vlissides (called the Gang of four) covers 23 patterns which have been chosen.

## What is a Pattern?

There are 4 essential elements of a design pattern:

- **Pattern name**
- **Problem description**
  - This describes when the pattern can be applied: to what kind of problem, and what pre-conditions need to be met
- **Solution description**
  - An abstract description of the solution in terms of a set of classes with particular functionalities and interrelationships
- **Consequences**
  - presenting the results and tradeoffs of using the pattern, helping you decide the best choice from among several promising alternatives.

## Different Types of Patterns

### Creational patterns

- The process of object **construction** and the instantiation process
  - Example: the **Singleton** pattern is for a class that has only one instance
  - Example: the **Abstract Factory** pattern provides an interface for creating families of related or dependent objects without specifying their concrete class.
  - Example: the **Factory Method** pattern defines an interface for creating an object of some class but defers instantiation to subclasses

### Structural Patterns

- **Composition** of classes/objects: how classes and objects are composed to form larger structures
  - Example: the **Adapter** pattern converts the interface of a class into another interface clients expect.
  - Example: the **Composite** pattern composes objects into tree-structures to represent part/whole relationships and lets clients treat individuals and groups uniformly.
  - Example: the **Decorator** pattern attaches additional responsibility to an object dynamically -- more flexibly than sub-classing.

### Behavioural Patterns

- The way classes and objects interact/patterns of **communication** between classes
  - Example: the **Iterator** pattern provides an interface for accessing elements of an aggregate, such as a vector or a list, without exposing the aggregates interface or internal structure.
  - Example: the **Observer** pattern defines a 1 to many dependency between objects so that when one changes state, all dependents are notified and updated.

![](https://i.postimg.cc/sx4690QT/dp1.png){: .w-100 .shadow .rounded-10 }


## Good design principles

- Program to **interfaces** not to an implementation
- **Separate what changes** from what does not
- **Loose couple** objects that interact
- Classes should be **open for extension**, but **closed for modification**
- Each class should have **one responsibility**
- Depend on **abstractions**, **not concrete** classes

## Good use of Design Pattern Principles

- Let design patterns emerge from your design, don’t use them just because you should
- Always choose the simplest solution that meets your need
- Always use the pattern if it simplifies the solution
- Know a good list of the design patterns out there
