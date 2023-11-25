---
title: Hoare Logic
date: 2023-11-25 21:48:00 +0530
categories: [ (CS) Learning Note, Automated Software Verification ]
tags: [computer science, software engineering, software verification, Model Checking]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Foreword](#foreword)
    * [Logic](#logic)
    * [Completely Convincing Arguments: Logical Fallacy](#completely-convincing-arguments-logical-fallacy)
    * [Completely Convincing Arguments: Sound Inferences](#completely-convincing-arguments-sound-inferences)
  * [What is Hoare Logic?](#what-is-hoare-logic)
    * [Preconditions](#preconditions)
    * [Postcondition](#postcondition)
    * [Hoare Triples](#hoare-triples)
      * [Some Examples of Hoare Triples](#some-examples-of-hoare-triples)
  * [Hoare Logic](#hoare-logic)
    * [Hoare Logic: Axioms](#hoare-logic-axioms)
    * [Hoare Logic: Assignment Examples](#hoare-logic-assignment-examples)
    * [Hoare Logic: Rules of Inference](#hoare-logic-rules-of-inference)
      * [consequence](#consequence)
      * [composition](#composition)
      * [conditionals](#conditionals)
<!-- TOC -->

---

## Foreword

### Logic

We can prove correctness of our algorithms (and programs) if we:
- understand what correctness means (i.e. the exact specification)
- can give a completely convincing argument that our code conforms to the correctness specification.


Definition, according to The Chambers Dictionary (TCD):
- logic /loj’ik/ (noun)
  1. The science and art of reasoning correctly
  2. The science of the necessary laws of thought

### Completely Convincing Arguments: Logical Fallacy

> If each man had a definite set of rules of conduct by which he regulated his life he would be no better than a machine. But there are no such rules, so men cannot be machines.
> 
> --- A. M. Turing, Computing Machinery and Intelligence, 1950.

More formally stated as a _rule of inference_:

![](https://i.postimg.cc/yYQnPWdk/hl1.png){: .w-55 .shadow .rounded-10 }

This is an example of a **logical fallacy** – an **incorrect form of argument** where the premises (stated above the bar) **do not entail the conclusion** (stated below the bar).

###  Completely Convincing Arguments: Sound Inferences

- A rule of inference is _sound_ if the conclusion is a logical consequence of the premises.
- In a sound rule of inference it is impossible for all the premises to be true and the conclusion to be false. For example:

![](https://i.postimg.cc/ZnsW2WCq/hl2.png){: .w-55 .shadow .rounded-10 }

- Sound arguments can be constructed this way to prove theorems from axioms (self-evident statements that require no proof).
- A formal proof can be stored in a file and checked by a computer.

## What is Hoare Logic?

- Introduced by Sir Tony Hoare in 1969.
- Followed in the footsteps of R. W. Floyd (who devised a similar system for flowcharts in 1967).
- Allows us to formally prove that a program satisfies its specification (contract). 

> Hoare logic provides a way of formally defining the semantics of a programming language (so-called **axiomatic semantics**).
{: .prompt-tip }
 
- Hoare logic is a logic for reasoning about programs. It involves:
  - a few basic axioms
  - some sound rules of inference
- To state and prove properties of programs using Hoare logic we need to understand the following terms:
  - **preconditions**
  - **postconditions**
  - **Hoare triples**
  - **invariants**
  - **variants**

### Preconditions

- A **precondition** is a property that has to be true just before a program is executed (i.e. just before an operation is performed).
- As a contract specification, a precondition can be treated as an _assumption_ by the programmer.
- An (informal) example:
  - “The initial values of x are in the range [−10, 60].”
- Intuitively, if a program receives inputs (i.e. starts executing in a state) which **violates** the precondition, then it has **no obligation to do anything sensible**.

### Postcondition

- A **postcondition** is a property that has to be true once the program is executed and terminates.
- As a contract specification, a postcondition can be treated as an _requirement_ (i.e. a contractual obligation to be fulfulled).
- An (informal) example:
  - “The array will be stored in non-decreasing order when the program finishes.”
- Intuitively, a program promises to achieve the postcondition (provided that the precondition is met). [It is also usually desirable for programs to terminate.]

### Hoare Triples

- A Hoare triple has the form: `{𝑃𝑅𝐸} 𝑃𝑟𝑜𝑔 {𝑃𝑂𝑆𝑇 }`
- where
  - `𝑃𝑅𝐸` is the precondition
  - `𝑃𝑂𝑆𝑇` is the postcondition
  - `𝑃𝑟𝑜𝑔` is the program.
- A Hoare triple states that `𝑃𝑟𝑜𝑔` will establish `𝑃𝑂𝑆𝑇` on completion, provided `𝑃𝑅𝐸` holds before execution of `𝑃𝑟𝑜𝑔`.

#### Some Examples of Hoare Triples

`{true} x:=10 {𝑥 > 0}`

`{true} x:=10 {𝑥 = 10}`

`{𝑥 > 2} x:=x+1 {𝑥 ≤ 3}`

`{true} x:=x+1 {???}`

How can we express that the value of `𝑥` has increased by executing the program statement `x:=x+1`?

`{true ∧ 𝑥 = 𝑣} x:=x+1 {𝑥 = 𝑣 + 1}`

where 𝑣 is a fresh variable.

## Hoare Logic

### Hoare Logic: Axioms

![](https://i.postimg.cc/mkp1nBjB/hl6.png){: .w-55 .shadow .rounded-10 }

- Two **axioms** of Hoare Logic:
  1. `{P} skip {P}`: This is a Hoare triple indicating that performing the `skip` operation (which does nothing) does not change the truth of the assertion `P`. Here, `P` is the precondition, `skip` is the program statement, and `P` is also the postcondition. It implies that if `P` is true before performing `skip`, it remains true afterwards.
  2. `{P₀} x := E {P}`: This is another Hoare triple, describing an assignment operation. `x := E` means the variable `x` is assigned the value of the expression `E`. In this axiom, `P₀` is a special precondition that represents the state of P but with every free occurrence of `x` (that is, occurrences of `x` not bound by other variables or function scopes) replaced by the expression `E`. If `P₀` is true before the assignment, then `P` will be true after the assignment.

### Hoare Logic: Assignment Examples

In practice, to check a Hoare triple `{𝑃𝑅𝐸} x:=E {𝑃𝑂𝑆𝑇}` we check `𝑃𝑅𝐸 → 𝑃𝑂𝑆𝑇0`. Examples:

`{𝑥 + 1 = 3} x:=x+1 {𝑥 = 3}`

`{𝑥 + 1 = 3 ∧ 𝑦 = 0} x:=x+1 {𝑥 = 3}`

`{𝑦 + 𝑧 = 5} x:=y+z {𝑥 ≥ 5}`

### Hoare Logic: Rules of Inference

#### consequence

![](https://i.postimg.cc/MHGT71zG/hl3.png){: .w-55 .shadow .rounded-10 }

#### composition

![](https://i.postimg.cc/85X2JvcD/hl4.png){: .w-55 .shadow .rounded-10 }

- Suppose we want to prove: `{𝑦 = 𝑧} x:=z+1; z:=y+1 {𝑧 = 𝑥}`
- Let `𝑅1 = 𝑦 + 1 = 𝑥`, so we need to prove (left sub-goal):`{𝑦 = 𝑧} x:=z+1 {𝑦 + 1 = 𝑥}`  (check `𝑦 = 𝑧` → `𝑦 + 1 = 𝑧 + 1`)
- And the right sub-goal: `{𝑦 + 1 = 𝑥} z:=y+1 {𝑧 = 𝑥}` (check `𝑦 + 1 = 𝑥` → `𝑦 + 1 = 𝑥`)

#### conditionals

![](https://i.postimg.cc/kX2TXZW2/hl5.png){: .w-55 .shadow .rounded-10 }


