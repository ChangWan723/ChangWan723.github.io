---
title: "Algorithmic Thinking: Greedy"
date: 2024-06-10 20:03:00 UTC
categories: [ (CS) Learning Note, Algorithm ]
tags: [ computer science, Algorithm ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is a Greedy Algorithm?](#what-is-a-greedy-algorithm)
    * [Key Principles](#key-principles)
    * [Applications of Greedy Algorithms](#applications-of-greedy-algorithms)
    * [Advantages of Greedy Algorithms](#advantages-of-greedy-algorithms)
    * [Disadvantages of Greedy Algorithms](#disadvantages-of-greedy-algorithms)
  * [Greedy Algorithms Cannot Always Give Optimal Solutions](#greedy-algorithms-cannot-always-give-optimal-solutions)
  * [Example: Fractional Knapsack Problem](#example-fractional-knapsack-problem)
    * [Steps](#steps)
    * [Implementation in Java](#implementation-in-java)
<!-- TOC -->

---

## What is a Greedy Algorithm?

A **greedy algorithm** is an approach to **solving problems by making the locally optimal choice** at each step with the hope of finding a global optimum. **This method does not always guarantee the best solution for every problem**, but it is simple and effective for some problems.

> **More precisely, the greedy algorithm is not a specific algorithm, but an algorithmic thinking (or algorithmic idea)** that can be used to guide us in designing specific algorithms and coding.
> 
> Besides this, other similar algorithmic thinking includes: partitioning, backtracking, dynamic programming.
{: .prompt-tip }

### Key Principles

1. **Local Optimality**: At each step, the algorithm makes a choice that looks best at the moment.
2. **Irrevocable Decisions**: Once a choice is made, it cannot be undone.
3. **Greedy Choice Property**: A global optimal solution can be (but not always) arrived at by selecting the local optimal choices.
4. **Optimal Substructure**: An optimal solution to the problem contains optimal solutions to the subproblems.

> Don't try to memorise the principles of the greedy algorithm, it doesn't make much sense. Practice is the most effective way to learn.
> 
> **The hardest part of the greedy algorithm is how to abstract the problem into a greedy algorithmic model (i.e., decompose the large optimal solution into smaller optimal solutions)**. Once this step is done, the coding of greedy algorithms is generally straightforward.
> 
> The correctness of the greedy algorithm seems obvious in most cases, but it is not easy to prove rigorously that the algorithm leads to an optimal solution.
{: .prompt-tip }

### Applications of Greedy Algorithms

Greedy algorithms are used in various fields and problems, including:

- **Huffman Coding**: For data compression.
- **Kruskal's and Prim's Algorithms**: For finding the Minimum Spanning Tree (MST) in a graph.
- **Fractional Knapsack Problem**: For maximizing profit with a given weight capacity.

### Advantages of Greedy Algorithms

- **Simplicity**: Greedy algorithms are typically easy to understand and implement.
- **Efficiency**: They are often more efficient in terms of time complexity compared to other approaches like dynamic programming.
- **Optimal Solutions**: For many problems, greedy algorithms provide optimal solutions.

### Disadvantages of Greedy Algorithms

- **Non-Optimal Solutions**: Greedy algorithms do not always yield the optimal solution for all problems.
- **Irrevocable Decisions**: Once a decision is made, it cannot be changed, which might lead to suboptimal solutions.

## Greedy Algorithms Cannot Always Give Optimal Solutions

**For example:**

In a weighted graph, we start at vertex `S` and find the shortest path to vertex `T`.

![](https://i.postimg.cc/brdTF0Qh/ga1.png){: .w-10 .shadow .rounded-10 }

According to the solution of the greedy algorithm, an edge with the lowest weight connected to the current vertex is chosen each time until the vertex `T` is found. **Following this idea, the shortest path we find is `S->A->E->T`**, and the length of the path is `1+4+4=9`. 

**However, this is not the shortest path.** `S->B->D->T` is the shortest path because the length of this path is `2+2+2=6`.

---

**Why doesn't the greedy algorithm work on this type of problem?**
  - **The main reason is that the previous choice affects the following choices.**
    - If we go from `S` to `A` in the first step, then the vertices and edges we face in the next step are completely different from going from `S` to `B`.

> **The greedy algorithm is suitable for those problems where the choices of subproblems do not affect each other.**
{: .prompt-tip }

## Example: Fractional Knapsack Problem

The fractional knapsack problem involves **maximizing the total value of items** placed in a knapsack with a fixed capacity, where **items can be divided** to fill the knapsack.

### Steps

1. **Calculate Value-to-Weight Ratio**: Calculate the ratio of value to weight for each item.
2. **Sort**: Sort the items based on this ratio in descending order.
3. **Select**: Add items to the knapsack in this order, taking fractions of items if necessary to maximize the total value.

### Implementation in Java

```java
public static double getMaxValue(int capacity, Item[] items) {
    Arrays.sort(items, Comparator.comparingDouble(i -> (double) i.value / i.weight).reversed());
    double totalValue = 0.0;

    for (Item item : items) {
        if (capacity == 0) break;

        if (item.weight <= capacity) {
            capacity -= item.weight;
            totalValue += item.value;
        } else {
            totalValue += item.value * ((double) capacity / item.weight);
            capacity = 0;
        }
    }
    return totalValue;
}
```
