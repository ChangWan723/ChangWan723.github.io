---
title: "Clean Code: Comments"
date: 2023-10-18 00:01:00 +0530
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/comments.png
---

> Comments are not like Schindler’s List. They are not “pure good.” Indeed, comments are, at best, a necessary evil. If our programming languages were expressive enough, or if we had the talent to subtly wield those languages to express our intent, we would not need comments very much --- perhaps not at all. 

> **“Don’t comment bad code, rewrite it.”**

Most of the time, we write comments because the code itself is **poorly readable**. So actively writing comments isn't commendable, it's rather a "failure".

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Comments Can "Lie"](#comments-can-lie)
  * [Comments Do Not Make Up for Bad Code](#comments-do-not-make-up-for-bad-code)
    * [Explain Yourself in Code](#explain-yourself-in-code)
  * [Good Comments](#good-comments)
    * [Legal Comments](#legal-comments)
    * [Informative Comments](#informative-comments)
    * [Explanation of Intent](#explanation-of-intent)
    * [Clarification](#clarification)
    * [Warning of Consequences](#warning-of-consequences)
    * [TODO Comments](#todo-comments)
    * [Amplification](#amplification)
    * [Javadocs in Public APIs](#javadocs-in-public-apis)
  * [Bad Comments](#bad-comments)
<!-- TOC -->

---

## Comments Can "Lie"

- Most programmers can't be bothered to maintain comments. This means that the **longer the comment exists**, the **further away from the meaning** of the code itself.
- The code keeps changing, but the comments don't automatically change with it. The **more comments** there are, the **less maintainable** the code becomes!
- **Inaccurate comments are much worse** than no comments at all. They **delude** and **mislead**. They may also set rules that no longer need to be followed.
- Only the code always **truly tells** you what it is doing.
- We do have to use comments sometimes, but we should try to **minimise their use**. Only use comments when you feel you have to!

>It is possible to make the point that programmers should be disciplined enough to keep the comments in a high state of repair, relevance, and accuracy. I agree, they should. But I would rather that energy go toward **making the code so clear and expressive that it does not need the comments** in the first place.

## Comments Do Not Make Up for Bad Code

The first and foremost rule is that clear and expressive code should always be prioritized over comments. **Comments should not be used to compensate for poorly written code**.

### Explain Yourself in Code

The best way to communicate intent is through the code itself, by using meaningful names, well-structured functions, and straightforward logic.

Bad Example. Using comments as a crutch:
```java
// Check if the user has enough balance to make a purchase
if (user.balance >= PRICE && user.accountStatus == ACTIVE) {
    // ...
}
```

Good Example. Self-commenting code:
```java
if (user.canAffordPurchase()) {
    // ...
}
```

## Good Comments

There are specific scenarios where comments are beneficial:

### Legal Comments

These are necessary for copyright or licensing information.

For example:
```java
// Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```

### Informative Comments

These provide additional, non-obvious information.

For example, we use comments to give the reader a **more intuitive view of the format** that the regular expression is validating
```java
// format matched: (kk:mm:ss EEE, MMM dd, yyyy)
Pattern timeMatcher = Pattern.compile("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```

### Explanation of Intent

These comments clarify the **developer's intention** behind a specific piece of code.

For example:
```java
public void testConcurrentAddWidgets() throws Exception {
  WidgetBuilder widgetBuilder = new WidgetBuilder(new Class[]{BoldWidget.class});
  String text = "'''bold text'''";
  ParentWidget parent = new BoldWidget(new MockWidgetRoot(), "'''bold text'''");
  AtomicBoolean failFlag = new AtomicBoolean();
  failFlag.set(false);
  
  //This is our best attempt to get a race condition by creating large number of threads.
  for (int i = 0; i < 25000; i++) {
    WidgetBuilderThread widgetBuilderThread = new WidgetBuilderThread(widgetBuilder, text, parent, failFlag);
    Thread thread = new Thread(widgetBuilderThread);
    thread.start();
  }
  assertEquals(false, failFlag.get());
}  
```

The comment in the code above is a better example. You may not agree with the solution, but **at least you can understand the programmer's intent**. 

But even for this better example, **we can still remove comments** by meaningful names and function extraction:

```java
public void attemptToTriggerRaceConditionByConcurrentWidgetAdditions() throws Exception {
    WidgetBuilder widgetBuilder = new WidgetBuilder(new Class[]{BoldWidget.class});
    ParentWidget parent = new BoldWidget(new MockWidgetRoot(), "bold text");
    AtomicBoolean failFlag = new AtomicBoolean(false);

    spawnMultipleThreadsToAddWidgets(widgetBuilder, parent, failFlag);

    assertEquals(false, failFlag.get());
}

private void spawnMultipleThreadsToAddWidgets(WidgetBuilder widgetBuilder, ParentWidget parent, AtomicBoolean failFlag) {
    for (int i = 0; i < 25000; i++) {
        WidgetBuilderThread widgetBuilderThread = new WidgetBuilderThread(widgetBuilder, "bold text", parent, failFlag);
        Thread thread = new Thread(widgetBuilderThread);
        thread.start();
    }
}
```
**Always try to minimise comments.**



### Clarification

These are useful for explaining complex algorithms, mathematics or obscure argument.

```java
public void testCompareTo() throws Exception
{
   WikiPagePath a = PathParser.parse("PageA");
   WikiPagePath ab = PathParser.parse("PageA.PageB");
   WikiPagePath b = PathParser.parse("PageB");
   WikiPagePath aa = PathParser.parse("PageA.PageA");
   WikiPagePath bb = PathParser.parse("PageB.PageB");
   WikiPagePath ba = PathParser.parse("PageB.PageA");
   
   assertTrue(a.compareTo(a) == 0); // a == a
   assertTrue(a.compareTo(b) != 0); // a != b
   assertTrue(ab.compareTo(ab) == 0); // ab == ab
   assertTrue(a.compareTo(b) == -1); // a < b
   assertTrue(aa.compareTo(ab) == -1); // aa < ab
   assertTrue(ba.compareTo(bb) == -1); // ba < bb
   assertTrue(b.compareTo(a) == 1); // b > a
   assertTrue(ab.compareTo(aa) == 1); // ab > aa
   assertTrue(bb.compareTo(ba) == 1); // bb > ba
}
```

### Warning of Consequences

These serve as warnings to other developers about potential consequences of altering certain parts of the code.

For example:
```java
// Don't run unless you have some time to kill.
public void testWithReallyBigFile()
{
   writeLinesToFile(10000000);
   
   response.setBody(testFile);
   response.readyToSend(this);
   String responseString = output.toString();
   assertSubString("Content-Length: 1000000000", responseString);
   assertTrue(bytesSent > 1000000000);
}
```

```java 
public static SimpleDateFormat makeStandardHttpDateFormat()
{
   //SimpleDateFormat is not thread safe, so we need to create each instance independently.
   SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss z");
   df.setTimeZone(TimeZone.getTimeZone("GMT"));
   return df;
}
```

### TODO Comments

`TODO` are jobs that the programmer thinks should be done, but for some reason can’t do at the moment.

For example:
```java 
//TODO-MdM these are not needed. We expect this to go away when we do the checkout model.
protected VersionInfo makeVersion() throws Exception
{
   return null;
}
```

Nowadays, most modern IDEs provide special gestures and features to locate all the `TODO` comments. **`TODO` comments can be used when appropriate, but remember to clean them up!**

### Amplification

A comment may be used to amplify the importance of something that may otherwise seem inconsequential.

For example:
```java 
String listItemContent = match.group(3).trim();
// the trim is real important. It removes the starting spaces that 
// could cause the item to be recognized as another list.
new ListItemWidget(this, listItemContent, this.level + 1);
return buildList(text.substring(match.end()));
```

### Javadocs in Public APIs

JavaDocs are an essential part of Java development, as they provide a structured way to document Java classes, methods, and fields in Public APIs.

If you are writing a public API, then you should certainly write good Javadocs for it. But keep in mind, Javadocs also can be just as misleading, nonlocal, and dishonest as any other kind of comment.

Examples of Javadocs:

```java 
/**
 * Represents a simple arithmetic calculator.
 * 
 * This calculator can perform basic arithmetic operations such as addition, subtraction,
 * multiplication, and division. Always ensure to check for potential arithmetic exceptions
 * when using the division operation.
 *
 * @author John Doe
 * @version 1.0
 * @since 2023-10-22
 */
public class Calculator {

    /**
     * Adds two numbers.
     *
     * @param a The first addend.
     * @param b The second addend.
     * @return The sum of a and b.
     */
    public double add(double a, double b) {
        return a + b;
    }
     
    // ...
}
```


## Bad Comments

Apart from the good comments mentioned above, the rest of the comments are almost all bad comments. And they should all be avoided:

1. **Mumbling**: Avoid unclear or non-informative comments.

2. **Redundant Comments**: Avoid comments that merely restate the obvious information. And avoid JavaDoc with no documentation value.

3. **Misleading Comments**: Avoid comments that are imprecise or potentially ambiguous.

4. **Mandated Comments**: Avoid comments that are required by process rather than providing value to the code. For example, specifying that every function must have a javadoc, or every variable must have a comment. Comments like this just clutter up the code, propagate lies, and lend to general confusion and disorganization.

5. **Journal Comments**: Avoid using comments as a journal of changes. It made sense to use Journal Comments before there was a source code control system. But now that `git` is so popular, there's no reason to use them anymore.

6. **Commented-Out Code**: Avoid leaving commented-out code. Use version control (`git`) instead. Others who see that commented-out code won’t have the courage to delete it. They’ll think it is there for a reason and is too important to delete. So commented-out code not only makes the code look messy, it's also confusing.

7. **HTML Comments**: Avoid using HTML in comments. It makes the comments hard to read. If comments are going to be extracted by some tool (like Javadoc) to appear in a Web page, then it should be the responsibility of that tool, and not the programmer.

8. **Too Much Information**: Avoid providing unnecessary or irrelevant details.

9. **In-obvious Connection**: Avoid comments that are not clearly connected to the code they are referencing.

10. **Position Markers**: Avoid using comments as position markers. Use other tools.


<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
