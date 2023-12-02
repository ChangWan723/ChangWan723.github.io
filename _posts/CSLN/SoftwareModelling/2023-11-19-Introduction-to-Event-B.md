---
title: Introduction to  Event-B
date: 2023-11-19 18:45:00 +0530
categories: [(CS) Learning Note, Software Modelling and Design]
tags: [computer science, Event-B, Set Theory]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Event-B?](#what-is-event-b)
  * [Basic Set Theory](#basic-set-theory)
    * [Set and Elements](#set-and-elements)
    * [Enumeration and Cardinality of Finite Sets](#enumeration-and-cardinality-of-finite-sets)
    * [Subset and Equality Relations for Sets](#subset-and-equality-relations-for-sets)
    * [Operations on sets](#operations-on-sets)
  * [What is contained in Event-B](#what-is-contained-in-event-b)
    * [Types](#types)
    * [Powersets](#powersets)
    * [Predicate Logic](#predicate-logic)
    * [Defining Set Operators with Logic](#defining-set-operators-with-logic)
  * [Examples of Event-B](#examples-of-event-b)
    * [Simple Event-B model: Counter](#simple-event-b-model-counter)
      * [Definition](#definition)
      * [Increasing and decreasing the Counter](#increasing-and-decreasing-the-counter)
    * [Simple Example: Dictionary](#simple-example-dictionary)
      * [Definition](#definition-1)
      * [Increasing and decreasing the Counter](#increasing-and-decreasing-the-counter-1)
      * [Checking if a word is in a dictionary: 2 cases](#checking-if-a-word-is-in-a-dictionary-2-cases)
    * [Example Requirements for a Building Control System](#example-requirements-for-a-building-control-system)
      * [Definition](#definition-2)
      * [Entering and Leaving the Building](#entering-and-leaving-the-building)
      * [Adding New Users](#adding-new-users)
<!-- TOC -->

---

## What is Event-B?

- System specifications are derived from **requirements**.
- System specification is an important **precursor** to design, implementation and testing.
- Event-B is a **formal language** for writing **high-level specifications** of computer systems.
- Event-B language includes **logic** and **set theory**.
- Formal specification is **more precise** and **consistent** than an informal (natural language) specification.
- Event-B typically used in **safety-critical** applications.

## Basic Set Theory

### Set and Elements

- A **set** is a collection of **elements**.
- Elements of a set are **not ordered**.
- Elements of a set may be numbers, names, identifiers, etc.
- Sets may be **finite** or **infinite**.
- Relationship between an element and a set: the element is a **member** of the set.

For **element** `x` and **set** `S`, we express the membership relation as follows: `x ∈ S`

### Enumeration and Cardinality of Finite Sets

- Finite sets can be expressed by **enumerating** the elements within braces.
  - for example: `{ 3, 5, 8 }`, `{ a, b, c, d }`
- The cardinality of a finite set is the number of elements in that set:
  - For example: `card( { 3, 5, 8 } ) = 3`, `card( { a, b, c, d } ) = 4`, `card( {} ) = 0`

### Subset and Equality Relations for Sets

- A set `S` is said to be **subset** of set `T` when every element of `S` is also an element of `T`. This is written as follows: `S ⊆ T`
  - `{ 5, 8 } ⊆ { 4, 5, 6, 7, 8 }`
- A set `S` is said to be equal to set `T` when `S ⊆ T` and `T ⊆ S`(no matter if they have the same number of elements): `S = T`
  - `{ 5, 8, 3 } = { 3, 5, 5, 8 }`

### Operations on sets

- **Union** of `S` and `T`: set of elements **in either** `S` or `T`. `S ∪ T`
- **Intersection** of `S` and `T`: set of elements **in both** `S` and `T`. `S ∩ T `
- **Difference** of `S` and `T`: set of elements **in** `S` **but not in** `T`. `S \ T`

**Example:**
`{a, b, c} ∪ {b, d} = {a, b, c, d}`

`{a, b, c} ∩ {b, d} = {b}`

`{a, b, c} \ {b, d} = {a, c}`

`{a, b, c} ∩ {d, e, f } = {}`

`{a, b, c} \ {d, e, f } = {a, b, c}`

## What is contained in Event-B

- Event-B **context** contains:
  - **Sets**: abstract types used in specification
  - **Constants**: logical variables whose value remain constant
  - **Axioms**: constraints on the constants. An axiom is a logical predicate.

- Event-B **machine** contains:
  - **Variables**: state variables whose values can change
  - **Invariants**: constraints on the variables that should always hold true. An invariant is a logical predicate.
  - **Initialisation**: initial values for the abstract variables
  - **Events**: guarded actions specifying ways in which the variables can change. Events may have parameters.

### Types

- All variables and expressions in B must have a type.
  - Types are represented by sets.
- Let `T` be a set and `x` a constant or variable.
  - `x ∈ T` specifies that **`x` is of type `T`**.
- All the elements of a set must have the same type.

---

![](https://i.postimg.cc/4xphGtTV/eb13.png){: .w-50 .shadow .rounded-10 }

- Basic types are introduced to represent the entities of the problem being modelled.

- Types help to structure specifications by differentiating objects.
- Types help to prevent errors by not allowing us to write meaningless things.
- Types can be checked by computer.

### Powersets

The **powerset** of a set `S` is the set whose elements are all subsets of `S`.

![](https://i.postimg.cc/wx57vNfk/eb14.png){: .w-80 .shadow .rounded-10 }

![](https://i.postimg.cc/9QH4FpV1/eb15.png){: .w-80 .shadow .rounded-10 }

### Predicate Logic

![](https://i.postimg.cc/X7YZZJyB/eb16.png){: .w-80 .shadow .rounded-10 }

### Defining Set Operators with Logic

![](https://i.postimg.cc/ryx6SCxv/eb17.png){: .w-80 .shadow .rounded-10 }

## Examples of Event-B

### Simple Event-B model: Counter

#### Definition

![](https://i.postimg.cc/mDYG9wNw/eb1.png){: .w-80 .shadow .rounded-10 }

- Invariants define valid system states.

#### Increasing and decreasing the Counter

![](https://i.postimg.cc/26trr6Gp/eb5.png){: .w-80 .shadow .rounded-10 }

- Events define **changes** to the system state.
- Events have **guards** and **actions**.
- Guards must be true for the actions to be executed.


### Simple Example: Dictionary

#### Definition

![](https://i.postimg.cc/s1dzGNbw/eb6.png){: .w-80 .shadow .rounded-10 }


#### Increasing and decreasing the Counter

![](https://i.postimg.cc/T1WGw6NK/eb7.png){: .w-80 .shadow .rounded-10 }

This event has a **parameter** `w` representing the word that is added to the set of known words.

#### Checking if a word is in a dictionary: 2 cases

![](https://i.postimg.cc/0jKRxK9T/eb8.png){: .w-80 .shadow .rounded-10 }

- Cases are represented by **separate events**.
- In both cases, `r!` represents a **result parameter**.
- We use the `!` convention to represent **result parameters**.

![](https://i.postimg.cc/JzXBdpZ8/eb9.png){: .w-80 .shadow .rounded-10 }

In both cases, **result** represents a `the output parameter`.

### Example Requirements for a Building Control System

- Specify a system that monitors users entering and leaving a building.
- A person can only enter the building if they are recognised by the monitor.
- The system should be aware of whether a recognised user is currently inside or outside the building.

#### Definition

![](https://i.postimg.cc/yxQvvstv/eb10.png){: .w-80 .shadow .rounded-10 }

#### Entering and Leaving the Building

![](https://i.postimg.cc/8CLNFP08/eb11.png){: .w-80 .shadow .rounded-10 }

#### Adding New Users

![](https://i.postimg.cc/Wpmcc1dC/eb12.png){: .w-50 .shadow .rounded-10 }

- New users cannot be registered yet.
- Newly registered users must be added either to in or out to preserve inv5.

