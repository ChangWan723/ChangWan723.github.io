---
title: Some Interesting Codes in Java
date: 2023-11-15 23:49:00 +0530
categories: [(CS) Learning Note, Java]
tags: [computer science, software engineering, Java]
pin: false
---

Java has some interesting and counter-intuitive code. If you run this code, it is possible that something unexpected will happen. By understanding them, we can avoid some bugs and get a better understanding of Java.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Precision Problems with Floating Point Numbers](#precision-problems-with-floating-point-numbers)
  * [switch](#switch)
    * [Example 1 (Without `break`)](#example-1-without-break)
    * [Example 2 (With `break` in the next one)](#example-2-with-break-in-the-next-one)
    * [Example 3 (`default` is at the top)](#example-3-default-is-at-the-top)
    * [Example 4 (`default` is at the top, and meet `default` conditions)](#example-4-default-is-at-the-top-and-meet-default-conditions)
  * [Autoboxing and Unboxing](#autoboxing-and-unboxing)
    * [Example 1 (Integer)](#example-1-integer)
    * [Example 2 (Double)](#example-2-double)
    * [Example 3 (`equals()`)](#example-3-equals)
    * [Example 4 (Integer and Long)](#example-4-integer-and-long)
  * [Addition of different types](#addition-of-different-types)
  * [Reference Copy and Shallow Copy](#reference-copy-and-shallow-copy)
<!-- TOC -->

---

## Precision Problems with Floating Point Numbers

``` 
public static void main(String[] args) {
    System.out.println(0.1 * 3 == 0.3); // false
    System.out.println(0.1 + 0.2 == 0.3); // false
    System.out.println(0.1 + 0.4 == 0.5); // true
    System.out.println(0.5 + 0.5 == 1); // true
    System.out.println(0.125 * 2 == 0.25); // true
    System.out.println(4.35 * 100 == 435); // false
}
```

Novices are often confused when using floating point numbers in java. This is because floating-point numbers (i.e., `float` and `double`) always involve a degree of uncertainty in Java, as these values are approximated to **represent real numbers using a finite number of bits (binary system)**.

- Java follows the IEEE 754 standard for floating-point arithmetic, which is used by most modern computers. The two primary types for floating-point numbers in Java are `float` and `double`.
  - **float**: This is a single-precision 32-bit IEEE 754 floating-point.
  - **double**: This is a double-precision 64-bit IEEE 754 floating-point.

We can see how this can happen by printing out the result using `println()`:

```java 
public static void main(String[] args) {
    System.out.println(0.3); // 0.3
    System.out.println(0.1 + 0.2); // 0.30000000000000004
    System.out.println(0.1 * 3); // 0.30000000000000004
    System.out.println(0.1 + 0.4); // 0.5
    System.out.println(0.5 + 0.5); //1.0
    System.out.println(0.125 * 2); // 0.25
    System.out.println(4.35 * 100); // 434.99999999999994
}
```

- `0.3` prints as expected because it's directly being printed **without any arithmetic operation** that introduces additional error.
- `0.1 + 0.2` results in a long decimal due to floating-point arithmetic. (The binary representation of `0.3` is `0.0100110011......`, which is infinite)
- `0.1 * 3` is similar to the addition, and the result has a floating-point representation error.
- `0.1 + 0.4` results in 0.5, which is exact. This calculation does not show a precision issue because `0.5` can be precisely represented in binary **as it is a power of the form `1/2`**, so it **can be accurately expressed in binary form**. (The binary representation of `0.5` is `0.1`)
- `0.5 + 0.5` results in 1.0, which is exact. Same as above.
- `0.125 * 2` results in 0.25, which is exact. Same as above. (The binary representation of `0.125` is `0.001`)
- `4.35 * 100` results in a value close to 435 but not exactly 435 due to the result has a floating-point representation error.

> These examples highlight the importance of using `BigDecimal` for precise monetary calculations in Java, where such a precision is critical.
{: .prompt-tip }

For example:

```java 
public static void main(String[] args) {
    BigDecimal price = new BigDecimal("4.35");
    BigDecimal quantity = new BigDecimal("100");
    System.out.println(price.multiply(quantity)); // 435.00
}
```

If we don't use `BigDecimal`, for equality checks, avoid direct comparison of floating-point numbers. Instead, **check if the absolute difference is within a small tolerance**:

```java
double result = 4.35 * 100;
double expected = 435.00;

final double EPSILON = 0.00001;
if (Math.abs(result - expected) < EPSILON) {
// Considered equal
}
```

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

What is the result? Obviously, both are "true".

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

### Example 3 (`equals()`)

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

### Example 4 (Integer and Long)

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
  - This checks if the `Integer` object `c` is equal to the `Integer` object resulting from `a+b`. Here, `a+b` is auto-boxed back to an `Integer` object. (Auto-boxed is triggered by `equals()`) The `equals()` method in the `Integer` class checks for value equality, and since both values are 3, the result is `true`.

- `System.out.println(g==(a+b));`
  - This checks if `g` (a `Long` with value 3) is equal to `a+b` (resulting in 3). Here, `a+b` is promoted to a `long` for the comparison, and since their values are the same, the result is `true`. (Automatic unboxing is triggered by `+` and `==`)

- `System.out.println(g.equals(a+b));`
  - This is a bit tricky. `g.equals(a+b)` checks if the `Long` object `g` is equal to the `Integer` object resulting from `a+b`. In Java, **`Long.equals()` checks for both value and type equality**. Since the types are different (`Long` vs `Integer`), the result is `false`.

- `System.out.println(g.equals(a+h));`
  - This checks if the `Long` object `g` is equal to the result of `a+h`. Here, `a+h` results in a `Long` object. Since both are `Long` objects with the same value (3), the result is `true`.

> - `==`: 
>   - **Usage with Primitive Types**: When used with primitive types (like int, char, double), it compares their values.
>   - **Usage with Objects**: When used with objects, it checks if both references are pointing to the same object, not comparing the actual content of the objects.
>
> - `.equals()`:
>   - **Usage**: This method must be used for comparing the content of objects. The behavior of `.equals()` is class-specific (it depends on how the `.equals()` method is overridden in the class).
{: .prompt-tip }


## Addition of different types

```java 
public static void main(String[] args) {
    Object object1 = 1 + 1 + "1";
    Object object2 = "1" + 1 + 1;

    System.out.println(object1);
    System.out.println(object2);
}
```

result:

``` 
21
111

```

- `1 + 1 + "1"`:
  - **The addition operations are evaluated from left to right.**
  - First, `1 + 1` is evaluated (because they are two integer literals), resulting in `2`.
  - Then `2` (which is now an integer) is added to `"1"` (a string literal). In Java, **when you add an integer to a string, the integer is converted to a string** and the two strings are concatenated.
  - So, the result is the string `"21"`.

- `"1" + 1 + 1`:
  - Again, evaluation is from left to right.
  - First, `"1"` (a string literal) is concatenated with `1` (an integer), which results in the string `"11"` because the integer is converted to a string.
  - Then, the string `"11"` is concatenated with the next `1` (an integer), resulting in the string `"111"`.


## Reference Copy and Shallow Copy

```java 
class ExampleObject implements Cloneable{
    public int primitiveValue = 1;

    public int[] arrValue = {1};

    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

``` 
public static void main(String[] args) {
    ExampleObject original = new ExampleObject(); // primitiveValue = 1, and arrValue[0] = 1
    
    ExampleObject copied = original; // Reference Copy
    copied.primitiveValue = 2;
    copied.arrValue[0] = 2;
    
    System.out.println(original.primitiveValue);
    System.out.println(original.arrValue[0]);
}
```

result:
``` 
2
2

```

> After reference copy, both reference variables **point to the same object in memory**, meaning **any changes done through one reference are reflected in the other**.
{: .prompt-tip }


``` 
public static void main(String[] args) throws CloneNotSupportedException {
    ExampleObject original = new ExampleObject(); // primitiveValue = 1, and arrValue[0] = 1

    ExampleObject copied = (ExampleObject) original.clone(); // Shallow Copy
    copied.primitiveValue = 2;
    copied.arrValue[0] = 2;

    System.out.println(original.primitiveValue);
    System.out.println(original.arrValue[0]);
}
```

result:
``` 
1
2

```

> A shallow copy of an object is **a new object** with copies of the values of the original object's fields. If the field value is a **primitive type**, a **direct copy of the value is made**. If the field is a reference to an **object**(arrays are objects in Java), it only **copies the reference**.
{: .prompt-tip }

More about Shallow Copy and Deep Copy: [What are reference copy, shallow copy and deep copy?](/posts/Basic-Knowledge-In-Java/#what-are-reference-copy-shallow-copy-and-deep-copy)

