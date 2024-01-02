---
title: Lists and Collections in Event-B
date: 2023-12-07 17:25:00 UTC
categories: [ (CS) Learning Note, Software Modelling and Design ]
tags: [computer science, Event-B ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Collection of Lists](#collection-of-lists)
    * [Modelling a list of items](#modelling-a-list-of-items)
  * [Queues](#queues)
    * [Modelling a Printer Queue](#modelling-a-printer-queue)
      * [Relating jobs and queue positions](#relating-jobs-and-queue-positions)
      * [Associating documents with jobs](#associating-documents-with-jobs)
      * [Adding a job to the queue](#adding-a-job-to-the-queue)
      * [Adding a job to the queue. Second version](#adding-a-job-to-the-queue-second-version)
      * [Removal of a job from queue](#removal-of-a-job-from-queue)
      * [Removal of a job from the queue. Second version](#removal-of-a-job-from-the-queue-second-version)
  * [Stack](#stack)
    * [Modelling a Printer Stack](#modelling-a-printer-stack)
      * [Removal of a job from stack](#removal-of-a-job-from-stack)
  * [Managing multiple queues](#managing-multiple-queues)
    * [Curried version of position](#curried-version-of-position)
      * [Disjointness of queues](#disjointness-of-queues)
      * [Adding a job to a queue](#adding-a-job-to-a-queue)
      * [Remove a job from a queue](#remove-a-job-from-a-queue)
  * [Collection of queues. Second Approach](#collection-of-queues-second-approach)
    * [Ordering within a queue](#ordering-within-a-queue)
      * [Adding a job to a queue](#adding-a-job-to-a-queue-1)
      * [Remove a job from a queue](#remove-a-job-from-a-queue-1)
  * [Partition](#partition)
    * [Representing States using Partition Operator](#representing-states-using-partition-operator)
    * [Partition](#partition-1)
      * [Examples of Partition](#examples-of-partition)
<!-- TOC -->

---


## Collection of Lists

- Set: unordered collection
- List: ordered collection
  - Items have a position in a list
  - Positions are ordered
  - We can use an ordered set to define positions, e.g., natural numbers

### Modelling a list of items

- Position as natural number: first item has the lowest position number, and more recent items have a higher position number
  - @inv1: `item ⊆ ITEM`
  - @inv2: `position ∈ item ⟶ POSITION`
- BUT: this allows two different items to have the same position

---

- List positions are injective
  - @inv1: `item ⊆ ITEM`
  - @inv2: `position ∈ item ↣ POSITION`

**Injective mapping**: each item has a single position and different jobs cannot be at the same position

## Queues

- Queues are useful for managing access to shared resources in a fair way.
- Physical queue, e.g., queue for check-in desk at airport
- Virtual queue, e.g., queue for aircraft landing slot
- Queue can be viewed as a **list**
- **Queues** are very common in computing to manage access to shared resources such as a CPU, memory, disk, communications channel

### Modelling a Printer Queue

- Queue: used to control access to some resource, e.g., printer
- First-in first-out (FIFO): jobs should be serviced in the order in which they are placed in a queue

#### Relating jobs and queue positions

- Position as integer: more recent items have higher position number
  - @inv1: `job ⊆ JOB`
  - @inv2: `position ∈ job ↣ POSITION`
- **Injective mapping**: each job has a single position and different jobs cannot be at the same position

#### Associating documents with jobs

- @inv1: `job ⊆ JOB`
- @inv2: `position ∈ job ↣ POSITION`
- @inv3: `document ∈ job → DOCUMENT` (each job has a single document, but different jobs can have a same document)



#### Adding a job to the queue

```
event QueueJob
  any j d p
  where
    @grd1: j ∈ JOB \ job
    @grd2: d ∈ DOCUMENT
    @grd3: p ∈ POSITION
    @grd4: p ∉ ran(position)
    @grd5 position ≠ ∅ ⇒ p>max(ran(position))
  then
    @act1: job ≔ job ∪ { j }
    @act2: document(j) ≔ d
    @act3: position(j) ≔ p
  end
```

- `@grd4: p ∉ ran(position)` and `@grd5 position ≠ ∅ ⇒ p>max(ran(position))` means: 
  - `p` is greater than all current positions in the list
  - We need `@grd4` and `@grd5` because we have to keep the Queue **in order**

#### Adding a job to the queue. Second version

```
event QueueJob
  any j d p
  where
    @grd1: j ∈ JOB \ job
    @grd2: d ∈ DOCUMENT
    @grd3: p ∈ POSITION
    @grd4: ∀ k · k ∈ job ⇒ p > position(k)
  then
    @act1: job ≔ job ∪ { j }
    @act2: document(j) ≔ d
    @act3: position(j) ≔ p
  end
```

- We can replace previous `@grd4` and `@grd5` with: 
  - `@grd4: ∀ k · k ∈ job ⇒ p > position(k)`


#### Removal of a job from queue

```
event DeQueueJob
  any j
  where
    @grd1: j ∈ job
    @grd2: position(j) = min(ran(position))
  then
    @act1: job ≔ job \ { j }
    @act2: document ≔ { j } ⩤ document
    @act3: position ≔ { j } ⩤ position
  end
```

#### Removal of a job from the queue. Second version

```
event DeQueueJob
  any j
  where
    @grd1: j ∈ job
    @grd2: ∀ k · k ∈ job ⇒ position(j) ≤ position(k)
  then
    @act1: job ≔ job \ { j }
    @act2: document ≔ { j } ⩤ document
    @act3: position ≔ { j } ⩤ position
  end
```

- `@grd2: ∀ k · k ∈ job ⇒ position(j) ≤ position(k)` means:
  - `j` is at the lowest position in the list
  - We need `@grd2` because we have to keep **FIFO** (First-in first-out) in the Queue

## Stack

- First-in first-out (FIFO): items that arrive earlier in the queue are removed earlier
- Last-in first-out (LIFO): items that arrive later in the queue are removed earlier
  - a LIFO queue is also referred to as a **stack**

### Modelling a Printer Stack

#### Removal of a job from stack

```
event DeQueueJob
  any j
  where
    @grd1: j ∈ job
    @grd2:  ∀ k · k ∈ job ⇒ position(j) ≥ position(k)
  then
    @act1: job ≔ job \ { j }
    @act2: document ≔ { j } ⩤ document
    @act3: position ≔ { j } ⩤ position
  end
```

- `@grd2:  ∀ k · k ∈ job ⇒ position(j) ≥ position(k)` means:
  - `j` is at the highest position in the list
  - We need `@grd2` because we have to keep **LIFO** (Last-in first-out) in the Stack

## Managing multiple queues

- Rather than managing a single print queue, we want to model a system that manages a collection of queues
- Introduce carrier set QUEUE to distinguish queues
- Associate each job with a queue as well as a position q
- Now the position is based not just on the job `j` but also on the queue `q`
  - Instead of `position(j)`
  - We need `position(q, j)`

### Curried version of position

- @inv1: `queue ⊆ QUEUE`
- @inv2: `job ⊆ JOB`
- @inv3: `position ∈ queue → ( job ⤔ POSITION )`

---

- Give a queue `q`,
  - `position(q)` is the **position table** for `q`
  - `position(q)(j)` is the **position** of job `j` on `q`

#### Disjointness of queues

- A job cannot be on more than one queue
  - @inv: `∀ q1, q2 · q1 ∈ queue ∧ q2 ∈ queue ∧ q1 ≠ q2 ⇒ dom (position(q1)) ∩ dom (position(q2)) = ∅`

#### Adding a job to a queue

```
event QueueJob
  any j d p q
  where
    @grd1: j ∈ JOB \ job
    @grd2: d ∈ DOCUMENT
    @grd3: q ∈ queue
    @grd4: p ∈ POSITION \ ran(position(q))
    @grd5 position ≠ ∅ ⇒ p>max(ran(position))
  then
    @act1: job ≔ job ∪ { j }
    @act2: document(j) ≔ d
    @act3: position(q) ≔ position(q) ∪ {j↦p}
  end
```

#### Remove a job from a queue

``` 
event DeQueueJob
  any j q
  where
    @grd1: j ∈ job
    @grd2: q ∈ queue
    @grd3: j ∈ dom(position(q))
    @grd4: position(q)(j) = min(ran(position(q)))
  then
    @act1: job ≔ job \ { j }
    @act2: document ≔ { j } ⩤ document
    @act3: position(q) ≔ { j } ⩤ position(q)
  end
```

## Collection of queues. Second Approach

@inv: `j_queue ∈ job → queue`

### Ordering within a queue

- For single queue we had injectivity:
  - @inv: position ∈ job ↣ POSITION
- This is **too strong** as ordering is only required within each queue
- Reformulation ordering invariant:
  - `@inv: ∀ j, k · j ∈ job ∧ k ∈ job ∧ j ≠ k ∧ j_queue(j) = j_queue (k) ⇒ position(j) ≠ position(k)`
  - This means two different jobs in the same queue cannot have the same position

#### Adding a job to a queue

```
event QueueJob
  any j d p q
  where
    @grd1: j ∈ JOB \ job
    @grd2: d ∈ DOCUMENT
    @grd3: q ∈ queue
    @grd4: p ∈ POSITION
    @grd5 ∀k · k ∈ job ∧ j_queue(k) = q ⇒ p > position(k)
  then
    @act1: job ≔ job ∪ { j }
    @act2: document(j) ≔ d
    @act3: position(j) ≔ p
    @act4: j_queue(j) ≔ q
  end
```

#### Remove a job from a queue

``` 
event DeQueueJob
  any j
  where
    @grd1: j ∈ job
    @grd2: q = j_queue(j)
    @grd3: ∀ k· k ∈ job ∧ j_queue(k) = q ⇒ position(j) ≤ position(k)
  then
    @act1: job ≔ job \ { j }
    @act2: document ≔ { j } ⩤ document
    @act3: position ≔ { j } ⩤ position
    @act4: j_queue ≔ { j } ⩤ j_queue
  end
```

## Partition

### Representing States using Partition Operator

- Entities can only be in **one state at a time**
  - so, states of a state machine are **disjoint**

---

- **sets** 
  - `USER`
- **variables** 
  - `user in out`
- **invariants**
  - `user ⊆ USER`
  - `user = in ∪ out`
  - `in ∩ out = ∅`

---

We can use **partition** operator to simplify **invariants**:

- **invariants**
  - `user ⊆ USER`
  - `partition(user, in, out)`

The **partition** operator provides a shorthand way of declaring that user is **partitioned** into **disjoint** subsets(in and out).

### Partition

- `S` is partitioned into n disjoint subsets `Ti` where `i ∈ 1..n`
  - `partition( S, T1, …, Tn )`
- More precisely:
  - `S` = `T1 ∪ … ∪ Tn`
  - `Ti ∩ Tk` = `∅` each `i, k` where `i≠k`
- Note that the number of arguments for the partition operator is not fixed

#### Examples of Partition

- Switches:
  - `partition(switch, off, on)`
- Assignments:
  - `partition(assignment, open, pending, passed, failed)`
- Printers:
  - `partition(printers, offline, ready, busy)`
