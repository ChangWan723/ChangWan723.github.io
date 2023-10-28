---
title: LTL Model Checking
date: 2023-10-27 19:02:00 +0530
categories: [ (CS) Learning Note, Automated Software Verification ]
tags: [ computer science, software engineering, software verification, Büchi Automaton, LTL, Transition Systems]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Model Checking using Automata](#model-checking-using-automata)
    * [From LTL to Automata](#from-ltl-to-automata)
    * [One of the Properties of Automata](#one-of-the-properties-of-automata)
    * [Use the Properties of Automata to Do Model Checking](#use-the-properties-of-automata-to-do-model-checking)
      * [Example 1](#example-1)
      * [Example 2](#example-2)
    * [Benefits and Limitations of Explicit State Model Checking](#benefits-and-limitations-of-explicit-state-model-checking)
<!-- TOC -->

---

## Model Checking using Automata

Transition systems can be transformed into Büchi automata (Place `Prop` in the middle of the line in the opposite direction of the arrow):

![](https://i.postimg.cc/251R09t6/lmc1.png){: .w-55 .shadow .rounded-10 }

- The states of the automaton correspond to states of the transition system, plus one additional initial state.
- There is one transition from the new (and only!) initial state to all the states corresponding to initial states in the transition system.
- All other transitions of the automaton correspond to transitions in the transition system.
- The alphabet of the automaton is the set of all subsets of `Prop`, that is `P(Prop)`. (`Prop = {n1, n2, t1, t2, c1, c2}`)
- The labels on automaton transitions are inherited from the target states in the transition system.
- All automaton states are accepting. (So all runs will be accepting!)

---

**Question**: What are the words accepted by the resulting automaton?

**Answer**: Exactly those infinite sequences of sets of atomic propositions that occur along computation paths through the transition system!

**For example**:

- atomic propositions: `Prop = {n1, n2, t1, t2, c1, c2}`
- `{n1, n2} → {t1, n2} → {c1, n2} → {n1, n2} → ...` occurs along a path through the transition system
- So, `{n1, n2}, {t1, n2}, {c1, n2}, {n1, n2},...` is accepted by the automaton

**Intuition**: runs of the automaton correspond to paths through the transition system.

---

- LTL formula involving `Prop` can also be transformed into an automaton over the alphabet `P(Prop)`.
  - infinite words over `P(Prop)` describe sequences of sets of atomic propositions
  - the resulting automaton should accept an infinite word precisely when the corresponding sequence satisfies the given formula
- since the model and the specification are both automata, we can use the theory of Büchi automata to do model-checking!


### From LTL to Automata

**For example (Mutual Exclusion)**:

Mutual Exclusion Property: `A G ¬(c1 ∧ c2)` (c1 and c2 are mutually exclusive)

![](https://i.postimg.cc/2y7wWCTb/lmc2.png){: .w-55 .shadow .rounded-10 }
_From LTL(`A G ¬(c1 ∧ c2)`) to Automata_

The above automaton accepts all infinite words not containing both c1 and c2 at the same time (i.e. within the same "symbol").

![](https://i.postimg.cc/8z6bddyg/lmc3.png){: .w-55 .shadow .rounded-10 }

---

A proper mutual exclusion system must also satisfy the **liveness property**: `A F c1` and `A F c2` (**critical state** `c1` and `c2` must be reachable)

![](https://i.postimg.cc/HxgHWtNY/lmc4.png){: .w-55 .shadow .rounded-10 }
_From LTL(`A F c1`) to Automata_

The above automaton accepts all infinite words eventually containing c1 as part of a "symbol".

### One of the Properties of Automata

Assuming the existence of automaton `A` and automaton `S`, and model satisfies the specification `L(A) ⊆ L(S)`, thus:

![](https://i.postimg.cc/5tszzph3/lmc5.png){: .w-55 .shadow .rounded-10 }

### Use the Properties of Automata to Do Model Checking

We can use the above one of **properties of automata** to do **model checking**:

#### Example 1

Check that the following automata `A` **satisfy mutual exclusivity** (`A G ¬(c1 ∧ c2)`):

![](https://i.postimg.cc/5NBRLpzh/lmc8.png){: .w-55 .shadow .rounded-10 }
_automaton `A` for a model_

---

**negation** of **mutual exclusion** (`A G ¬(c1 ∧ c2)`) is: `A F (c1 ∧ c2)`

---

We assume that the automata of `A F (c1 ∧ c2)` is `B`

![](https://i.postimg.cc/0QYB7VRb/lmc6.png){: .w-55 .shadow .rounded-10 }
_From LTL(`A F (c1 ∧ c2)`) to Automata `B`_

---

The above automaton means that only `c1 ∧ c2` can reach to **accepting states(final states)**. So, product automaton of `A ∩ B` will be:

![](https://i.postimg.cc/PqvwBVdJ/lmc7.png){: .w-55 .shadow .rounded-10 }
_Product automaton of `A ∩ B`, no accepting states(final states)_

---

Product automaton has **no accepting states**, hence does not accept any infinite word. 

Since the language accepted by the product automaton (`A ∩ B`) is **empty**. `L(A ∩ B) = ∅`, so, `L(A) ∩ L(B) = ∅`. 

`B` is the negation of `mutual exclusion`, Then, according to the properties of automata, `L(A) ⊆ mutual exclusion`.

So, automata `A` **satisfy mutual exclusivity** `A G ¬(c1 ∧ c2)`.


#### Example 2

Check that the following automata `A` **satisfy liveness property** (`A F c2`):

![](https://i.postimg.cc/5NBRLpzh/lmc8.png){: .w-55 .shadow .rounded-10 }
_automaton `A` for a model_

---

**negation** of **liveness property** (`A F c2`) is: `A G ¬c2`

---

We assume that the automata of `A G ¬c2` is `B`

![](https://i.postimg.cc/2S8ZB2R5/lmc9.png){: .w-55 .shadow .rounded-10 }
_From LTL(`A G ¬c2`) to Automata `B`_

---

The above automaton means that `¬c2` is **global**, or `c2` can't exist. So, product automaton of `A ∩ B` will be:

![](https://i.postimg.cc/9FSsSNm4/lmc10.png){: .w-55 .shadow .rounded-10 }
_Product automaton of `A ∩ B`, has accepting states(final states)_

---

Product automaton **has accepting states**, hence accept some infinite words.

Since the language accepted by the product automaton (`A ∩ B`) is **not empty**. `L(A ∩ B) ≠ ∅`, so, `L(A) ∩ L(B) ≠ ∅`.

`B` is the negation of `liveness property`, Then, according to the properties of automata, `L(A) ⊄ liveness property`.

So, automata `A` do **not satisfy liveness property** `A F c2`.

### Benefits and Limitations of Explicit State Model Checking

The above examples are **Explicit State Model Checking**.

> Explicit State Model Checking:
> 
> Explicit State Model Checking is a verification method that explores all possible states of a system to ensure it meets specified properties. It explicitly examines each state, but can be resource-intensive due to the state explosion problem.
{: .prompt-tip }

**Benefits:**
- automatic
- exhaustive
- produces counter-examples

**Limitations:**
- state explosion problem – partially addressed by **symbolic model checking**
- only works for finite-state systems
