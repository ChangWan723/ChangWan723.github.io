---
title: Software Modelling and Design
date: 2023-10-11 16:48:00 +0530
categories: [(CS) Learning Note, Software Modelling]
tags: [computer science, software engineering, Software Modelling]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Modelling/Design?](#what-is-modellingdesign)
  * [Why Do We Model Software?](#why-do-we-model-software)
  * [The design/modelling process](#the-designmodelling-process)
  * [What is Good Design?](#what-is-good-design)
  * [Design Principles](#design-principles)
    * [Design Principle 1: Modularisation](#design-principle-1-modularisation)
    * [Design Principle 2: Abstraction](#design-principle-2-abstraction)
    * [Design Principle 3: Encapsulation](#design-principle-3-encapsulation)
    * [Design Principle 4: Coupling](#design-principle-4-coupling)
    * [Design Principle 5: Cohesion](#design-principle-5-cohesion)
    * [Design Principle 6: Separation of Interface and Implementation](#design-principle-6-separation-of-interface-and-implementation)
    * [Design Principle 7: Sufficiency](#design-principle-7-sufficiency)
    * [Design Principle 8: Completeness](#design-principle-8-completeness)
  * [Levels of design](#levels-of-design)
  * [Related Blogs](#related-blogs)
<!-- TOC -->

---

## What is Modelling/Design?

- What do we want to build?
  - **Software Model**: A **description** (textual or visual) of any aspects of a software system such as **requirements**, **architecture**, **behaviour**, **structure**, or **concurrency** model
- How do we write this down?
  - **Software Modelling**: The practice of creating and analysing **software models**.
- What is Design?
  - Design is the process of deciding **how software will meet requirements**.

> You may be thinking:
> - Modelling is a waste of time
> - We need to show something to the customer really quickly
> - We are judged by the amount of (Line of Code)LOC/month
> - We expect or know that the schedule is too tight
> - Skip requirements engineering and design phases
> 
> However, **The longer you postpone coding, the sooner you’ll be finished. Modeling is important for large projects!**
{: .prompt-warning }

## Why Do We Model Software?

Several camps in modelling:
- Those who use models to **document** important decisions, outcome of different analyses
- Those who use models to **communicate** about software
- Those who use models to **validate** software
- Those who use models to **generate** software

**Why Build Models:**

1. Modelling can **guide** your **exploration**:
   - can help you **figure out** what **questions** to ask
   - can help to **reveal** key **design decisions**
   - can help you to **uncover problems**
     - e.g. **conflicting** or **infeasible** requirements, **confusion** over terminology, scope, etc. 

2. Modelling can help us **check** our **understanding**
   - **Reason** about the model to **understand** its consequences
   - Does it have the properties we **expect**?
   - Animate the model to help us **visualise/validate** the requirements

3. Modelling can help us **communicate**
   - Provide useful **abstracts** that focus on the point you want to make without overwhelming people with detail
   - To make sense of the world…

## The design/modelling process

The design process consists mainly 4 activities:
1. Postulate a solution
2. Build a model of the solution
3. Evaluate the model against original requirements
   - There is an interaction between requirements engineering, architectural, and detailed design
4. Elaborate the model to produce a detailed specification of the solution

---

- Designer formulates and develops an **abstract** model **representative** of the **solution**
- The design process is **not straightforward** because of the nature of software
  - The **complexity** of software
  - The problem of **conformity**
  - The (apparent) ease of **changeability**
  - The **invisibility** of software

**Forms of Design Representation:**
- Textual
- Diagrammatical
- Mathematical

**Examples:**
- State Charts
- Data Flow Diagram (DFD)
- Entity Relationship Diagram (ERD)
- Unified Modeling Language (UML)
- Formal Methods (Event-B)


## What is Good Design?

**Some Criteria for a Good Design:**
- It can meet the known **requirements** (**functional and nonfunctional**)
- It is **maintainable**:
  - i.e., it can be adapted to meet future requirements
- It is straightforward to explain to the **stakeholders**
- It makes **appropriate** use of existing technology,
  - e.g., **reusable** components
  - documented using known **standards**

## Design Principles

- Modularity, coupling and cohesion
  - Hierarchical structure and model decomposition
- Encapsulation & information hiding
- Abstraction: to focus on main properties and manage complexity
- Limit complexity
  - Models of a complex system shouldn’t necessarily to be complex

### Design Principle 1: Modularisation

- This principle drives the **continues decomposition** of the software system until **fine-grained** components are created.
  - **Rational**: it allows software systems to be **manageable** at all phased of the development life-cycle.
  - When you **modularise** a **design**, you are also modularising requirements, programming, test cases, etc.

- Plays a key role during all design activities.
  - it provides a roadmap for software development starting from **coarse-grained** components that are further modularised into **fine-grained** components directly related to code.
  - Leads to designs that are easy to **understand**, resulting in systems that are easier to develop and **maintain**.

---

But how do we devise the “modularisation strategy”?
- It turns out that two other principles can effectively guide designers during this process
  - **Abstraction**
  - **Encapsulation**

### Design Principle 2: Abstraction

- Abstraction is to focuses on **essential features**, while deferring unnecessary details to the later stages.
  - The principle of **modularisation** specifies **what needs to be done**.
  - The principle of **abstraction** provides **guidance as to how it should be done**.

### Design Principle 3: Encapsulation

- Principle that deals with providing access to the services of **abstracted entities** by **exposing** only the information that is **essential** to carry out such services while hiding details of how the services are carried out.
  - When applied to **data**, encapsulation provides access only to the**necessary data** of abstracted entities, no more, no less.
  - Encapsulation and abstraction go hand in hand.
    - When we do **abstraction**, we **hide details**…
    - When we do **encapsulation**, we revise our abstractions to enforce that abstracted entities only **expose essential information, no more, no less**.
  - Encapsulation forces us to **create good abstractions**!

### Design Principle 4: Coupling

- Refers to the manner and degree of **interdependence** between software modules.

- **Measurement of dependency** between units. The **higher** the **coupling**, the **higher** the **dependency** and vice versa.

>**Types of Coupling:**
> 
>1. Content/Code coupling
>  - The most **severe** type, since it refers to modules that modify and rely on internal information of other modules.
>
>2. Data coupling
>  - Dependency through **data passed** between modules, e.g., through function parameters.
>  - Does not depend on other modules’ internals or globally accessible data, therefore, design units are shielded from changes in other places.
{: .prompt-tip }


>**Consequences of Coupling:**
> 
>In all cases, a high degree of coupling gives rise to **negative** side effects.
>- Quality, in terms of **reusability** and **maintainability**, decrease.
>- When coupling increase, so does **complexity** of managing and **maintaining** design units.
{: .prompt-tip }

### Design Principle 5: Cohesion

- The manner and degree to which the tasks performed by a single software module are related to one another.

- The manner and degree to which the tasks performed by a single software module are related to one another.

- **Cohesion** can be classified as:
  - **Functional** cohesion
  - **Procedural** (or sequential) cohesion
  - **Temporal** cohesion
  - **Communication** cohesion

- **High** cohesion is **good**, **low** cohesion is **bad**…

### Design Principle 6: Separation of Interface and Implementation

- Deals with creating modules in such way that a **stable interface** is identified and **separated from its implementation**.

- **Not the same thing as encapsulation!**
  - While **encapsulation** dictates **hiding the details** of implementation,
  - this principle dictates their **separation**, so that **different implementations of the same interface** can be **swapped** to provide **modified** or **new behavior**.

### Design Principle 7: Sufficiency

- Sufficiency measures how well the designed units are at **providing only the services that are sufficient** for achieving the intent (no more)
- Deals with capturing **enough characteristics** of the abstraction to permit meaningful interaction
- Must provide a full set of operations to allow a client properly interact with the abstraction.
- Implies minimal interface

### Design Principle 8: Completeness

- Deals with interface capturing all the essential
characteristics of the abstraction.
- Implies an interface general enough for any prospective
client
- Completeness is subjective and carried too far can have
unwanted results.

>**Sufficiency** is about meeting basic requirements, **completeness** is about ensuring all essential requirements, nuances, and details are addressed.
{: .prompt-tip }

## Levels of design

- Design occurs at different levels, e.g. someone must decide:
  - how is your system split up into subsystems?
    - high-level, or architectural design
  - what are the classes in each subsystem?
    - low-level, or detailed design

- At each level, decisions needed on
  - what are the **responsibilities** of each component/class ?
  - what are the **interfaces**?
  - what **messages** are exchanged, in what **order**?

## Related Blogs

- [Unified Modelling Language (UML)](/posts/Unified-Modelling-Language-(UML)/)
