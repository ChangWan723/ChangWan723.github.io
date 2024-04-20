---
title: Recursive
date: 2023-09-08 12:45:00 UTC
categories: [ (CS) Learning Note, Algorithm ]
tags: [ computer science, Algorithm ]
pin: false
---


Recursive algorithms are a fascinating aspect of programming and algorithm design, offering elegant solutions to complex problems by allowing a function to call itself. 

Recursive algorithms are a double-edged sword in computer science—capable of reducing complex problems to simple, elegant solutions but at the cost of potential performance and memory issues.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is a Recursive Algorithm?](#what-is-a-recursive-algorithm)
    * [Advantages of Recursive Algorithms](#advantages-of-recursive-algorithms)
    * [Disadvantages of Recursive Algorithms (Use Iteration to Avoid)](#disadvantages-of-recursive-algorithms-use-iteration-to-avoid)
    * [Applications of Recursive Algorithms](#applications-of-recursive-algorithms)
  * [Example: Climb Stairs](#example-climb-stairs)
  * [Tail Recursion: a Concept to Optimise Recursion](#tail-recursion-a-concept-to-optimise-recursion)
    * [Benefits of Tail Recursion](#benefits-of-tail-recursion)
    * [Tail Recursion vs. Non-Tail Recursion](#tail-recursion-vs-non-tail-recursion)
<!-- TOC -->

---

## What is a Recursive Algorithm?

A recursive algorithm solves a problem by dividing it into smaller, more manageable sub-problems of the same type as the original. It typically has two components:
- **Base Case:** The simplest instance of the problem which can be solved directly.
  - Recursion must have one or more base cases, which are the **termination conditions** that stop the recursion.
- **Recursive Case:** A part of the solution that involves the function calling itself.
  - The solution of a **problem can be decomposed** into the solution of several sub-problems.
  - The solution idea for this problem and the **sub-problem is exactly the same**, except for the different data sizes

**Recursion is often contrasted with iteration**, which uses loops to solve problems. While both approaches can solve many of the same problems, recursion can lead to more straightforward and easier-to-understand code for complex tasks.

### Advantages of Recursive Algorithms

- **Simplicity:** Recursive code is often cleaner and easier to write than its iterative counterparts, especially for problems inherently recursive like tree traversals.
- **Reduction of Code:** Recursion can reduce the necessity for complex loops and auxiliary data structures, leading to more concise code.

### Disadvantages of Recursive Algorithms (Use Iteration to Avoid)

- **Memory Consumption:** Each recursive call adds a new layer to the stack, which can lead to significant memory use. This is particularly problematic with deep recursion that involves many recursive calls.
- **Performance Issues:** Recursive calls can be inefficient due to overhead from repeated function calls and stack management.
  - Each recursive call needs to save the state of the function in memory, which can lead to additional overhead.
  - In contrast, iteration is easier to optimise in compilers or interpreters.
- **Risk of Stack Overflow:** Excessive recursion can lead to stack overflow errors, particularly if the termination condition is not defined properly or the problem domain is too large.

> - In most cases, iteration is more efficient than recursion. **For scenarios with high-performance requirements, we should try to use the iteration.**
>   - When feasible, converting a recursive algorithm to an iterative one can reduce memory usage and increase performance.
{: .prompt-tip }

### Applications of Recursive Algorithms

Recursive algorithms are particularly suited for tasks where the problem can naturally be divided into similar sub-problems. Some common applications include:

- **Sorting Algorithms:** Quick sort and merge sort are classical examples that use recursion for dividing arrays into smaller segments to be sorted.
- **Searching Algorithms:** Binary search is an efficient recursive algorithm for finding an item in a sorted array.
- **Tree and Graph Traversals:** Techniques like depth-first search (DFS) for trees and graphs are naturally recursive as they explore each branch before moving to the next.
- **Generating Permutations:** Recursion is a natural fit for backtracking algorithms used in solving combinatorial problems like generating permutations or solving puzzles like the N-Queens problem.

## Example: Climb Stairs

> The key to writing recursive code is to: 
>    1. Find the rules of how to break down a large problem into smaller ones and **write recursive formulas** based on the rules.
>    2. **Find termination conditions.**
>    3. **Translating** recursive formulas and termination conditions **into code**.
{: .prompt-tip }


Here’s a simple example of a recursive algorithm:

If there are `n` stairs, and you can cross 1 or 2 stairs at a time, how many ways are there to walk the `n` stairs?

- In fact, all walks can be divided into two categories based on the first step:
  1. The first step is 1 stair
  2. The first step is 2 stair
- So, The `n` stairs are the same as `1 step followed by n-1 steps` + `2 steps followed by n-2 steps`. 
  - Recursive formulas: `f(n) = f(n-1) + f(n-2)`
- Termination conditions is `f(1)=1` and `f(2)=2`.
  1. When there is one stair, there is only one way to go. `f(1)=1`
  2. When there are two stairs, there are only two ways to go. `f(2)=2`

Then, translate recursive formulas and termination conditions into code:

```java
public static int climbStairs(int n) {
    if (n <= 2) {
        return n;
    } else {
        return climbStairs(n - 1) + climbStairs(n - 2);
    }
}
```

Or, we can use iteration (more complex but more efficient):

```java
public static int climbStairs(int n) {
    if (n <= 2) {
        return n;
    } else {
        int current = 0, prev1 = 1, prev2 = 2;
        for (int i = 3; i <= n; i++) {
            current = prev1 + prev2;
            prev1 = prev2;
            prev2 = current;
        }
        return current;
    }
}
```

> - When we use recursion, we may get confused, which is normal because the human brain is really not good at understanding recursion. 
> - **The key to using recursion is that we need to abstract it into a recursive formula.** 
>   - **Don't try to break down each step of recursion with your human brain**, which only creates a barrier for yourself to understand.
>   - There's no need to think layer by layer down to subproblems and sub-sub-problems. **Block out the recursive details**, it's much easier to understand this way.
{: .prompt-tip }

## Tail Recursion: a Concept to Optimise Recursion

Tail recursion is a powerful concept in computer programming that allows for more efficient recursive function calls. **This specific setup enables compilers and interpreters to optimize the recursive calls and reduce the risk of stack overflow**, making it an essential technique for writing clean and efficient code, especially in functional programming languages.


- In essence, **tail recursion** is a form of recursion where **the recursive call is the last operation performed by the function.** 
  - There is **no need to keep any state from the current frame** of the function if the recursive call is the last statement because there are no operations left to perform in that frame. 
  - This **allows for optimizations** such as tail call elimination or tail call optimization (TCO), **where the compiler optimizes the recursion to iterative loop execution that consumes less stack space.**

### Benefits of Tail Recursion

1. **Memory Efficiency**: Tail recursion helps in saving memory because each function call does not have to maintain its own stack frame. This is particularly beneficial in languages that support optimization for tail calls.

2. **Prevent Stack Overflow**: For programming languages that support tail call optimization, tail recursion can handle larger input sizes without worrying about stack overflow.

3. **Performance Improvement**: By eliminating unnecessary stack frames, tail recursion can speed up function execution compared to non-tail recursion.

### Tail Recursion vs. Non-Tail Recursion

To understand tail recursion better, let's compare it with non-tail recursion:

- **Non-Tail Recursion**: A recursive function is considered non-tail recursive if it performs additional operations after it makes a recursive call. An example is the recursive addition function, which involves addition after the recursive call:

```c
int recursiveAdd(int n) {
    if (n == 1)
        return 1;
    else
        return n + recursiveAdd(n - 1);
}
```

When we call `recursiveAdd(5)`, the stack frame needs to store the following information:

``` 
recursiveAdd(5)
5 + recursiveAdd(4)
5 + (4 + recursiveAdd(3))
5 + (4 + (3 + recursiveAdd(2)))
5 + (4 + (3 + (2 + recursiveAdd(1))))
5 + (4 + (3 + (2 + 1)))
5 + (4 + (3 + 3))
5 + (4 + 6)
5 + 10
15
```

---


- **Tail Recursion**: If the recursive call is the last thing executed by the function, then it is tail recursive. For instance, an accumulator can be used to maintain the state, and the final operation is the recursive call:

```c
int recursiveAdd(int n, int acc) {
    if (n == 0)
        return acc;
    else
        return recursiveAdd(n - 1, n + acc);
}

int recursiveAdd(int n) {
    return recursiveAdd(n, 0);
}
```

When we call `recursiveAdd(5)`, the stack frame needs to store the following information:

``` 
recursiveAdd(5, 0)
recursiveAdd(4, 5)
recursiveAdd(3, 9)
recursiveAdd(2, 12)
recursiveAdd(1, 14)
recursiveAdd(0, 15)
15
```

In the tail recursive version of `recursiveAdd`, the state is carried through an additional parameter `acc`, allowing the function to be optimized by the compiler.

> The core idea of tail recursion is to **pass changing arguments to the recursive function's variables**
{: .prompt-tip }

> - **Not all programming languages are capable of optimizing tail recursion.** 
>   - Functional programming languages like Haskell and Scheme natively support and optimize tail recursive functions. 
>   - In contrast, languages like Python and Java do not automatically optimize tail recursion.
> - **So tail recursion is not important, just need to understand the concept in general.**
>   - To optimise the performance of recursion or to prevent stack overflow, **it is best to replace recursion with iteration.**
{: .prompt-tip }

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
