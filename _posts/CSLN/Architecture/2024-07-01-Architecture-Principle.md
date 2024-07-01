---
title: Three Principles of Architecture Design
date: 2024-07-01 22:00:00 UTC
categories: [ (CS) Learning Note, Architecture ]
tags: [ software engineering , architecture]
pin: false
---

With the ever-changing business, emerging technologies, and diverse design concepts, it may seem difficult to have a common set of guidelines to apply to all architectural design scenarios. But in the history of the development of architecture design, there are several common principles implied, which are:
- **the principle of appropriateness**
- **the principle of simplicity** 
- **the principle of evolution**

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Principle of Appropriateness](#principle-of-appropriateness)
    * [Definition](#definition)
    * [Key Aspects](#key-aspects)
    * [Example](#example)
  * [Principle of Simplicity](#principle-of-simplicity)
    * [Definition](#definition-1)
    * [Key Aspects](#key-aspects-1)
    * [Example](#example-1)
  * [Principle of Evolution](#principle-of-evolution)
    * [Definition](#definition-2)
    * [Key Aspects](#key-aspects-2)
    * [Example](#example-)
<!-- TOC -->

---

## Principle of Appropriateness

> **Appropriateness is better than industry-leading.**
{: .prompt-tip }

### Definition

**The Principle of Appropriateness dictates that the architecture should be tailored to the specific requirements and constraints of the system it supports.** This principle emphasizes the need for the architecture to be context-sensitive, considering factors such as the problem domain, stakeholder needs, team situations and technological environment.

### Key Aspects

- **Fit for Purpose**: The architecture should be designed to meet the functional and non-functional requirements of the system. This includes performance, scalability, security, and usability.
- **Context Sensitivity**: The architecture should take into account the specific context in which the system will operate. This includes understanding the business domain, user expectations, and operational constraints.
- **Avoiding Overengineering**: The architecture should avoid unnecessary complexity and features that do not add value to the system. Overengineering can lead to increased costs and maintenance burdens.

### Example

**Architecture design should not strive for the best, but the most suitable.** For example, a small-scale business team ambitiously proposed to make a "billion-user platform" to compete with Meta, and the final result is, unsurprisingly, a failure.

**Specific projects should focus on different architectures depending on the corresponding requirements.** For example, in a real-time financial trading system, the architecture must prioritize low latency and high availability. An appropriate architecture might use in-memory data stores and event-driven processing to meet these stringent requirements. In contrast, a content management system for a blog may prioritize ease of use and flexibility, requiring a different architectural approach.

## Principle of Simplicity

> **Simplicity is better than complexity.**
{: .prompt-tip }

### Definition

**The Principle of Simplicity advocates for keeping the architecture as simple as possible while still meeting all requirements.** Simplicity reduces complexity, making the system easier to understand, develop, and maintain.

### Key Aspects

- **KISS (Keep It Simple, Stupid)**: The KISS principle is generally applied in code programming, but is also applied to architectural design. Focus on straightforward and clear designs. Avoid unnecessary complexity that does not provide significant benefits.
- **Minimalism**: Implement only what is necessary to meet the system's requirements. (We can pursue high standards during the requirement creation phase. But once the requirements are defined, we just need to meet them.) In subsequent iterations of the release, we can add functionality or improve the standard gradually as needed.
- **Clarity and Readability**: The architecture should be easy to understand and communicate. This facilitates collaboration among team members and stakeholders.

### Example

A microservices architecture can quickly become complex with many small, independent services. Applying the Principle of Simplicity might involve consolidating some services or using a monolithic approach for smaller applications, reducing overhead and simplifying the deployment and management process.

## Principle of Evolution

> **Evolution is better than one-step**
{: .prompt-tip }

### Definition

**For buildings, timelessness is the theme. But for software, changing is the theme.**

The Principle of Evolution recognizes that software systems need to adapt to changing requirements, technologies, and business environments. An evolutionary architecture is designed to be flexible and resilient, allowing for incremental changes and continuous improvement.

### Key Aspects

- **Flexibility**: The architecture should accommodate changes without requiring significant rework. This includes modular design, loose coupling, and the use of interfaces and abstractions.
- **Scalability**: The system should be able to scale in response to increasing loads and new requirements. This involves designing for both horizontal and vertical scaling.
- **Continuous Improvement**: The architecture should support ongoing development and refinement, allowing for the incorporation of new technologies and best practices.

### Example 

In a rapidly evolving technology landscape, an e-commerce platform must be able to integrate new payment methods, support increased traffic during sales events, and adapt to changing consumer behaviors. An evolutionary architecture might use microservices, containerization, and continuous deployment pipelines to ensure the system can adapt and grow over time.

<br>

---

**Reference:**

- Li, Yunhua (2018) _Learn Architecture from 0_. Geek Time.
