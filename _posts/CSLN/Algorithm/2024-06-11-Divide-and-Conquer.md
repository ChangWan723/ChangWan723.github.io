---
title: "Algorithmic Thinking: Divide-and-Conquer"
date: 2024-06-11 22:20:00 UTC
categories: [ (CS) Learning Note, Algorithm ]
tags: [ computer science, Algorithm ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is a Divide-and-Conquer Algorithm?](#what-is-a-divide-and-conquer-algorithm)
    * [Key Principles](#key-principles)
    * [Advantages of Divide-and-Conquer Algorithms](#advantages-of-divide-and-conquer-algorithms)
    * [Disadvantages of Divide-and-Conquer Algorithms](#disadvantages-of-divide-and-conquer-algorithms)
    * [Applications of Divide-and-Conquer Algorithms](#applications-of-divide-and-conquer-algorithms)
  * [Example 1: MergeSort](#example-1-mergesort)
    * [Steps](#steps)
    * [Implementation in Java](#implementation-in-java)
  * [Example 2: Closest Pair of Points in 2D Plane](#example-2-closest-pair-of-points-in-2d-plane)
    * [Steps](#steps-1)
    * [Implementation in Java](#implementation-in-java-1)
<!-- TOC -->

---

## What is a Divide-and-Conquer Algorithm?

Divide-and-conquer is a powerful algorithmic paradigm that solves complex problems by breaking them down into simpler subproblems, solving each subproblem independently, and then combining their solutions to solve the original problem.

A divide-and-conquer algorithm works by recursively breaking down a problem into two or more subproblems of the same or related type until these become simple enough to be solved directly. The solutions to the subproblems are then combined to give a solution to the original problem.

### Key Principles

Divide-and-Conquer algorithms are generally better suited to be implemented with recursion. Each level of recursion involves these three operations:

1. **Divide**: Split the problem into smaller subproblems.
2. **Conquer**: Recursively solve the subproblems.
3. **Combine**: Merge the solutions of the subproblems to solve the original problem.

> The problems that can be solved by the Divide-and-Conquer algorithm generally need to satisfy the following conditions:
> 1. **The problem can be split into subproblems which are similar to the original problem** (the same problem-solving model).
> 2. **The subproblems can be solved independently** (there is no relevance between the subproblems).
>    - This is the most obvious difference between the Divide-and-Conquer and Dynamic Programming.
> 3. **The problem has a split termination condition** (it can be solved directly when the problem is small enough);
> 4. **Subproblems can be merged into the original problem.**
>    - The complexity of this merge operation cannot be too high. Otherwise it will not be possible to reduce the overall complexity of the algorithm.
{: .prompt-tip }

### Advantages of Divide-and-Conquer Algorithms

- **Efficiency**: Divide-and-conquer algorithms can reduce the time complexity of problems, making them more efficient.
- **Simplicity**: These algorithms break down complex problems into simpler subproblems, making them easier to solve and understand.
- **Parallelism**: Subproblems can often be solved in parallel, improving performance on multi-core processors.

### Disadvantages of Divide-and-Conquer Algorithms

- **Overhead**: Recursion and combining solutions can introduce overhead, particularly for small subproblems.
- **Complexity**: Implementing divide-and-conquer algorithms can be more complex due to the need to split and merge solutions.

### Applications of Divide-and-Conquer Algorithms

Divide-and-conquer algorithms are used in various fields and for solving different types of problems, including:

- **Sorting Algorithms**: QuickSort, MergeSort.
- **Multiplication of Large Numbers**: Karatsuba Algorithm.
- **Computational Geometry**: Closest Pair of Points.

## Example 1: MergeSort

MergeSort is a classic example of a divide-and-conquer algorithm that sorts an array by recursively splitting it into halves, sorting each half, and then merging the sorted halves.

### Steps

1. **Divide**: Split the array into two halves.
2. **Conquer**: Recursively sort each half.
3. **Combine**: Merge the two sorted halves to produce the sorted array.

### Implementation in Java

```java
public static void mergeSort(int[] array, int left, int right) {
    if (left < right) {
        int middle = (left + right) / 2;
        mergeSort(array, left, middle);
        mergeSort(array, middle + 1, right);
        merge(array, left, middle, right);
    }
}

private static void merge(int[] array, int left, int middle, int right) {
    int n1 = middle - left + 1;
    int n2 = right - middle;

    int[] leftArray = new int[n1];
    int[] rightArray = new int[n2];

    for (int i = 0; i < n1; i++) {
        leftArray[i] = array[left + i];
    }
    for (int j = 0; j < n2; j++) {
        rightArray[j] = array[middle + 1 + j];
    }

    int i = 0, j = 0;
    int k = left;

    while (i < n1 && j < n2) {
        if (leftArray[i] <= rightArray[j]) {
            array[k] = leftArray[i];
            i++;
        } else {
            array[k] = rightArray[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        array[k] = leftArray[i];
        i++;
        k++;
    }

    while (j < n2) {
        array[k] = rightArray[j];
        j++;
        k++;
    }
}
```

## Example 2: Closest Pair of Points in 2D Plane

 Given `n` points in a 2D plane, the goal is to find the pair of points with the smallest Euclidean distance between them.

### Steps

1. **Divide**: Sort the points based on their x-coordinates and split them into two halves.
   - Split termination condition: when the size of the set of points is small enough (e.g. less than 3), use the brute force solution (Time Complexity : `O(n)`).
2. **Conquer**: Recursively find the closest pair of points in each half.
   - Recursively find the smallest distances in both subarrays. Let the distances be `dl` and `dr`. Find the minimum of `dl` and `dr`. Let the minimum be `d`.
3. **Combine**: Compare the minimum distance found in each half with the minimum distance across the split line.
   - The combining step needs to consider the closest point pairs that cross the split line: find all points whose `x` coordinate is closer than `d` to the middle vertical line. 
   - Build an array `strip[]` of all such points. From the first look, it seems to be a `O(n^2)` step, but it is actually `O(n)`. It can be proved geometrically that for every point in the strip, we only need to check at most 7 points after it (note that strip is sorted according to Y coordinate). See [this](https://people.csail.mit.edu/indyk/6.838-old/handouts/lec17.pdf) for more analysis.

![](https://i.postimg.cc/SRXBSZrh/dac1.png){: .w-10 .shadow .rounded-10 }
_find the smallest distances in both subarrays_

![](https://i.postimg.cc/KvtZtzPy/dac2.png){: .w-10 .shadow .rounded-10 }
_build an array strip[]_

### Implementation in Java

```java 
// entry function that takes and sorts the array of points, and calls the recursive function.
public static PointPair findClosestPair(Point[] points) {
    Point[] Px = points.clone();
    Point[] Py = points.clone();

    Arrays.sort(Px, Comparator.comparingInt(p -> p.x));
    Arrays.sort(Py, Comparator.comparingInt(p -> p.y));

    return closestPairRec(Px, Py);
}

// recursive implementation of the Divide-and-Conquer method to partition the set of points and find the closest point pairs.
private static PointPair closestPairRec(Point[] Px, Point[] Py) {
    int n = Px.length;
    if (n <= 3) {
        return bruteForce(Px);
    }

    int mid = n / 2;
    Point midPoint = Px[mid];

    Point[] Qx = Arrays.copyOfRange(Px, 0, mid);
    Point[] Rx = Arrays.copyOfRange(Px, mid, n);

    Point[] Qy = Arrays.stream(Py).filter(p -> p.x <= midPoint.x).toArray(Point[]::new);
    Point[] Ry = Arrays.stream(Py).filter(p -> p.x > midPoint.x).toArray(Point[]::new);

    PointPair leftPair = closestPairRec(Qx, Qy);
    PointPair rightPair = closestPairRec(Rx, Ry);

    PointPair bestPair = leftPair.distance < rightPair.distance ? leftPair : rightPair;

    Point[] strip = Arrays.stream(Py).filter(p -> Math.abs(p.x - midPoint.x) < bestPair.distance).toArray(Point[]::new);
    PointPair splitPair = closestSplitPair(strip, bestPair.distance);

    return splitPair.distance < bestPair.distance ? splitPair : bestPair;
}

// when the point set size is small, a brute force algorithm is used directly
private static PointPair bruteForce(Point[] points) {
    double minDist = Double.MAX_VALUE;
    PointPair closestPair = null;

    for (int i = 0; i < points.length; i++) {
        for (int j = i + 1; j < points.length; j++) {
            double dist = distance(points[i], points[j]);
            if (dist < minDist) {
                minDist = dist;
                closestPair = new PointPair(points[i], points[j], dist);
            }
        }
    }
    return closestPair;
}

// find the possible closest point pairs
private static PointPair closestSplitPair(Point[] strip, double delta) {
    double minDist = delta;
    PointPair closestPair = null;

    for (int i = 0; i < strip.length; i++) {
        for (int j = i + 1; j < strip.length && (strip[j].y - strip[i].y) < minDist; j++) {
            double dist = distance(strip[i], strip[j]);
            if (dist < minDist) {
                minDist = dist;
                closestPair = new PointPair(strip[i], strip[j], dist);
            }
        }
    }
    return closestPair != null ? closestPair : new PointPair(null, null, minDist);
}

// calculate the Euclidean distance between two points.
private static double distance(Point p1, Point p2) {
    return Math.sqrt(Math.pow((p1.x - p2.x), 2) + Math.pow((p1.y - p2.y), 2));
}
```

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
- https://www.geeksforgeeks.org/closest-pair-of-points-using-divide-and-conquer-algorithm/
