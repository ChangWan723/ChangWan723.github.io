---
title: Unified Modelling Language (UML)
date: 2023-10-17 16:07:00 +0530
categories: [(CS) Learning Note, Software Modelling and Design]
tags: [software engineering, Software Modelling and Design, UML, OOP]
pin: false
---

UML, or Unified Modeling Language, is a standardized visual language designed to model and document software systems. It plays a pivotal role in software engineering, bridging the gap between conceptualization and implementation.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is UML?](#what-is-uml)
  * [Key Benefits of UML](#key-benefits-of-uml)
  * [Classification of UML Diagrams](#classification-of-uml-diagrams)
    * [Class Diagram](#class-diagram)
    * [Object Diagram](#object-diagram)
    * [Use Case Diagram](#use-case-diagram)
    * [Sequence Diagram](#sequence-diagram)
    * [Activity Diagram](#activity-diagram)
    * [Component Diagram](#component-diagram)
    * [Deployment Diagram](#deployment-diagram)
    * [State Diagram (State Machine Diagram)](#state-diagram-state-machine-diagram)
    * [Package Diagram](#package-diagram)
    * [Communication (Collaboration) Diagram](#communication-collaboration-diagram)
    * [Interaction Overview Diagram](#interaction-overview-diagram)
    * [Timing Diagram](#timing-diagram)
    * [Composite Structure Diagram](#composite-structure-diagram)
    * [Profile Diagram](#profile-diagram)
  * [UML in Common Use](#uml-in-common-use)
  * [Related Blogs](#related-blogs)
<!-- TOC -->

---

## What is UML?

UML stands for **Unified Modeling Language**. It is a standard notation that provides a consistent way to visualize the design of a system. UML is mainly known for its diagrams, which offer different views of a software system.

- Standard language for **specifying**, **visualising**, **constructing**, and **documenting** the artifacts of software systems, business modelling and other non-software systems.
- The UML represents a collection of best engineering practices that have proven successful in the modelling of large and complex systems.
  - The UML is mostly used in developing **object-oriented** software and the software development process.
- The UML uses mostly **graphical notations** to express the design of software projects.
- UML is **not a “process”**. (That is, it doesn’t tell you how to do things, only what you can do.)

## Key Benefits of UML

1. **Visualization**: UML provides a clear and standardized way to represent system architectures, components, relationships, and processes.
2. **Standardization**: As an industry-standard, UML promotes consistency across projects.
3. **Communication**: UML diagrams enhance communication between team members and stakeholders by providing a clear visual representation of system components and their interactions.

We need UML to:
- help develop efficient, effective and correct designs, particularly Object-Oriented designs.
- communicate clearly with project stakeholders (concerned parties: developers, customer, etc).
- Using the UML helps project teams communicate, explore potential designs, and validate the various aspects of the software design.

## Classification of UML Diagrams

![](https://i.postimg.cc/43gWjL2w/uml1.png){: .w-100 .shadow .rounded-10 }

### Class Diagram
- **Purpose**: Represents the static structure of a system.
- **Components**: Classes, interfaces, associations, and generalizations.

### Object Diagram
- **Purpose**: Shows a complete or partial view of the structure of a modeled system at a specific time.
- **Components**: Object instances and their relationships.

### Use Case Diagram
- **Purpose**: Describes a system’s functional requirements, as well as the external entities interacting with the system.
- **Components**: Use cases, actors, and their relationships.

### Sequence Diagram
- **Purpose**: Represents the sequence of activities in a system in terms of sequential flow.
- **Components**: Actors, lifelines, messages, and activations.

### Activity Diagram
- **Purpose**: Represents workflows and business processes.
- **Components**: Activities, action flows, decisions, guards, forks/joins, and swimlanes.

### Component Diagram
- **Purpose**: Describes the organization and interrelationships of system components.
- **Components**: Components, interfaces, and their relationships.

### Deployment Diagram
- **Purpose**: Depicts the physical resources in a system, including nodes, components, and the connections between them.
- **Components**: Nodes and their relationships.

### State Diagram (State Machine Diagram)
- **Purpose**: Describes the behavior of an entity (class, interface, etc.) in response to internal and external stimuli.
- **Components**: States, transitions, events, and actions.

### Package Diagram
- **Purpose**: Represents the division of a model into functional units, showing the dependencies between the packages.
- **Components**: Packages and their relationships.

### Communication (Collaboration) Diagram
- **Purpose**: Shows interactions between objects focusing on the structural organization.
- **Components**: Objects and their links, illustrating the flow of messages.

### Interaction Overview Diagram
- **Purpose**: Combines activity and sequence diagrams to show a high-level view of interactions in the system.
- **Components**: Interaction fragments, decisions, initial/final nodes, and interactions.

### Timing Diagram
- **Purpose**: Shows the behavior of objects in a given timeframe, focusing on the timing constraints.
- **Components**: Lifelines, states, and state transitions.

### Composite Structure Diagram
- **Purpose**: Represents the internal structure of a class (or any other classifier) and the collaborations that this structure makes possible.
- **Components**: Classes, ports, parts, connectors, and collaborations.

### Profile Diagram
- **Purpose**: Provides a mechanism to customize UML models for particular domains and platforms.
- **Components**: Stereotypes, tagged values, and constraints.

## UML in Common Use

Models used mainly for **requirements**:
- **Use case diagram** shows a set of use cases and actors and their relationships.
- **Activity diagram** (flowchart) shows the flow from one activity to another activity within a system.

Models used mainly for systems **architecture**:
• **Component diagram** shows the organisation and dependencies among a set of components.
• **Deployment diagram** shows the configuration of processing nodes and the components that live on them.

Models used mainly for **detailed design**:

- **Class diagram**: shows a set of classes, interfaces, and collaborations with their relationships.
- **Sequence diagrams**: time ordering of messages
- **State diagrams** and **activity diagrams** also are widely used.

## Related Blogs

- [Use Case Diagrams in UML](/posts/Use-Case-Diagrams-in-UML/)
- [Class Diagrams in UML](/posts/Class-Diagrams-in-UML/)
- [State Machine Diagrams in UML](/posts/State-Machine-Diagrams-in-UML/)
- [Sequence Diagrams in UML](/posts/Sequence-Diagram-in-UML/)
- [Activity Diagrams in UML](/posts/Activity-Diagrams-in-UML/)
