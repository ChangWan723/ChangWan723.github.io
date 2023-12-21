---
title: Limitations in Refactoring
date: 2023-12-21 20:30:00 UTC
categories: [(CS) Learning Note, Refactoring]
tags: [software engineering, Refactoring, code]
pin: false
---

We know the benefits of refactoring. We know the palpable difference they can make to our work. But we must also be clear about the limitations.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Refactoring with Databases](#refactoring-with-databases)
    * [Strategies for Database Refactoring:](#strategies-for-database-refactoring)
  * [Changing Interfaces](#changing-interfaces)
    * [Mitigating Interface Change Issues](#mitigating-interface-change-issues)
  * [When Shouldn't You Refactor?](#when-shouldnt-you-refactor)
<!-- TOC -->

---


## Refactoring with Databases

- Refactoring code that interacts with databases can be particularly tricky. Database schemas are often rigid, and changes can have far-reaching implications.
   - Most business applications are **tightly coupled to the database schema** that supports them. That's one reason that the database is difficult to change.
   - Another reason is **data migration**. Even if you minimise the dependencies between the database schema and the object model, changing the database schema can force you to migrate data

### Strategies for Database Refactoring:
- **Separate Layer**: In non-object databases, one way to solve this problem is to insert a Separate Layer between the object model and the database model, which isolates changes in each of the two models. Such a Separate Layer adds complexity to the system but gives you a lot of flexibility.
- **Migration Scripts**: For object databases, some object-oriented databases provide automatic migration between different data models. For not having this function, changes can be managed systematically using database migration scripts.

## Changing Interfaces

Modifying interfaces can be problematic, especially if they are widely used across the system. Changes can ripple out, affecting numerous components.

> For example, `Rename Method`, a simple refactoring technique, is the Changing Interfaces.
>    - Sometimes you'll find that renaming a public method can cause a lot of trouble.
>    - You should also use the deprecation feature provided by Java to mark the old interface as `deprecated`. This way the caller will notice it.
{: .prompt-tip }


### Mitigating Interface Change Issues

- **Deprecate, Don’t Delete**: Instead of immediately removing old methods, deprecate them first. When you want to change the name of the API, leave the old API and encourage users to call the new API. 
- **Adapter Patterns**: Use the Adapter Pattern to bridge the old and new interfaces, providing backward compatibility.
- **Publish APIs carefully**: Try not to expose APIs to external users if you can. Don't publish APIs too early either.

## When Shouldn't You Refactor?

- **Code doesn't Work**: If the code doesn't work at all, you shouldn't refactor it, you should rewrite it. Remember, before refactoring, the code must at least work in most cases.
- **Near a Deadline**: Avoid major refactorings when close to a critical deadline.
- **In the Absence of Tests**: If there’s a lack of sufficient testing, refactoring can introduce more problems than it solves.
- **When Rewriting is More Feasible**: In cases where the codebase is too outdated or convoluted, a rewrite might be more efficient.

<br>

---

**Reference:**

- Fowler, M. and Beck, K. (1999) _Refactoring : improving the design of existing code._ Reading, MA: Addison-Wesley (The Addison-Wesley object technology series).
