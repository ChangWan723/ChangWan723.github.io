---
title: Automated Software Verification
date: 2023-10-01 19:39:00 +0530
categories: [(CS) Learning Note, Automated Software Verification]
tags: [computer science, software engineering, software verification]
pin: false
---

This module aims is to give an understanding of Automated Software Verification:
- key principles and techniques
- use of a range of verification tools
- both formal verification and testing covered

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Automated Verification？](#what-is-automated-verification)
    * [Model checking](#model-checking)
    * [Deductive program verification](#deductive-program-verification)
    * [Testing](#testing)
  * [Validation versus Verification](#validation-versus-verification)
  * [Software Verification Approaches](#software-verification-approaches)
  * [Related Blogs](#related-blogs)
<!-- TOC -->

---

## What is Automated Verification？

- Verification amounts to checking that a (software) system behaves as intended. In this case the system is said to be correct.
- Wide range of automated verification techniques:
  - model checking
  - deductive verification
  - symbolic execution
  - automated testing
  - ...
- Some of these provide guarantees on correctness (i.e. that the system always behaves as intended)

### Model checking

- Explicit state model checking
  - modelling software systems;
  - the temporal logic LTL;
  - model checking LTL
- Symbolic model checking
  - symbolic modelling of software
  - Binary Decision Diagrams
  - the [NuXMV model checker](https://nuxmv.fbk.eu)
- Bounded model checking
  - basic concepts of BMC
  - SAT solvers
  - the [CBMC model checker](https://www.cprover.org/cbmc/)

### Deductive program verification

- Hoare logic
- loop termination
- [Frama-C](https://frama-c.com/): use WP plugin for verification

### Testing

- types of testing
- automated software testing
  - regression testing, fuzz testing
  - symbolic and concolic testing


## Validation versus Verification

- validation: 
  - check that the program we are building fulfills its intended purpose (meets the user needs)
  - Ensure that the **specification** of the software system **satisfy the requirements** of the stakeholders (customers, users, administrators, ...)
  - _Are we building the right product?_
  - the _specification_ is correct (**validation**)

- verification: 
  - check that the program meets its requirements and design specifications
  - Ensure that the **finished** product **satisfies the specification**.
  - _Are we building the product right?_
  - the program meets its _specification_ (**verification**)

## Software Verification Approaches

- peer review
  - manual code inspection, no software execution
  - subtle errors (algorithm design, concurrency) difficult to detect
- testing
  - software is executed to catch errors
  - amounts to 30-50% of development costs
  - effective in the early stages but time-consuming in later stages
  - difficult for concurrent or distributed systems
  - only some executions are explored
- simulation
  - performed on an abstraction, or model, of the actual program
  - only some behaviours are explored

<br>

- **formal verification approaches offer correctness guarantees**
  - deductive verification:
    - checking correctness properties of either programs or their models
    - theorem provers used to prove correctness (e.g. invariant properties)
    - not fully automatic, but several good tools exist, e.g. KeY, Frama-C
    - works on infinite state systems
  - model checking:
    - checking properties of either models or code
    - performs exhaustive exploration of all possible behaviours
    - works only on systems with finite state spaces
    - fully automatic

## Related Blogs

- [Modelling Programs with Transition Systems](/posts/Transition-Systems/)
- [Linear Temporal Logic (LTL)](/posts/Linear-Temporal-Logic/)
- [Büchi Automaton](/posts/Büchi-Automaton/)
- [Explicit State Model Checking](/posts/Explicit-State-Model-Checking/)
- [Symbolic Model Checking](/posts/Symbolic-Model-Checking/)
- [Binary Decision Diagrams](/posts/Binary-Decision-Diagrams/)
- [NuSMV Model Checker](/posts/NuSMV-Model-Checker/)
- [SAT Problem and DPLL](/posts/SAT-Solvers/)
- [Bounded Model Checking](/posts/Bounded-Model-Checking/)
- [Hoare Logic](/posts/Deductive-Verification/)
