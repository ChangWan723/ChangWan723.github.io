---
title: "Linked Lists: The Opposite of Arrays"
date: 2023-09-05 11:45:00 UTC
categories: [ (CS) Learning Note, Algorithm and Data Structure ]
tags: [ computer science, Data Structure ]
pin: false
---

In the realm of data structures, linked lists are as fundamental as arrays but come with their own unique set of advantages for certain use cases. 

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Different Types of Linked Lists](#different-types-of-linked-lists)
    * [Singly Linked List](#singly-linked-list)
    * [Circular Linked List](#circular-linked-list)
    * [Doubly Linked List](#doubly-linked-list)
    * [Doubly Circular Linked List](#doubly-circular-linked-list)
  * [Linked List vs Array](#linked-list-vs-array)
  * [Examples of the Advantages of Linked Lists: Implementing LRU Cache](#examples-of-the-advantages-of-linked-lists-implementing-lru-cache)
<!-- TOC -->

---

## Different Types of Linked Lists

Linked lists are a collection of nodes where each node contains data and a reference to the next node in the sequence. Here's a brief overview of the various types:


### Singly Linked List

A singly linked list is the simplest type of linked list, in which each node contains data and a reference to the next node in the sequence. It's a unidirectional chain, which means you can traverse the list in only one direction, from the head to the last node.

![](https://i.postimg.cc/Ss3YdKYn/ll1.png){: .w-10 .shadow .rounded-10 }

**Advantages:**
- Efficient insertion and deletion compared to arrays.
- Dynamic size allows the list to expand according to the program’s needs.

**Disadvantages:**
- Accessing an element has `O(n)` time complexity.
- One-way traversal can be limiting for certain operations.

### Circular Linked List

A circular linked list is a variation of a singly linked list where the last node points back to the first node, forming a loop. This can also be a doubly circular linked list if every node has two references (to both the next and previous nodes).

![](https://i.postimg.cc/26VBnWyp/ll2.png){: .w-10 .shadow .rounded-10 }

**Advantages:**
- Useful for implementing queues, as it allows continuous access to nodes.
- The circular nature is useful for round-robin scheduling and turn-based games.

**Disadvantages:**
- More complex to manage due to the risk of infinite looping if not handled correctly.

### Doubly Linked List

In a doubly linked list, each node holds a reference to both the next and the previous node. This two-way link allows for traversal in both directions, which can greatly simplify certain operations.

![](https://i.postimg.cc/C58BQVbm/ll3.png){: .w-10 .shadow .rounded-10 }

**Advantages:**
- Bidirectional traversal makes some operations more convenient.
- It's easier to delete a node without traversing the list, given a pointer to the node.

**Disadvantages:**
- Each node requires extra memory for an additional pointer.
- Slightly more complex to implement than singly linked lists.


### Doubly Circular Linked List

A doubly circular linked list is a complex data structure that combines the features of both doubly linked lists and circular linked lists. Each node has two links and the last node links to the first node, making the entire list navigable in both directions in a loop.

![](https://i.postimg.cc/wxRmvDnL/ll4.png){: .w-10 .shadow .rounded-10 }

**Advantages:**
- Allows for backward traversal from any point in the list.
- It is beneficial for applications that require wrapping from the last element to the first repeatedly.

**Disadvantages:**
- The most complex of the linked list structures to implement and manage.

## Linked List vs Array

While linked lists and arrays are both linear data structures, they have several differences:

**Advantages of Linked Lists:**

- **Dynamic Size:** They can grow and shrink during execution, as they don't have a fixed size.

- **Ease of Insertions/Deletions:** Adding or removing elements is generally an `O(1)` operation, not requiring shifts in the structure.

![](https://i.postimg.cc/zvSr2d29/ll5.png){: .w-10 .shadow .rounded-10 }

> **Is the time complexity of adding or removing elements in Linked Lists always `O(1)`?**
> - **No**, it depends on the **exact implementation** and the **location of the operation**.
> - **For a singly linked list:**
>   - If inserting or deleting the **head node** or the **next node**, the time complexity is typically `O(1)` because only the known pointer needs to be modified.
>   - However, if inserting or deleting the **current node** or **a node at a specified position**, it requires traversing the list to find the predecessor node at that position, making the average time complexity `O(n)`.
> - **For a doubly linked list:**
>   - No matter inserting or deleting the **head node**, **current node** or the **next node**, the time complexity is typically `O(1)` because it is easy to get pre-node.
>   - However, inserting or deleting **a node at a specified position** still has a time complexity of `O(n)` because traversal is necessary to find the node at that position.
> 
> Therefore, **doubly linked lists are more efficient than singly linked lists.** That's why in real software development, doubly linked lists are more widely used than singly linked lists, even though they consume more memory.
{: .prompt-tip }

**Disadvantages of Linked Lists:**

- **Memory Usage:** Each element requires extra memory for a pointer, which can be significant compared to arrays.

- **Sequential Access:** Direct access is not possible; you must traverse the list from the beginning to reach an element.

---

**Advantages of Arrays:**

- **Cache Friendliness:** Due to contiguous memory allocation, arrays tend to make better use of CPU caching.

- **Direct Access:** Arrays allow `O(1)` access time for elements with their indices.

**Disadvantages of Arrays:**

- **Fixed Size:** Once declared, the size of the array cannot be changed without creating a new array.

- **Costly Insertions/Deletions:** Especially in the middle of the array, as other elements need to be shifted.

## Examples of the Advantages of Linked Lists: Implementing LRU Cache

An LRU cache algorithm ensures that the least recently used items are discarded first when the cache reaches its capacity. **Due to the easy movement of nodes in a linked list, it is well suited to implement the LRU Cache algorithm.** 

Here’s how it can be implemented with linked lists:

1. **Each node represents a cache item.** The head of the list is the most recently used item, and the tail is the least recently used.

2. **When an item is accessed or added:** Move it to the head of the list. If it's a new item and the cache is full, remove the item at the tail.

3. **When an item needs to be removed:** Detach the node from the list.

The linked list allows for constant-time additions and removals, making it efficient for an LRU cache. **It is much more complex to implement LRU cache using an array structure** (requiring a lot of element movement or complex algorithm design).

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
