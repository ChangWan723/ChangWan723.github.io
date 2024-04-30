---
title: "Binary Search Tree: Embodiment of Binary Search"
date: 2023-09-16 12:00:00 UTC
categories: [ (CS) Learning Note, Data Structure ]
tags: [ computer science, Data Structure ]
pin: false
---

Binary Search Trees (BSTs) are a fundamental data structure that allows for efficient search, insertion, and deletion operations. **Central to the utility of BSTs is the binary search algorithm**, which enables quick data retrieval by halving the search space with each step.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is a Binary Search Tree?](#what-is-a-binary-search-tree)
    * [Advantages of Binary Search Trees](#advantages-of-binary-search-trees)
    * [Disadvantages of Binary Search Trees](#disadvantages-of-binary-search-trees)
  * [Core Operations in Binary Search Trees](#core-operations-in-binary-search-trees)
    * [Search](#search)
    * [Insert](#insert)
    * [Delete](#delete)
  * [Difference Between BST and Binary Search](#difference-between-bst-and-binary-search)
  * [Why Are BSTs Sometimes Used Instead of Hash Tables?](#why-are-bsts-sometimes-used-instead-of-hash-tables)
<!-- TOC -->

---

## What is a Binary Search Tree?

A **Binary Search Tree (BST)** is a node-based binary tree data structure which has the following properties:
- The **left subtree** of a node contains only nodes with keys **lesser** than the node’s key.
- The **right subtree** of a node contains only nodes with keys **greater** than the node’s key.
- The left and right subtree each must also be a binary search tree.

![](https://i.postimg.cc/QCCCHx3n/image20.png){: .w-10 .shadow .rounded-10 }
_Binary Search Trees_

### Advantages of Binary Search Trees

1. **Ordered Structure**: BSTs maintain their elements in an ordered state. Traversing a binary search tree using **Inorder Traversal can output the ordered sequence of data** with a time complexity of `O(n)`, which is very efficient.
   - So, **BSTs** also called an **ordered** or **sorted binary trees**.
2. **Dynamic Data Structure**: BSTs can grow and shrink dynamically, making it easier to manage data with changing datasets.
3. **Efficient Operations**: If the tree is balanced, operations such as search, insert, and delete can be done in `O(log n)` time.

### Disadvantages of Binary Search Trees

1. **Performance Dependency on Tree Height**: The efficiency of operations depends on the height of the tree. In the worst case (e.g., when the tree becomes a linked list), operations can degrade to `O(n)`.
2. **Need for Rebalancing**: BSTs can become unbalanced with numerous operations, necessitating periodic rebalancing to maintain optimal performance.

## Core Operations in Binary Search Trees

### Search

To search for a value in a BST, start from the root and compare the value with the root. If the value is greater than the root, search the right subtree. Similarly, if the value is less than the root, search the left subtree. This process is repeated until the value is found or the remaining subtree is null.

![](https://i.postimg.cc/8CFqP7s0/image21.png){: .w-10 .shadow .rounded-10 }
_Search `19`_

### Insert

To insert a value in a BST, start from the root and compare the value with the root. If the value is greater than the root, and if the right child is null, insert the value here, or move to the right child. Do the opposite if the value is less than the root. Continue this process until the correct position is found.

![](https://i.postimg.cc/jSGrf6Vb/image22.png){: .w-10 .shadow .rounded-10 }
_Insert `55`_

### Delete

Deletion in a BST is more complex:
- **Node to be deleted is leaf**: Simply remove from the tree.
- **Node to be deleted has one child**: Copy the child to the node and delete the child.
- **Node to be deleted has two children**: Find the smallest node in the right subtree of this node and replace it.

![](https://i.postimg.cc/DzX5WLhR/image23.png){: .w-10 .shadow .rounded-10 }
_Delete `55`, `13`, `18`_

> There is also a very simple and tricky way of deleting in a binary search tree, which is to **simply mark the node to be deleted as "deleted"**, but not actually remove the node from the tree.
> - This way the originally deleted node still needs to be stored in memory, which **would be a waste of memory space, but the deletion operation becomes much simpler**.
{: .prompt-tip }

> No matter insertion, deletion or search operation, the **time complexity** is actually proportional to the height of the tree, that is, `O(height)`. 
> - So, the height of the binary search tree is critical. To be efficient, we need to **make sure that the height of the binary search tree is low**, i.e., make sure that it is a **balanced binary tree**.
{: .prompt-tip }

## Difference Between BST and Binary Search


- **Binary Search**: Binary search is an **algorithm** used to efficiently find a target value within a sorted array or list. Its primary goal is to **search** a specific element in a collection of data by repeatedly dividing the search space in half.
- **Binary Search Tree**: A binary search tree is a **data structure** used to store and organize data in a hierarchical manner. It's designed to facilitate efficient **searching**, **insertion**, and **deletion** operations.

> **Compared to Binary Search in a sorted array**: 
> - **BSTs** allow for **efficient insertion and deletion operations** 
>   - Unlike arrays where insertion and deletion can be costly due to shifting elements. 
> - But if not properly managed, **BSTs can become unbalanced**, leading to degradation in performance.
>   - In worst-case scenarios, an unbalanced BST can degenerate into a linked list, resulting in linear time complexity for search, insertion, and deletion operations.
{: .prompt-tip }

## Why Are BSTs Sometimes Used Instead of Hash Tables?

While **HashMaps** offer average-case **constant-time complexity** for inserts, deletes, and searches, **they do not maintain any order among elements** and require **extra memory for addressing collisions**. So, here are reasons why one might prefer BSTs over HashMaps:
- **Order Maintenance**: BSTs maintain elements in a sorted order, which is beneficial for applications that require ordered data traversal.
- **Lower Memory Overhead**: Unlike HashMaps, which need to handle hashing and potential collisions, BSTs generally use less memory.
- **Predictable Performance**: The performance of HashMaps can become unpredictable in scenarios involving poor hash functions or high collision rates, whereas the performance of BSTs is more transparent and consistent.
- **Simple Structure**: The construction of a hash table is more complex than a binary search tree. And there are many things to consider for hash table. For example, the design of the hash function, conflict resolution, expansion, shrinking and so on.


<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
