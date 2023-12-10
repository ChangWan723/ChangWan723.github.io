---
title: Symbolic Model Checking
date: 2023-11-05 18:51:00 UTC
categories: [ (CS) Learning Note, Automated Software Verification ]
tags: [computer science, software verification, Model Checking, LTL]
pin: false
---

In the realms of computer science and formal verification, Symbolic Model Checking stands as a crucial technique, especially in verifying complex systems like digital circuits and software programs. 

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Symbolic Model Checking?](#what-is-symbolic-model-checking)
    * [The Birth and Evolution of Symbolic Model Checking](#the-birth-and-evolution-of-symbolic-model-checking)
    * [Key Components of Symbolic Model Checking](#key-components-of-symbolic-model-checking)
  * [Explicit versus Symbolic Modelling of Software Systems](#explicit-versus-symbolic-modelling-of-software-systems)
  * [Symbolic Modelling of Systems](#symbolic-modelling-of-systems)
    * [Represent a System Symbolically](#represent-a-system-symbolically)
      * [Boolean Connectives and Notation](#boolean-connectives-and-notation)
      * [Symbolic Representation of Systems](#symbolic-representation-of-systems)
      * [Example: Noughts and Crosses](#example-noughts-and-crosses)
    * [Represent a Program Symbolically](#represent-a-program-symbolically)
      * [Boolean Programs](#boolean-programs)
    * [How to Represent a Boolean Program?](#how-to-represent-a-boolean-program)
      * [Example of Encoding assignments Trans](#example-of-encoding-assignments-trans)
      * [Example of Encoding if-then-else statements Trans](#example-of-encoding-if-then-else-statements-trans)
      * [Example of Encoding while statements Trans](#example-of-encoding-while-statements-trans)
      * [Trans of Previous Example](#trans-of-previous-example)
      * [How do We Encode `PC = Li` as A Boolean Formula?](#how-do-we-encode-pc--li-as-a-boolean-formula)
  * [Symbolic Model Checking](#symbolic-model-checking)
    * [A Simple Example](#a-simple-example)
    * [Computing Reachable States](#computing-reachable-states)
    * [Checking Safety Properties](#checking-safety-properties)
    * [Checking LTL Properties](#checking-ltl-properties)
  * [BDDs and Symbolic Model Checking](#bdds-and-symbolic-model-checking)
<!-- TOC -->

---

## What is Symbolic Model Checking?

Symbolic Model Checking is an approach used in the field of formal verification to prove or disprove properties of a system (often hardware or software) modeled formally with mathematical objects. Unlike traditional model checking that enumerates all possible states of a system, symbolic model checking uses mathematical symbols to represent and explore state spaces efficiently.

### The Birth and Evolution of Symbolic Model Checking

Symbolic Model Checking emerged in the 1980s as a response to the limitations of explicit state model checking. The primary challenge was the state explosion problem, where the number of states grows exponentially with the number of components in a system. Symbolic approaches, particularly those utilising Binary Decision Diagrams (BDDs), offer a way to compactly represent and manipulate large state spaces.

### Key Components of Symbolic Model Checking

1. **Model Representation**: The system model is often represented using Kripke structures or similar formalisms, encompassing states and transitions.

2. **Property Specification**: Properties to be verified are specified using temporal logics like CTL (Computation Tree Logic) or LTL (Linear Temporal Logic).

3. **Symbolic Algorithms**: Algorithms that manipulate symbolic representations, like BDDs, to explore possible states and verify the specified properties.

## Explicit versus Symbolic Modelling of Software Systems

**Explicit Modelling:**

- **transition systems** model software systems **explicitly**
  - each node represents a system state
  - each edge represents an atomic state change
- this suffers from **state space explosion**
  - the number of states grows exponentially with the number of variables
  - a system with n Boolean variables can have 2^n states
- so, transition systems are inadequate to model systems with more than a few variables

**Symbolic Modelling**:

- in contrast, **symbolic model checking** avoids explicitly constructing the state space of a system, and instead represents it as a formula in propositional logic
  - this allows for **compact representations**, e.g. using **Binary Decision Diagrams (BDDs)**

## Symbolic Modelling of Systems

### Represent a System Symbolically

#### Boolean Connectives and Notation

- **boolean connectives**: ¬ (not), ∨ (or), ∧ (and), → (implies), ↔ (if and only if, means that the result is `true` when the values of the **two variables are the same**, and `false` when **they are different**.)
- V = {v1, . . . , vn} set of **boolean variables**


#### Symbolic Representation of Systems

![](https://i.postimg.cc/g0y6NdLS/smc1.png){: .w-55 .shadow .rounded-10 }

#### Example: Noughts and Crosses

![](https://i.postimg.cc/2yScC0fY/smc2.png){: .w-55 .shadow .rounded-10 }

- **Variables and Domain**:
  - Variables: `V = {x1, . . . , x9, t}`. Domain(value of Variables):`D = { –, X, O, A, B }`
  - variable `xi` encodes the content of cell `i`
    - `–` stands for empty cell
    - `X` stands for marked by player A
    - `O` stands for marked by player B
  - variable `t` encodes the player who moves next (A or B)

> An explicit representation of the state space would use ≈ 40000 states!
{: .prompt-warning }

- **Initial configurations**:
  - Init: `(x1 = −) ∧ (x2 = −) ∧ . . . ∧ (x9 = −) ∧ (t = A ∨ t = B)`
  - (all cells are **empty** and either player A or player B can start)

- **Transition relation**:
  - (either player A or player B can move, if it is her turn, and mark one of the empty cells)

![](https://i.postimg.cc/TYDdx02g/smc3.png){: .w-55 .shadow .rounded-10 }

- **Winning condition for player A (B is similar)**:

![](https://i.postimg.cc/5tcpGx78/smc4.png){: .w-55 .shadow .rounded-10 }

### Represent a Program Symbolically

```
int x,y = 0,0;
while (true)
  x,y = (x+1) mod 3, x+1;
```

- **variables**: `x`, `y` with domain `int` (bounded!)

![](https://i.postimg.cc/ZY3N78ks/smc5.png){: .w-55 .shadow .rounded-10 }

#### Boolean Programs

- in the previous examples, the **domains(values)** for the variables are **not Boolean**
- to encode `Init` and `Trans` as _propositional logic formulas_, we would need to encode each program variable using several **boolean variables**
- to avoid doing this (for convenience), we restrict to **Boolean programs**:
  - only **Boolean variables**
  - only **ASSIGNMENT**, **IF**, and **WHILE** statements
  - no procedure calls

### How to Represent a Boolean Program?

Example of a Boolean Program:
```
begin
L1 : x1 = false;
L2 : while (x1 ∧ x2) do
L3 :    x1 = true;
L4 : endwhile;
L5 : if (x1 ∨ x2) then
L6 :    x1 = x1 ↔ x2;
L7 : else
L8 :    x2 = x1 ↔ x2;
L9 : endif
L10 :
end
```
(`L1 - L10` is program counters)

> Program counters `L` **represents** the position **where the previous statement finished executing**, it does not mean that the next statement is going to be executed.
> 
> For example: 
>   - `L7` means: `x1 = x1 ↔ x2` has finished executing, the next step should break `if` directly. So, the next of `L7` **should be `L10`**!
>   - `L7` **doesn't** means: `else` is going to be executed. So, the next of `L7` **should not be `L8`**!
> 
> **It is important to understand this description. Otherwise, looking at the following Encoding example is going to be confusing.**
{: .prompt-warning }

- **variables**:
  - `V = {x1, x2, PC}`
- **domain**:
  - `D = {F, T, L1, . . . , L10}`
  - still not Boolean!
- **transitions**:
  - Trans = ?

It seems hard to get `Trans`, so let's look at a few simple examples first:

#### Example of Encoding assignments Trans

![](https://i.postimg.cc/CKfJgYFH/smc6.png){: .w-55 .shadow .rounded-10 }

#### Example of Encoding if-then-else statements Trans

![](https://i.postimg.cc/nh9PGNX5/smc7.png){: .w-55 .shadow .rounded-10 }

#### Example of Encoding while statements Trans

![](https://i.postimg.cc/yN0jxZdp/smc8.png){: .w-55 .shadow .rounded-10 }

#### Trans of Previous Example

![](https://i.postimg.cc/0Q1cKtGD/smc9.png){: .w-55 .shadow .rounded-10 }


#### How do We Encode `PC = Li` as A Boolean Formula?

Representation on the previous slide is **still not a Boolean formula**! We need to encode `PC = Li` as a boolean formula.

- assume the values of the program counter (L1, . . . , L10 in the previous example) can be represented using n bits (4 in the example)
- use Boolean variables `pc0, . . . , pc_n−1` to encode the value of the program counter
  - e.g. use variables `pc0, pc1, pc2, pc3` to encode integers `i ∈ {1, . . . , 10}` (and thus the formula `PC = Li`). For example: `i` = 6 (i.e. `0110` in binary), the formula `PC = L6` is encoded as `(pc3 ↔ 0) ∧ (pc2 ↔ 1) ∧ (pc2 ↔ 1) ∧ (pc3 ↔ 0)`

> Similar encodings can be done for programs with variables of types other than Boolean!
{: .prompt-tip }

## Symbolic Model Checking

### A Simple Example

![](https://i.postimg.cc/43N2H6L3/smc13.png){: .w-55 .shadow .rounded-10 }

![](https://i.postimg.cc/D0WtJrzG/smc14.png){: .w-55 .shadow .rounded-10 }

### Computing Reachable States

![](https://i.postimg.cc/jjbW5CCZ/smc10.png){: .w-55 .shadow .rounded-10 }

### Checking Safety Properties

![](https://i.postimg.cc/XqC3dczF/smc11.png){: .w-55 .shadow .rounded-10 }

### Checking LTL Properties

![](https://i.postimg.cc/8PdcYNZv/smc12.png){: .w-55 .shadow .rounded-10 }

## BDDs and Symbolic Model Checking

- [binary decision diagrams](/posts/Binary-Decision-Diagrams/) (BDDs) are a canonical form to represent **Boolean functions**
  - often more compact than traditional normal forms
  - can be manipulated efficiently
- reachable state space can be represented as a BDD
- property verification uses iterative computations on the reachable state space
