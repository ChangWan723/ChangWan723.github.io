---
title: Multithreading in Java
date: 2024-02-21 19:53:00 UTC
categories: [(CS) Learning Note, Java]
tags: [software engineering, Java]
pin: false
---

## Understanding Multithreading in Java

Multithreading is a core concept of Java programming that allows multiple threads to run concurrently within a single process. This concurrency model enables developers to perform multiple operations simultaneously, making applications more efficient and responsive.

### Key Benefits of Multithreading

- **Improved Application Performance:** By allowing multiple operations to run in parallel, especially on multi-core processors, multithreading can significantly enhance application performance.
- **Better Resource Utilization:** Multithreading enables applications to make optimal use of available CPU resources by keeping idle time to a minimum.
- **Enhanced Responsiveness:** User interface applications can remain responsive to user input while performing background operations on separate threads.

## Implementing Multithreading (Thread, Runnable, and Callable) in Java

Java provides multiple ways to implement multithreading, including extending the `Thread` class and implementing the `Runnable` or `Callable` interfaces. The `java.util.concurrent` package further simplifies multithreading with high-level concurrency constructs.

- **Thread**
  - **A `Thread` is a class that represents a thread of execution in a Java program.**
    When you extend the `Thread` class, you must override its `run()` method
    with the code you want the thread to execute.
  - Starting the thread is done by creating an instance of your `Thread` subclass
    and calling its `start()` method, which internally calls the `run()` method.
  - Extending the `Thread` class can be limiting because it forces your class to
    inherit from `Thread` when it might actually need to inherit from another class
    (since Java does not support multiple inheritance).
- **Runnable**
  - **`Runnable` is an interface that you implement in a class whose instances will be
    executed by a thread.** It has a single method called `run()`.
  - Unlike extending `Thread`, implementing `Runnable` allows your class to
    extend other classes.
  - To execute a `Runnable`, you pass an instance of your `Runnable` class to a
    `Thread` instance and call the `start()` method on the `Thread`. This is a
    more flexible approach than extending `Thread` because it allows you to
    implement `Runnable` in classes that extend other classes.
- **Callable**
  - **`Callable` is an interface similar to `Runnable` but with some key differences.**
    It was introduced in Java 5 to handle cases where a task needs to return a result
    and/or throw an exception.
  - The `Callable` interface has a method called `call()` which can return a
    value of a specified type and can throw an exception.
  - `Callable` tasks need to be run by an `ExecutorService`. When you submit a
    `Callable` to an `ExecutorService`, you get a `Future` object back. This
    `Future` can be used to retrieve the `Callable`'s result, providing a way to
    handle the result of the asynchronous task once it completes.
  - `Callable` is more versatile than `Runnable` when it comes to exception
    handling and returning results.

### Example of `Thread`

The `Thread` class is the fundamental building block of Java's concurrency model. When you create a new thread, you're creating a new concurrent path of execution within your program. You can create a thread by extending the `Thread` class and overriding its `run` method.

```java
class MyThread extends Thread {

    @Override
    public void run() {
        System.out.println("This is a thread running by extending Thread class.");
    }

    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.start(); // Start the thread
    }
}
```

### Example of `Runnable`

`Runnable` is a functional interface in Java that represents a task to be run by a thread. **Unlike extending the Thread class, implementing the Runnable interface does not create a thread.** Instead, it defines a task that can be executed by any thread. The Runnable interface is a better choice when you only need to override the run method without requiring the full overhead of the Thread class.

```java 
class MyRunnable implements Runnable {

    @Override
    public void run() {
        System.out.println("This is a thread running by implementing Runnable interface.");
    }

    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable());
        thread.start(); // Start the thread
    }
}
```

### Example of `Callable`

`Callable` is similar to `Runnable` but more powerful. It represents a task that returns a result and may throw an exception. `Callable` tasks are executed by an `ExecutorService`, and the result is retrieved through a `Future` object.

```java 
class MyCallable implements Callable<String> {
    public String call() throws Exception {
        // Perform task and return a result
        return "Callable executed: " + Thread.currentThread().getName();
    }

    public static void main(String[] args) throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newFixedThreadPool(1);
        Future<String> future = executor.submit(new MyCallable());

        // Retrieves the result of the callable
        String result = future.get();
        System.out.println(result);

        executor.shutdown();
    }
}
```

## Thread Pools in Java

Thread pools are a crucial feature of Java's concurrency framework, managing a pool of worker threads. The thread pool reuses a fixed number of threads to execute tasks, reducing the overhead of creating and destroying threads for each task.

### Advantages of Thread Pools

- **Resource Management:** Thread pools limit the number of simultaneous threads, preventing resource exhaustion.
- **Improved Performance:** Reusing existing threads reduces the latency associated with thread creation.
- **Task Queuing and Execution Management:** Thread pools efficiently manage a queue of tasks, executing them as threads become available.

### Example of Thread Pools

Java's `ExecutorService` interface provides a flexible mechanism for asynchronous task execution. The `Executors` class offers convenient factory methods for creating different types of thread pools.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolDemo {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(5);

        for (int i = 0; i < 10; i++) {
            Runnable worker = new WorkerThread("" + i);
            executor.execute(worker);
        }
        executor.shutdown();
        while (!executor.isTerminated()) {
        }
        System.out.println("Finished all threads");
    }
}

class WorkerThread implements Runnable {
    private final String command;

    public WorkerThread(String command) {
        this.command = command;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + " Start. Command = " + command);
        // Task execution logic here
        System.out.println(Thread.currentThread().getName() + " End.");
    }
}
```
