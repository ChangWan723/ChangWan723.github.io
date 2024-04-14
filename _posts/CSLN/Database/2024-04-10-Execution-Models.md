---
title: Execution Models in Databases Query Processing
date: 2024-04-10 17:55:00 UTC
categories: [ (CS) Learning Note, Database ]
tags: [ computer science, Database ]
pin: false
---

- A physical query plan is a tree of physical plan operators
- The **execution model** defines:
  - the interface that connects operators to each other
    - Relation(s) in, relation out
    - Producer-consumer relationship
  - how data is propagated between operators
  - how operators are scheduled

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Synchronous Execution Models](#synchronous-execution-models)
    * [Pipelining](#pipelining)
    * [Iterators](#iterators)
  * [Asynchronous Execution Models](#asynchronous-execution-models)
    * [The Push Model](#the-push-model)
    * [The Pull Model](#the-pull-model)
    * [The Stream Model](#the-stream-model)
<!-- TOC -->

---

## Synchronous Execution Models

- The operator interface is synchronous:
  - Operators don’t generate tuples until getNext() is called
  - In reality, different operators will have different evaluation times
  - Some operators may block – causing the whole plan to block

### Pipelining

- **Pipelining**: read input, process, propagate output to next operator
- Benefits of pipelining:
  - No buffering (because no materialisation)
  - Faster execution (no materialisation, so no disk I/Os)
  - More in-memory operations 
- Not all operators can be pipelined
  - Some require intermediate relations to be materialised
  - Some operators will always block

### Iterators

- Standard interface on each operator:
  - open() 
  - getNext() 
  - close() 
- Query engine calls the interface on the root operator
- Calls to interface are propagated down the tree

![](https://i.postimg.cc/qgf4FMxB/em1.png){: .w-10 .shadow .rounded-10 }
{: .prompt-tip }


## Asynchronous Execution Models

- Asynchronous implementation by introducing buffering:
  - Within the operator calling the interface (the push model)
  - Within the operator being called (the pull model)
  - In the connections between operators (the stream model)
- Asynchronous implementations minimise time during which blocking occurs

### The Push Model

- Propagate from the leaves upwards
  - Producer propagates tuples as soon as they’re available
  - Producer propagates tuples regardless of whether consumer has yet called
    getNext()
  - Consumer buffers incoming tuples until it calls getNext()
- Minimises idle time, good for pipelining

### The Pull Model

- Propagation driven from the root
  - Producer buffers tuples until getNext() is called
  - On-demand, close to pure implementation

### The Stream Model

- Connections as first-class objects:
  - FIFO queues of tuples
  - Producer propagates tuples to the queue as soon as they’re available
  - Consumer call to getNext() does not block if there’s something in the queue
- Asynchronous operators (but synchronous streams), good for parallelisation
