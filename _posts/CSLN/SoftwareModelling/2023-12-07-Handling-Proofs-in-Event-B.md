---
title: Handling Proofs in Event-B
date: 2023-12-07 16:16:00 UTC
categories: [ (CS) Learning Note, Software Modelling and Design ]
tags: [computer science, Event-B ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Sequent](#sequent)
  * [Invariant Preservation PO](#invariant-preservation-po)
    * [An Example](#an-example)
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

## Sequent

- A **sequent** consists of **Hypotheses** (`H`) and a **Goal** (`G`), written `H ⊢ G`
- A sequent is valid if `G` follows from `H`
- Event-B **proof obligations** (PO) are **sequent** of the form: `Assumptions ⊢ Goal`

## Invariant Preservation PO

- Assume: variables `v` and invariant `Inv`
- Assume event of this form:
  - `Ev` = any `x` when `Grd` then `v := Exp` end
- To prove `Ev` preserves `Inv`: prove that the following sequent is valid: 
  - `INV: Inv , Grd ⊢ Inv[ v := Exp ]`
- That is, prove that the **updated invariant**, `Inv[ v := Exp ]`, follows from the **invariant**, `Inv`, and the **guard**, `Grd`

### An Example

- Invariant: x ≤ MAX
- Event:
  - `Inc` = when `x<MAX` then `x := x+1` end
- To prove `Ev` preserves `x ≤ MAX` we have this PO:
  - PO: `x ≤ MAX, x<MAX ⊢ x+1 ≤ MAX`
    - Inv: `x ≤ MAX`
    - GRD: `x < MAX`

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
