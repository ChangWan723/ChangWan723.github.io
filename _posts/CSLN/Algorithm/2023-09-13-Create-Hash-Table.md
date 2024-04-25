---
title: How to Design a Hash Table
date: 2023-09-13 12:00:00 UTC
categories: [ (CS) Learning Note, Algorithm and Data Structure ]
tags: [ computer science, Data Structure ]
pin: false
---


Designing a good hash table involves not just implementing the basic functionalities but also ensuring it meets the high standards of performance, reliability, and scalability required in production environments.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Design Considerations for Hash Tables](#design-considerations-for-hash-tables)
    * [Choosing the Right Hash Function](#choosing-the-right-hash-function)
    * [Dynamic Resizing](#dynamic-resizing)
    * [Handling Collisions](#handling-collisions)
    * [Memory Efficiency](#memory-efficiency)
    * [Concurrency Support](#concurrency-support)
  * [Dynamic Resizing of Hash Tables](#dynamic-resizing-of-hash-tables)
    * [When to Resize](#when-to-resize)
    * [Challenges and Considerations](#challenges-and-considerations)
  * [Strategies to Avoid Inefficient Resize](#strategies-to-avoid-inefficient-resize)
    * [Gradual Expansion](#gradual-expansion)
    * [Proactive Monitoring](#proactive-monitoring)
    * [Elastic Resizing](#elastic-resizing)
  * [Example of an Industrial Grade Hash Table: HashMap in Java](#example-of-an-industrial-grade-hash-table-hashmap-in-java)
    * [Initial Size](#initial-size)
    * [Load Factor and Dynamic Expansion](#load-factor-and-dynamic-expansion)
    * [Handling Collisions](#handling-collisions-1)
    * [Hash Function](#hash-function)
<!-- TOC -->

---

## Design Considerations for Hash Tables

### Choosing the Right Hash Function

- A good hash function for a hash table should have the following characteristics:
  - **Uniform Distribution**: The hash function should distribute keys uniformly across the array to minimize collisions.
  - **Efficiency**: It should be computationally efficient to avoid becoming a bottleneck.
  - **Adaptability**: Capable of handling a range of key types and sizes.

### Dynamic Resizing

- **Load Factor Management**: Monitor the load factor (ratio of number of stored entries to the table's capacity) and resize the hash table (typically doubling the size) when it exceeds a certain threshold (e.g., 0.75).
- **Resizing Strategy**: Ensure resizing is done efficiently to redistribute all entries and minimize performance impact during resizing.

### Handling Collisions

- **Chaining vs. Open Addressing**: Choose between chaining (storing collisions in a linked list) and open addressing (probing for another empty slot). Chaining is simpler and more straightforward, while open addressing is more space-efficient.

### Memory Efficiency

- **Pre-allocation**: Consider pre-allocating larger memory blocks to minimize frequent memory allocations.
- **Reasonable Memory Usage**: Not wasting too much memory space.

### Concurrency Support

- **Locking Mechanisms**: Implement fine-grained locking or lock-free structures to allow safe concurrent access by multiple threads.
- **Thread-Safe Design**: Ensure operations are atomic and consistent, using mutexes or other synchronization primitives where necessary.

## Dynamic Resizing of Hash Tables

Dynamic resizing in hash tables is the process of adjusting the size of the underlying array or bucket list based on the current load factor. The load factor, typically defined as the ratio of the number of entries to the number of slots, is used to determine when resizing is necessary.

### When to Resize

- **Upsizing**: When the load factor exceeds a certain upper threshold (commonly set between 0.7 and 0.8), the hash table is resized by increasing its capacity. **This expansion helps reduce the load factor, thereby decreasing the likelihood of collisions and maintaining fast access times.**
  - The process of upsizing usually involves **reapplying for a larger hash table and moving all data** to this new hash table. **This also involves recalculating the hash code for each existing element** based on the new array size and finding its new position in the resized array.
- **Downsizing**: Conversely, if the load factor falls below a lower threshold (such as 0.2), the hash table may shrink to reduce space inefficiency. 
  - Downsizing is generally not necessary. Since we mostly care more about execution efficiency and can tolerate consuming a little bit more memory space, then we don't need to go through the trouble of downsizing.

### Challenges and Considerations

- **Resizing Cost**: Resizing a hash table can be costly since it involves rehashing all existing entries to new positions in the newly sized array. This operation is `O(n)` and can lead to performance hiccups if not handled carefully.
- **Choosing Resize Points**: Setting optimal thresholds for resizing requires careful consideration to balance between performance and memory usage. Too frequent resizing can degrade overall performance, while too sparse resizing might not adequately address collision issues.
- **Concurrency Issues**: In multi-threaded environments, resizing needs to be thread-safe to prevent data corruption. This usually involves locking mechanisms that can temporarily hinder concurrent operations.

## Strategies to Avoid Inefficient Resize

### Gradual Expansion

**Gradual Expansion is suitable for large amounts of data.** Rather than resizing the hash table drastically whenever the load factor threshold is reached, implement a more **gradual** expansion strategy. This involves expanding the hash table incrementally and distributing the rehashing process over several insert operations. This method can **significantly reduce the latency spikes** associated with resizing.

> From the user's point of view, although in most cases, the insertion of a data operation is very fast, but the occasional very slow insertion operation will also make the user uncomfortable. At this point, a "one-time" capacity expansion is not appropriate, which could lead to latency spikes.
{: .prompt-tip }

- What is Gradual Expansion?
  - **After the loading factor touches the threshold, we only apply for new hash table, but do not move the old data to the new hash table.**
  - When there is new data to be inserted, we insert the new data into the new hash table and take a data from the old hash table and put it into the new hash table.
  - Each time we insert a data into the hash table, we repeat the above process. After several insertion operations, all the data in the old hash table will be moved to the new hash table bit by bit.
  - Thus there is no "one-time" data moving, and latency spikes can be avoided.

![](https://i.postimg.cc/pL4jk0r4/image10.png){: .w-10 .shadow .rounded-10 }

### Proactive Monitoring

Implement monitoring of both the load factor and the growth trends of the hash table data. By understanding data insertion patterns, you can predict when resizing will be necessary and prepare for it in advance, thus smoothing out the computational cost over time.

### Elastic Resizing

Consider implementing an elastic resizing mechanism that adjusts the resizing behavior based on the current usage and performance metrics. If the system is under heavy load, postpone aggressive resizing to avoid further performance degradation. Conversely, during periods of low activity, more aggressive resizing could be performed to prepare for future demands.

## Example of an Industrial Grade Hash Table: HashMap in Java

`HashMap` in Java uses an array and linked lists (or trees for large lists) to store map entries. It uses hashing to convert keys to indexes of arrays. This design allows it to offer constant time performance for `get` and `put` operations under ideal conditions.

### Initial Size

- The default initial size (capacity) of HashMap is 16, and it is the number of buckets in the hash table. 
  - This default value can be modified. **But the value is always a power of 2.**
    - **The power of 2 allows the use of bitwise `AND` to calculate the bucket index appropriately.**
    - For example, if you specify a capacity of 100, Java will adjust it to 128, which is the next power of two after 100.
  - If you know the approximate amount of data in advance, you can reduce the number of dynamic resizes by modifying the default initial size, which will greatly improve the performance of HashMap.

### Load Factor and Dynamic Expansion

- The default **load factor** is `0.75`, which offers a good trade-off between time and space costs. 
  - When the number of elements in the HashMap exceeds `0.75 * capacity`, the expansion will be launched, and each expansion will be twice the original size.

### Handling Collisions

- HashMap uses the **Chaining** to resolve conflicts.
  - If the liked list is too long, the performance of HashMap will be seriously affected. 
  - So, in the JDK1.8 version, Java introduced the red-black tree in HashMap. And when the length of the linked list is too long (more than 8), the linked list is converted to a red-black tree, which improves worst-case performance from `O(n)` to `O(log n)`.
  - When the number of red-black tree nodes is less than 8, the red-black tree is converted to a linked list. This is because there is no performance advantage of a red-black tree compared to a linked list when the amount of data is small.


### Hash Function

The design of the hash function in HashMap is not complex and pursues simplicity, efficiency and uniformity of distribution.

**Hash Function** of HashMap:

```java 
int hash(Object key) {
    int h = key.hashCode()；
    return (h ^ (h >>> 16)) & (capacity - 1);
}
```

Let's break down how it works:

1. **Calculate Hash Code**: First, it calculates the hash code of the key object using `hashCode()`. 
   - The `hashCode()` method of the key object generates an integer hash code representing the object's value. This hash code is used as the basis for determining the bucket index.

2. **XOR and Shift**: It then performs an `XOR` (`^`) operation with the shifted version (`>>> 16`) of `h`. 
   - The shift operation (`>>> 16`) moves the bits of `h` 16 positions to the right. 
   - This step is intended to mix the bits of the hash code in order to **improve the distribution of hash values.**

3. **Bitwise `AND`**: Finally, it performs a bitwise `AND` (`&`) operation with (`capacity - 1`). 
   - `& (capacity - 1)`: This is why the capacity must always be a power of 2 (since all bits of `capacity - 1` are set to `1`, which is appropriate for `AND (&)`).
   - This operation ensures that the resulting hash code falls within the range of valid bucket indices by masking out the higher bits.
   - This is done by keeping only the lower bits of the hash code, discarding any higher bits that might cause the index to exceed the capacity of the hash table.

<br>

---

**Reference:**

- Wang, Zheng (2019) _The Beauty of Data Structures and Algorithms_. Geek Time.
