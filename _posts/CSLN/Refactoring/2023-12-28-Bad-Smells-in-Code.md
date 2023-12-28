---
title: Bad Smells in Code
date: 2023-12-28 18:24:00 UTC
categories: [(CS) Learning Note, Refactoring]
tags: [software engineering, Refactoring, code]
pin: false
---

**Bad smells** in refactoring refer to certain patterns or characteristics in code that **suggest a need for refactoring**. They are called "smells" because **they are not necessarily bugs or errors, but they indicate weaknesses in the design that may cause problems in the future.** This blog will cover some common bad smells.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Duplicated Code](#duplicated-code)
  * [Long Method](#long-method)
  * [Large Class](#large-class)
  * [Long Parameter List](#long-parameter-list)
  * [Divergent Change](#divergent-change)
  * [Shotgun Surgery](#shotgun-surgery)
  * [Feature Envy](#feature-envy)
  * [Data Clumps](#data-clumps)
  * [Primitive Obsession](#primitive-obsession)
  * [Switch Statements](#switch-statements)
  * [Temporary Field](#temporary-field)
  * [Inappropriate Intimacy](#inappropriate-intimacy)
  * [Lazy Class](#lazy-class)
  * [Alternative Classes with Different Interfaces](#alternative-classes-with-different-interfaces)
  * [Incomplete Library Class](#incomplete-library-class)
  * [Speculative Generality](#speculative-generality)
  * [Parallel Inheritance Hierarchies](#parallel-inheritance-hierarchies)
  * [Message Chains](#message-chains)
  * [Middle Man](#middle-man)
  * [Data Class](#data-class)
  * [Refused Bequest](#refused-bequest)
  * [Comments](#comments)
<!-- TOC -->

---

## Duplicated Code

**Symptom**: The same code structure appears in more than one place.

**Solution**: Use techniques like extraction (`Extract Method` or `Extract Class`) or `Pulling Up Methods/Fields` in a superclass if duplication occurs across subclasses.

## Long Method

**Symptom**: A method that has grown too long, making it hard to understand.

**Solution**: Break down the method into smaller, more focused methods. Utilize `Extract Method` and `Replace Temp with Query` where applicable.

## Large Class

**Symptom**: A class trying to do too much, often characterized by an excessive number of fields.

**Solution**: Use `Extract Class` to divide responsibilities into separate classes.

## Long Parameter List

**Symptom**: Methods with a large number of parameters are hard to understand and use.

**Solution**: Employ techniques like `Replace Parameter with Method Call` or `Introduce Parameter Object` to simplify.

## Divergent Change

**Symptom**: When one class is often changed in different ways for different reasons. (Violation of SRP)

**Solution**: Use `Extract Class` to split the class into separate classes, each handling one aspect of the original class’s responsibilities.

## Shotgun Surgery

**Symptom**: A change that needs to be applied to a lot of different classes.

**Solution**: Use `Move Method` or `Move Field` to consolidate the changes into a single class or closely related classes.

## Feature Envy

**Symptom**: A method that seems more interested in a class other than the one it actually resides in.

**Solution**: Use `Move Method` to move the method to the class it is most interested.

## Data Clumps

**Symptom**: Similar chunks of data cropping up in multiple places.

**Solution**: Group the data together into a new class using `Extract Class`.

## Primitive Obsession

**Symptom**: Overuse of primitives (like integers, strings, and booleans) instead of small objects for simple tasks.
   - While primitive types are fundamental and necessary, over-reliance on them can lead to several issues:
      - **Lack of clarity**: Using primitives can make the code less clear. For example, representing a date as a string or an integer doesn't provide immediate understanding of the format or the value being represented.
      - **Duplication**: When you use primitive types, there's a tendency to duplicate logic. For example, validation logic for a specific type of data might be repeated in several places.
      - **Lack of encapsulation**: Primitive types don't encapsulate behavior. This means any logic related to the data must be implemented outside the representation of the data, leading to scattered and less cohesive code.

**Solution**: Replace data values with objects using techniques like `Replace Data Value with Object`.

## Switch Statements

**Symptom**: Complex `switch` or `if` statements, especially with type checking and casting.

**Solution**: Often indicative of missing polymorphism. Use 'Replace Conditional with Polymorphism'.

## Temporary Field

**Symptom**: Fields that are only set and used under certain conditions. This can lead to code that is difficult to understand and maintain for several reasons:
   - **Inconsistency**: Since the fields are only set in certain situations, the object's state can be inconsistent. This makes it harder to understand the state of an instance of the class at any given point.
   - **Complexity in Class Design**: The presence of temporary fields often indicates that a class is trying to do too much or is handling scenarios that should be broken down into separate classes.
   - **Null Checks and Conditional Logic**: The code often needs additional null checks or conditional logic to handle these fields, leading to more complex and error-prone code.

**Solution**: If a field is only used in certain situations, it might indicate that the responsibilities of the class can be split into two or more classes.  Use `Extract Class` to split the class into separate classes. Using `Introduce Null Object` can help to avoid null checks throughout the code.

## Inappropriate Intimacy

**Symptom**: Classes that have too many details about each other.

**Solution**: Classes that are overly familiar with each other can be decoupled using `Move Method/Field`. Use `Extract Class` to put the commonality in a new Class.

## Lazy Class

**Symptom**: Classes that do too little to justify their existence. Often this might be a class that used to pay its way but has been downsized with refactoring.

**Solution**: If you have subclasses that aren't doing enough, try to use `Collapse Hierarchy` to merge the subclass and superclass. Nearly useless components should be subjected to `Inline Class`.

## Alternative Classes with Different Interfaces

**Symptom**: Similar classes with different methods to do the same thing.

**Solution**: Make the interfaces of these classes consistent through `Rename Method` and `Move Method`.

## Incomplete Library Class

**Symptom**: A library class may not provide all the necessary features, and may lack some necessary features.

**Solution**: If there are just a couple of methods that you wish the library class had, use `Introduce Foreign Method`. If there is a whole load of extra behavior, you need `Introduce Local Extension`.

## Speculative Generality

**Symptom**: Unused or unnecessary abstractions, often 'just in case'. (over-design)

**Solution**: If you have abstract classes that aren't doing much, use `Collapse Hierarchy`. Unnecessary delegation can be removed with `Inline Class`.

## Parallel Inheritance Hierarchies

**Symptom**: Every time you make a subclass of one class, you also have to make a subclass of another.

**Solution**: Use `Move Method` and `Move Field` to merge hierarchies.

## Message Chains

**Symptom**: This occurs when a client gets data or invokes actions by navigating multiple objects' relationships in a chain-like manner.

```java 
// Example of a Message Chain
String streetName = order.getCustomer().getAddress().getStreet();
```

**Solution**: Break up the chain using `Hide Delegate`. Use `Extract Method` to take a piece of the code that uses it and then `Move Method` to push it down the chain.

## Middle Man

**Symptom**: A class that does little beyond delegating to another class. While delegation is a useful and common technique in software design, overusing it can lead to an unnecessary increase in complexity and a decrease in the readability and maintainability of the code.

**Solution**: `Remove Middle Man` to let the client call the end-method directly.

## Data Class

**Symptom**: Classes that have fields, getters, and setters but no additional functionality. These are classes that hold just some data. Almost certainly, their details are manipulated by other classes (otherwise, their existence would be almost meaningless).

**Solution**: Try to use `Move Method` to move behavior into the data class. If you can't move a whole method, use `Extract Method` to create a method that can be moved. After a while you can start using `Hide Method` on the getters and setters.

## Refused Bequest

**Symptom**: A subclass that doesn’t use all the methods and properties inherited from its parent class. In this case, sooner or later, someone will call a superclass method that shouldn't have been called.

**Solution**: Use `Replace Inheritance with Delegation` or remove the inheritance altogether.


## Comments

> When you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous.

**Symptom**: Over-reliance on comments to explain complex code.

**Solution**: Use `Rename Method` and `Extract Method` to refactor the code to make it self-explanatory, reducing the need for comments.

<br>

---

The various refactoring techniques in the above (like `Extract Method`, `Hide Method`, `Replace Inheritance with Delegation`, etc.) can be found at the following links:
   - [Refactoring Techniques](https://refactoring.guru/refactoring/techniques)

<br>

---

**Reference:**

- Fowler, M. and Beck, K. (1999) _Refactoring : improving the design of existing code._ Reading, MA: Addison-Wesley (The Addison-Wesley object technology series).
