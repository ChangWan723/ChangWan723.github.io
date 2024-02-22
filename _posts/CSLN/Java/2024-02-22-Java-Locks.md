---
title: Locks in Java
date: 2024-02-22 19:16:00 UTC
categories: [(CS) Learning Note, Java]
tags: [software engineering, Java]
pin: false
---

In the world of Java concurrency, understanding and effectively using locks is crucial for building reliable and efficient multi-threaded applications. Locks in Java provide a mechanism for controlling access to shared resources, ensuring that only one thread can access a resource at a time, thereby preventing data corruption and ensuring thread safety.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Types of Locks in Java](#types-of-locks-in-java)
    * [Intrinsic Locks (Synchronized Blocks)](#intrinsic-locks-synchronized-blocks)
    * [Reentrant Locks](#reentrant-locks)
    * [ReadWriteLock](#readwritelock)
    * [StampedLock](#stampedlock)
  * [Best Practices for Using Locks](#best-practices-for-using-locks)
  * [Different Locks in Programming](#different-locks-in-programming)
    * [Optimistic Locks](#optimistic-locks)
    * [Pessimistic Locks](#pessimistic-locks)
    * [Spin Locks](#spin-locks)
    * [Read/Write Locks](#readwrite-locks)
    * [Reentrant Locks](#reentrant-locks-1)
    * [Fair Locks](#fair-locks)
<!-- TOC -->

---

## Types of Locks in Java

At its core, a lock is a tool for synchronisation, a means to control access to blocks of code or resources that should not be accessed by more than one thread simultaneously. The Java Concurrency API provides several locking mechanisms, each designed for specific scenarios and use cases.

### Intrinsic Locks (Synchronized Blocks)

Intrinsic locks, or monitor locks, are the most fundamental form of locks in Java, **used in synchronised blocks or methods.** Every Java object has an intrinsic lock associated with it. When a thread enters a synchronized block, it acquires the intrinsic lock, and when it exits the block, it releases the lock.

```java
public void synchronizedMethod() {
    
    // The content in brackets is a reference to an object as a lock. It can be replaced by any other object, but cannot be `null`.
    // When a thread enters this synchronised block, it acquires the object lock and locks the lock (Other threads attempting to acquire the object lock will not succeed.).
    synchronized(this) {  
        // critical section
    }
}
```

```java 
// When a thread enters the method, it acquires the internal lock on the object.
public synchronized void syncMethod() {
    // critical section
}
```


### Reentrant Locks

ReentrantLock is a class from the `java.util.concurrent.locks` package that provides the same basic behavior as intrinsic locks but with extended capabilities, such as timeout for lock acquisition, interruptible lock acquisition, and fairness policy.

Reentrant locks offer **more flexibility** and control than intrinsic locks, making them suitable for more complex locking scenarios.

```java
public class ReentrantLockExample {
    private final ReentrantLock lock = new ReentrantLock();

    public void perform() {
        lock.lock();
        try {
            // critical section
        } finally {
            lock.unlock();
        }
    }
}
```

### ReadWriteLock

> **Why do we need ReadWriteLock?**
>
> Although `ReentrantLock` and `synchronized` are simple and useful, they have some behavioural limitations, which is "overbearing" (exclusive). ReadWriteLock is based on the principle that **multiple read operations are not required to be mutually exclusive, because read operations do not change the data and therefore do not interfere with each other.**
{: .prompt-tip }

ReadWriteLock is an interface that allows a lock to be shared among multiple readers or to be exclusive to a writer, **improving performance in scenarios where reads are more frequent than writes**.

```java
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class ReadWriteLockExample {
private final ReadWriteLock lock = new ReentrantReadWriteLock();

    public void read() {
        lock.readLock().lock();
        try {
            // reading section
        } finally {
            lock.readLock().unlock();
        }
    }

    public void write() {
        lock.writeLock().lock();
        try {
            // writing section
        } finally {
            lock.writeLock().unlock();
        }
    }
}
```

During operation, if the read lock is attempting to lock when the write lock is held by a thread, the read lock will not be available and you will have to wait for the other side to finish the operation, which automatically ensures that you will not read the wrong data.

### StampedLock

ReadWriteLock in practice, its performance is not satisfactory, mainly because of the relatively large overhead. Therefore, the JDK introduced StampedLock, in providing similar read and write locks at the same time, but also supports optimised read mode.

> Optimised read is based on the assumption that in most cases a read operation does not conflict with a write operation. 
> 
> - The strategy is to try to read first, and then check whether it's in write mode with `validate()`:
>   - If not in write mode, the overhead is successfully avoided;
>   - If in write mode, it tries to acquire a read lock.
{: .prompt-tip }

The optimistic read lock, acquired by calling `tryOptimisticRead()`, is a **non-blocking read mode**. It doesn't prevent the acquisition of a write lock and should be used when read operations are short and the risk of write operations occurring during the read is low. After reading, the validity of the optimistic read lock should be checked using the `validate(stamp)` method.

```java 
public class StampedLockExample {
    private final StampedLock lock = new StampedLock();
    private double x, y;

    // Method to move a point, protected by a write lock
    public void move(double deltaX, double deltaY) {
        long stamp = lock.writeLock(); // Acquire the write lock
        try {
            x += deltaX;
            y += deltaY;
        } finally {
            lock.unlockWrite(stamp); // Release the write lock using the stamp
        }
    }

    // Optimistic read method
    public double distanceFromOrigin() {
        long stamp = lock.tryOptimisticRead(); // Acquire an optimistic read lock
        double currentX = x, currentY = y; // Try to read first
        if (!lock.validate(stamp)) { // Check if the lock is still valid. (If result of validate(stamp) is true, then return directly)
            stamp = lock.readLock(); // Acquire a read lock if the optimistic read was not valid
            try {
                currentX = x;
                currentY = y;
            } finally {
                lock.unlockRead(stamp); // Release the read lock
            }
        }
        return Math.sqrt(currentX * currentX + currentY * currentY);
    }
}
```

## Best Practices for Using Locks

- **Minimize Lock Contention:** Keep synchronized sections as short as possible to reduce lock contention and improve application performance.
- **Prefer Intrinsic Locks for Simplicity:** Use intrinsic locks (synchronized blocks/methods) for simple synchronization needs to keep the code clean and straightforward.
- **Use ReentrantLock for Advanced Features:** When you need advanced features like timed lock acquisition or interruptible locks, opt for `ReentrantLock`.
- **Optimize Read-Heavy Operations with ReadWriteLock or StampedLock:** When dealing with data structures that are frequently read but infrequently modified, `ReadWriteLock` can significantly improve performance.
- **Always Release Locks in a Finally Block:** Ensure that locks are released in a `finally` block to avoid deadlock situations, even if an exception is thrown in the critical section.


## Different Locks in Programming

### Optimistic Locks

Optimistic locking is based on the **assumption that multiple transactions can complete without affecting each other.** Instead of locking the resource when accessing it, optimistic locking allows concurrent access and relies on checking whether the resource was altered before the current transaction commits. If a conflict is detected (usually through versioning or timestamps), the transaction is rolled back.


**Advantages**:
- Reduced lock contention.
- Improved performance in low-collision environments.

**Use Cases**:
- Database transactions.
- Concurrent data structures with infrequent writes.


### Pessimistic Locks

Pessimistic locking **assumes that conflicts are common** and thus locks resources to prevent other transactions from accessing them simultaneously. This approach guarantees that once a resource is locked, no conflicting changes can be made until the lock is released.


**Advantages**:
- Guarantees consistency in high-collision environments.
- Prevents the need for rollback in most cases.

**Use Cases**:
- Database transactions with high contention.
- Critical sections of code that must not be executed concurrently.


### Spin Locks

Spin locks are a low-level synchronization mechanism where threads "spin" **in a loop while waiting for the lock to become available.** They are useful when the wait time is expected to be short, as they **avoid the overhead associated with traditional locking and unlocking**.


**Advantages**:
- Low overhead for short wait times.
- Immediate access to the resource once it becomes available.

**Use Cases**:
- Multi-threaded applications with short critical sections.
- Low-level system programming where thread suspension is expensive.


### Read/Write Locks

Read/write locks **allow multiple readers to access the resource concurrently**, as long as no writes are happening. When a write lock is acquired, all other read and write operations are blocked until the write completes, optimizing performance in read-heavy scenarios.


**Advantages**:
- Increased concurrency for read operations.
- Exclusive access for write operations.

**Use Cases**:
- Caching systems.
- Database systems with heavy read operations.


### Reentrant Locks

Reentrant locks **allow the same thread to acquire the same lock multiple times** without causing a deadlock. They track the number of acquisitions and require the thread to release the lock the same number of times before it is truly released.


**Advantages**:
- Flexibility for nested lock acquisition.
- Avoidance of self-deadlock.

**Use Cases**:
- Recursively executed code blocks.
- Complex transactional operations requiring repeated locking.


### Fair Locks

Fair locks ensure that threads **acquire locks in the order they requested them, preventing "starvation"** where a thread might never obtain a lock because other threads keep acquiring it first.


**Advantages**:
- Predictable thread scheduling.
- Prevention of thread starvation.

**Use Cases**:
- Systems requiring high predictability.
- Applications where thread priority is critical.

