---
title: "Binary Search: The Power of O(log n)"
date: 2023-09-10 12:00:00 UTC
categories: [ (CS) Learning Note, Algorithm]
tags: [ computer science, Algorithm ]
pin: false
---


Binary search is a classic algorithm in computer science with time complexity `O(log n)`, renowned for its efficiency in searching sorted arrays. Unlike linear search, which scans each element sequentially, binary search halves the search space with each step, making it a much faster alternative for large datasets.

> - **Sometimes, algorithms of `O(log n)` time complexity are more efficient than `O(1)`.** This is because:
>   - **For `O(log n)`, even if `n` is very very large, the corresponding `log n` is small.** 
>   - And the Big O notation method for time complexity **omits constants**, factors, and lower order terms. So, **`O(1)` It is possible to represent a relatively large constant value, such as `O(1000)`, `O(10000)`.**
{: .prompt-tip }

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction of Binary Search](#introduction-of-binary-search)
    * [Limitations of Binary Search](#limitations-of-binary-search)
  * [How Binary Search Works](#how-binary-search-works)
    * [Implementing Binary Search](#implementing-binary-search)
    * [Implementing Binary Search in a Circularly Sorted Array](#implementing-binary-search-in-a-circularly-sorted-array)
<!-- TOC -->

---

## Introduction of Binary Search

Binary search is a divide-and-conquer algorithm that **efficiently locates the position of a target value within a sorted array.** By comparing the target value to the middle element of the array, binary search quickly narrows down the area in which the target can be found, either by discarding the left half or the right half of the array.

### Limitations of Binary Search

- **Requirement for Sorted Input**: Binary search requires the input array to be sorted beforehand. If the array is not sorted, binary search cannot be applied directly, and sorting the array can add a time complexity of O(n log n).
- **Inapplicable to Non-Random Access Data Structures**: Binary search cannot be applied to data structures with non-random access, such as linked lists, because it relies on the ability to access elements by index.
- **Not Suitable for Excessive Data Volume**: Binary search is efficient with large amounts of data, but at the same time, it is also very demanding on memory. The implementation of binary search requires data structures that support random access, which **requires space contiguity** and is demanding on memory.

## How Binary Search Works

The process of binary search involves repeatedly dividing the search interval in half. If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half. Otherwise, narrow it to the upper half. Repeatedly check until the value is found or the interval is empty. Here’s a step-by-step breakdown:

1. **Initialize**: Start with two pointers, one pointing to the first index of the array (`low`) and the other to the last index (`high`).
2. **Middle Element**: Find the middle element of the array.
3. **Comparison**:
   - If the middle element is equal to the target value, the search is complete.
   - If the target value is smaller, continue the search on the left half, setting `high` to `mid - 1`.
   - If the target value is larger, continue on the right half, setting `low` to `mid + 1`.
4. **Repeat**: Continue the process until `low` exceeds `high`, indicating that the target is not in the array.

### Implementing Binary Search

Here is a simple implementation of binary search:

```java
public int binarySearch(int[] arr, int target) {
    int low = 0;
    int high = arr.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2; // Here we can use bit operations (int mid = low + ((high - low) >> 2)) to get a more efficient operation
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1;
}
```

> Some considerations for implementing binary search:
> 1. **Loop Exit Condition**: Note that it is `low<=high`, not `low<high`. Using `low<high` causes the boundary case (`low=high`) to be unchecked.
> 2. **Overflow Protection**: In some programming languages, calculating the middle index as `(low + high) / 2` can lead to overflow when the volume of data is large. Using `low + (high - low) / 2` prevents this issue.
> 3. **Updates to Low and High**: Note that it is `low=mid+1` and `high=mid-1`, not `low=mid` and `high=mid`. Using the latter may result in an infinite loop.
{: .prompt-warning }


### Implementing Binary Search in a Circularly Sorted Array

For a sorted array that is circularly sorted, such as `4, 5, 6, 1, 2, 3`, implementing a binary search algorithm to find a value equal to a given value requires a modification of the standard binary search approach. Here's how you can do it: 

```java
public int binarySearch(int[] arr, int target) {
    int left = 0;
    int right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        }

        if (nums[mid] >= nums[0]) { // Left half in order
            if (nums[0] <= target && target < nums[mid]) { // The target value is in the left half
                right = mid - 1; // Search in the left half
            } else {
                left = mid + 1; // Search in the right half
            }
        } else { // Right half in order
            if (nums[mid] < target && target <= nums[nums.length - 1]) { // The target value is in the right half
                left = mid + 1; // Search in the right half
            } else {
                right = mid - 1; // Search in the left half
            }
        }
    }

    return -1;
}
```

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
