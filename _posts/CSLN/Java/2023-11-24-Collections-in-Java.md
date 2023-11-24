---
title: Some Java basics
date: 2023-11-24 20:00:00 +0530
categories: [(CS) Learning Note, Java]
tags: [computer science, software engineering, Java]
pin: false
---

Java Collections Framework is a pivotal component of Java programming, designed to handle groups of objects. It offers a more flexible and sophisticated framework for storing and manipulating groups of data as compared to traditional arrays. In this blog, we'll explore the different types of collections in Java and their distinct characteristics.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction to Java Collections](#introduction-to-java-collections)
  * [Types of Collections in Java](#types-of-collections-in-java)
    * [List](#list)
    * [Set](#set)
    * [Queue](#queue)
    * [Map](#map)
  * [Comparing Different Collections](#comparing-different-collections)
    * [Lists: ArrayList vs. LinkedList vs. Vector](#lists-arraylist-vs-linkedlist-vs-vector)
    * [Sets: HashSet vs. TreeSet vs. LinkedHashSet vs. ConcurrentHashSet](#sets-hashset-vs-treeset-vs-linkedhashset-vs-concurrenthashset)
    * [Maps: HashMap vs. TreeMap vs. LinkedHashMap vs. Hashtable](#maps-hashmap-vs-treemap-vs-linkedhashmap-vs-hashtable)
    * [Queues and Deques: PriorityQueue vs. ArrayDeque](#queues-and-deques-priorityqueue-vs-arraydeque)
<!-- TOC -->

---

## Introduction to Java Collections

The Java Collections Framework provides a set of interfaces and classes for storing and manipulating groups of data as objects. The primary benefits include reduced programming effort, increased performance, and the ability to handle different types of data structures.

## Types of Collections in Java

### List

- **Features**: Ordered collection (also known as a sequence). Lists can contain duplicate elements.
- **Implementation Classes**: `ArrayList`, `LinkedList`, `Vector`
- **Use Case**: When you need an ordered collection that can contain duplicates.

### Set

- **Features**: A collection that cannot contain duplicate elements.
- **Implementation Classes**: `HashSet`, `LinkedHashSet`, `TreeSet`
- **Use Case**: When you need to ensure that no duplicates are stored in the collection.

### Queue

- **Features**: Holds elements prior to processing. Queues typically order elements in a FIFO (first-in-first-out) manner.
- **Implementation Classes**: `LinkedList`, `PriorityQueue`
- **Use Case**: When you need to process elements in a specific order.

### Map

- **Features**: An object that maps keys to values. A map cannot contain duplicate keys, and each key can map to at most one value.
- **Implementation Classes**: `HashMap`, `LinkedHashMap`, `TreeMap`
- **Use Case**: When you need to maintain key-value associations.

## Comparing Different Collections

### Lists: ArrayList vs. LinkedList vs. Vector

- **ArrayList**:
  - Resizable-array implementation.
  - Fast random access.
  - Good for storing and accessing data.
  - Not synchronized.
- **LinkedList**:
  - Doubly-linked list implementation.
  - Better at add and remove operations.
  - Preferred for dynamic insertions and deletions.
  - Not synchronized.
- **Vector**:
  - Similar to ArrayList, but synchronised.
  - Slower than ArrayList due to synchronisation.
  - Legacy class but useful in multithreaded environments.

### Sets: HashSet vs. TreeSet vs. LinkedHashSet vs. ConcurrentHashSet

- **HashSet**:
  - Implements Set Interface backed by a hash table (actually a HashMap instance).
  - Best performance; offers constant time for basic operations.
  - No order guarantee for iteration.
- **TreeSet**:
  - Implements NavigableSet Interface backed by a TreeMap.
  - Elements are sorted in natural order.
  - Offers log(n) time for most operations.
- **LinkedHashSet**:
  - Hash table and linked list implementation of the Set interface.
  - Maintains insertion order.
  - Slightly slower than HashSet for adding and querying.
- **ConcurrentHashSet**: 
  - Similar to HashSet but thread-safe
  - part of java.util.concurrent package.


### Maps: HashMap vs. TreeMap vs. LinkedHashMap vs. Hashtable

- **HashMap**:
  - Stores key-value pairs.
  - Offers constant-time performance for get and put methods.
  - Iteration order is not predictable.
  - Not synchronized.
  - `null` keys and values are supported
- **TreeMap**:
  - Red-Black tree based NavigableMap implementation.
  - Keys are sorted in natural order.
  - get and put methods have log(n) time complexity.
  - `null` values are supported, but `null` keys are not supported
- **LinkedHashMap**:
  - Hash table and linked list implementation of the Map interface.
  - Predictable iteration order (insertion order).
  - Slightly slower than HashMap.
  - `null` keys and values are supported
- **Hashtable**:
  - Similar to HashMap but synchronized.
  - Slower than HashMap due to synchronization.
  - A legacy class, generally avoided in new code.
  - `null` keys and values are not supported
- **ConcurrentHashMap**: 
  - Thread-safe variant of HashMap
  - part of java.util.concurrent
  - allows concurrent read and updates with thread safety.
  - `null` keys and values are not supported

### Queues and Deques: PriorityQueue vs. ArrayDeque

- **PriorityQueue**:
  - Queue implementation that orders elements based on their values.
  - Ideal for tasks like CPU and Disk Scheduling.
- **ArrayDeque**:
  - Resizable-array implementation of the Deque interface.
  - More efficient than Stack and LinkedList.
