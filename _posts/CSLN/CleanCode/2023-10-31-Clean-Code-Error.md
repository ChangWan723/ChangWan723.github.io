---
title: "Clean Code: Error Handling"
date: 2023-10-31 20:35:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/error.jpg
---

> Many code bases are completely dominated by error handling. When I say dominated, I don’t mean that error handling is all that they do. I mean that it is nearly impossible to see what the code does because of all of the scattered error handling. **Error handling is important, but if it obscures logic, it’s wrong.**

Writing clean code involves handling errors in a way that makes the code more robust and easier to maintain.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Use Exceptions Rather Than Return Codes](#use-exceptions-rather-than-return-codes)
  * [Write Your Try-Catch-Finally Statement First](#write-your-try-catch-finally-statement-first)
  * [Use Unchecked Exceptions](#use-unchecked-exceptions)
  * [Provide Context with Exceptions](#provide-context-with-exceptions)
  * [Define Exception Classes in Terms of a Caller's Needs](#define-exception-classes-in-terms-of-a-callers-needs)
  * [Don't Return Null](#dont-return-null)
  * [Don't Pass Null](#dont-pass-null)
<!-- TOC -->

---

## Use Exceptions Rather Than Return Codes

Using exceptions for error handling is often cleaner than using return codes. Exceptions allow you to separate the correct path from the error handling, making the code more readable and maintainable.

```java
// Using return codes. The caller must check for errors immediately after the call.
if (user.save() == SaveResult.FAILED) {
  handleError();
}

// Using exceptions. Allow you to separate the correct path from the error handling.
try {
  user.save();
} catch (SaveException e) {
  handleError();
}
```

## Write Your Try-Catch-Finally Statement First

Writing the `try-catch-finally` statement first when you are writing code that could throw exceptions. It helps you define what the user of the code should expect, no matter what goes wrong with the code that is executed in the `try`.

This will have the following benefits:
1. **Reducing code bugs**: By determining how errors are handled in the first place, programmers can ensure that exceptions that are handled in an appropriate way, avoiding errors that are ignored or mishandled.
2. **Focus on Business Logic**: Once the error handling structure is in place, you can focus solely on implementing the business logic without worrying about how to handle errors, leading to cleaner and more efficient code.
3. **Ensure Resource Release**: In the `try-finally`, you can ensure that resources are properly released in the event of an exception, preventing resource leaks.


## Use Unchecked Exceptions

- Programmers should **convert predictable Errors (Exceptions) into normal process** whenever possible, rather than using exceptions. If you have to use exceptions, you should **use Unchecked Exceptions**.
- Using unchecked (runtime) exceptions **eliminates** the need for the calling code to **handle exceptions it doesn't know how to handle**.
- Checked exceptions **violate the Open/Closed Principle**, **increase coupling** between methods, classes, etc.

> The price of checked exceptions is an **Open/Closed Principle violation**. If you throw a checked exception from a method in your code and the `catch` is three levels above, you must declare that exception in the signature of each method between you and the catch. This means that a change at a low level of the software can force signature changes on many higher levels. The changed modules must be rebuilt and redeployed, even though nothing they care about changed.

## Provide Context with Exceptions

When throwing an exception, provide enough context to help diagnose the problem.

For example:
```java
throw new UserNotFoundException("User not found with ID: " + userId);
```

## Define Exception Classes in Terms of a Caller's Needs

Create exception classes that are meaningful to the caller and encapsulate the error information.

```java
public class UserNotFoundException extends RuntimeException {
  public UserNotFoundException(String message) {
    super(message);
  }
}
```

## Don't Return Null

- If you are calling a null-returning method from a third-party API, consider wrapping that method with a method that throws an exception or returns an optional.
- Returning `null` from methods can lead to NullPointerExceptions. Instead, **throw an exception** or **return an optional**.

```java
// Returning null
public User findUser(String userId) {
  //...
  return null;
}

// Throwing an exception
public User findUser(String userId) {
   //...
   throw new UserNotFoundException("User not found with ID: " + userId);
}

// Returning an optional
public Optional<User> findUser(String userId) {
  //...
  return Optional.empty();
}
```

---

If we return `null` in our code, it means we have to check the object we are using:

```java
public List<Order> getUserOrders(int userId) {
    // If there are no orders for the user...
    return null;
}

...

List<Order> orders = getUserOrders(userId);
if (orders == null) {
    System.out.println("User has no orders.");
} else {
    for (Order order : orders) {
        // Process the order
    }
}
```

We can avoid null-returning by using Collections.emptyList() in `getUserOrders`. This makes the **code cleaner** and also **reduces the risk** of `NullPointerExceptions`:

```java
public List<Order> getUserOrders(int userId) {
    // If there are no orders for the user...
    return Collections.emptyList();
}

...

List<Order> orders = getUserOrders(userId);
for (Order order : orders) {
    // Process the order
}
```

> When I worked at Huawei, colleagues in my group didn't follow this rule very well. This leads to our project **crashing often due to null pointers**, and the error logs were **full of `NullPointerExceptions`**.
> 
> And every time I did code review, my colleagues would always remind me if I did null-pointer checking on the variables. It was really annoying and time-wasting. 
> 
> So, please don't return null.
{: .prompt-tip }

> When we return `null`, we are essentially creating work for ourselves and foisting problems upon our callers. All it takes is **one missing `null`** check to send an application **spinning out of control**. 

## Don't Pass Null

- Returning `null` from methods is bad, but passing `null` into methods is worse. (Unless you are working with an API which expects you to pass `null`)

> In most programming languages there is no good way to deal with a `null` that is passed by a caller accidentally. Because this is the case, the rational approach is to forbid passing `null` by default. When you do, **you can code with the knowledge that a `null` in an argument list is an indication of a problem**, and end up with far fewer careless mistakes.

<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
