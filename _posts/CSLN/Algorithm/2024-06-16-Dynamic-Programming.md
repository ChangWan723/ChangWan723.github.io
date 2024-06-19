---
title: "Algorithmic Thinking: Dynamic Programming"
date: 2024-06-16 18:16:00 UTC
categories: [ (CS) Learning Note, Algorithm ]
tags: [ computer science, Algorithm ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is Dynamic Programming?](#what-is-dynamic-programming)
    * [Key Principles](#key-principles)
    * [Advantages of Dynamic Programming](#advantages-of-dynamic-programming)
    * [Disadvantages of Dynamic Programming](#disadvantages-of-dynamic-programming)
    * [Applications of Dynamic Programming](#applications-of-dynamic-programming)
  * [Example 1: Fibonacci Sequence](#example-1-fibonacci-sequence)
    * [Recursive Solution](#recursive-solution)
    * [Dynamic Programming Solution](#dynamic-programming-solution)
  * [Example 2: 0/1 Knapsack](#example-2-01-knapsack)
    * [Problem Statement](#problem-statement)
    * [Backtracking Solution](#backtracking-solution)
    * [Dynamic Programming Solution](#dynamic-programming-solution-1)
<!-- TOC -->

---

## What is Dynamic Programming?

Dynamic Programming (DP) is a powerful algorithmic technique used to solve complex problems by breaking them down into simpler subproblems. Unlike other methods, **DP solves each subproblem only once and stores the results**, ensuring efficiency and avoiding redundant computations.

**Dynamic Programming is an optimization approach that transforms a problem into a sequence of interdependent subproblems.** By solving each subproblem just once and storing the results, DP avoids the exponential time complexity often seen in naive recursive approaches.

### Key Principles

1. **Overlapping Subproblems**: The problem can be broken down into smaller, overlapping subproblems that can be solved independently.
2. **Optimal Substructure**: The optimal solution to the problem can be constructed from the optimal solutions of its subproblems.
3. **Memoization or Tabulation**: Use a table to store the results of subproblems to avoid redundant computations.

> **What kind of problems are suitable to be solved by dynamic programming?**
> 
> - **One model with three features**
>   - **One model: Multi-Stage Optimal Decision-Making Model**
>     - We generally use dynamic programming to solve optimal problems. And the process of solving a problem involves multiple decision-making stages. Each decision stage corresponds to some states. We then look for a set of states among them that produce the final optimal value.
>   - **Three features: Optimal Sub-Structure, No After-Effects, and Repeated Sub-Problems**
>      1. **Optimal Sub-Structure**: The optimal solution of a problem contains the optimal solutions of the sub-problems. This means that the later stage's state can be deduced from the previous stage's state.
>     2. **No After-Effects**: This has two implications. The first implication is that when deducing later stage's states, we are only concerned with the previous stage's state value, regardless of how the state was deduced. The second implication is that once the stage state is determined, it is not affected by subsequent stages. (No After-Effects does not mean that the subproblems do not affect each other.)
>     3. **Repeated Sub-Problems**: Different decisions may generate duplicate states.
{: .prompt-tip }

> **The problems that are suitable for Dynamic Programming are similar to those for Divide-and-Conquer algorithms:**
> - **They are both able to split a big problem into smaller problems.**
> - The difference is: 
>   - the **subproblems of Divide-and-Conquer** must be **independent**.
>   - the **subproblems of Dynamic Programming** are **interdependent** (This means that each subproblem needs the results of the previous subproblem to make a decision. So the results of the subproblem need to be saved for other subproblems. Otherwise, there would be a lot of repeated calculations).
{: .prompt-tip }

### Advantages of Dynamic Programming

- **Efficiency**: Reduces the time complexity of problems by storing results of subproblems and avoiding redundant computations.
- **Optimal Solutions**: Guarantees finding an optimal solution if the problem satisfies the optimal substructure property.
- **Wide Applicability**: Can be applied to a variety of optimization and combinatorial problems.

### Disadvantages of Dynamic Programming

- **Space Complexity**: May require significant memory to store results of subproblems, especially for problems with large input sizes.
- **Complexity**: Designing a dynamic programming solution can be more complex and require a deep understanding of the problem structure.

### Applications of Dynamic Programming

Dynamic Programming is used in various fields to solve a wide range of problems, including:

- **Optimization Problems**: Finding the shortest path, maximum profit, minimum cost, etc.
- **Combinatorial Problems**: Counting the number of ways to arrange objects, subsets, partitions, etc.
- **String Processing**: Longest common subsequence, edit distance, string matching.
- **Game Theory**: Solving games with perfect information, such as chess and tic-tac-toe.
- **Bioinformatics**: Sequence alignment, protein folding.

## Example 1: Fibonacci Sequence

The Fibonacci sequence is a classic example of a problem that can be solved efficiently using dynamic programming. The Fibonacci number is defined as: `F(n) = F(n-1) + F(n-2)`

### Recursive Solution

The naive recursive solution has exponential time complexity because **it recalculates the same values multiple times.**

```java
public static int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

### Dynamic Programming Solution

Using dynamic programming, we store the results of subproblems in an array, achieving linear time complexity.

```java
public static int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    int[] dp = new int[n + 1];
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

## Example 2: 0/1 Knapsack

The 0/1 Knapsack problem involves selecting items with given weights and values to maximize the total value without exceeding the weight capacity of the knapsack. Each item can either be included in the knapsack (1) or not included (0), hence the name 0/1 Knapsack.

### Problem Statement

Given:
- `n` items, each with a weight `w[i]` and a value `v[i]`
- A knapsack with a maximum weight capacity `W`

Find:
- The maximum total value that can be obtained without exceeding the weight capacity `W`

### Backtracking Solution

In [Algorithmic Thinking: Backtracking](/posts/Backtracking/#example-2-01-knapsack), I **solved this 0/1 Knapsack problem with backtracking.** But exhaustively enumerating all the scenarios may **include a lot of repeated calculations, resulting in low efficiency (time complexity is exponential: `O(2^n)`)**.

**We can try to reduce these repeated calculations:**
- **For example, we can save all the recursive states. If the state has already been calculated, return it directly.**

---

**Optimised backtracking implementation:**

```java
private static int maxValue = 0; // To store the maximum profit
private static final Set<String> states = new HashSet<>(); // To store the recursive states

// Begin with: knapsack(weights, values, capacity, 0, 0, 0);
public static void knapsack(int[] weights, int[] values, int capacity, int index, int currentWeight, int currentValue) {
    if (index == weights.length) {
        if (currentValue > maxValue) {
            maxValue = currentValue;
        }
        return;
    }
    
    String curState = index + "." + currentWeight +"." +currentValue;
    if (states.contains(curState)) { // If the state has already been calculated, return it directly.
        return;
    }
    states.add(curState);

    knapsack(weights, values, capacity, index + 1, currentWeight, currentValue); // don't pack it in
    if (currentWeight + weights[index] <= capacity) { // Pruning: If the capacity has been exceeded, do not pack it.
        knapsack(weights, values, capacity, index + 1, currentWeight + weights[index], currentValue + values[index]); // pack it in 
    }
}
```

**In fact, this contains the idea of reducing repeated calculations in dynamic programming.** And its execution efficiency is already close to the dynamic programming (at the cost of higher space complexity).

### Dynamic Programming Solution

We use a 2D array `dp` where `dp[i][w]` represents the maximum value that can be obtained using the first `i` items with a weight capacity `w`. (time complexity is exponential:`O(n*w))`)

1. **Initialization**: Initialize a 2D array `dp` where `dp[i][w]` represents the maximum value using the first `i` items with weight capacity `w`.
2. **Fill the Table**: Iterate through each item and weight capacity, updating the `dp` table based on whether the current item is included or excluded.
3. **Result**: The value in `dp[n][w]` will be the maximum value that can be obtained with the given capacity.

```java
public static int knapsack(int[] weights, int[] values, int capacity) {
    int n = weights.length;
    int[][] dp = new int[n + 1][capacity + 1];

    for (int i = 1; i <= n; i++) {
        for (int w = 0; w <= capacity; w++) {
            if (weights[i - 1] <= w) {
                dp[i][w] = Math.max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
            } else {
                dp[i][w] = dp[i - 1][w];
            }
        }
    }

    return dp[n][capacity];
}
```

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
