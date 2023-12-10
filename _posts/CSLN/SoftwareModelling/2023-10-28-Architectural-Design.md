---
title: Architectural Design
date: 2023-10-28 16:44:00 UTC
categories: [(CS) Learning Note, Software Modelling and Design]
tags: [software engineering, architecture]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Architecture?](#what-is-architecture)
    * [Role of Software Architecture](#role-of-software-architecture)
    * [Architectural Design](#architectural-design)
    * [A Good Software Architecture](#a-good-software-architecture)
  * [Why is Architecture Important?](#why-is-architecture-important)
    * [Architectural Goals and Constraints](#architectural-goals-and-constraints)
    * [Effects of non-functional requirements](#effects-of-non-functional-requirements)
  * [Architectural Views](#architectural-views)
    * [4 + 1 View Model of Software Architecture](#4--1-view-model-of-software-architecture)
      * [Development view](#development-view)
      * [Physical view](#physical-view)
      * [Logical view](#logical-view)
      * [Process view](#process-view)
      * [Scenarios](#scenarios)
  * [Architectural Patterns](#architectural-patterns)
    * [Model-View-Controller (MVC) Architecture](#model-view-controller-mvc-architecture)
      * [Introduction to MVC Architecture](#introduction-to-mvc-architecture)
      * [The Organisation of the MVC Architecture](#the-organisation-of-the-mvc-architecture)
      * [Example](#example)
    * [Layered Architecture](#layered-architecture)
      * [Introduction to Layered Architecture](#introduction-to-layered-architecture)
      * [The Organisation of the Layered Architecture](#the-organisation-of-the-layered-architecture)
      * [Example](#example-1)
    * [Pipe and Filter Architecture](#pipe-and-filter-architecture)
      * [Introduction to Pipe and Filter Architecture](#introduction-to-pipe-and-filter-architecture)
      * [Example](#example-2)
    * [Repository Architecture](#repository-architecture)
      * [Introduction to Repository Architecture](#introduction-to-repository-architecture)
      * [Example](#example-3)
    * [Client-Server Architecture](#client-server-architecture)
      * [Introduction to Client-Server Architecture](#introduction-to-client-server-architecture)
      * [Example](#example-4)
    * [Microservices Architecture](#microservices-architecture)
      * [Introduction to Microservices Architecture](#introduction-to-microservices-architecture)
      * [The Organisation of the Layered Architecture](#the-organisation-of-the-layered-architecture-1)
  * [Key Points of Architecture](#key-points-of-architecture)
<!-- TOC -->

---

## What is Architecture?

> Architecture is the fundamental organization of a system, embodied in its components, their relationships to each other and the environment, and the principles governing its design and evolution.

> The software architecture of a program or computing system is the structure or structures of the system, which comprise software elements, the externally visible properties of those elements, and the relationships among them.


### Role of Software Architecture

Architecture is the decomposition of system into:
- **Software Elements**
  - Elements are captured as abstractions
  - Correspond to high level system modules or components
- **Component interfaces**
  - Externally visible properties of elements
  - Describe element features exposed to others
  - Typically represent services provided to other elements
- **Component responsibilities**
  - What does a component precisely do
  - Relationships of elements
  - How do elements interact with others

### Architectural Design

- An **early** stage of the system **design process**.
- Represents the link between **Requirements** specification and **design** processes.
- Often carried out in parallel with some specification activities.
- It involves **identifying** major system **components** and their **communications**.

### A Good Software Architecture

- Considers all the system:
  - Functional requirements
  - Non-functional requirements
- Helps us understand the system:
  - Divides the system meaningfully
  - Abstract complicated details
- Provides the framework for:
  - Realisation
  - Project Planning
  - Project Organisation
  - Integrate all the development artefacts
  - Provide documentation


## Why is Architecture Important?

- Handling **complexity**
- **Communication** among stakeholders
- Documenting Early Design Decisions
  - SA is a transferable, reusable model
- Architecture focuses on **issues** that will be **difficult/impossible** to **change** once the system is built.
  - Quality attributes like **security**, **performance**
  - Other non-functional requirements like cost, **deployment** and adopted **technologies**
- Crucial changes in software engineering have increased the importance of architecture, these changes include:
  - Scale
  - Distribution
  - Security

### Architectural Goals and Constraints

- The architecture will be formed by considering:
  - **functional** requirements, captured in the Use-Case Model
  - **non-functional** requirements, quality attributes.
- However, there are **constraints** imposed by the environment in which the software must operate that will shape the architecture:
  - need to **reuse** existing assets
  - imposition of various **standards**
  - need for **compatibility** with existing systems

### Effects of non-functional requirements

The choice of the architectural style depends heavily on the non-functional requirements
- **Performance**: localise critical operations within a small number of components deployed on the same node rather than distributed
- **Security**: layered architecture with the most critical assets protected in the inner layers
- **Safety**: safety related components are co-located
- **Availability**: include redundant components
- **Maintainability**: use self-contained components that can be readily changed

## Architectural Views

- Large software systems require structures from multiple perspectives (views)
- A single view is not sufficient to address all the requirements


### 4 + 1 View Model of Software Architecture

- The views are used to describe the system from the viewpoint of different stakeholders, such as end-users, developers and project managers.
  1. Physical view
  2. Logical view
  3. Process view
  4. Development view
  5. ( +1 ) Scenarios

![](https://i.postimg.cc/15HvRsp7/sa1.png){: .w-65 .shadow .rounded-10 }

#### Development view

- The development view illustrates a system from a programmer's perspective and is concerned with software management.
  - This view is also known as the **implementation** view.
  - It uses the UML **Component diagra**m or **Package diagram**

![](https://i.postimg.cc/BQQVKjQf/sa2.png){: .w-65 .shadow .rounded-10 }
_Example of package diagram_

#### Physical view

- The physical view depicts the system from a system engineer's point of view.
  - It is concerned with the topology of software components and the physical connections between these components. This view is also known as the **deployment view**.
  - UML diagrams used to represent the physical view include the **deployment diagram**.

![](https://i.postimg.cc/L6wGFH2d/sa3.png){: .w-65 .shadow .rounded-10 }
_Example of deployment diagram_

#### Logical view

- The logical view is concerned with the functionality that the system provides to end-users.
  - UML diagrams used to represent the logical view include, **class diagrams**, and **state diagrams**.

#### Process view

- The process view deals with the **dynamic** aspects of the system, explains the system **processes** and how they **communicate**, and focuses on the **runtime behaviour** of the system.
  - The process view addresses **concurrency**, **distribution**, **integrators**, **performance**, and **scalability**, etc.
  - UML diagrams to represent process view include the **sequence diagram**, **communication diagram**, **activity diagram**.

#### Scenarios

- The description of an architecture is illustrated using a small set of **use cases**, or **scenarios**, which become a fifth view.
  - The scenarios describe sequences of interactions between **components** and between **processes**.
  - They are used to identify architectural elements and to **illustrate** and **validate** the architecture design.
  - They also serve as a starting point for tests of an architecture prototype. This view is also known as the **use case view**.

## Architectural Patterns

- An architectural pattern is a proven **structural organisation** schema for software systems.
- An architectural pattern is a stylised **description** of good **design practice**, which has been tried and tested in different environments.
- An architectural pattern/style is a description of **component** and **connector** types and a pattern of their runtime control and/or data transfer.
  - **Components**: define the locus of computation
    - Examples: filters, databases, components, objects, clients/servers
  - **Connectors**: mediate component interactions
    - Examples: method call, pipes, event broadcast, shared memory, message passing 

---

- Patterns are a means of **representing**, **sharing** and **reusing** knowledge.
- Patterns should include information about **when** they are and **when** they are not useful.
- Patterns may be represented using **tabular** and **graphical descriptions**.

### Model-View-Controller (MVC) Architecture

**Problem**: separation of UI from application is desirable due to expected UI adaptations

**Context**: interactive applications with a flexible UI

**Solution**:    
- system model: UI (View and Controller Component(s)) is decoupled from the application (Model component)
- components: collections of procedures (module)
- connectors: procedure calls
- control structure: single thread

#### Introduction to MVC Architecture

- Description:
  - Separates presentation and interaction from the system data.
  - The system is structured into **three logical components** that interact with each other.
    - The **Model component** manages the system data and associated operations on that data.
    - The **View component** defines and manages how the data is presented to the user.
    - The **Controller component** manages user interaction (e.g., key presses, mouse clicks, etc.) and passes these interactions to the View and the Model.

- Example:
  - the architecture of a web-based application system organized using the MVC pattern.

- When used:
  - Used when there are multiple ways to view and interact with data. Also used when the future requirements for interaction and presentation of data are unknown.

- Advantages:
  - Allows the data to change independently of its representation and vice versa.
  - Supports presentation of the same data in different ways with changes made in one representation shown in all of them.

- Disadvantages:
  - Can involve additional code and code complexity when the data model and interactions are simple.

#### The Organisation of the MVC Architecture

![](https://i.postimg.cc/vBtSpPVg/sa4.png){: .w-65 .shadow .rounded-10 }

#### Example

![](https://i.postimg.cc/wM2J8rHr/sa5.png){: .w-65 .shadow .rounded-10 }
_Web Application Architecture Using the MVC Pattern_

### Layered Architecture

**Problem**: distinct, hierarchical classes of services. “Concentric circles” of functionality

**Context**: a large system that requires decomposition (e.g., virtual machines, OSI model)

**Solution**:
- system model: hierarchy of layers, often limited visibility
- components: collections of procedures (module)
- connectors: (limited) procedure calls
- control structure: single or multiple threads

---

- Used to model the interfacing of sub-systems.
- Organises the system into a set of layers (or abstract machines) each of which provide a set of services.
- Supports the incremental development of sub-systems in different layers. When a layer interface changes, only the adjacent layer is affected.
- However, often artificial to structure systems in this way


#### Introduction to Layered Architecture

- Description:
  - Organizes the system into layers with related functionality associated with each layer.
  - A layer provides services to the layer above it
  - so the lowest-level layers represent core services that are likely to be used throughout the system.

- Example:
  - A layered model of a system for sharing copyright documents held in different libraries

- When used:
  - Used when building new facilities on top of existing systems;
  - when the development is spread across several teams with each team responsibility for a layer of functionality
  - when there is a requirement for multi-level security.

- Advantages:
  - Allows replacement of entire layers so long as the interface is maintained. Redundant facilities (e.g., authentication) can be provided in each layer to increase the dependability of the system

- Disadvantages:
  - In practice, providing a clean separation between layers is often difficult and a high-level layer may have to interact directly with lower-level layers rather than through the layer immediately below it. Performance can be a problem because of multiple levels of interpretation of a service request as it is processed at each layer


#### The Organisation of the Layered Architecture

![](https://i.postimg.cc/pVf35Jq1/sa6.png){: .w-65 .shadow .rounded-10 }

#### Example

![](https://i.postimg.cc/fLZjGmmJ/sa7.png){: .w-65 .shadow .rounded-10 }
_The Architecture of the LIBSYS System_

### Pipe and Filter Architecture

- **Functional transformations**, process their inputs to produce outputs.
- May be referred to as a pipe and filter model (as in UNIX shell).
  - Variants of this approach are widespread. When transformations are **sequential**, this is a **batch** sequential model which is extensively used in data **processing** systems.
- **Not** really suitable for **interactive** systems.
- Provides a structure for systems that produce a **stream of data**
- Each **processing** step is **encapsulated** in a **filter** component
- Data **is passed** through **pipes**
  - Pipes can be used for **buffering** or for **synchronisation**
- This pattern divides the task of a system into several **processing steps**. The steps are connected by the **data flow**
  - The output of a step is the input for the next step
- Common examples:
  - Pipe-filter in the Unix shell commands
    - cat file \| grep xyz \| sort \| uniq > out
  - Compilers

#### Introduction to Pipe and Filter Architecture

- Description:
  - The processing of the data in a system is organised so that each processing component (filter) is discrete and carries out one type of data transformation.
  - The data flows (as in a pipe) from one component to another for processing.

- Example:
  - A pipe and filter system used for processing invoices.

- When used:
  - Commonly used in data processing applications (both batch and transaction-based) where inputs are processed in separate stages to generate related outputs.

- Advantages:
  - Easy to understand and supports transformation reuse. Workflow style matches the structure of many business processes. Evolution by adding transformations is straightforward. It Can be implemented as either a sequential or concurrent system.

- Disadvantages:
  - The format for data transfer has to be agreed upon between communicating transformations. Each transformation must parse its input and un-parse its output to the agreed form. This increases system overhead and may mean that it is impossible to reuse functional transformations that use incompatible data structures.

#### Example

![](https://i.postimg.cc/SKhFX1cR/sa8.png){: .w-65 .shadow .rounded-10 }
_A Three-Pass Compiler_

![](https://i.postimg.cc/6QfsCVh0/sa9.png){: .w-65 .shadow .rounded-10 }
_pipe and filter architecture used for processing invoices_


### Repository Architecture


#### Introduction to Repository Architecture

- Description:
  - All data in a system is managed in a central repository that is accessible to all system components.
  - Components do not interact directly, only through the repository.

- Example:
  - An IDE where the components use a repository of system design information.
  - Each software tool generates information which is then available for use by other tools

- When used:
  - You should use this pattern when you have a system in which large volumes of information are generated that has to be stored for a long time. You may also use it in data-driven systems where the inclusion of data in the repository triggers an action or tool.

- Advantages:
  - Components can be independent: they do not need to know of the existence of other components. Changes made by one component can be propagated to all components. All data can be managed consistently (e.g., backups done at the same time) as it is all in one place.

- Disadvantages:
  - The repository is a single point of failure, so problems in the repository affect the whole system. Maybe inefficiencies in organising all communication through the repository. Distributing the repository across several computers may be challenging.

#### Example

![](https://i.postimg.cc/mgshRs86/sa10.png){: .w-65 .shadow .rounded-10 }
_A Repository Architecture for an IDE_

![](https://i.postimg.cc/2S7ySKtj/sa11.png){: .w-65 .shadow .rounded-10 }
_A Repository Architecture For a Language Processing System_

### Client-Server Architecture

- **Distributed** system model which shows how **data** and **processing** are distributed across a range of components.
  - Can be implemented on a single computer.
- Set of **stand-alone servers** which provide specific services such as printing, data management, etc.
- Set of **clients** which call on these services.
- **Network** which allows clients to access servers.

#### Introduction to Client-Server Architecture

- Description:
  - In a client-server architecture, the functionality of the system is organised into services, with each service delivered from a separate server. Clients are users of these services and access servers to make use of them.

- Example:
  - A film and video/DVD library organized as a client-server system

- When used:
  - Used when data in a shared database has to be accessed from a range of locations. Because servers can be replicated, may also be used when the load on a system is variable.

- Advantages:
  - The principal advantage of this model is that servers can be distributed across a network. General functionality (e.g., a printing service) can be available to all clients and does not need to be implemented by all services.

- Disadvantages:
  - Each service is a single point of failure so susceptible to denial of service attacks or server failure. Performance may be unpredictable because it depends on the network as well as the system. Maybe management problems if servers are owned by different organizations.

#### Example

![](https://i.postimg.cc/PJ591PXF/sa12.png){: .w-65 .shadow .rounded-10 }
_A Client-Server Architecture for a Film Library_


### Microservices Architecture

- The microservices architecture pattern takes the approach of building small independent applications that communicate with each other in order for the entire system (application) to work.
- The microservices pattern allows us to deploy these small applications independently, thereby providing a high degree of application and component decoupling within the application.

#### Introduction to Microservices Architecture

- Description:
  - An application is divided into multiple small services, each running in its own process and communicating with lightweight protocols.
  - Each service is responsible for a specific business functionality and can be developed independently by different teams.
  - Services can be deployed independently and can be written in different programming languages.
  - Services communicate with each other via APIs or messaging protocols.

- Example:
  - An e-commerce application can be divided into several microservices, such as:
    - User Service: Handles user registration and authentication.
    - Catalog Service: Manages product catalog and inventory.
    - Order Service: Handles order placement and payment processing.
    - Shipping Service: Manages order shipping and delivery.

- When used:
  - Large and complex applications that require scalability and flexibility.
  - Applications that are developed by multiple teams or require frequent updates and deployments.
  - Organizations that want to adopt DevOps practices and continuous delivery.

- Advantages:
  - Scalability: Each service can be scaled independently to meet demand.
  - Flexibility: Services can be developed in different programming languages and frameworks.
  - Faster Time to Market: Independent services can be developed, tested, and deployed faster.
  - Easier Maintenance: Smaller, independent services are easier to maintain and troubleshoot.

- Disadvantages:
  - Complexity: Managing multiple services and their interactions can be complex.
  - Data Consistency: Ensuring data consistency across services can be challenging.
  - Network Latency: Communication between services can introduce latency.
  - Operational Overhead: Managing and monitoring multiple services can require additional resources.


#### The Organisation of the Layered Architecture

![](https://i.postimg.cc/RhChfQn5/sa13.png){: .w-65 .shadow .rounded-10 }


## Key Points of Architecture

- A software architecture is a description of how a software system is organized.
- Architecture can be viewed:
  - As a way of organising the work of the development team.
  - As a means of assessing components for reuse.
  - As a vocabulary for talking about application types.
- Architecture may be documented from several different perspectives or views.
- Architectural design decisions include decisions on the type of application, the distribution of the system, the architectural styles to be used.
- Architectural patterns are a means of reusing knowledge about generic system architectures.
  - In reality, we use a **combination** of architectural patterns
