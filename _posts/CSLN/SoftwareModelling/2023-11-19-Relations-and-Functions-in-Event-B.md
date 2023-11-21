---
title: Relations and Functions in Event-B
date: 2023-11-19 20:20:00 +0530
categories: [ (CS) Learning Note, Software Modelling and Design ]
tags: [ computer science, software engineering, Event-B ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Ordered Pairs and Cartesian Products](#ordered-pairs-and-cartesian-products)
    * [Cartesian Products: Definition and Examples](#cartesian-products-definition-and-examples)
    * [Cartesian Product is a Type Constructor](#cartesian-product-is-a-type-constructor)
    * [Sets of Order Pairs](#sets-of-order-pairs)
  * [Relations](#relations)
    * [Domain and Range](#domain-and-range)
    * [Relational Image](#relational-image)
  * [Functions](#functions)
    * [Partial Functions](#partial-functions)
      * [Function Application](#function-application)
      * [Well-definedness](#well-definedness)
      * [Example of Birthday Book](#example-of-birthday-book)
    * [Total Functions](#total-functions)
      * [Example of Modelling with Total functions](#example-of-modelling-with-total-functions)
  * [Restriction and Substraction](#restriction-and-substraction)
    * [Domain Restriction](#domain-restriction)
    * [Domain Subtraction](#domain-subtraction)
    * [Domain and Range](#domain-and-range-1)
    * [Example of Removing Entries from the Directory](#example-of-removing-entries-from-the-directory)
  * [Function Overriding](#function-overriding)
    * [Example of Modifying a birthday](#example-of-modifying-a-birthday)
  * [Relational Inverse](#relational-inverse)
    * [Example of Inversing Queries](#example-of-inversing-queries)
  * [Relational Composition](#relational-composition)
<!-- TOC -->

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

| Predicate  | Definition     |
|------------|----------------|
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

## Functions

### Partial Functions

Special kind of relation: each domain element has **at most one range element** associated with it. `f ∈ X⇸Y`

- To declare `f` as a partial function
  - This says that `f` is a **many-to-one** relation
  - Each domain element is mapped to one range element: `x ∈ dom(f) ⇒ card( f [{x}] ) = 1`
  - More usually formalised as a uniqueness constraint: `x ↦ y1 ∈ f` ∧ `x ↦ y2 ∈ f` ⇒ `y1 = y2`

#### Function Application

We can use **function application** for **partial functions**.

- If `x ∈ dom(f)`, then we write `f(x)` for the **unique** range element associated with `x` in `f`.
- If `x ∉ dom(f)` , then `f(x)` is **undefined**.
- If `card(f [{x}] ) > 1` , then `f(x)` is **undefined**.

![](https://i.postimg.cc/jq32sF7z/rf5.png){: .w-10 .shadow .rounded-10 }

Example:

![](https://i.postimg.cc/90L7VXjT/rf4.png){: .w-10 .shadow .rounded-10 }

#### Well-definedness

| Predicate | Well-definedness condition |
|-----------|----------------------------|
| f(x)      | x ∈ dom(f) ∧ f ∈ X ↦ Y     |

The following definition of function application assumes that `f(x)` **is well-defined**:

| Predicate | Definition |
|-----------|------------|
| y = f(x)  | x ↦ y ∈ f  |

#### Example of Birthday Book

- Birthday book relates people to their birthday.
- Each person can have at most one birthday.
- People can share birthdays.

![](https://i.postimg.cc/qvyKNr9Q/rf6.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/GpzHDmzP/rf7.png){: .w-10 .shadow .rounded-10 }

### Total Functions

A total function **is a special kind of partial function**. To declare `f` as a total function: `f ∈ X → Y`

This means that `f` **is well-defined for every element** in `X`, i.e., `f ∈ X → Y` is shorthand
for `f ∈ X⇸Y ∧ dom(f) = X`

#### Example of Modelling with Total functions

We can re-write the invariant for the birthday book to use total functions:

![](https://i.postimg.cc/05D2JqxH/rf12.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/8kH9Yybz/rf13.png){: .w-10 .shadow .rounded-10 }

## Restriction and Substraction

### Domain Restriction

Given `R ∈ S ↔ T` and `A ⊆ S`, the domain restriction of `R` by `A` is writen: `A ▷ R`

Restrict relation `R` so that it only contains pairs whose first part is in the set `A`.

**Example:**

`directory = { mary ↦ 287573, mary ↦ 398620, john ↦ 829483, jim ↦ 398620 }`

`{john, jim, jane} C directory = { john ↦ 829483, jim ↦ 398620 }`

### Domain Subtraction

Given `R ∈ S ↔ T` and `A ⊆ S`, the domain subtraction of `R` by `A` is written `A ⩤ R`

Remove those pairs from `R` whose first part is in `A`.

**Example:**

`directory = { mary ↦ 287573, mary ↦ 398620, john ↦ 829483, jim ↦ 398620 }`

`{john, jim, jane} C directory = { mary ↦ 287573, mary ↦ 398620 }`

### Domain and Range

Assume `R ∈ S ↔ T` and `A ⊆ S` and `B ⊆ T`

| Predicate     | Definition          |                    |
|---------------|---------------------|--------------------|
| x ↦ y ∈ A ◁ R | x ↦ y ∈ R  ∧  x ∈ A | domain restriction |
| x ↦ y ∈ A ⩤ R | x ↦ y ∈ R  ∧  x ∉ A | domain restriction |
| x ↦ y ∈ R ▷ B | x ↦ y ∈ R  ∧  y ∈ B | domain restriction |
| x ↦ y ∈ R ⩥ B | x ↦ y ∈ R  ∧  y ∉ B | domain restriction |

### Example of Removing Entries from the Directory

![](https://i.postimg.cc/RV88M1BK/rf8.png){: .w-10 .shadow .rounded-10 }

## Function Overriding

![](https://i.postimg.cc/13nMR40d/rf9.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/0j36Q5Pk/rf10.png){: .w-10 .shadow .rounded-10 }

### Example of Modifying a birthday

![](https://i.postimg.cc/J4VxPRbV/rf11.png){: .w-10 .shadow .rounded-10 }

## Relational Inverse

![](https://i.postimg.cc/ZnQRZ6d7/rf14.png){: .w-10 .shadow .rounded-10 }

### Example of Inversing Queries

![](https://i.postimg.cc/KvNbnPzd/rf15.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/jjvvcjNq/rf16.png){: .w-10 .shadow .rounded-10 }

## Relational Composition

![](https://i.postimg.cc/jjKtNMQ0/rf17.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/VLpjYC9b/rf18.png){: .w-10 .shadow .rounded-10 }

