---
title: "Graph Traversal: Breadth-First Search and Depth-First Search"
date: 2023-09-19 12:00:00 UTC
categories: [ (CS) Learning Note, Algorithm]
tags: [ computer science, Algorithm ]
pin: false
---

Graph traversal is a fundamental aspect of working with graph data structures, involving the process of visiting all vertices in a graph in a systematic manner. Two of the most widely used traversal algorithms are Breadth-First Search (BFS) and Depth-First Search (DFS).

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Breadth-First Search (BFS)](#breadth-first-search-bfs)
    * [Introduction](#introduction)
    * [How BFS Works](#how-bfs-works)
    * [Example Implementation](#example-implementation)
    * [Applications of BFS](#applications-of-bfs)
  * [Depth-First Search (DFS)](#depth-first-search-dfs)
    * [Introduction](#introduction-1)
    * [How DFS Works](#how-dfs-works)
    * [Example Implementation](#example-implementation-1)
    * [Applications of DFS](#applications-of-dfs)
  * [BFS vs. DFS](#bfs-vs-dfs)
<!-- TOC -->

---

## Breadth-First Search (BFS)

### Introduction

Breadth-First Search (BFS) is a traversal algorithm that starts at a specified root node and explores all its neighboring nodes at the present depth level before moving on to nodes at the next depth level. It is particularly useful for finding the shortest path on unweighted graphs.

![](https://i.postimg.cc/GhdvVgNS/bd1.png){: .w-10 .shadow .rounded-10 }

### How BFS Works

1. **Initialization**: Start from the root node, mark it as visited, and enqueue it.
2. **Traversal**: Dequeue a node from the front of the queue, visit its unvisited neighbors, mark them as visited, and enqueue them.
3. **Repetition**: Repeat the process until the queue is empty.



### Example Implementation

Here’s a simple example of BFS in Python:

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)

    while queue:
        vertex = queue.popleft()
        print(vertex, end=" ")

        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

### Applications of BFS

- **Shortest Path**: BFS is used in unweighted graphs to find the shortest path between two nodes.
- **Level Order Traversal**: BFS is used in tree structures for level-order traversal.
- **Connected Components**: It helps in finding all connected components in an undirected graph.

## Depth-First Search (DFS)

### Introduction

Depth-First Search (DFS) is a traversal algorithm that starts at a specified root node and explores as far as possible along each branch before backtracking. DFS can be implemented using recursion or an explicit stack.

![](https://i.postimg.cc/G28hMDvj/bd2.png){: .w-10 .shadow .rounded-10 }

### How DFS Works

1. **Initialization**: Start from the root node, mark it as visited.
2. **Traversal**: Recursively visit an unvisited neighbor, mark it as visited, and repeat until no unvisited neighbors are left.
3. **Backtracking**: Backtrack to the previous node and repeat the process for other unvisited neighbors.

### Example Implementation

Here’s a simple example of DFS in Python using recursion:

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    print(start, end=" ")

    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

### Applications of DFS

- **Path Finding**: DFS is used to find paths from the source to the destination in a graph.
- **Topological Sorting**: Used in Directed Acyclic Graphs (DAGs) for topological sorting.
- **Cycle Detection**: DFS helps in detecting cycles in both directed and undirected graphs.
- **Connected Components**: DFS is used to identify connected components in a graph.
- **Maze and Puzzle Solving**: It is used in algorithms for solving mazes and puzzles where the solution path needs to be explored.

## BFS vs. DFS

- **Strategy**:
  - BFS explores neighbors level by level, ensuring all nodes at the present depth are visited before moving deeper.
  - DFS explores as far as possible along each branch before backtracking.

- **Data Structures**:
  - BFS uses a **queue** to manage the nodes to be visited.
  - DFS uses a **stack** (or recursion, which implicitly uses the call stack) to manage the nodes to be visited.

- **Use Cases**:
  - BFS is optimal for finding the shortest path in unweighted graphs.
  - DFS is useful for problems involving traversing the entire graph, pathfinding, and connectivity analysis.

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
