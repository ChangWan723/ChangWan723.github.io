---
title: Security By Design
date: 2023-11-13 16:35:00 +0530
categories: [ (CS) Learning Note, Software Security and Safety]
tags: [software engineering, software security]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Software Security?](#what-is-software-security)
    * [Security Dimensions](#security-dimensions)
    * [The Difference Between Software Safety and Software Security](#the-difference-between-software-safety-and-software-security)
  * [What is Security By Design?](#what-is-security-by-design)
  * [Security Design Principles](#security-design-principles)
    * [Assign the least privilege possible](#assign-the-least-privilege-possible)
    * [Separate responsibilities](#separate-responsibilities)
    * [Trust cautiously](#trust-cautiously)
    * [Simplest solution possible](#simplest-solution-possible)
    * [Audit sensitive events](#audit-sensitive-events)
    * [Fail securely & use secure defaults](#fail-securely--use-secure-defaults)
    * [Never rely upon obscurity](#never-rely-upon-obscurity)
    * [Implement defence in depth](#implement-defence-in-depth)
    * [Never invent security technology](#never-invent-security-technology)
    * [Find the weakest link](#find-the-weakest-link)
<!-- TOC -->

---

## What is Software Security?

- Security is a risk management business
  - **loss** of time, money, privacy, reputation, advantage
  - **insurance model**: balance costs against risk of loss

- Software security is the idea of engineering software so that it continues to **function correctly under malicious attack.**

- Software security is about **tools, techniques and methods** to support the development and maintenance of systems that can **resist malicious attacks** that are intended to damage a computer-based system or its data.


### Security Dimensions

- **Confidentiality**
  - Information in a system may be **disclosed** or made **accessible** to people or programs that are not authorized to have access to that information.
- **Integrity**
  - Information in a system may be **damaged** or **corrupted**, making it unusual or unreliable.
- **Availability**
  - Access to a system or its data that is normally **available may not be possible**.

### The Difference Between Software Safety and Software Security

- **Software Safety**: This is concerned with ensuring that software operates without causing unacceptable risk or harm. The focus is on **preventing** software from behaving in unintended or hazardous ways that could lead to accidents or **harm to people, property, or the environment**. It's more about the software's reliability and its ability to operate without causing unintended damage.
- **Software Security**: This deals with protecting software from malicious attacks and unauthorized access. The focus is on **safeguarding** software and its associated data against **intentional threats such as hacking, viruses, and cyberattacks**. It's about defending against external threats that aim to exploit vulnerabilities.

> **Software Safety** is to ensure that **the software** is not harmful to **others, other systems, other environments, etc.** 
> 
> **Software Security** is to ensure that **others, other systems, other environments, etc.**, are not harmful to **the software**.
{: .prompt-tip }

## What is Security By Design?

- Security by design is an approach that builds a system with security in mind right **from the beginning**.
  - A proactive approach to security
  - focuses on incorporating security measures throughout the development and implementation process

- Consider security throughout the SDLC (software development life cycle)

![](https://i.postimg.cc/NGPcB0xf/sbd.png){: .w-65 .shadow .rounded-10 }
_Introducing Security to SDLC (System Development Life Cycle)_

## Security Design Principles

>Principles: a fundamental truth or proposition serving as the foundation for belief or action


We define a security design principle as:
- a declarative statement made with the intention of guiding security design decisions in order to meet the goals of a system

### Assign the least privilege possible

- Why?
  - Broad privileges allow malicious or accidental access to protected resources
- Principle
  - Limit privileges to the minimum for the context
- Tradeoff
  - Less convenient; less efficient; more complexity
- Example
  - Run server processes as their own users with exactly the set of privileges they require 

### Separate responsibilities

- Why?
  - Achieve control and accountability; limit the impact of successful attacks; make attacks less attractive
- Principle
  - Separate and compartmentalise responsibilities and privileges
- Tradeoff
  - Development and testing costs; operational complexity: Troubleshooting more difficult
- Example
  - "Payments" module administrators have no access to or control over "Orders" module features 

### Trust cautiously

- Why?
  - Many security problems are caused by inserting malicious intermediaries in communication paths
- Principle
  - Assume unknown entities are untrusted; have a clear process to establish trust; validate who is connecting
- Tradeoff
  - Operational complexity (particularly failure recovery); reliability; some development overhead
- Example
  - Don't accept untrusted RMI connections; use client certificates; credentials or network controls, scan OSS (Open Source Software)

### Simplest solution possible

- Why?
  - Security requires understanding of design: complexity is rarely understood; simplicity allows analysis
- Principle
  - Actively design for simplicity; avoid complex failure modes, implicit behaviour, unnecessary features,...
- Tradeoff
  - Hard decision on features and sophistication. It needs a serious design effort to be simple.
- Example
  - Does the system really need dynamic runtime configuration via a custom DSL? 


### Audit sensitive events

- Why?
  - Provide a record of activity; deter wrong doing; provide a log to reconstruct the past; provide a monitoring point
- Principle
  - Record all security significant events in a tamper-resistant store
- Tradeoff
  - Performance; operational complexity; dev cost
- Example
  - Record changes to "core" business entities in an append-only store with (user, ip, timestamp, entity, event)

### Fail securely & use secure defaults

- Why?
  - Default passwords, ports & rules are "open doors". Failure and restart states often default to "insecure"
- Principle
  - Force changes to security sensitive parameters. Think through failures: to be secure but recoverable
- Tradeoff
  - Convenience
- Example
  - Don't allow "SYSTEM/MANAGER" after installation
  - On failure don't disable or reset security controls

### Never rely upon obscurity

- Why?
  - Hiding things is difficult: someone is going to find them, accidentally if not on purpose
- Principle
  - Assume attacker with perfect knowledge, this forces secure system design
- Tradeoff
  - Designing a truly secure system takes time and effort
- Example
  -  Assume an attacker will guess a "port knock" network request sequence or a password obfuscation technique

### Implement defence in depth

- Why?
  - Systems do get attacked; breaches do happen; mistakes are made. So, we need to minimise the impact.
- Principle
  - Don't rely on a single point of security; secure every level; stop failures at one level propagating
- Tradeoff
  - Redundancy of policy; complex permission and troubleshooting; can make recovery difficult;
- Example
  - Access control in UI, services, database, OS

### Never invent security technology

- Why?
  - Security technology is difficult to create: avoiding vulnerabilities is difficult
- Principle
  - Don't create your own security technology: always use a proven component
- Tradeoff
  - Time to assess security technology; effort to learn it; complexity
- Example
  - Don't invent your own SSO mechanism; secret storage or crypto libraries; choose proven components

### Find the weakest link

- Why?
  - "Paper Wall" problem: common when focus is on technologies not threats
- Principle
  - Find the weakest link in the security chain and strengthen it: repeat! (Threat modelling) 
- Tradeoff
  - Significant effort required; often reveals problems at the least convenient moment!
- Example
  - Data privacy threat: encrypted communication but with unencrypted database storage and backups

