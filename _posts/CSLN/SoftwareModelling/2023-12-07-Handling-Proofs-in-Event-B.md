---
title: Proof-Based Verification in Event-B
date: 2023-12-07 16:16:00 UTC
categories: [ (CS) Learning Note, Software Modelling and Design ]
tags: [computer science, Event-B ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Validation and Verification](#validation-and-verification)
    * [Validation](#validation)
    * [Verification](#verification)
      * [What is Formal Verification?](#what-is-formal-verification)
  * [Proof Obligations (PO)](#proof-obligations-po)
    * [Sequent of PO](#sequent-of-po)
    * [Some Components of PO in Event-B](#some-components-of-po-in-event-b)
      * [Invariant Preservation of PO](#invariant-preservation-of-po)
    * [Substitution of PO](#substitution-of-po)
    * [Using Event Parameters in PO](#using-event-parameters-in-po)
    * [Examples of PO](#examples-of-po)
      * [Example 1](#example-1)
      * [Example 2](#example-2)
  * [Examples of Addressing an unproved Proof Obligation (PO)](#examples-of-addressing-an-unproved-proof-obligation-po)
    * [Example of Event 1](#example-of-event-1)
      * [unprovable](#unprovable)
      * [Try strengthening the hypotheses](#try-strengthening-the-hypotheses)
      * [Try weakening the Goal](#try-weakening-the-goal)
    * [Example of Event 2](#example-of-event-2)
      * [unprovable](#unprovable-1)
      * [Try weakening the Goal](#try-weakening-the-goal-1)
      * [Try strengthening the hypotheses](#try-strengthening-the-hypotheses-1)
      * [Modify the guard](#modify-the-guard)
      * [Add another invariant](#add-another-invariant)
<!-- TOC -->

---

## Validation and Verification

### Validation

**Definition**: Validation is the process of evaluating the final product to ensure it meets the business needs and requirements of the end-users. It is about ensuring that the software does what the user really requires.

- **Requirements validation**:
   - The extent to which (informal) requirements satisfy the needs of the stakeholders
- **Model validation**:
   - The extent to which (formal) model accurately captures the (informal) requirements

### Verification

**Definition**: Verification is the process of evaluating the intermediate products of a software development lifecycle to ensure that the software meets the specified requirements at each stage.

- **Model verification**:
   - The extent to which a model correctly **maintains invariants** or refines another (more abstract) model
   - Measured, e.g., by degree of validity of proof obligations

- **Code verification**:
   - The extent to which a program correctly implements a specification/model

#### What is Formal Verification?

- Formal verification is the act of **proving or disproving** the correctness of a formal model with respect to a certain set of **anticipated properties**, using **mathematical techniques**.

- It is important to answer the following questions:
  - How do we describe the system?
  - How do we express the properties?

## Proof Obligations (PO)

- Proof Obligations (PO) are **mathematical theorems** derived from a **formal model** (or program)
- PO are used to verify properties of models such as **invariant preservation**.
- A PO is a **sequent** of the form `Hypotheses ⊢ Goal`
  - This means we should prove the **goal** while assuming that the **hypotheses** are true.
  - Example 
    - `x < MAX` ⊢ `x+1 ≤ MAX`
    - Prove that `x+1 ≤ MAX` if `x < MAX`

- In addition to mathematical operators and rules, the validity of a PO could be derived from deductive rules of **logic and set theory**. For example:
  - `S ⊆ T` ⇔ `( ∀x · x ∈ S ⇒ x ∈ T )`
  - `X ∈ ( S ∪ T)` ⇔ `( x ∈ S ∨ x ∈ T )`

### Sequent of PO

- A **sequent** consists of **Hypotheses** (`H`) and a **Goal** (`G`), written `H ⊢ G`
- A sequent is valid if `G` follows from `H`
- Event-B **proof obligations** (PO) are **sequent** of the form: `Assumptions ⊢ Goal`

### Some Components of PO in Event-B

- **Well-definedness (WD)**
  - e.g, avoid division by zero, partial function application
- **Invariant preservation (INV)**
  - each event maintains invariants
- **Guard strengthening (GRD)**
  - Refined event only is possible when abstract event is possible
- **Simulation (SIM)**
  - update of abstract variable correctly simulated by update of concrete variable

#### Invariant Preservation of PO

- Assume: 
  - variables `v` and invariant `Inv`
- Assume event of this form:
  - `Ev` = **any** `x` **when** `Grd` **then** `v := Exp` **end**
- To prove `Ev` preserves `Inv`: 
  - prove that the following sequent is valid: 
    - INV: `Inv , Grd` ⊢ `Inv[ v := Exp ]`
    - That is, prove that the **updated invariant**, `Inv[ v := Exp ]`, follows from the **invariant**, `Inv`, and the **guard**, `Grd`

### Substitution of PO

- Replace all **free** occurrences of variable `x` by expression `E` in predicate `P`:
  - P [ x:=E ]
- Example:
  - `(0<n ∧ n≤10)[n:=7]` ⇔  `0<7 ∧ 7≤10`
- Bound variables are quantified variables:
  - `(∀n · n>0 ⇒ 1≤n)[n:=7]` ⇔  `(∀n · n>0 ⇒ 1≤n)`
  – Here `n` is **bound** in the predicate so is **not substituted**.
- **Free variables** are variables that appear in P that are **not bound** within `P`

### Using Event Parameters in PO

- Event has the form:
  - `Ev` = **any** `x` **where** `P(x,v)` **then** `v := exp(x,v)` **end**
  - INV: `I(v), P(x,v)` ⊢ `I( exp(x,v) )`

### Examples of PO

#### Example 1

- **Invariant**: 
  - `x ≤ MAX`
- **Event**:
  - `Inc` = **when** `x<MAX` **then** `x := x+1` **end**
- **To prove** `Ev` preserves `x ≤ MAX` we have this PO:
  - PO: `x ≤ MAX, x<MAX` ⊢ `x+1 ≤ MAX`
    - Inv: `x ≤ MAX`
    - GRD: `x < MAX`

#### Example 2

- Invariant: 
  - `x+y = C`
- Event:
  - `x , y := x+1 , y−1`
- PO for example:
  - `x+y=C` ⊢ `(x+1) + (y-1) = C`

## Examples of Addressing an unproved Proof Obligation (PO)

![](https://i.postimg.cc/0jZ47smz/hp1.png){: .w-80 .shadow .rounded-10 }
_Invariants_

### Example of Event 1

#### unprovable
![](https://i.postimg.cc/0jpVCqwY/hp2.png){: .w-80 .shadow .rounded-10 }
_an unproved Proof Obligation_

- We need to prove the Goal, which is `u ∈ in ∪ out`. But it is unprovable now.
- To change a PO to **make it provable**, we can:
  - **Strengthen** the hypotheses, or
  - **Weaken** the goal

#### Try strengthening the hypotheses

- we can **strengthen** the hypotheses by adding **invariants** or **guards** to the model.
  - adding **guards** to events: `u ∈ in ∪ out `

![](https://i.postimg.cc/Yq89Cnn0/hp3.png){: .w-80 .shadow .rounded-10 }

- In this case, it is not clear how an invariant would help, so we add a **guard**.
- However, this guard means Register is never enabled!
  - `inv2`, `inv3` and `grd2` together make `grd3` false!
  - So, it is **not a good solution**

#### Try weakening the Goal

- We can **weakening** the goal by adding **actions** to the model.
  - adding **actions** to events: `out ≔ out ∪ {u} `

![](https://i.postimg.cc/k5kTkyWX/hp4.png){: .w-80 .shadow .rounded-10 }

- This results in a weaker goal:
  - It is easier to prove that `u ∈ out ∪ {u}` than `u ∈ out`

### Example of Event 2

#### unprovable

![](https://i.postimg.cc/RFQdYJ9W/hp5.png){: .w-80 .shadow .rounded-10 }
_an unproved Proof Obligation_

- Here the guard is weak, so the hypotheses are not strong enough to prove the goal

#### Try weakening the Goal

![](https://i.postimg.cc/d00TF787/hp6.png){: .w-80 .shadow .rounded-10 }

- Here, act3 has resulted in a weaker goal that is provable
- However, this now means that any user can enter and will automatically get registered when they enter!
- So, this does not satisfy the requirements. It is **NOT a good solution**.

#### Try strengthening the hypotheses

![](https://i.postimg.cc/NGR8pHbY/hp7.png){: .w-80 .shadow .rounded-10 }

- This guard is strong enough to prove the PO
- But it allows a user already in the building to enter!
- The guard needs to be stronger to reflect our assumption that only users who are outside can enter

#### Modify the guard

![](https://i.postimg.cc/59k3HVPQ/hp8.png){: .w-80 .shadow .rounded-10 }

- Now, the hypotheses is not strong enough
- We need a hypothesis that says if **u is out then u is registered**
- Should this be an additional guard or an invariant?
- Make it an invariant **because this is a property of all registered users, not just the particular user who is entering**

#### Add another invariant

![](https://i.postimg.cc/SNchQkqk/hp9.png){: .w-80 .shadow .rounded-10 }

- Adding the invariant inv3 makes the PO provable
- And it matches our commonsense understanding
