---
title: Extension Refinement in Event-B
date: 2023-11-28 18:35:00 +0530
categories: [ (CS) Learning Note, Software Modelling and Design ]
tags: [computer science, Event-B ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Refinement?](#what-is-refinement)
  * [Extension Example: add ownership to secure database](#extension-example-add-ownership-to-secure-database)
    * [Original Example](#original-example)
    * [Adding Object Ownership in the Original Example](#adding-object-ownership-in-the-original-example)
<!-- TOC -->

---

## What is Refinement?

- **Refinement** means
  - step-wise introduction of details of a model
  - It is easier to reason about a less-detailed abstraction than about the full model

- **Refinement** is a process of enriching or modifying a model in order to
  - **augment** the functionality being modelled, or
  - **explain how** some purpose is achieved

-  In a refinement step we refine one model M1 to another model M2
  - M2 is a refinement of M1 
  - M1 is an abstraction of M2

- We can perform a series of refinement steps to produce a series of models M1, M2, M3
- Facilitates abstraction: we can postpone treatment of some system features to later refinement steps


---

**Refinement**:

- Begin with a very abstract view of the model
  - focus on the **purpose**
  - and **most important properties** first
- Introduce more details and properties when convenient
- Until the implementation is reached
  - implementation-related properties are often difficult to model
  - introducing them gradually simplifies this task

## Extension Example: add ownership to secure database

### Original Example
- We consider a secure database. Each object in the database has a data component.
- Each object has a classification between 1 and 10.
- Users of the system have a clearance level between 1 and 10.
- Users can only read and write objects whose classification is no greater than the user’s clearance level.

---

![](https://i.postimg.cc/ZYgRvN41/er1.png){: .w-80 .shadow .rounded-10 }
_Diagram for secure database_

![](https://i.postimg.cc/tT4drMSS/er2.png){: .w-80 .shadow .rounded-10 }

![](https://i.postimg.cc/dQGkkT2H/er5.png){: .w-80 .shadow .rounded-10 }

### Adding Object Ownership in the Original Example

- Extend the database specification so that each object has an owner.
- The clearance associated with that owner must be at least as high as the classification of the object.
- Only the owner of an object is allowed to delete it.

---

![](https://i.postimg.cc/xTJNgzYS/er3.png){: .w-80 .shadow .rounded-10 }

![](https://i.postimg.cc/kgFjX44L/er4.png){: .w-80 .shadow .rounded-10 }

- Note we must list all the variables: those from M1 that we wish to retain as well as new ones
  - Here _owner_ is a new variable
  - We do not repeat invariants of M1 in M2

---

We have two ways of add **Refinement** in **Event** (the two ways are equivalent):

![](https://i.postimg.cc/hP2cYS8b/er7.png){: .w-80 .shadow .rounded-10 }
_Use **refines**_

![](https://i.postimg.cc/05pNVRHc/er6.png){: .w-80 .shadow .rounded-10 }
_Use **extends**_

