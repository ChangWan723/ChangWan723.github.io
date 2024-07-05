---
title: Some Java basics
date: 2023-11-18 10:00:00 UTC
categories: [(CS) Learning Note, Java]
tags: [software engineering, Java]
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
  * [What is the Garbage Collector and how does it work?](#what-is-the-garbage-collector-and-how-does-it-work)
  * [What is the difference between abstract class and interface in Java?](#what-is-the-difference-between-abstract-class-and-interface-in-java)
  * [What is generic in Java? Why do we need to use it?](#what-is-generic-in-java-why-do-we-need-to-use-it)
  * [How is the `final` applied differently between variables, methods, and classes in Java?](#how-is-the-final-applied-differently-between-variables-methods-and-classes-in-java)
  * [Access Levels of Different Modifiers in Java](#access-levels-of-different-modifiers-in-java)
  * [What is static block in Java?](#what-is-static-block-in-java)
  * [What is the order of loading the parts of Java classes?](#what-is-the-order-of-loading-the-parts-of-java-classes)
  * [What is a Comparator and Comparable in Java?](#what-is-a-comparator-and-comparable-in-java)
  * [What are the Strong Reference，Soft Reference，Weak Reference and Phantom Reference in Java?](#what-are-the-strong-referencesoft-referenceweak-reference-and-phantom-reference-in-java)
  * [Why do we have to override `hashCode()` when we override `equals()`?](#why-do-we-have-to-override-hashcode-when-we-override-equals)
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

## What is the Garbage Collector and how does it work?

The Garbage Collector (GC) in Java is a form of automatic memory management that aims to reclaim memory occupied by objects that are no longer in use by the program. This is crucial in Java because it prevents memory leaks and manages heap memory, where Java objects are stored.

Here's an overview of how it works:

- **Object Creation and Heap Allocation**
  - In Java, when you create an object using the new keyword, it's allocated memory in the heap. This is the area of memory used for dynamic memory allocation.
- **Reachability Analysis**
  - The garbage collector periodically checks for objects that are no longer reachable from any references in the executing code. An object is considered "live" or "reachable" if it's accessible through at least one chain of references from any active part of the program, like stack variables (local variables, parameters), static variables, or active Java threads.
- **Mark and Sweep**
  - **Mark**: The GC traverses from the root nodes (like static variables, thread stacks) and marks all reachable objects.
  - **Sweep**: After marking, the GC sweeps through the heap and removes objects that were not marked, thus reclaiming their memory.
- **Types of Collectors**:
  - **Serial Garbage Collector**: Simple, for single-threaded environments.
  - **Parallel Garbage Collector**: Also known as Throughput Collector, it uses multiple threads for the GC process and is suitable for multi-threaded applications.
  - **Concurrent Mark Sweep (CMS) Collector**: Minimizes application pause times by doing most of the garbage collection work concurrently with the application threads.
  - **G1 Garbage Collector**: Designed for large heap sizes, it divides the heap into regions and prioritizes collecting regions with the most garbage first.
- **Generational Collection**: Java GC often uses a generational memory model, where the heap is divided into:
  - **Young Generation**: Where new objects are created. It's further divided into one Eden space and two Survivor spaces.
  - **Old Generation**: For objects that have survived multiple GC cycles in the Young Generation.
  - **Permanent Generation (or Metaspace in newer versions)**: Holds metadata like class definitions.
- **Garbage Collection Phases**
  - **Minor GC**: Cleans the Young Generation when it’s full. It's relatively fast but frequent.
  - **Major (or Full) GC**: Cleans the Old Generation. It's usually slower and can cause noticeable pauses in the application.

By managing memory automatically, Java's Garbage Collector helps avoid common problems like memory leaks and dangling pointers, which are common in languages with manual memory management. However, it's also important for developers to understand GC behavior to write efficient and performance-optimized Java applications.

## What is the difference between abstract class and interface in Java?

In Java, abstract classes and interfaces are used for different purposes and have key differences:

- **Usage Intent**
  - Abstract Class: Sharing code (combining common features of subclasses). 
  - Interface: Defining a contract (what you can see from outside the class).
- **Method Implementation**:
  - Abstract Class: Can have both abstract (no implementation) and concrete (with implementation) methods.
  - Interface: Originally only allowed abstract methods, but since Java 8, they can also include default and static methods with implementations.
- **Fields**:
  - Abstract Class: Can have instance variables and can be non-static and non-final.
  - Interface: All fields are implicitly public, static, and final.
- **Inheritance**:
  - Abstract Class: A class can extend only one abstract class, supporting single inheritance.
  - Interface: A class can implement multiple interfaces, allowing for multiple inheritance of type.
- **Constructors**:
  - Abstract Class: Can have constructors.
  - Interface: Cannot have constructors.
- **Access Modifiers**:
  - Abstract Class: Members can have any access modifier (private, protected, public).
  - Interface: Before Java 9, all methods were implicitly public; Java 9 introduced private methods in interfaces.

> - If we want to represent an `is-a` relationship, and we're solving a code reuse problem, we'll use an `abstract class`. 
> - If we want to represent a `has-a` relationship, and we're defining an abstract contract, we'll use an `interface`.
{: .prompt-tip }

## What is generic in Java? Why do we need to use it?

Generics in Java are a feature that allows you to write classes, interfaces, and methods where the **type of data is specified as a parameter**. 

Using generics, you can create code that is more flexible and safer, reducing runtime errors and the need for casts. 

Here's why generics are important:
1. **Type Safety**: Generics enforce type safety by allowing you to specify the exact data types to be used. This reduces errors at runtime because any attempt to use the wrong type can be caught at compile time.
2. **Elimination of Casts**: Without generics, you had to cast objects retrieved from a collection. With generics, you specify the type of objects stored in a collection, eliminating the need for casting and reducing the chance of runtime errors.
3. **Code Reuse**: Generics enable you to write code that is independent of data types. For example, a single generic class like ArrayList<T> can be used with any object type, promoting code reuse.

## How is the `final` applied differently between variables, methods, and classes in Java?

- **Final Variables**: 
  - When applied to a variable, `final` indicates that the variable's value cannot be changed once it is initialized.
  - Final variables can be initialised either at the time of declaration or in the constructor for instance variables.
  - It can be used to primitive types and object references:
    - For primitive types, this means the value itself cannot change.
    - For object references, it means the reference cannot change to point to a different object, although the object's state (its fields) can still be modified unless those fields are also `final`.
- Final Methods:
  - A `final` method cannot be overridden by subclasses.
  - This is used to prevent a change in the behaviour of the method, ensuring consistency across different subclasses.
  - Final methods can be inherited but maintain their finality.
- Final Classes:
  - A `final` class cannot be subclassed.
  - This is often done to maintain the integrity of the class and ensure that its implementation is not altered through inheritance.
  - All methods in a final class can implicitly be considered as final, but fields need to be explicitly marked as final to have the constant behaviour.

## Access Levels of Different Modifiers in Java

| Modifier    | 	Class | 	Package | 	Subclass | 	World |
|-------------|--------|----------|-----------|--------|
| public      | 	Y	    | Y	       | Y         | 	Y     |
| protected   | 	Y	    | Y        | 	Y	       | N      |
| no modifier | 	Y	    | Y        | 	N        | 	N     |
| private     | 	Y     | 	N       | 	N        | 	N     |


## What is static block in Java?

In Java, a static block, also known as a static initialisation block, is a block of code that **is executed when the class is first loaded into the JVM** (Java Virtual Machine). Static blocks are used to initialise static variables or to perform static initializations that require more than a single line of code. 

## What is the order of loading the parts of Java classes?

- The order of loading the parts of Java classes:
  1. **Parent Class Static Variables and Static Blocks**: Firstly, the static variables and static blocks of the parent class are loaded and executed in the order they are declared in the parent class.
  2. **Child Class Static Variables and Static Blocks**: Next, the static variables and static blocks of the child class are loaded and executed in the order they are declared in the child class. These operations occur after the static initialization of the parent class, during the loading process of the child class.
  3. **Parent Class Instance Variables, Instance (non-Static) Blocks, and Constructors**: When creating an instance of the child class, the constructor of the parent class is called first, followed by the initialization of instance variables and instance (non-Static) blocks in the parent class, in the order they are declared. Constructors are called during this stage, completing the initialization of the parent class object.
  4. **Child Class Instance Variables, Instance (non-Static) Blocks, and Constructors**: Subsequently, the instance variables and instance (non-Static) blocks of the child class are loaded and executed in the order they are declared in the child class. Finally, the constructor of the child class is called, completing the initialization of the child class object.

## What is a Comparator and Comparable in Java?

In Java, Comparator and Comparable are two interfaces used for defining custom orderings of objects, but they are used in different contexts:

- Comparable Interface:
  - **Purpose**: The Comparable interface is used to define the natural ordering of objects of a class. It must be implemented by the class whose objects you want to sort.
  - **Method**: This interface contains a single method, `compareTo(T o)`, that compares this object with the specified object for order.
  - **Usage**: When a class implements `Comparable`, it gives a way to compare its instances. For example, if you have a `Person` class, implementing Comparable could allow you to define a natural order (e.g., by age or name).
  - **Collections Sorting**: Classes that implement `Comparable` can be easily sorted using utility methods like `Collections.sort()` or `Arrays.sort()` without specifying any additional comparator.

```java 
public class Person implements Comparable<Person> {
    private String name;
    private int age;

    // Constructor, getters, and setters

    @Override
    public int compareTo(Person other) {
        return this.age - other.age; // Ascending order of age
    }
}

// Usage:
List<Person> people = Arrays.asList(new Person("Alice", 30), new Person("Bob", 25));
Collections.sort(people); // Sorts by natural ordering (age)
```

- Comparator Interface:
  - **Purpose**: The `Comparator` interface is used to define an ordering, but it's separate from the objects to be ordered. It allows defining multiple different orderings for a class.
  - **Method**: The interface defines the `compare(T o1, T o2)` method used to compare two objects of the same type.
  - **Usage**: It’s useful when you need to sort instances of a class that did not implement `Comparable`, or you need a different sorting order than the one provided by `Comparable`.
  - **Collections Sorting**: You can pass a `Comparator` instance to utility methods like `Collections.sort()` or `Arrays.sort()` to sort based on the order defined by the Comparator.

```java 
public class NameComparator implements Comparator<Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.getName().compareTo(p2.getName()); // Ascending order of names
    }
}

// Usage:
List<Person> people = Arrays.asList(new Person("Alice", 30), new Person("Bob", 25));
Collections.sort(people, new NameComparator()); // Sorts by name
```

In summary, `Comparable` is for defining a natural, usually single, ordering for objects of a class, **intrinsic to the class itself**. `Comparator`, on the other hand, is **for externalized orderings** that can be different from.

## What are the Strong Reference，Soft Reference，Weak Reference and Phantom Reference in Java?


- **Strong Reference** 
  - Strong references are the most common type of references in Java. Any object actively referenced in the application is considered strongly referenced.
  - Strong references are straightforward and natural in programming. They ensure that objects remain in memory as long as needed by the application.

```java
Object strongObject = new Object();
```

- **Soft Reference**
  - Soft references are used for memory-sensitive caching. Objects with only soft references are cleared by the garbage collector in response to memory demand.
  - Soft references are ideal for caches that should be cleared when memory is needed. They help in avoiding `OutOfMemoryError` by allowing the garbage collector to reclaim space if necessary.

```java
SoftReference<Object> softReference = new SoftReference<>(new Object());
```

- **Weak Reference** 
  - Weak references are weaker than soft references. The garbage collector can reclaim an object with only weak references at any time.
  - Weak references are useful for metadata, mappings, or listeners that should not prevent their referents from being garbage collected. They are often used in scenarios like caching, tracking, and managing resources that can be recreated.

```java
WeakReference<Object> weakReference = new WeakReference<>(new Object());
```

- **Phantom Reference**
  - Phantom references are the weakest type of references. An object with a phantom reference is considered to be already finalized but not reclaimed.
  - Phantom references are used for post-mortem clean-up actions or pre-recycling actions. They allow for safe cleanup operations without the risk of `OutOfMemoryError`.


```java
PhantomReference<Object> phantomReference = new PhantomReference<>(new Object(), referenceQueue);
```

## Why do we have to override `hashCode()` when we override `equals()`?

In simple words, this is because we need to **maintain the contract between the two methods.**

> - **The contracts between `hashCode()` and `equals()`:**
>   - In Java, we use `equals()` to detect whether an object is equal to another object.
>   - **If two objects are equal (`equals()`), their hash codes (`hashCode()`) must also be equal.**
>   - If two objects are not equal (`equals()`), there is no requirement that hash codes (`hashCode()`) must be different. (This is because hash conflicts are generally unavoidable, i.e. different content hashes out the same value.)
>
> Based on the above contract, **in Java, if two objects have different hash codes (`hashCode()`), they must not be equal (`equals()`).** If two objects have the same hash code (`hashCode()`), they are not necessarily equal (`equals()`). 
{: .prompt-tip }


**Failing to adhere to these contracts can lead to unexpected results when using various Java APIs.** 

For example, collections like `HashSet`, `HashMap`, or `Hashtable` rely on the `hashCode()` to organise and search for objects efficiently. 

- `HashSet`, `HashMap`, and `Hashtable` compare hash codes first to determine if two Objects are the same:
  - If two objects have different hash codes (`hashCode()`), they can be directly determined to be different.
  - If two objects have the same hash code (`hashCode()`), call `equals()` further to determine if they are the same.

**So, if we don’t override `equals()` and `hashCode()` correctly, Objects that should be the same are recognised as different in Java (For example, two same Objects are stored in a HashSet).**
