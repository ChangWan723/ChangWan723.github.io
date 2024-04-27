---
title: Designing a Generic, High-Performance Sorting Algorithm
date: 2023-09-09 12:30:00 UTC
categories: [ (CS) Learning Note, Algorithm]
tags: [ computer science, Algorithm ]
pin: false
---


In the quest for efficiency and versatility in software development, the design of sorting algorithms plays a pivotal role. A well-crafted sorting algorithm can significantly enhance the performance of applications, especially those involving complex data management tasks.

> **Sorting functions are very frequently used** and very basic functions in every system or language (like C, Java), and **performance should be optimised to the extreme.**
{: .prompt-tip }

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Principles of High-Performance Sorting Algorithms](#principles-of-high-performance-sorting-algorithms)
  * [Some Examples about Generic, High-Performance Sorting](#some-examples-about-generic-high-performance-sorting)
    * [How to Optimise Quick Sort?](#how-to-optimise-quick-sort)
    * [How `qsort()` Work in Glibc?](#how-qsort-work-in-glibc)
    * [TimSort: How `Arrays.sort()` and `Collection.sort()` Work in Java?](#timsort-how-arrayssort-and-collectionsort-work-in-java)
<!-- TOC -->

---

## Principles of High-Performance Sorting Algorithms

When designing a sorting algorithm, the goal is to achieve efficiency in terms of **time and space complexity** while ensuring **adaptability** and **stability** across different types of data and use cases. Here are some guiding principles:

1. **Adaptive:** A good sorting algorithm should adapt its behavior based on the input data. It should optimize its operations to handle data that is already partially sorted or exhibits patterns. It should optimise its operation according to the different sizes or characteristics of the input data.

2. **Stable:** For applications where the relative order of equal elements needs to be preserved (e.g., in multi-key sorting), stability is a crucial feature.

3. **Low Overhead:** Especially important in lightweight applications, or when sorting small arrays, the algorithm should have minimal overhead.

4. **Scalable:** The algorithm should perform well as the size of the dataset grows, maintaining efficiency in both time and space.

5. **Hybrid Approach:** Combining two or more sorting techniques can leverage the strengths of each under different conditions.

## Some Examples about Generic, High-Performance Sorting

### How to Optimise Quick Sort?

1. **Choosing the Right Pivot**: Sometimes, the time complexity of Quick Sort gets worse because of poor pivot selection.
   - **Median-of-Three:** A common approach is to choose the median of the first, middle, and last elements of the array as the pivot. This method tends to improve performance on sorted or nearly sorted arrays.
   - **Random Pivot:** Randomly selecting a pivot element reduces the likelihood of encountering the worst-case scenario and gives QuickSort a probabilistic guarantee of good performance. This method does not guarantee a better selection of Pivots each time, but it is also unlikely that the Pivots will be poorly selected each time
2. **Optimizing Partitioning**
   - **Three-way Partitioning (Dual-Pivot Quick Sort):** Dual-Pivot Quick Sort divides the array into three parts by choosing two Pivots, the left element is less than the first Pivot, the middle element is between the first and second Pivots, and the right element is greater than the second Pivot. The left, middle and right parts are then recursively sorted separately. This is particularly useful for arrays with many duplicate elements, which can reduce the times that elements swap positions.
3. **Reducing Recursion**
   - **Replace recursion with iteration** Replace recursive calls dealing with larger arrays with iteration.
4. **Ensuring Stability**
   - **Stable Partitioning:** To make QuickSort stable, you can employ a stable partitioning algorithm, though this might incur additional space complexity.

### How `qsort()` Work in Glibc?

The `qsort()` function in Glibc is an implementation of the QuickSort algorithm and is widely used across various programming scenarios in C due to its efficiency and general applicability.

`qsort()` is an optimised QuickSort. It works in the following steps:

1. **Choosing a Pivot**: The pivot selection is crucial for QuickSort’s performance. Glibc's qsort() uses a "median-of-three" strategy to choose the pivot, which typically involves comparing the first, middle, and last elements of the partition. This method helps avoid the worst-case performance on already sorted arrays.
2. **Partitioning**: Once the pivot is selected, the array is divided into two partitions. Elements less than the pivot go to the left, and elements greater go to the right.
3. **Recursive Sorting**: The function then recursively sorts the sub-arrays formed by the partitioning. Unlike a naive QuickSort, Glibc’s qsort() implements several strategies to reduce the depth of recursive calls and manage stack usage efficiently.
4. **Insertion Sort for Small Arrays**: For smaller sub-arrays, Glibc switches to insertion sort, which is more efficient for small datasets. This hybrid approach significantly improves the overall performance of the sorting process.

### TimSort: How `Arrays.sort()` and `Collection.sort()` Work in Java?

TimSort, named after Tim Peters who implemented it for Python in 2002, exemplifies these principles. Java adopted TimSort in its `Arrays.sort()` and `Collection.sort()` method due to its superior performance with real-world data. TimSort is a hybrid of merge sort and insertion sort, bringing together the best of both worlds: the speed of insertion sort on small arrays and the scalability of merge sort for larger datasets.

TimSort is an optimised MergeSort. It works in the following steps:

1. **Identify Runs:** The array is scanned sequentially to identify "runs" (either ascending or descending sequences of data).

2. **Sort Runs:** Each run is sorted using binary insertion sort, which is very efficient for small segments.

3. **Merge Runs:** Sorted runs are merged using a technique inspired by merge sort. TimSort employs a sophisticated merging strategy that minimizes comparisons and uses a temporary array to facilitate efficient merging.

---

Here’s a simplified example of how you might implement a basic version of TimSort in Java:

```java
public class TimSort {
    private static final int RUN = 32; // optimal length of a run

    // Function to sort an array using TimSort
    public static void sort(int[] arr, int n) {
        // Sort individual subarrays of size RUN
        for (int i = 0; i < n; i += RUN) {
            binaryInsertionSort(arr, i, Math.min((i + 31), (n - 1)));
        }

        // Start merging from size RUN (or 32). It will merge to form size 64, then 128, 256 and so on ....
        for (int size = RUN; size < n; size = 2 * size) {
            for (int left = 0; left < n; left += 2 * size) {
                // Find ending point of left subarray
                int mid = left + size - 1;
                int right = Math.min((left + 2 * size - 1), (n - 1));

                // Merge subarrays arr[left...mid] & arr[mid+1...right]
                merge(arr, left, mid, right);
            }
        }
    }
}
```

This example provides a basic framework for TimSort, demonstrating the practical application of hybrid sorting techniques for achieving high performance in Java’s array sorting.

> The above is just the most basic implementation of TimSort, showing its basic idea. Actual TimSort is more complex than this.
{: .prompt-warning }

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
