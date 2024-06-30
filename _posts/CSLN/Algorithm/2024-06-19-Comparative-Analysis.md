---
title: Comparison of Four Algorithmic Thinking
date: 2024-06-19 20:00:00 UTC
categories: [ (CS) Learning Note, Algorithm ]
tags: [ computer science, Algorithm ]
pin: true
---

The four algorithmic thinking (Greedy, Divide-and-Conquer, Backtracking, and Dynamic Programming) is essential for solving complex problems efficiently. But what's the difference between them? Which algorithm should we choose if we encounter a complex problem?

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Overview of the Four Algorithmic Thinking](#overview-of-the-four-algorithmic-thinking)
    * [Greedy](#greedy)
    * [Divide-and-Conquer](#divide-and-conquer)
    * [Backtracking](#backtracking)
    * [Dynamic Programming](#dynamic-programming)
  * [Similarities and Differences](#similarities-and-differences)
    * [Similarities: Breaking Down the Problem into Subproblems](#similarities-breaking-down-the-problem-into-subproblems)
    * [Differences: They are Suitable for Different Types of Subproblems](#differences-they-are-suitable-for-different-types-of-subproblems)
<!-- TOC -->

---


## Overview of the Four Algorithmic Thinking

### Greedy

Greedy algorithms make a series of choices, each of which looks best at the moment, with the hope of finding a global optimum. They do not reconsider their choices, making them straightforward but sometimes suboptimal.

### Divide-and-Conquer

Divide-and-conquer algorithms split a problem into smaller subproblems, solve each subproblem independently, and combine their solutions to solve the original problem.

### Backtracking

Backtracking algorithms build solutions incrementally and backtrack as soon as an invalid solution is reached. They explore all possible configurations, making them exhaustive but often inefficient for large problems.

### Dynamic Programming

Dynamic programming (DP) is an optimisation technique that solves problems by breaking them down into simpler subproblems, storing the results of these subproblems to avoid redundant calculations. DP is effective for problems with overlapping subproblems and optimal substructure.

## Similarities and Differences

### Similarities: Breaking Down the Problem into Subproblems

All four algorithms are used to **solve complex problems by breaking them down into simpler subproblems.**

Therefore, if you find a complex problem difficult to solve, and it can be broken down into simpler subproblems, you should consider using one of the four algorithms. 

### Differences: They are Suitable for Different Types of Subproblems

- **Greedy**: It is suitable for the problems where the **decisions (choices)** of subproblems do **not affect** each other. 
  - This means that we can choose the optimal solution at each stage without worrying about influencing the choice of subsequent optimal solutions
- **Divide-and-Conquer**: It is suitable for the problems where the subproblems are not connected and **independent** of each other. And each subproblem is usually not about making decisions (choices).
  - This means that we cannot break the problem down into multi-stage subproblems. And each subproblem is on the same level (and the final result is usually merged out), not derived in stages.
- **Backtracking**: It is suitable the problems where the subproblems with **no regularity**.
  - The backtracking algorithm is equivalent to the exhaustive search. Because we don’t know the regularity of the scenario, we have to traverse all the solutions.
- **Dynamic programming**: It is suitable for the problems where the subproblems are **interdependent** of each other. And the decisions (choices) of each subproblem can interfere with each other.
  - This means that each subproblem needs the results of the previous subproblem to make a decision. So the results of the subproblem need to be saved for other subproblems. Otherwise, there would be a lot of repeated calculations

---

| Algorithmic Thinking         | Approach                                 | Optimal Solution               | Efficiency                              | Example                             |
|------------------|------------------------------------------|--------------------------------|-----------------------------------------|-----------------------------------------|
| Greedy           | Locally optimal choice at each step      | Sometimes                      | Efficient                               | Fractional Knapsack         |
| Divide-and-Conquer | Divide, solve subproblems, combine     | Often (sometimes no optimal solution is involved) | Efficient for independent subproblems, but need to merge subproblems | MergeSort, QuickSort, Closest Pair of Points in 2D Plane    |
| Backtracking     | Incremental solution, backtrack on failure | Yes (exhaustive search)        | Often inefficient                       | N-Queens, Sudoku, Hamiltonian Path      |
| Dynamic Programming | Break down, solve once, store results | Yes                            | Time-efficient, but needs extra space              | 0/1 Knapsack, Longest Common Subsequence |

---

> **Divide-and-Conquer is fundamentally different from the other three algorithms in subproblem division**: Divide-and-Conquer cannot divide the problem into multi-stage subproblems (each subproblem is on the same level, not derived in stages).
{: .prompt-tip }

> **The Backtracking algorithm has a wide range of suitability.** Basically, we can use the Backtracking algorithm to solve any problem (but not efficient) that can be solved by Dynamic Programming and Greed.
{: .prompt-tip }

> **The Greedy algorithm is actually a special case of a Dynamic Programming**: where decisions (choices) of subproblems do not affect each other. In this case, each subproblem does not need the results of the previous subproblem to make a decision. So the results of the subproblem do not need to be saved.
{: .prompt-tip }

---

- **More about:**
  - [Algorithmic Thinking: Greedy](/posts/Greedy-Algorithms/)
  - [Algorithmic Thinking: Divide-and-Conquer](/posts/Divide-and-Conquer/)
  - [Algorithmic Thinking: Backtracking](/posts/Backtracking/)
  - [Algorithmic Thinking: Dynamic Programming](/posts/Dynamic-Programming/)
