---
title: Getters/Setters Are Evil in OOP
date: 2024-02-25 19:48:00 UTC
categories: [(CS) Learning Note, OOP]
tags: [software engineering, OOP]
pin: true
---

Many developers, after writing an OO class, will first habitually add Getter/Setter for it (many compilers or libraries, such as Lombok, will also provide the ability to quickly add Getter/Setter). This is highly unrecommended behaviour. **In fact, adding the Getter/Setter should be a last resort after considering all better alternatives.**

> **Many developers always have the habit of writing useless or even harmful sample code. They are just used to write this way, but they never know why they write this way.**
> 
> Getter/Setter is such sample code.
{: .prompt-tip }

> Beans have private variables manipulated by getters and setters. The quasi-encapsulation of beans seems to **make some OO purists feel better but usually provides no other benefit.**
>
> --- Robert C. ("Uncle Bob")

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Why Are Getters/Setters Evil in OOP?](#why-are-getterssetters-evil-in-oop)
    * [They Could Break Encapsulation](#they-could-break-encapsulation)
      * [Understanding Encapsulation](#understanding-encapsulation)
      * [Useless Getters and Setters](#useless-getters-and-setters)
    * [They Could Violate The Law of Demeter](#they-could-violate-the-law-of-demeter)
    * [They Could Violate Tell-Don't-Ask Principle](#they-could-violate-tell-dont-ask-principle)
  * [Getters/Setters with Additional Functionality (like validation) Are Not Getters/Setters](#getterssetters-with-additional-functionality-like-validation-are-not-getterssetters)
  * [Some Situations Where Getter/Setter Cannot Be Avoided](#some-situations-where-gettersetter-cannot-be-avoided)
    * [Best Practices for Using Getters and Setters:](#best-practices-for-using-getters-and-setters)
<!-- TOC -->

---

## Why Are Getters/Setters Evil in OOP?

**General drawbacks from Getter/Setter:**

- **Exposure of Implementation Details:** Getters and setters might reveal too much about an object's internal structure, leading to increased coupling between objects.
- **Violation of Object's Integrity:** Allowing external entities to change an object's state directly can lead to invalid or inconsistent object states if proper validation is not enforced.

### They Could Break Encapsulation

#### Understanding Encapsulation

Encapsulation is about bundling the data (attributes) and methods (functions) that operate on the data into a single unit, typically a class, and restricting access to the internals of that class. This concept promotes data hiding, where the object's state is kept private, and interaction occurs through a well-defined interface.

However, **misuse of Getters and Setters can break the Encapsulation**. They could expose implementation details.

#### Useless Getters and Setters

Getters and setters are methods used to access (get) and modify (set) the private variables of a class. For example:

```java
public class Employee {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

We can access the private variable `name` directly via Getter/Setter.

**But in fact, many Getter/Setter will be as useless as the above code.** The code above is practically the same as the code below:

```java
public class Employee {
    public String name;
}
```

**Actually, the below code is better. At least it reduces useless code.**

### They Could Violate The Law of Demeter

**The Law of Demeter** (also known as **the principle of least knowledge**) states that an object should only communicate with its immediate friends and not with strangers. This promotes a loose coupling between objects, making the system easier to maintain.

Getters and Setters expose member variables in the class. **Once these member variables are exposed, it means that other classes may communicate with them.** Even if they don't do so now, it exposes this risk to the future.

### They Could Violate Tell-Don't-Ask Principle

> **Tell-Don't-Ask** is a principle that helps people remember that object-orientation is about bundling data with the functions that operate on that data. **It reminds us that rather than asking an object for data and acting on that data, we should instead tell an object what to do.** 
> 
> This encourages to move behavior into an object to go with the data.

![](https://i.postimg.cc/CxTdHkT4/1708896690561.png){: .w-65 .shadow .rounded-10 }
_Tell-Don't-Ask Principle_

Getters and Setters expose data in the class. It means that internal data can be asked and acted by other classes, which violates Tell-Don't-Ask Principle.

---

> However, blind adherence to the Tell-Don't-Ask Principle and The Law of Demeter can sometimes introduce unnecessary complexity into code.
>   - Sometimes a Getter can save a lot of trouble.
> 
> Remember, **DO NOT blindly follow any principles.** All the principles are to help us make the most suitable design
{: .prompt-warning }

## Getters/Setters with Additional Functionality (like validation) Are Not Getters/Setters

- Many people stick with Getters and Setters because they think they can add some additional functionality to Getters and Setters.
  - For example, in the Getter, transform the returned value, and in the setter, add correctness validation.
- But in my opinion, **Getters/Setters with additional functionality are not pure Getters/Setters any more!**
  - We should give these Getters/Setters more **appropriate names**.

---

For example:

```java 
public void setAge(int age) {
    if (age >= 0 && age <= 150) {
        this.age = age;
    } else {
        throw new IllegalArgumentException("Age must be between 0 and 150");
    }
}
```

The above `setAge()` is not a pure Setter. We should **give it a more appropriate name, like: `setValidatedAge()`.** This reminds the caller that the method is not a simple setter, but will validate the age.



## Some Situations Where Getter/Setter Cannot Be Avoided

> Use Getter/Setter only if you have to use it.
{: .prompt-tip }

- **Lazy Initialization**: Getters can be used for lazy initialization, where the object's property value is not calculated or initialized until it's needed.
- **Thread Safety**: In multi-threaded environments, getters and setters can be used to synchronize access to mutable shared resources to ensure thread safety.
- **Interfacing with Frameworks or Libraries**: Many frameworks and libraries expect the JavaBeans convention (getters and setters) for property access, especially in areas like serialization, ORM (Object-Relational Mapping), and bean introspection.
- **Supporting Data Binding**: For example, in UI frameworks, data binding often requires getters and setters to dynamically update the UI based on changes to the data model.
- **Different Access Levels**: For example, the getter may be public, but the setter could be protected.

### Best Practices for Using Getters and Setters:

- **Encapsulate Behavior, Not Just State:** Objects should provide methods that encapsulate complex behaviors involving their state, rather than merely offering state access through getters and setters.
- **Use with Purpose:** Only implement getters or setters for properties that genuinely require external access or modification. Not every private variable needs a getter and setter.
- **Consider Alternatives:** Explore design patterns and principles, such as Command, Strategy, or encapsulating variations in behavior, that might offer more encapsulated approaches to achieving your goals.


<br>

---

**Reference:**

- Fowler, M. (2013) _Bliki: Tell dont ask, martinfowler.com._ Available at: https://martinfowler.com/bliki/TellDontAsk.html (Accessed: 25 February 2024). 

- Scottshipp (2017) _Avoid getters and setters whenever possible, DEV Community._ Available at: https://dev.to/scottshipp/avoid-getters-and-setters-whenever-possible-c8m (Accessed: 25 February 2024). 
