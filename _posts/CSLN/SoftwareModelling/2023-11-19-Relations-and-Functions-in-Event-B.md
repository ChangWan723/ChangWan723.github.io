---
title: Relations and Functions in Event-B
date: 2023-11-19 20:20:00 +0530
categories: [ (CS) Learning Note, Software Modelling and Design ]
tags: [ computer science, software engineering, Event-B ]
pin: false
---

## Ordered Pairs and Cartesian Products

- An **ordered pair** is an element consisting of two parts: a **first** part and a **second** part.
  - An ordered pair with first part x and second part y is written: `x↦y`
- The **Cartesian product** of two sets is the **set of pairs** whose first part is in `S` and the second part is
  in `T`.
  - The Cartesian product of S with T is written: `S × T`

### Cartesian Products: Definition and Examples

![](https://i.postimg.cc/9MDgbT0R/rf1.png){: .w-80 .shadow .rounded-10 }

### Cartesian Product is a Type Constructor

- `S × T` is a new type constructed from types `S` and `T`.

- Cartesian product is the type constructor for ordered pairs.

Given `x ∈ S`, `y ∈ T`, we have `x ↦ y ∈ S × T`

![](https://i.postimg.cc/K895Wzdn/rf2.png){: .w-50 .shadow .rounded-10 }

### Sets of Order Pairs

- A database can be modelled as a set of ordered pairs:
  - `directory = { mary ↦ 287573, mary ↦ 398620, john ↦ 829483, jim ↦ 398620 }`

`directory` has type: `directory ∈ P(Person × PhoneNum)`

## Relations

- A **relation** is a set of **ordered pairs**.
- A relation is a common modelling structure, so Event-B has a special notation for it: `T ↔ S = P(T × S)`
  - So we can write: `directory ∈ Person ↔ PhoneNum`
- Do not confuse the arrow symbols:
  - `↔` combines two **sets** to form a **set**: `T ↔ S = P(T × S)`
  - `↦` combines two **elements** to form an **ordered pair**: `x ↦ y ∈ S × T`

### Domain and Range

- The **domain** of a relation `R` is the set of **first parts** of all the pairs in `R`, written: `dom(R)`
- The **range** of a relation `R` is the set of **second parts** of all the pairs in `R`, written: `ran(R)`

| Predicate  | Definition      |
|------------|-----------------|
| x ∈ dom(R) | ∃y · x ↦ y ∈ R |
| y ∈ ran(R) | ∃x · x ↦ y ∈ R |

### Relational Image

`directory = { mary ↦ 287573, mary ↦ 398620, john ↦ 829483, jim ↦ 398620 }`

Relational image examples:

- `directory[ {mary} ] = { 287573, 398620 }`
- `directory[ { john, jim } ] = { 829483, 398620 }`

Assume `R ∈ S ↔ T `and `A ⊆ S`, the **relational image** of set `A` under relation `R` is written `R[A]`

| Predicate | Definition             |
|-----------|------------------------|
| y ∈ R[A]  | ∃x · x ∈ A ∧ x ↦ y ∈ R |


### Partial Functions

Special kind of relation: each domain element has **at most one range element** associated with it.

![](https://i.postimg.cc/Qt2K6Km6/rf3.png){: .w-10 .shadow .rounded-10 }

- To declare `f` as a partial function
  - This says that `f` is a **many-to-one** relation
  - Each domain element is mapped to one range element: `x ∈ dom(f) ⇒ card( f [{x}] ) = 1`
  - More usually formalised as a uniqueness constraint: `x ↦ y1 ∈ f` ∧ `x ↦ y2 ∈ f` ⇒ `y1 = y2`

### Function Application

We can use **function application** for **partial functions**.

- If `x ∈ dom(f)`, then we write `f(x)` for the **unique** range element associated with `x` in `f`.
- If `x ∉ dom(f)` , then `f(x)` is **undefined**.
- If `card(f [{x}] ) > 1` , then `f(x)` is **undefined**.

![](https://i.postimg.cc/jq32sF7z/rf5.png){: .w-10 .shadow .rounded-10 }

Example:

![](https://i.postimg.cc/90L7VXjT/rf4.png){: .w-10 .shadow .rounded-10 }
