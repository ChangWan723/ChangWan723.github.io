---
title: Software Project Management and Secure Development
date: 2023-10-01 17:55:00 +0530
categories: [(CS) Learning Note, Software Project Management and Secure Development]
tags: [computer science, software engineering, project management]
pin: false
---

This module is for undertaking large software projects. It introduces the high-level strategies required for managing projects from their genesis to completion.

This module also introduces secure engineering of software systems. 

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What does it contain?](#what-does-it-contain)
  * [Software Development](#software-development)
    * [Software Product Attributes](#software-product-attributes)
    * [Development Costs](#development-costs)
  * [Why Secure software development?](#why-secure-software-development)
    * [Examples of Software Flaws](#examples-of-software-flaws)
    * [Examples of Software Bugs](#examples-of-software-bugs)
<!-- TOC -->

---

## What does it contain?

1. Managing the software development process: 

   - Estimating the effort in software projects
   - Contracts, planning and monitoring projects
   - Costing and budgeting of projects
   - Models of Software Projects

2. Security by design:

   - Security models, and principles of secure computing
   - Software Engineering methodology for secure systems
   - Security and trust issues in software system design

## Software Development

### Software Product Attributes

- Maintainability
  - to allow for evolution to meet changing specs.

- Dependability
  - failure should not result in physical or economic damage.
- Efficiency 
  - system resources should be used efficiently. 
  - Usability 
  - Appropriate user interface and documentation should exist.

### Development Costs

- Cost is a central theme of any engineering process.
- Determined by the software’s complexity, reliability, ...
- Determined by “bugs” in the development process.

## Why Secure software development?

- The **target of attacks** has changed
  - Attackers traditionally, focus on operating system and network
  - Now the focus shifted to web applications, web browsers, mobile devices, embedded software
- The **attackers’ nature** has changed
  - Traditionally, hackers are amateurs motivated by fun
  - Increasingly, hackers are professional organized crime and state-sponsored attackers
- Many attacks starts by **exploiting a vulnerability**
  - A security-relevant software defect that can be exploited to produce an undesired behavior
  - A software defect is present when the software behaves incorrectly.
- Defects can be present in the software **design** and in its **implementation**
  - A **flaw** is a defect in the design
  - A **bug** is a defect in the implementation

### Examples of Software Flaws

- Authentication flaws
  - Authenticate an entity based on IP address or MAC address
  - Not automatic log out from a session
  - Not storing password encrypted or hashed
  - No limited life-time for authentication credentials
- Authorization flaws
  - Fail to revoke access/permission
- Incorrect use of cryptography
  - Rolling your own cryptographic algorithms or implementations
  - Misuse of libraries and algorithms
  - Poor key management
  - Randomness that is not random

### Examples of Software Bugs

- Buffer overflow
- SQL injection
- Cross-site scripting
- Cross-Site Request Forgery (CSRF)
