---
title: "Clean Code: Objects and Data Structure"
date: 2023-10-29 16:50:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/structure.png
---

>There is a reason that we keep our variables private. We don’t want anyone else to depend on them. We want to keep the freedom to change their type or implementation on a whim or an impulse. Why, then, do so many programmers automatically add getters and setters to their objects, exposing their private variables as if they were public?

When writing clean code, understanding how to effectively use objects and data structures is crucial.


---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Data Abstraction](#data-abstraction)
  * [Data/Object Anti-Symmetry](#dataobject-anti-symmetry)
  * [The Law of Demeter](#the-law-of-demeter)
  * [Data Transfer Objects](#data-transfer-objects)
<!-- TOC -->

---

## Data Abstraction

Data abstraction is about representing data in the most concise way **without exposing unnecessary details**. Instead of using primitive data types or public variables, we should use abstract data types that **encapsulate our data**.


For example, in the following example, we don't need to expose the data using getters and setters.
```java
public class Point {
private double x;
private double y;

    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double distanceTo(Point other) {
        return Math.sqrt(Math.pow(other.x - this.x, 2) + Math.pow(other.y - this.y, 2));
    }
}
```

## Data/Object Anti-Symmetry

Objects and data are the **opposite** of each other. **Objects expose behavior and hide data**, whereas **data structures expose data and have no significant behavior**. It's important to decide whether we want the flexibility offered by objects or the transparency of data structures.

> - **Procedure-oriented** code (code using data structures) makes it **easy to add new functions without changing the existing data structures**.
> - **Object-oriented** code, on the other hand, makes it **easy to add new classes without changing existing functions**.
{: .prompt-tip }

For example:

---

Let's consider an example of transport vehicles. We can write this program using procedure-oriented approach and object-oriented approach.

**Procedure-oriented approach** (We can write procedure-oriented code using object-oriented languages like Java. Actually, **Object-oriented is not simply a language, it's also a programming approach, even a philosophy.**): 

```java
public class Car {
    public String brand;
    public int numberOfDoors;
}

public class Bicycle {
    public String type;
    public boolean hasBell;
}

public class VehicleActions {
    public void start(Object vehicle) {
        if (vehicle instanceof Car) {
            System.out.println("Starting car's engine...");
        } else if (vehicle instanceof Bicycle) {
            System.out.println("Pedaling the bicycle...");
        }
    }
    
    public void describe(Object vehicle) {
        if (vehicle instanceof Car) {
            Car car = (Car) vehicle;
            System.out.println("This is a " + car.brand + " car with " + car.numberOfDoors + " doors.");
        } else if (vehicle instanceof Bicycle) {
            Bicycle bike = (Bicycle) vehicle;
            System.out.println("This is a " + bike.type + " bicycle. Does it have a bell? " + bike.hasBell);
        }
    }
}

```

In the procedure-oriented approach, **if we want to add new functionality** for all vehicles (e.g. to get the operation method of each vehicle), we just need to add a new function in `VehicleActions` class. **We don't need to modify any existing vehicle class**(Assuming that the data structure is complete). However, if we want to add a new vehicle, we have to change all the functions related to vehicles.

> **Procedure-oriented approach** emphasises the procedure and **does not divide the functions (procedures) according to different classes (data structures)**.
> 
> So it is easy to add new functions (procedures). But adding a new class (data structure) will be troublesome, because all functions (procedures) will be affected.
{: .prompt-tip }

**Object-oriented approach**:
```java
public interface Vehicle {
    void start();
    void describe();
}

public class Car implements Vehicle {
    public String brand;
    public int numberOfDoors;

    public void start() {
        System.out.println("Starting car's engine...");
    }

    public void describe() {
        System.out.println("This is a " + brand + " car with " + numberOfDoors + " doors.");
    }
}

public class Bicycle implements Vehicle {
    public String type; // 如：Mountain, Road, Hybrid
    public boolean hasBell;

    public void start() {
        System.out.println("Pedaling the bicycle...");
    }

    public void describe() {
        System.out.println("This is a " + type + " bicycle. Does it have a bell? " + hasBell);
    }
}
```

In the object-oriented approach, **if we want to add a new vehicle**, such as `Boat`, we simply create a new class that implements the `Vehicle` interface and define the `start` and `describe` method in that class. This way, **we don't need to modify any existing function**. However, if we need to add new functionality for all vehicles (e.g. to get the operation method of each vehicle), we have to make changes in each vehicle class. (Even then, in the object-oriented approach, we still don't need to modify any functions. **So as far as scalability is concerned, OO is better than PO.**)

> **Object-oriented approach** emphasises the object, and will **divide the same function (procedure) into corresponding classes according to different data structures.**
>
> So it is easy to add a new class (data structure). But adding new functions (procedures) will be troublesome, because all functions (procedures) need to be divided in different classes (data structures).
{: .prompt-tip }


> In any complex system there are going to be times when we want to add new data types rather than new functions. For these cases objects and OO are most appropriate. On the other hand, there will also be times when we’ll want to add new functions as opposed to data types. In that case procedural code and data structures will be more appropriate.
>
> Mature programmers know that the idea that everything is an object is a myth. Sometimes you really do want simple data structures with procedures operating on them.



## The Law of Demeter

The Law of Demeter (also known as the principle of least knowledge) states that an object should only communicate with its immediate friends and not with strangers. This promotes a loose coupling between objects, making the system easier to maintain.

A method `f` of a class `C` should only call the methods of these:

- `C`
- An object created by `f`
- An object passed as an argument to `f`
- An object held in an instance variable of `C`

For Example:

```java
// Violating the Law of Demeter
class A {
    B b;

    void method() {
        C c = b.getC();
        c.doSomething();
    }
}

// Adhering to the Law of Demeter
class A {
    B b;

    void method() {
        b.doSomething();
    }
}
```

## Data Transfer Objects

Data Transfer Objects (DTOs) are simple data structures used to transfer data between systems. They should not contain any business logic but can have serialization mechanisms. DTOs are very useful structures, especially when communicating with databases or parsing messages from sockets, and so on.

JavaBean is such objects, For example:

```java
// A JavaBean
public class Person implements Serializable {
    private String name;
    private int age;

    // Constructor with no parameters
    public Person() {}

    // Getter and Setter
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

Beans have parameterless constructor and private variables manipulated by getters and setters. And beans should not contain other business logic.

**Classes with only getters and setters are more data structures rather than true objects.** When you add Getter and Setter to each private variable and there is no other business logic, it means that the private variable is no different from the public one. In this case, it seems better for us to use public variables directly:

```java
public class Person implements Serializable {
    public String name;
    public int age;
}
```

This can **reduce useless sample code** and make the class **more simple and easy to understand**.

> Beans have private variables manipulated by getters and setters. The quasi-encapsulation of beans seems to make some OO purists feel better but usually provides no other benefit.

But then again, Getter and Setter seem to be useful and necessary in beans as well. Because:

1. **Compatibility with Frameworks and Libraries**: Many Java frameworks and libraries, such as JPA, BeanUtils, and PropertyEditors, expect objects to adhere to the JavaBean convention.
2. **Data Encapsulation and Validation**: Setters can validate or transform data before assigning it.
3. **API Stability**: Using getters and setters allows for changing the internal implementation without altering the API.

> The important thing is:
>
> **Try not to write useless sample code. Always think about why you are writing the code before you write it!**
{: .prompt-warning }


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
