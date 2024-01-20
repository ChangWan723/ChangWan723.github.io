---
title: Threat Modelling
date: 2024-01-20 18:01:00 UTC
categories: [ (CS) Learning Note, Software Security and Safety]
tags: [software engineering, software security]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Ways to find Security Issues: Threat Modelling](#ways-to-find-security-issues-threat-modelling)
    * [Basic Concepts & Terminology](#basic-concepts--terminology)
  * [Basic Design Patterns for Secure Systems](#basic-design-patterns-for-secure-systems)
  * [Properties of a Good System Model](#properties-of-a-good-system-model)
  * [Threat Modelling Approaches](#threat-modelling-approaches)
  * [Data Flow Diagrams](#data-flow-diagrams)
    * [Example of DFD](#example-of-dfd)
      * [context diagram](#context-diagram)
      * [level 1 diagram](#level-1-diagram)
  * [Attack Trees](#attack-trees)
    * [Example](#example)
  * [Threat Modelling Methodologies: STRIDE](#threat-modelling-methodologies-stride)
    * [STRIDE workflow](#stride-workflow)
    * [Mapping STRIDE to DFD element types](#mapping-stride-to-dfd-element-types)
    * [Example](#example-1)
  * [Threat Modelling Methodologies: LINDDUN](#threat-modelling-methodologies-linddun)
    * [LINDDUN Steps](#linddun-steps)
    * [Mapping LINDDUN to DFD element types](#mapping-linddun-to-dfd-element-types)
  * [Threat Modelling Methodologies: CIA triad](#threat-modelling-methodologies-cia-triad)
<!-- TOC -->

---

## Ways to find Security Issues: Threat Modelling

- Threat modeling is a engineering technique you can use to help you identify **threats**, **attacks**, **vulnerabilities**, and **countermeasures** that could affect your application.

- **Threat Modelling**:
  - Think about security issues early
  - Understand your requirements better
  - Don’t write bugs into the code
  - Improved stakeholder confidence

- The following **four questions** should be enough to help you decide whether your threat modelling effort will be successful:
  1. What are we working on?
  2. What can go wrong?
  3. What are we going to do about it?
  4. Did we do a good job?

![](https://i.postimg.cc/FRD8LBkZ/tm1.png){: .w-65 .shadow .rounded-10 }

### Basic Concepts & Terminology

- Asset: Anything we need to protect
- Threat: Anything that could let someone or something obtain, damage, or destroy an asset, if we fail to protect against it
- Weakness: An underlying defect that modifies behaviour or functionality
- Vulnerability: A weakness or gap in our protection efforts
- Risk: The potential for loss, damage, or destruction of an asset, due to a threat’s having successfully exploited a vulnerability

## Basic Design Patterns for Secure Systems

- **Zero trust**: ignores any prior trust relationships and verifies.
- **Design by contract**: incoming inputs to be of certain format.
- **Least privilege**: run using the most restrictive privilege.
- **Defense in depth**: multifaceted and layered defense.
- **Keeping things simple**: Avoid overengineering.
- **No secret sauce**: obscurity is not a means of security.
- **Separation of privilege**: separation of duties.
- **Consider the human factor**: security acceptable to users.
- **Effective logging**: know that something happened.
- **Fail secure**: When a system fail, it should remain secure.
- **Build in, not bolt on**: Security added from the beginning.

## Properties of a Good System Model

- **Accurate**
  - Free of inaccurate or misleading information
- **Meaningful**
  - Information is not just data
- **Representative**
  - Representative of either the design intentions or the realised implementation
- **Living**
  - The System is not static, so is your model
  - It Should reflect the current system design

## Threat Modelling Approaches

- **Asset-centric** approach
  - Focuses on important assets that should be defended
  - Examines the accessibility of assets to attackers and how threats affect the system as a whole
- **Attacker-centric** approach
  - Point of view of the attacker
  - Uses **attack trees**, threat catalogs and lists to identify entry points to the system
- **System-centric** approach = Architecture or design-centric
  - Considers the system, the system decomposition into different components (software + hardware), and the interaction between the system components as well as with external actors and interface elements.
  - Usually expressed with **DFDs (Data Flow Diagrams)** to show how the data flows through the system

## Data Flow Diagrams

**Data Flow Diagram (DFD)** is a graphical representation of the "flow" of data through an information system. It visually depicts how data moves within the system, the processes that transform this data, and the storage and external entities that interact with the system.

DFDs are used in the analysis and design phases of the system development lifecycle to provide an overview of how data is processed and transferred within a system. They are a key tool in structured analysis and design methods, helping to simplify complex systems and understand subsystems and components.

![](https://i.postimg.cc/tggcFHWM/tm2.png){: .w-65 .shadow .rounded-10 }
_Data Flow Diagram (DFD): elements_

### Example of DFD

Online Streaming Service:

A subscription-based streaming service (e.g., Netflix) allows members to watch movies and TV shows on an internet-connected device. 

Users should be able to:
  - Pay their subscriptions to get their membership
  - Login to their accounts, search for movie/program, view the details of the movie/program and watch their selection
  - Note: Registering for a new account is out of scope

#### context diagram

A Context Diagram, also known as a Level 0 DFD, is the highest level view of a system. It's a simple illustration that shows the system as a single high-level process, with its relationship to external entities (such as users, external systems, or data sources). It serves as the entry point in the DFD.

![](https://i.postimg.cc/sxTLtyBk/tm3.png){: .w-65 .shadow .rounded-10 }
_context diagram of Online Streaming Service_

#### level 1 diagram

The Level 1 DFD decomposes the main process (the system) from the Context Diagram into sub-processes, providing a more detailed view of the system's functioning.

![](https://i.postimg.cc/x1Mw1wBz/tm4.png){: .w-65 .shadow .rounded-10 }
_level 1 diagram of Online Streaming Service_

## Attack Trees

Attack Trees are a method used in security and risk management to model potential threats against a system or target.

### Example

![](https://i.postimg.cc/Wzm9vVdN/tm5.png){: .w-65 .shadow .rounded-10 }
_attack tree of Online Streaming Service_

## Threat Modelling Methodologies: STRIDE

STRIDE is a model used for **identifying security threats** in software applications. It was developed by Microsoft as part of its Secure Development Lifecycle. The acronym STRIDE stands for six categories of security threats:

- **Spoofing**: Impersonating someone or something else
- **Tampering**: Modifying data or code
- **Repudiation**: Claiming to have not performed an action
- **Information disclosure**: Exposing information to someone not authorised to see it
- **Denial of Service**: Deny or degrade service to users
- **Elevation of privilege**: Gain capabilities without proper authorisation

STRIDE is primarily used for identifying potential vulnerabilities in software systems during the design phase. By categorizing threats, it helps developers and security professionals focus on different aspects of security and apply appropriate countermeasures.

### STRIDE workflow

![](https://i.postimg.cc/x1Gb3dWT/tm6.png){: .w-65 .shadow .rounded-10 }

### Mapping STRIDE to DFD element types

![](https://i.postimg.cc/V6Jqg8qG/tm7.png){: .w-65 .shadow .rounded-10 }

### Example

![](https://i.postimg.cc/ZqCvtLW0/tm8.png){: .w-65 .shadow .rounded-10 }

## Threat Modelling Methodologies: LINDDUN

LINDDUN is a **privacy-focused** threat modelling methodology. It is designed to help identify privacy risks in software systems and guide the development of privacy-preserving systems. The name LINDDUN stands for different types of privacy threats:

- **Linkability**: The possibility to link data or activities of a person across multiple sets of data or services.
- **Identifiability**: The ability to identify the individual behind data.
- **Non-repudiation**: The inability of individuals to deny their actions, leading to potential privacy breaches.
- **Detectability**: The ability to ascertain that an item of interest or a person is present.
- **Disclosure of Information**: Unauthorized access to personal data.
- **Unawareness**: Lack of awareness of individuals about the collection, processing, and dissemination of their data.
- **Non-compliance**: Failure to adhere to legal, contractual, or other obligations regarding data privacy.

LINDDUN is used in the early stages of system design to ensure that privacy considerations are integrated into the architecture of information systems. It assists in systematically analyzing the flow of personal data and identifying potential privacy threats.

### LINDDUN Steps

![](https://i.postimg.cc/LsQ9RdcM/tm9.png){: .w-65 .shadow .rounded-10 }

### Mapping LINDDUN to DFD element types

![](https://i.postimg.cc/76NNbVND/tm10.png){: .w-65 .shadow .rounded-10 }

## Threat Modelling Methodologies: CIA triad

- CIA triad One of the most important security principles is the CIA triad, which stands for:
  - **Confidentiality**
  - **Integrity**
  - **Availability**

![](https://i.postimg.cc/zvSL5zTG/tm11.png){: .w-65 .shadow .rounded-10 }
_example of CIA triad_
