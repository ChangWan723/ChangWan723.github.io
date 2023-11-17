---
title: Modelling Programs with Transition Systems
date: 2023-10-06 22:42:00 +0530
categories: [(CS) Learning Note, Automated Software Verification]
tags: [computer science, software engineering, software verification, Transition Systems]
pin: false
---

In the realm of theoretical computer science and formal methods, understanding system behavior is crucial. One of the foundational models used for this purpose is the **Transition System**.


---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction to Transition System](#introduction-to-transition-system)
    * [What is a Transition System?](#what-is-a-transition-system)
    * [Applications of Transition Systems](#applications-of-transition-systems)
  * [Transition Systems as Models of Systems](#transition-systems-as-models-of-systems)
  * [Transition Systems, Formally](#transition-systems-formally)
  * [Transition Systems as Models of Programs](#transition-systems-as-models-of-programs)
  * [Extracting Transition Systems from Concurrent Programs](#extracting-transition-systems-from-concurrent-programs)
  * [Why Use Transition Systems to Model Checking?](#why-use-transition-systems-to-model-checking)
<!-- TOC -->

---

## Introduction to Transition System

### What is a Transition System?

A transition system is a mathematical model that describes the behavior of systems in terms of states and the transitions between those states. It provides a structured way to represent and reason about system dynamics.

### Applications of Transition Systems

Transition systems are not just theoretical constructs; they have practical applications in various areas:

- **Automata Theory**: Finite state machines, foundational in formal languages and automata studies, can be viewed as specific transition systems.

- **Model Checking**: For verifying that software or hardware systems adhere to certain properties, transition systems model the system behavior, which is then checked using model checkers.

- **Concurrency Theory**: To analyze the behavior of systems operating concurrently, transition systems offer invaluable insights.

- **Operational Semantics**: For defining how programming languages operate, transition systems specify how program execution alters its state.

## Transition Systems as Models of Systems

- modelling a (software) system amounts to identifying:
  - its internal state at any given time,
  - which state(s) each state can transition into.

- informally, transition systems are graphs with nodes representing system states and edges representing atomic state changes
  - we label states with their relevant properties

![](https://i.postimg.cc/HshDGvG5/trans-1.png){: .w-55 .shadow .rounded-10 }
_simple traffic light model (paths through the graph correspond to system behaviours)_

We use a set _Prop_ of **atomic propositions** to describe basic properties of states.
- e.g. _Prop_ = {red, amber, green}

## Transition Systems, Formally

A **transition system** T over _Prop_ is given by:
- a finite set S of **states**
- a subset S0 ⊆ S of **initial states**
- a **transition relation** R ⊆ S × S between states
- a **valuation** V : S → P(Prop) giving, for each state s ∈ S, the atomic propositions which are true in that state:V(s) ⊆ Prop

<br>

**an Example:**

---

![](https://i.postimg.cc/HshDGvG5/trans-1.png){: .w-55 .shadow .rounded-10 }
_Prop = {red, amber, green}_

- set of states: S = { s0, s1, s2, s3 }
- set of initial states: { s0 }
- transition relation: { (s0, s1), (s1, s2), (s2, s3), (s3, s3), (s3, s0) }
  - notation: s0 → s1 , s1 → s2
- valuation V gives labelling of states with atomic propositions:
  - V(s0) = {red}
  - V(s1) = {red, amber}
  - V(s2) = {green} 
  - V(s3) = {amber}

---

## Transition Systems as Models of Programs

- states model **program states**
  - this includes **values** stored in all memory (stack/heap) plus the **program counter**
  - **program states** = **values** + **program** **counter**
- transitions model **atomic computation steps** (arising from executing atomic program statements)
- atomic propositions describe basic **properties of states** (e.g. values of program variables)
- **maximal paths** starting in an initial state correspond to possible **program executions**  
  - **maximal paths**: paths that cannot be extended any further

<br>

**an Example** of Extracting Models from a **Sequential** Program:

---

![](https://i.postimg.cc/63pS8Cnn/trans2.png){: .w-75 .shadow .rounded-10 }

> - **transitions** match **atomic** program statements (**single** program steps)
> - we can use atomic propositions to describe
>   - variable **values**, e.g. x=2 (true in s5, s6), y=2 (true in s3, s4),
>   - values of the **program counter**, e.g. PC = l2 (true in s2, s4, s6, s8).
{: .prompt-tip }

---

<br>

**an Example** of Extracting Models from **Concurrent** Programs:

---

![](https://i.postimg.cc/kG0RVF65/trans3.png){: .w-75 .shadow .rounded-10 }

> The above transition system is **nondeterministic**: there are several ways of proceeding from a given state (Because of **concurrency**).
{: .prompt-tip }

> We will look at concurrent programs:
> - several processes/threads executing **concurrently** and communicating through shared variables
> - usual sequential constructs: **assignments**, **if** , **while** , **skip** , . . .
> - concurrency primitives: e.g. **wait** , **lock** , **unlock** statements
{: .prompt-tip }

---

## Extracting Transition Systems from Concurrent Programs

Outline of general procedure:
1. annotate the entry and exit points of basic program statements with process counters
2. the states of the transition system are tuples consisting of:
  - the values of **global variables**
  - the values of **local process variables**
  - the values of **process counters**
3. transitions between states correspond to individual atomic steps in one of the processes.
4. atomic propositions are of the following forms
  - _var_ = _v_ with _var_ a program variable and _v_ a possible value for _var_
  - PCi = l with i a process and l the entry point of a statement in process i
    - so _n0_ in the diagram is a shorthand for _PC0 = n0_

## Why Use Transition Systems to Model Checking?

We can use a model of the program to **check some problems**.

<br>

**For example:**

---

The following program implements a simple **mutual exclusion protocol**:

![](https://i.postimg.cc/j2xZgfRv/trans4.png){: .w-75 .shadow .rounded-10 }

we represent such programs using transition systems:

![](https://i.postimg.cc/QxBpXmY1/trans5.png){: .w-75 .shadow .rounded-10 }
_V(s) = (turn, PC0, PC1)_

---

**We can use a model of this program to check:**
1. Can the program reach a state where both P0 and P1 are using the shared resource? (**This would violate mutual exclusion.**)
  - sufficient to check for a state **s** with (PC0 = c0, PC1 = c1) ∈V(s).
  - We can see by looking at the diagram that (PC0 = c0, PC1 = c1) ∈V(s) does not exist. So, **it doesn't violate mutual exclusion.**
2. Does there exist an execution of the program where **P1 never accesses the shared resource**? (**This would violate fairness.**)
  - sufficient to check if a path through the graph exists which starts in an initial state and never reaches states **s** with (PC1 = c1) ∈V(s).
  - We can see by looking at the diagram that the path exists. So, **P1 may never access the shared resource**.
  - **Fairness is conditionally satisfied**: it works under the assumption that both processes are functioning correctly and have roughly equal opportunities to run. If one process fails or is much slower, the other process can monopolize the critical section, leading to unfairness or even starvation.

> You might say, "I can get the answer straight away by looking at the code. And I don't need Transition Systems". This is because this mutual exclusion program is very simple. **Transition Systems are vital when it comes to more complex programs.**
{: .prompt-tip }
