---
title: "Clean Code: Meaningful Names"
date: 2023-10-13 17:26:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: true
image:
  path: /assets/img/posts/name.png
---

> Names are everywhere in software. We name our variables, our functions, our arguments, classes, and packages. We name our source files and the directories that contain them. We name our jar files and war files and ear files. We name and name and name. Because we do so much of it, we’d better do it well.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Why Are Meaningful Names Important?](#why-are-meaningful-names-important)
  * [The Power of Meaningful Names](#the-power-of-meaningful-names)
    * [code example, version 1](#code-example-version-1)
    * [code example, version 2](#code-example-version-2)
    * [code example, version 3](#code-example-version-3)
    * [code example, version 4](#code-example-version-4)
  * [Rules for Creating Good Names](#rules-for-creating-good-names)
    * [Be Intention-Revealing](#be-intention-revealing)
    * [Avoid Disinformation](#avoid-disinformation)
    * [Make Meaningful Distinctions](#make-meaningful-distinctions)
    * [Use Pronounceable Names](#use-pronounceable-names)
    * [Use Searchable Names](#use-searchable-names)
    * [Avoid Encodings](#avoid-encodings)
      * [Hungarian Notation](#hungarian-notation)
      * [Member Prefixes](#member-prefixes)
      * [Interfaces and Implementations](#interfaces-and-implementations)
    * [Avoid Mental Mapping](#avoid-mental-mapping)
    * [Class Names Should Be Nouns](#class-names-should-be-nouns)
    * [Method Names Should Be Verbs](#method-names-should-be-verbs)
    * [Opt for Simplicity over Cleverness](#opt-for-simplicity-over-cleverness)
    * [Consistent Lexicon](#consistent-lexicon)
<!-- TOC -->

---

## Why Are Meaningful Names Important?

> **There are only two hard things in Computer Science: cache invalidation and naming things.**
>
> —— Phil Karlton
{: .prompt-tip }

The significance of Meaningful Names:

1. **Clarity**: Names provide a quick insight into the purpose and functionality of a piece of code.
2. **Reduced Need for Comments**: Well-named entities often make comments redundant, as the name itself is self-documenting.
3. **Ease of Maintenance**: Future developers (or even you, months down the line) can understand and modify the code with less effort.
4. **Professionalism**: Taking the time to name things well reflects a commitment to craftsmanship and quality.

## The Power of Meaningful Names

Naming might seem like a small aspect of coding, but **it carries immense weight in the realm of Clean Code**. By adhering to these simple rules, you not only make your code more readable but also elevate the overall quality of your software.

---

**For example**, let's take a look at the following code:

### code example, version 1
```java
public List<int[]> fetch() {
    List<int[]> lst = new ArrayList<int[]>();
    for (int[] y : arraySet) {
        if (y[2] == 1)
            lst.add(y);
    }
    return lst;
}
```

There are no complex expressions. Spacing and indentation are reasonable. **This code is already very simple, but you still can't read it quickly to understand what it's doing, much less what business it's handling. Why?** The problem isn’t the simplicity of the code but the **implicity** of the code (implicity: the degree to which the context is not explicit in the code itself).

What this code is doing? What is the significance of `arraySet`, the value `1`, `y`, etc.? The answers to these questions are not present in the code sample, **but they could have been.**

Suppose we later discover that this code is part of a weather application, where arraySet represents a list of daily weather data, and the third element of each array indicates if it rained that day (1 for rain, 0 for no rain). **With this context, we can make the code more understandable**:

### code example, version 2
```java
public List<int[]> getRainyDays() {
    List<int[]> rainyDays = new ArrayList<int[]>();
    for (int[] dailyWeather : weatherData) {
        if (dailyWeather[RAIN_INDEX] == IS_RAINY)
            rainyDays.add(dailyWeather);
    }
    return rainyDays;
}
```

>In this revised version:
> - The method's name is changed to `getRainyDays`, which clearly **communicates its purpose**.
> - arraySet is renamed to `weatherData` for **clarity**.
> - The magic number 1 is replaced with a named constant `IS_RAINY`.
> - The magic index 2 is replaced with a named constant `RAIN_INDEX`.
{: .prompt-tip }

Notice that the **simplicity of the code has not changed**. It still has exactly the same number of operators and constants, with exactly the same number of nesting levels. But **the code has become much more explicit.**

We can go further and write a simple class for dailyWeather instead of using an array of `int[]`. It can include an intention-revealing function (call it `isRainy`) to hide the magic numbers. It results in a new version of the function:

### code example, version 3
```java
public List<DailyWeather> getRainyDays() {
    List<DailyWeather> rainyDays = new ArrayList<int[]>();
    for (DailyWeather dailyWeather : weatherData) {
        if (dailyWeather.isRainy())
            rainyDays.add(dailyWeather);
    }
    return rainyDays;
}
```

With these simple name changes, it’s not difficult to understand what’s going on. **This is the power of choosing good names**.

Is this the best code yet? Of course not! In fact, with Java code, we can **make this code even better!** (The following optimisation is not "Meaningful Name" related)

We can use Java 8's Stream API for a **more concise and readable approach**:

### code example, version 4
```java
public List<DailyWeather> getRainyDays() {
    return weatherData.stream()
                      .filter(DailyWeather::isRainy)
                      .collect(Collectors.toList());
}
```

It's the same function, look at how much difference there is between [version 1](#code-example-version-1) and [version 4](#code-example-version-4). **This is the beauty and art of Clean Code!** When you read good Clean Code, you will heartily exclaim, "**Yes, that's what good code looks like!**"

The code in [version 4](#code-example-version-4) is already quite clean and efficient. However, the definition of "better" may vary depending on our goals (e.g., performance, readability, extensibility, etc.). This code may also need to be optimised for specific projects. **Remember: code is never perfect!**

---

## Rules for Creating Good Names

> In general, a good name should **clearly** and **precisely** express its intention and **not contain redundant** information.
{: .prompt-tip }

### Be Intention-Revealing

- A name should tell you **why it exists, what it does, and how it's used**. Instead of generic names like `temp` or `data`, use names that reflect the purpose.
- Take care with your names and **change them** when you **find better ones**.
- Choosing names that **reveal intent** can make it much easier to understand and change code.
- If a name **requires a comment**, then the name **does not reveal its intent**.

```java
// Instead of this:
int d; // elapsed time in days

// Use this:
int elapsedTimeInDays;
```


### Avoid Disinformation

- We should avoid words whose entrenched meanings vary from our intended meaning. For example, `hp`, `aix`, and `sco` would be poor variable names because they are the names of Unix platforms or variants.
- Do not refer to a grouping of accounts as an `accountList` unless it’s actually a `List`. Otherwise, it may lead to false conclusions. The word list means something specific to programmers. (Same as: `Map`, `Array`, etc.)
- Beware of using names which vary in small ways. How long does it take to spot the subtle difference between a `XYZControllerForEfficientHandlingOfStrings` in one module and, somewhere a little more distant, `XYZControllerForEfficientStorageOfStrings`? The words have frightfully similar shapes.
- Don't use names that might mislead the reader. For instance, avoid using the letter `O` and `l` as a variable name since it can be confused with the number `0` and `1`.

Just look at how maddening the following code is:

```java
int a = l;
if ( O == l )
  a = O1;
else
  l = 01;
```

### Make Meaningful Distinctions

- **Avoid Number-series naming** (a1, a2, .. aN). It is the opposite of intentional naming. Such names are not disinformative — they are noninformative; they provide no clue to the author’s intention.

- **Avoid noise words** that don't provide additional information. Names like `ProductData` and `ProductInfo` are indistinct and don't provide clarity on their differences. `Info` and `Data` are indistinct noise words like `a`, `an`, and `the`. How is `NameString` better than `Name`? Would a `Name` ever be a floating point number? **Noise words are redundant.**

### Use Pronounceable Names

- If you can't pronounce it, you'll likely find discussing it difficult.

>A company I know has `genymdhms` (generation date, year, month, day, hour, minute, and second) so they walked around saying “gen why emm dee aich emm ess”. I have an annoying habit of pronouncing everything as written, so I started saying “gen-yah-muddahims.” It later was being called this by a host of designers and analysts, and we still sounded silly. But we were in on the joke, so it was fun. Fun or not, we were tolerating poor naming.

### Use Searchable Names

- Single-letter names or numeric constants can be hard to locate across a codebase. Descriptive names can be quickly found. One might easily grep for `MAX_CLASSES_PER_STUDENT`, but the number 7 could be more troublesome.
- Single-letter names can ONLY be used as local variables inside short methods. **The length of a name should correspond to the size of its scope.**

### Avoid Encodings

**Encoding type or scope** information into names simply adds an **extra burden of deciphering**. It is an unnecessary mental burden when trying to solve a problem. Encoded names are seldom pronounceable and are easy to mis-type.

#### Hungarian Notation

Nowadays, as compilers evolve, HN and other forms of **type encoding become outdated**. They make it harder to change the name or type of variable, function, or class. **They make it harder to read the code**. And they create the possibility that the encoding system will mislead the reader.
 
```java
PhoneNumber phoneString; // name not changed when type changed!
```

>In days of old, when we worked in name-length-challenged languages, we violated this rule out of necessity, and with regret. Fortran forced encodings by making the first letter a code for the type. Early versions of BASIC allowed only a letter plus one digit. Hungarian Notation (HN) took this to a whole new level.
> 
> HN was considered to be pretty important back in the Windows C API, when everything was an integer handle or a long pointer or a void pointer, or one of several implementations of “string” (with different uses and attributes). The compiler did not check types in those days, so the programmers needed a crutch to help them remember the types.
> 
> In modern languages we have much richer type systems, and the **compilers remember and enforce the types**. What’s more, **there is a trend toward smaller classes and shorter functions** so that people can usually see the point of declaration of each variable they’re using.

#### Member Prefixes

Don’t prefix member variables with m_ anymore. Classes and functions should be small enough. Use an editing environment that highlights or colorizes members to make them distinct.

> Besides, people quickly learn to ignore the prefix (or suffix) to see the meaningful part of the name. The more we read the code, the less we see the prefixes. Eventually the **prefixes become unseen clutter and a marker of older code**.

#### Interfaces and Implementations

When naming an interface and its implementation, avoid prefixes like 'I'. Prefer simple names for interfaces (e.g., ShapeFactory) and differentiate the concrete implementations if needed (e.g., ShapeFactoryImp).

> These are sometimes a special case for encodings. For example, say you are building an ABSTRACT FACTORY for the creation of shapes. This factory will be an interface and will be implemented by a concrete class. What should you name them? `IShapeFactory` and `ShapeFactory`? I prefer to **leave interfaces unadorned**. The preceding `I`, so common in today’s legacy wads, is a distraction at best and **too much information at worst**. I don’t want my users knowing that I’m handing them an interface. I just want them to know that it’s a `ShapeFactory`. So if I must encode either the interface or the implementation, I choose the implementation. Calling it `ShapeFactoryImp`, or even the hideous `CShapeFactory`, is preferable to encoding the interface.

### Avoid Mental Mapping

Readers shouldn't have to mentally translate your names into other names they already know. For example, using **unclear variable** names may result in the reader needing to **spend extra time and effort** to surmise or remember what it represents. This naming method can make the code more difficult to read. **Be explicit.**

>This is a problem with single-letter variable names. Certainly a loop counter may be named i or j or k (though never l!) if its scope is very small and no other names can conflict with it. This is because those single-letter names for loop counters are traditional. However, in most other contexts a single-letter name is a poor choice; it’s just a place holder that the reader must mentally map to the actual concept.


### Class Names Should Be Nouns

Classes represent objects or concepts, so names like `Customer`, `Account`, or `AddressParser` are appropriate.

### Method Names Should Be Verbs

Methods perform actions, so names like `save`, `delete`, or `calculateTotal` are fitting.

### Opt for Simplicity over Cleverness

It's better to be straightforward than to be witty. Remember, your code is for humans first.

>Will they know what the function named `HolyHandGrenade` is supposed to do? Sure, it’s cute, but maybe in this case `DeleteItems` might be a better name. Choose clarity over entertainment value.

>Say what you mean. Mean what you say.

### Consistent Lexicon

Don't use different words to mean the same thing, it can cause distress. Stick to the same naming style.

> It’s confusing to have a `controller` and a `manager` and a `driver` in the same code base. What is the essential difference between a `DeviceManager` and a `ProtocolController`? Why are both not `controllers` or both not `managers`? Are they both Drivers really? The name leads you to expect two objects that have very different type as well as having different classes. 
> 
> **A consistent lexicon is a great boon to the programmers who must use your code.**


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
