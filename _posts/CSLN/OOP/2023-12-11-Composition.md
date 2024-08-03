---
title: Why do We Need to Use More Composition and Less Inheritance?
date: 2023-12-11 00:10:00 UTC
categories: [(CS) Learning Note, OOP]
tags: [software engineering, OOP, SOLID]
pin: false
---

While inheritance is a fundamental OOP concept, its overuse can lead to various problems. Many people think that inheritance is an Anti-Pattern and should rarely be used, or even not used at all.

> Actually, inheritance is a great feature, but it is very difficult to use it well. In my observation, more than 90% of programmers don't know how to use inheritance. That's why composition is recommended.
{: .prompt-tip }

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction to Inheritance and Composition](#introduction-to-inheritance-and-composition)
  * [Why Is Inheritance Not Recommended?](#why-is-inheritance-not-recommended)
    * [The Pitfalls of Overusing Inheritance](#the-pitfalls-of-overusing-inheritance)
  * [How Do We Use Composition to Replace Inheritance?](#how-do-we-use-composition-to-replace-inheritance)
  * [Practical Example](#practical-example)
    * [Inheritance Approach (Not Recommended)](#inheritance-approach-not-recommended)
    * [Composition Approach (Recommended)](#composition-approach-recommended)
  * [Is Composition Always Better Than Inheritance?](#is-composition-always-better-than-inheritance)
<!-- TOC -->

---

## Introduction to Inheritance and Composition

- **Inheritance**: In OOP, inheritance allows a class to inherit properties and methods from another class. It's a way to form `is-a` relationships between classes.

- **Composition**: Composition involves building complex objects by combining simpler ones. It's a way to form `has-a` relationships between classes.


## Why Is Inheritance Not Recommended?

- **Deep inheritance levels and complex inheritance relationships can impact code readability and maintainability.**
- **Inheritance**, while one of the pillars of object-oriented programming, **is invasive**. This is because subclasses are forced to inherit all properties and methods of the superclass, even if they don't need them.

### The Pitfalls of Overusing Inheritance

1. **Tight Coupling**: Inheritance can lead to tight coupling between parent and child classes, making the system more rigid and less modular.
2. **Fragile Base Class Problem**: Changes in the base class can have unforeseen effects in derived classes.
3. **Inflexibility in Code Reuse**: Inheriting from a class typically means taking all its methods and properties, even if only a few are needed.

## How Do We Use Composition to Replace Inheritance?

- Inheritance has three main roles: 
  1. to express **`is-a` relationships**; 
  2. to support **polymorphism**;
  3. to **reuse code**.

---

- These three roles can be achieved through the composition with other technical solutions:
  1. For `is-a` relationship, we can replace it with `has-a` relationship through **composition**.
  2. For **polymorphism**, we can use **interface** to support.
  3. For **code reuse**, we can achieve it through **delegation**.
- Theoretically, through the three technical means of **composition**, **interface**, and **delegation**, we can completely replace inheritance, and use no or fewer inheritance relationships in our projects, especially some complex inheritance relationships.

> **Delegation** is a concept in OOP that helps in dividing responsibilities among objects. Delegation is **using a reference (or pointer) to another class** to let it **complete a certain responsibility**.
> 
> - In layman's terms, the **Delegation** is: 
>   - **You delegate someone to do something for you.**
{: .prompt-tip }

> **Delegation vs. Interface Inheritance:**
> 
> - **Delegation:**
>    - Allows the behaviour of an object to be changed **dynamically** at runtime.
>    - **Lower coupling**. Compliance with the DIP.
>    - Each class has clearer responsibilities. Compliance with the SRP. In this way, the more complex the system, the more **reusable** the code will be.
>    - Better **Scalability**, **Flexibility** and **Maintainability**
> - **Interface Inheritance:**
>    - In **simple scenarios**, it can **avoid over-engineerin**g and keep the code simple.
>    - It allows the class itself to provide specific behaviour **without relying on other objects.**
> 
> **Delegations** generally provide more flexibility and maintainability, especially in complex systems that require dynamic behaviour and low coupling.
> 
> **Interface inheritance**, on the other hand, may be more straightforward and easier to understand in scenarios where the structure is simple and the behaviour is stable.
{: .prompt-tip }

## Practical Example

Consider a class `Bird` that needs functionality for flying and eating. Using inheritance, you might create a base class `Pigeon` and inherit from it. However, this approach becomes problematic when you need to introduce birds that don’t fly, such as `Ostrich`.

### Inheritance Approach (Not Recommended)

```java
public class Bird {
    public void eat() { /* ... */ }

    public void fly() { /* ... */ }
}

public class Pigeon extends Bird {
    // Pigeon can fly and eat
}

public class Ostrich extends FlyingBird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostriches can't fly"); // Ostrich can't fly. Violation of LSP
    }
}
```

### Composition Approach (Recommended)

```java
public interface FlyingBehavior {
    void fly();
}

public interface EatingBehavior {
    void eat();
}

public class Ostrich {
    private EatingBehavior eatingBehavior;  // Delegation 

    public Pigeon(EatingBehavior eat) {
        this.eatingBehavior = eat;
    }

    public void performEat() {
        eatingBehavior.eat();
    }
}

public class Pigeon {
    private FlyingBehavior flyingBehavior; // Delegation 
    private EatingBehavior eatingBehavior; // Delegation 

    public Pigeon(FlyingBehavior fly, EatingBehavior eat) {
        this.flyingBehavior = fly;
        this.eatingBehavior = eat;
    }

    public void performFly() {
        flyingBehavior.fly();
    }

    public void performEat() {
        eatingBehavior.eat();
    }
}
```

In this composition-based approach, `Ostrich` is more flexible and not tied to a specific behaviour.

## Is Composition Always Better Than Inheritance?

- While we encourage more composition and less inheritance, **composition isn't perfect** and inheritance isn't useless.
- From the above example, **composition** instead of inheritance **means doing a finer-grained** splitting of classes. This also means that **we have to define more classes and interfaces**.  
  - The increase of classes and interfaces will **increase the complexity and maintenance cost** of the code.
- Therefore, in the actual development of the project, we still need to choose whether to use inheritance or composition according to the specific situation.
  - If the inheritance structure between classes is stable, the inheritance level is shallow, and the inheritance relationship is not complex, we can boldly use inheritance.
  - On the contrary, the more unstable the system is, the deeper the inheritance level is, and the more complex the inheritance relationships are, we should try to use composition instead of inheritance.

> In fact, no design principles and ideas can be followed mindlessly. **The important thing is that we understand the essence of each design principle and idea** and get the balance in the actual project to make the most suitable design.
> 
> **Any design principles and ideas are just guidelines, not silver bullets.**
{: .prompt-warning }
