---
title: "Clean Code: Functions"
date: 2023-10-18 00:01:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/functions.jpg
---

Functions form the building blocks of our software. Their importance cannot be overstated.

>**Master programmers think of systems as stories to be told rather than programs to be written.** They use the facilities of their chosen programming language to construct a much richer and more expressive language that can be used to tell that story. Part of that domain-specific language is the hierarchy of functions that describe all the actions that take place within that system. In an artful act of recursion those actions are written to use the very domain-specific language they define to tell their own small part of the story.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Why do we care about functions?](#why-do-we-care-about-functions)
  * [Rules for Good Functions](#rules-for-good-functions)
    * [Small!](#small)
    * [Do One Thing](#do-one-thing)
    * [One Level of Abstraction per Function](#one-level-of-abstraction-per-function)
    * [Switch Statements](#switch-statements)
    * [Descriptive Names](#descriptive-names)
    * [Function Arguments](#function-arguments)
    * [Have No Side Effects](#have-no-side-effects)
    * [Command and Query Separation](#command-and-query-separation)
    * [Exceptions over Returning Error Codes](#exceptions-over-returning-error-codes)
    * [Don't Repeat Yourself](#dont-repeat-yourself)
    * [Don't Try to Follow All the Rules When You Start](#dont-try-to-follow-all-the-rules-when-you-start)
<!-- TOC -->

---

## Why do we care about functions?

Let's look at the following code: 

```java
public List<Transaction> processTransactions(List<Transaction> transactions) {
    List<Transaction> output = new ArrayList<>();
    for (Transaction transaction : transactions) {
        if (transaction.isValid()) {
            if (user.isActive()) {
                if (transaction.getAmount() > 1000) {
                    if (transaction.getCurrency().equals("USD")) {
                        if (user.getCountry().equals("USA")) {
                            transaction.setFee(0.01);
                            output.add(transaction);
                            if (transaction.getType().equals("REFUND")) {
                                transaction.setAmount(transaction.getAmount() - transaction.getFee());
                                output.add(transaction);
                            }
                        } else {
                            transaction.setFee(0.02);
                            output.add(transaction);
                            if (transaction.getType().equals("REFUND")) {
                                transaction.setAmount(transaction.getAmount() - transaction.getFee());
                                output.add(transaction);
                            }
                        }
                    }
                }
            }
        }
    }
    return output;
}
```

This piece of **code has Meaningful Names**. Spacing and indentation are **reasonable**. And Functions are not **complicated**. **But how long does it take you to fully understand it?** 3 minutes? 5 minutes? I'm sure reading this code does make you uncomfortable. This code is **full of `if` statements** and has **a lot of nesting**. There is also **code duplication**.

However, with the help of some simple Java 8's Stream API, ternary expressions, guard clause, and a little restructuring, (**No naming changes**) **we can greatly optimise this code**. The effective lines of code for the `processTransactions` function **have been optimised to 8 lines**. Although we split out 3 new functions, **these are fairly simple** (one or two effective line of code). With a basic understanding of the Java Stream API, you can understand this code in a very short time.

```java
public List<Transaction> processTransactions(List<Transaction> transactions) {
    if (!user.isActive())
       return Collections.emptyList();

    return transactions.stream()
            .filter(Transaction::isValid)
            .filter(this::isLargeUSDTransaction)
            .map(this::assignFeesBasedOnCountry)
            .map(this::handleRefundType)
            .collect(Collectors.toList());
}

private boolean isLargeUSDTransaction(Transaction transaction) {
    return transaction.getAmount() > 1000 && "USD".equals(transaction.getCurrency());
}

private Transaction assignFeesBasedOnCountry(Transaction transaction) {
    transaction.setFee("USA".equals(user.getCountry()) ? 0.01 : 0.02);
    return transaction;
}

private Transaction handleRefundType(Transaction transaction) {
    transaction.setAmount("REFUND".equals(transaction.getType()) ? transaction.getAmount() - transaction.getFee() : transaction.getAmount());
    return transaction;
}
```

>The 3 split functions are very simple. **Is it necessary to define such simple functions?** Actually, it has some **advantages**: 
> - It makes the programme more **readable**; 
> - It makes the code **reusable**. 
>
>However, it also has a **disadvantage**: 
> - When it is called frequently, there is a loss of performance of the application due to the **overhead of calling the function**. (In fact, with compiler development, this problem is **negligible in modern compilers**. And we also can optimise it using `inline` functions, but `inline` functions have their drawbacks: code bloat)
>
>**There is never perfect code**, we need to change our code according to the real project.
{: .prompt-tip }

## Rules for Good Functions

### Small!

>The first rule of functions is that **they should be small**. The second rule of functions is that **they should be smaller than that**.

- Keep the length of the function **under 20 lines**
- that functions should not be large enough to hold nested structures. The indent level of a function **should not be greater than one or two**.
- The blocks within `if` statements, `else` statements, `while` statements, and so on **should be one line long** (should be a function call). In this way, it can
   - keep the enclosing function small
   - create self-documenting code (the functions have Meaningful Names)

> Tip:
> 
> If each function is **small** enough, it means that **there will be a large number of function calls**, affecting the **performance** of the program. 
> 
> While function calls do have some performance overhead (e.g., stack operations), **this overhead is negligible in most modern applications.** Especially in non-performance-critical applications like desktop apps or web services. Most **performance bottlenecks** tend to occur in I/O operations, database queries, network calls, or the efficiency of algorithms.
> 
> In most cases, code readability, clarity, and maintainability are more crucial. So, **prioritize writing clear and organized code.** Optimize for performance only when it becomes an actual problem.
{: .prompt-tip }

### Do One Thing

>FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT **WELL**. THEY SHOULD DO IT **ONLY**.

Functions should do one thing and do it well. They should not be multifaceted. If a function is doing more than one action, it becomes harder to read, modify, and debug.

**How to know whether a function is doing only one thing?**
1. **The Single Responsibility Principle (SRP)**
   - The SRP, a part of the SOLID principles, states that a class should have only one reason to change.
2. **Level of Abstraction**
   - A function should operate at a single level of abstraction. If you find that some operations are high-level (like business rules) and others are low-level (like string manipulations), the function might be doing multiple things.
3. **Number of Tasks**
   - A clear indicator is the number of tasks a function performs. If a function is responsible for multiple tasks, it's doing more than one thing.
4. **Unit Testing**
   - When writing unit tests, if you find that testing a function requires checking multiple behaviors or results, it's an indicator that the function might be doing too much.
5. **Comments**
   - If you find yourself using comments to separate sections inside a function, it's a red flag. Each section probably deserves its function.
6. **Descriptive Naming**
   - If it's challenging to give a function a concise, descriptive name, it might be doing too much. Names like `processDataAndSaveAndNotify()` are clear signs.


### One Level of Abstraction per Function

Maintaining a consistent level of abstraction within a function aids in readability. Mixing high-level logic with details can be confusing. Functions should either describe a concept in a high-level or define computations, not both.



### Switch Statements

>It’s also hard to make a switch statement that does one thing. By their nature, switch statements always do N things.

`Switch` cases can often be long and violate the "Do One Thing" principle.We'd be better to deal with this situation using polymorphism, encapsulating each case within its class or function.

>My general rule for switch statements is that they can be tolerated if they appear only once, are used to create polymorphic objects, and are hidden behind an inheritance relationship so that the rest of the system can’t see them.

### Descriptive Names

>Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment.

Use descriptive names for functions. The length of the name is secondary to its clarity. Longer, descriptive names are preferred over short, ambiguous ones.

```
function calculateEstimatedShippingTime() {
// Implementation here
}
```

And be consistent in your names. Use the same phrases, nouns, and verbs in the function names you choose for your modules.


### Function Arguments

A smaller number of arguments is preferable. Ideally:

1. Zero arguments (niladic)
2. One argument (monadic)
3. Two arguments (dyadic)
4. Three arguments (triadic)

>When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own.

- Avoid more than three when possible. 
- Avoid flag arguments, which claims that functions do more than one thing.

### Have No Side Effects

Functions should not have any hidden side effects, meaning they should not change any state or alter data unexpectedly. This ensures that functions remain pure and predictable.

### Command and Query Separation

>Returning error codes from command functions is a subtle violation of command query separation.

Functions should either do something (a command) or answer something (a query) but not both. This means a function should either change the state of an object or return some information about it, but not simultaneously.



### Exceptions over Returning Error Codes

It's cleaner to throw exceptions rather than returning error codes. This separates the error-handling from the main logic.


Extract Try/Catch Blocks:

```java
public void delete(Page page) {
    try {
        deletePageAndAllReferences(page);
    } catch (Exception e) {
        logError(e);
    }
}

private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
}

private void logError(Exception e) {
    logger.log(e.getMessage());
}
```

>In the above, the delete function is all about error processing. It is easy to understand and then ignore. The deletePageAndAllReferences function is all about the processes of fully deleting a page. Error handling can be ignored. This provides a nice separation that makes the code easier to understand and modify

**Functions should do one thing. Error handing is one thing.**

### Don't Repeat Yourself

Look at the example at the top of this blog, it's doing the same thing in the last `if` and `else` code block.

> Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling or eliminating it.

### Don't Try to Follow All the Rules When You Start

> Writing software is like any other kind of writing. When you write a paper or an article, you get your thoughts down first, then you massage it until it reads well. The first draft might be clumsy and disorganized, so you wordsmith it and restructure it and refine it until it reads the way you want it to read.

When writing a function, you don't start out with a function that follows all the rules, but only after polishing the code at a later stage, disassembling the function, changing the name, eliminating duplicates, and other manipulations.


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
