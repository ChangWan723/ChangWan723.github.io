---
title: Some Java basics
date: 2023-11-18 10:00:00 +0530
categories: [(CS) Learning Note, Java]
tags: [computer science, software engineering, Java]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What are the characteristics of Java?](#what-are-the-characteristics-of-java)
    * [Advantage](#advantage)
    * [Limitation](#limitation)
  * [What are reference copy, shallow copy and deep copy?](#what-are-reference-copy-shallow-copy-and-deep-copy)
<!-- TOC -->

---

## What are the characteristics of Java?

### Advantage

1. **Platform Independence**: Java's most significant promise is "Write Once, Run Anywhere" (WORA), meaning that once you write a Java application, it can run on any device that has the Java Virtual Machine (JVM) installed, regardless of the architecture or platform.
2. **Robustness**: Java emphasizes early checking for possible errors, as Java compilers are able to detect many problems that would first show up at execution time in other languages. It also removes certain types of programming errors, such as memory leaks or pointer errors, by managing memory through garbage collection.
3. **Object-Oriented**: Everything in Java is an object, which encapsulates data and behavior, making the code more modular, flexible, and adaptable to change. Java supports core object-oriented concepts like inheritance, encapsulation, polymorphism, and abstraction.
4. **Rich APIs**: Java provides a rich set of APIs that can handle everything from networking and database connectivity to XML parsing and user interface design.
5. **Powerful Development Tools**: The Integrated Development Environments (IDEs) available for Java, such as Eclipse and IntelliJ IDEA, provide powerful debugging capabilities and make the coding process more efficient and less prone to error.
6. **Enterprise Standard**: Java EE (Enterprise Edition) provides an API and runtime environment for developing and running large-scale, multi-tiered, scalable, and secure network applications.
7. **Multithreaded**: Java supports multithreaded programming, which allows multiple threads to run concurrently within a single program. This can improve performance by utilizing CPU resources more efficiently.
8. **High Performance**: Java bytecode is designed to be executed at high speeds by the JVM. Performance is further enhanced in modern JVMs through the use of Just-In-Time (JIT) compilers that translate bytecode into native machine code at runtime.


### Limitation

1. **Performance Overhead**: Java can be slower than native languages such as C or C++ because Java code runs on a JVM. The level of abstraction provided by the JVM can result in additional overhead during execution, although just-in-time (JIT) compilers and advanced garbage collection techniques have significantly narrowed this gap.
2. **Memory Consumption**: Java's garbage collection and object-oriented overhead can lead to greater memory consumption compared to languages where the developer has direct control over memory allocation and cleanup.
3. **Lesser Control Over Lower Level Features**: Java does not provide direct access to low-level system details that are available in languages like C++. This lack of control can be a hindrance when developing applications that require high performance and system-level control.


## What are reference copy, shallow copy and deep copy?

- **Reference Copy (Reference Assignment)**:
  - This is the simplest form of copying, achieved by simply assigning one reference variable to another.
  - After the assignment, both reference variables point to the same object in memory, meaning any changes done through one reference are reflected in the other.
  - **No new object is created.**

```java 
MyClass object1 = new MyClass();
MyClass object2 = object1; // Reference copy: object2 now points to the same object as object1.
```

![](https://i.postimg.cc/QxNwWx9R/bkj2.png){: .w-50 .shadow .rounded-10 }
_Reference Copy (Reference Assignment)_

- **Shallow Copy**:
  - A shallow copy of an object is a new object with copies of the values of the original object's fields. If the field value is a primitive type, a direct copy of the value is made. If the field is a reference to an object, it only copies the reference. Thus, **both the original and the copied object will refer to the same object instance in the case of reference fields.**
  - Shallow copies are fast and easy to create but can lead to side effects if not used properly.

```java 
class ShallowCopyExample implements Cloneable {
    int[] arr = {1, 2, 3};

    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

// Usage
ShallowCopyExample original = new ShallowCopyExample();
ShallowCopyExample copied = (ShallowCopyExample) original.clone();

```

- **Deep Copy**:
  - A deep copy involves creating a new object and then copying the fields of the original object to the new object. If the original object contains references to other objects, a new copy of each referenced object is created as well. This recursive copy ensures that **any objects referenced by the original object are also duplicated, rather than just copying the references.**
  - Deep copies are more complex and may be more resource-intensive to create but are safer because they do not inadvertently share parts of objects between two object instances.

```java
class DeepCopyExample implements Cloneable {
    int[] arr = {1, 2, 3};

    public Object clone() throws CloneNotSupportedException {
        DeepCopyExample copy = (DeepCopyExample) super.clone();
        copy.arr = this.arr.clone(); // Creates a new array and copies the content.
        return copy;
    }
}

// Usage
DeepCopyExample original = new DeepCopyExample();
DeepCopyExample copied = (DeepCopyExample) original.clone();
```

![](https://i.postimg.cc/2SPpn7mJ/bkj1.png){: .w-100 .shadow .rounded-10 }


