---
title: Introduction to Formal Methods & Event-B
date: 2023-11-19 10:49:00 +0530
categories: [(CS) Learning Note, Software Modelling and Design]
tags: [computer science, software engineering, Event-B]
pin: false
---

> In computer science, **formal methods** are mathematically rigorous techniques for the specification, development, analysis, and verification of software and hardware systems. The use of formal methods for software and hardware design is motivated by the expectation that, as in other engineering disciplines, performing appropriate mathematical analysis can contribute to the reliability and robustness of a design.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Why Do We Need Formal Methods & Event-B?](#why-do-we-need-formal-methods--event-b)
    * [The Limitation of V Model in Software Development](#the-limitation-of-v-model-in-software-development)
    * [Software Defects](#software-defects)
    * [Software Artefact Issues](#software-artefact-issues)
    * [Need for Precision and Abstraction](#need-for-precision-and-abstraction)
    * [Testing vs Proving](#testing-vs-proving)
  * [What are Formal Methods?](#what-are-formal-methods)
  * [Introduction to Event-B](#introduction-to-event-b)
    * [Event-B in Software Development](#event-b-in-software-development)
    * [Events In Event-B Formalism](#events-in-event-b-formalism)
  * [A Simple Event-B Example: CoffeeClub](#a-simple-event-b-example-coffeeclub)
    * [Modelling REQ1](#modelling-req1)
      * [Events](#events)
      * [Initialisation Event](#initialisation-event)
    * [Modelling REQ2](#modelling-req2)
    * [Modelling REQ3](#modelling-req3)
  * [Operational Interpretation of Event-B](#operational-interpretation-of-event-b)
<!-- TOC -->

---

## Why Do We Need Formal Methods & Event-B?

### The Limitation of V Model in Software Development

In V model, many specification errors are detected only after a lot of development has been undertaken:

![](https://i.postimg.cc/GtSWrhYT/fm1.png){: .w-80 .shadow .rounded-10 }

So, defects discovered too late:

- Requirements and architecture defects make up approximately 70% of all system defects.
- 80% of these defects are discovered late in the development life cycle

### Software Defects

- Software Faults Are Due to:
  - **Requirements defects**: incomplete, ambiguous requirements or failure to specify the environment in which the software will be used.
  - **Design defects**: not satisfying the requirements, incomplete design or documentation defects
  - **Code defects**: Failure of code to conform to software designs. 

### Software Artefact Issues

- Use of natural languages in Requirement Engineering
  - Natural language Ambiguity
  - Inconsistencies
- Software is more error sensitive
  - Conventional engineering is tolerant
- Too much complexity
  - Complexity of requirements
  - Complexity of operating environment
  - Complexity of design
- Harder to test
  - Complete test is impossible
  - Has correlated failures

### Need for Precision and Abstraction

- Precision through early-stage models
  - Amenable to analysis by tools
  - Identify and fixing ambiguities and inconsistencies as early as possible
- Mastering complexity through abstraction
  - Focus on what a system does (its purpose) at early stages of modelling
  - Incremental analysis and design: answering the question of how later on

![](https://i.postimg.cc/wvdycLWF/fm2.png){: .w-80 .shadow .rounded-10 }


### Testing vs Proving

- The purpose of software **testing** is to **identify the errors**, faults, or missing requirements in contrast to actual requirements.
  - Testing provides evidence of software faults (**negative evidence**)
- What happens if we can ascertain or establish the correctness or validity of solutions; to verify; to prove certain aspects or properties of software
  - If you **prove** that something is true or correct, you provide evidence showing that it is definitely true or correct.
  - Proof provides **positive evidence** of software correctness
- Which one is better, testing or proof?
  - **We need both** 


## What are Formal Methods?

- Formal methods refer to mathematically based techniques for the specification, development and verification of software and hardware systems.
- What kind of mathematics?
  - Discrete mathematics, set theory, logic
- **Advantages** of formal methods
  - Encourages us to **think before coding**
  - Do some **reasoning**
  - Help us to remove **ambiguities**
  - Enforce the **consistency** of the specification and modelling 

## Introduction to Event-B

### Event-B in Software Development

- Event-B: A **formal language** for writing **high-level specifications** of computer systems
  - System specifications are **derived from requirements** (**abstraction**)
  - System specification can be gradually **turned into design** (**refinement**)

- Event-B language includes first order logic and set theory
  - Formal specification is **more precise** and **consistent** than an informal (natural language) specification. 
- Event-B typically used in safety-critical or mission-critical applications.

### Events In Event-B Formalism

- A System **model** is represented by a **construct** called “**Machine**”
- A Machine is made of a number of **Events** representing the **behaviour** of the system
- An **Event** is made of **guards** and **actions**
- The **Guards** denote the **enabling condition** of the event
- The **Actions** denote the way the **state is modified** by the event
- **Guards** and **actions** are written using **set-theoretic expressions**
- The **state** of the model is represented using **variables**

## A Simple Event-B Example: CoffeeClub

- For a coffee club, we require a Moneybank that stores money used by the coffee club.
- A Few requirements of the Moneybank:
  - REQ1: We need a money bank for storing and reclaiming finite, non-negative funds for a coffee club.
  - REQ2: We need an operation for adding money to the money bank.
  - REQ3: We need an operation for removing money from the money bank; but it cannot remove more money than the money bank contains.

### Modelling REQ1

REQ1: We need a money bank for storing and reclaiming finite, non-negative funds for a coffee club.
![](https://i.postimg.cc/Jhv2bG74/fm3.png){: .w-80 .shadow .rounded-10 }

- The invariants specify the properties that the variables (the state) must satisfy before and after every event. 

#### Events

- Events model possible **behaviour** of the system presented in a **machine**
- Events include:
  - the **conditions** under which the behaviour can occur (guards)
  - and **how** the state of the machine is **changed** (actions)
- The machine always should **start** from a **known state**
- Thus, we need an **Initialisation** event, a special **unconditional** event
  - occurs in a machine **once only**
  - **before** any other event
  - initialises the machine’s **variables** to values that **establish** the **invariant**. 

#### Initialisation Event

- Variables do not have any known value before initialisation.

![](https://i.postimg.cc/nLdtNvKF/fm4.png){: .w-80 .shadow .rounded-10 }

### Modelling REQ2

REQ2: We need an operation for adding money to the money bank. 

![](https://i.postimg.cc/yxK4ZvsT/fm5.png){: .w-80 .shadow .rounded-10 }

### Modelling REQ3

REQ3: We need an operation for removing money from the money bank; 
- but it cannot remove more money than the money bank contains.

![](https://i.postimg.cc/xds3HCQp/fm6.png){: .w-80 .shadow .rounded-10 }

## Operational Interpretation of Event-B

- An event execution is supposed to take no time
  - Thus, no two events can occur simultaneously
- When all events have false guards, the discrete system stops
- When more than one event have true guards, one of them is chosen nondeterministically and its action modifies the state
- The previous phase is repeated (if possible)
