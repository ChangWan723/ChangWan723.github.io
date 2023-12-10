---
title: "Clean Code: Formatting"
date: 2023-10-25 23:27:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/formatting.jpg
---


Writing clean code is not just about functionality; it's also about readability and maintainability. One of the essential aspects that significantly impact readability is the formatting of the code.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Importance of Good Formatting](#importance-of-good-formatting)
  * [Principles of Formatting in Clean Code](#principles-of-formatting-in-clean-code)
    * [Vertical Formatting](#vertical-formatting)
    * [Horizontal Formatting](#horizontal-formatting)
    * [Team Rules](#team-rules)
<!-- TOC -->

---

## Importance of Good Formatting

Good formatting improves the readability of the code, making it easier to understand, maintain, and debug. Consistent formatting creates a visual structure that helps developers navigate the codebase efficiently.

## Principles of Formatting in Clean Code

### Vertical Formatting

- **Small code files**: Small code files are usually easier to understand than large files are. As for Java, it's better to keep a source code file to about 200 lines, not more than 500 lines. (It should not be a hard and fast rule, but should be considered highly desirable.)

- **The newspaper metaphor**: A good newspaper always puts the headline at the forefront and the details at the back. Good code should look like this. Code files' names should be simple but explanatory. And we should put public and high-level concepts at the top of the file. Detail should increase as we move downward. 

>If the newspaper were just one long story containing a disorganized agglomeration of facts, dates, and names, then we simply would not read it.

- **Vertical Openness Between Concepts**: Use blank lines to separate concepts (package declaration, the import, functions, etc.) and improve clarity.

- **Vertical Density**: Related lines of code should be grouped together without blank lines.

- **Vertical Distance**: Related codes should be closeed to each other. 
  1. **Variable Declaration**: Variables should be declared as close to their usage as possible.
  2. **Instance Variables**: It should be declared at the top of the class. Because in a well-designed class, they are used by many of the methods in the class.
  3. **Dependent Functions**: If one function calls another, they should be vertically close, and the caller should be above the callee.
  4. **Conceptual Affinity**: Certain bits of code want to be near other bits. They have a certain conceptual affinity. The stronger that affinity, the less vertical distance there should be between them.

### Horizontal Formatting

- **Short code lines**: Generally, the shorter the lines of code, the more readable it is. The number of characters in a line of code should be under 80, preferably not more than 120.

- **Horizontal Openness and Density**: Use spaces to separate operators and operands, and group related expressions.

- **Horizontal Alignment**: **Don't** pursue every line of code variable names, parameter names, etc. on a horizontal alignment of it. This usually doesn't help and just adds to the workload.

- **Indentation**: Use consistent indentation to separate different nesting levels (the structure of loops, conditions, and blocks).

- **Dummy Scopes**: Try not use a dummy body of a `while` or `for` statement. If you have to use it, please make sure that the dummy body is properly indented and surrounded by braces. Otherwise, this can mislead the reader.

### Team Rules

Consistency is key to good formatting. It's essential to establish and follow team-wide formatting rules.

- **Code Formatting Tools**: Utilize tools and linters to enforce consistent formatting automatically.
- **Code Reviews**: Use code reviews as an opportunity to reinforce formatting standards.

<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
