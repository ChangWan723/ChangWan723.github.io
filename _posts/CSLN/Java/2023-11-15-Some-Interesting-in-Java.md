---
title: Some Interesting Codes in Java
date: 2023-11-15 23:49:00 +0530
categories: [(CS) Learning Note, Java]
tags: [computer science, software engineering, Java]
pin: false
---

Java has some interesting counter-intuitive code. If you run this code, it is possible that something unexpected will happen. By understanding them, we can avoid some bugs and get a better understanding of Java.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [switch](#switch)
    * [Example 1 (Without `break`)](#example-1-without-break)
    * [Example 2 (With `break` in the next one)](#example-2-with-break-in-the-next-one)
    * [Example 3 (`default` is at the top)](#example-3-default-is-at-the-top)
    * [Example 4 (`default` is at the top, and meet `default` conditions)](#example-4-default-is-at-the-top-and-meet-default-conditions)
  * [Autoboxing and Unboxing](#autoboxing-and-unboxing)
    * [Example 1 (Integer)](#example-1-integer)
    * [Example 2 (Double)](#example-2-double)
    * [Example 4 (`equals()`)](#example-4-equals)
    * [Example 3 (Integer and Long)](#example-3-integer-and-long)
<!-- TOC -->

---

## switch

Generally in the actual development, we will add `break` after the `case` statement, but without `break` will report errors? The answer is "no", but this will have some unexpected results. 

### Example 1 (Without `break`)

Let's look at the following code:

```java 
public static void main(String[] args) {
    int flag = 2;
    switch (flag) {
        case 1:
            System.out.println("case1");
        case 2:
            System.out.println("case2");
        case 3:
            System.out.println("case3");
        default:
            System.out.println("default");
    }
}
```

The result is not `case2`. It will be:

```
case2
case3
default

```

>If there is no break after a `case` statement that satisfies the condition, **subsequent cases will run without the judgement**, and the statement in the `default` will also be executed.
{: .prompt-tip }

### Example 2 (With `break` in the next one)

```java 
public static void main(String[] args) {
    int flag = 1;
    switch (flag) {
        case 1:
            System.out.println("case1");
        case 2:
            System.out.println("case2");
            break;
        case 3:
            System.out.println("case3");
        default:
            System.out.println("default");
    }
}
```

result:

``` 
case1
case2

```

>If there is no break in a statement that meets the case condition, it will continue down the line, but if it **meets a break, it will be interrupted**.
{: .prompt-tip }

### Example 3 (`default` is at the top)

```java 
public static void main(String[] args) {
    int flag = 1;
    switch (flag) {
        default:
            System.out.println("default");
        case 1:
            System.out.println("case1");
        case 2:
            System.out.println("case2");
        case 3:
            System.out.println("case3");
    }
}
```

result:

``` 
case1
case2
case3

```

### Example 4 (`default` is at the top, and meet `default` conditions)

```java 
public static void main(String[] args) {
    int flag = 0;
    switch (flag) {
        default:
            System.out.println("default");
        case 1:
            System.out.println("case1");
        case 2:
            System.out.println("case2");
        case 3:
            System.out.println("case3");
    }
}
```

result:

``` 
default
case1
case2
case3

```

> The `default` statement is executed when there are no matching cases, and **this is regardless of the location of the `default`**.
{: .prompt-tip }


## Autoboxing and Unboxing

### Example 1 (Integer)

```java 
public static void main(String[] args) {
    int i1 = 100;
    int i2 = 100;
    int i3 = 200;
    int i4 = 200;

    System.out.println(i1 == i2);
    System.out.println(i3 == i4);
}
```

What is the result? Obviously, both are "true". No problem.

result:

``` 
true
true

```

But how about this:

```java 
public static void main(String[] args) {
    Integer i1 = 100;
    Integer i2 = 100;
    Integer i3 = 200;
    Integer i4 = 200;

    System.out.println(i1 == i2);
    System.out.println(i3 == i4);
}
```

What is the result? Both are "true"? Or Both are "false"? It's all wrong. The result is:

``` 
true
false

```

---

Why? To get to the reason, we need to mention the concept of **"Autoboxing and Unboxing"** in Java.

> **Autoboxing** is the automatic conversion of a primitive data type (e.g., int, double) to its corresponding wrapper class (e.g., Integer, Double) when needed.
> 
> **Unboxing** is the automatic conversion of a wrapper class object back to its corresponding primitive data type when needed.
{: .prompt-tip }

For example:

```java 
public class Main {
    public static void main(String[] args) {
        Integer intObject = 10;  // Autoboxing
        int intPrimi = intObject; // Unboxing
    }
}
```
We can decompile the above code using the `javap -c` command:

![](https://i.postimg.cc/zXLqFqDF/si1.png){: .w-100 .shadow .rounded-10 }

And we can see that `Integer.valueOf()` is called during Autoboxing. Let's look at the source code for `Integer.valueOf()`:

```java
static final int low = -128;
static final int high = 127;
 
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
```

So, the value of `i1` and `i2` in the above code is `100` (between -128 and 127), so it will take the already existing object directly from the `cache`, so `i1` and `i2` **are pointing to the same object**. And the objects of `i3` and `i4` are newly created, so they **are two different objects**.

> **This design can significantly improve performance.** The reason is that in some common cases, Java programs will frequently use some small integer values (between -128 and 127). By sharing objects in the cache, you can reduce the pressure of object creation and GC, thus improving the efficiency of the program.
{: .prompt-tip }

### Example 2 (Double)

```java 
public static void main(String[] args) {
    Double i1 = 100.0;
    Double i2 = 100.0;
    Double i3 = 200.0;
    Double i4 = 200.0;

    System.out.println(i1 == i2); // false
    System.out.println(i3 == i4); // false
}
```

>The `valueOf()` of the classes `Integer`, `Short`, `Byte`, `Character`, and `Long` have the cache. But the `valueOf()` of `Double` and `Float` do not.
{: .prompt-warning }

### Example 4 (`equals()`)

```java 
public static void main(String[] args) {
    Integer i1 = 100;
    Integer i2 = 100;
    Integer i3 = 200;
    Integer i4 = 200;

    System.out.println(i1.equals(i2)); // true
    System.out.println(i3.equals(i4)); // true
}
```

`equals()` checks for **value** and **type** equality. If **value** and **type** both is same, the result is `true`.

### Example 3 (Integer and Long)

```java 
public static void main(String[] args) {
    Integer a = 1;
    Integer b = 2;
    Integer c = 3;
    Long g = 3L;
    Long h = 2L;

    System.out.println(c==(a+b)); // true
    System.out.println(c.equals(a+b)); // true
    System.out.println(g==(a+b)); // true
    System.out.println(g.equals(a+b)); // false
    System.out.println(g.equals(a+h)); // true
}
```

> When both operands of the `==` operator are references to wrapper types, **it compares whether they point to the same object.** However, if one of the operands is an expression (i.e., contains arithmetic operations), **it compares the numerical values** (i.e., **automatic unboxing is triggered**).
{: .prompt-warning }

- `System.out.println(c==(a+b));`
  - This checks if `c` (an `Integer` with value 3) is equal to the result of `a+b` (which also results in 3). In Java, the `+` operation between two `Integer` objects results in an `int` primitive. Since `c` is auto-unboxed to an `int`, the comparison is between two `int` values. The result is `true`.

- `System.out.println(c.equals(a+b));`
  - This checks if the `Integer` object `c` is equal to the `Integer` object resulting from `a+b`. Here, `a+b` is auto-boxed back to an `Integer` object. The `equals()` method in the `Integer` class checks for value equality, and since both values are 3, the result is `true`.

- `System.out.println(g==(a+b));`
  - This checks if `g` (a `Long` with value 3) is equal to `a+b` (resulting in 3). Here, `a+b` is promoted to a `long` for the comparison, and since their values are the same, the result is `true`. (Automatic unboxing is triggered)

- `System.out.println(g.equals(a+b));`
  - This is a bit tricky. `g.equals(a+b)` checks if the `Long` object `g` is equal to the `Integer` object resulting from `a+b`. In Java, **`equals()` checks for both value and type equality**. Since the types are different (`Long` vs `Integer`), the result is `false`.

- `System.out.println(g.equals(a+h));`
  - This checks if the `Long` object `g` is equal to the result of `a+h`. Here, `a+h` results in a `Long` object. Since both are `Long` objects with the same value (3), the result is `true`.
