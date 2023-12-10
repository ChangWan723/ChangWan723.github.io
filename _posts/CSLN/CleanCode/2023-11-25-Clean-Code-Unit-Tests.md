---
title: "Clean Code: Unit Tests"
date: 2023-11-25 00:26:00 UTC
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/unittests.jpg
---

Unit tests are a fundamental part of writing clean, maintainable, and robust code. They guide the design, provide documentation, and safeguard against future changes or refactoring. By adhering to the principles of TDD and maintaining clean tests, we ensure that our code not only works as intended but also remains adaptable and resilient in the face of change.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [The Three Laws of TDD](#the-three-laws-of-tdd)
  * [Keeping Tests Clean](#keeping-tests-clean)
    * [The Importance of Clean Tests](#the-importance-of-clean-tests)
    * [Characteristics of a Clean Test](#characteristics-of-a-clean-test)
  * [Building Testable Code](#building-testable-code)
  * [Test Coverage](#test-coverage)
    * [Ensuring Adequate Coverage](#ensuring-adequate-coverage)
    * [Pitfalls to Avoid](#pitfalls-to-avoid)
  * [F.I.R.S.T Principles of Testing](#first-principles-of-testing)
<!-- TOC -->

---

## The Three Laws of TDD

TDD is a software development process where the developer writes a test before writing just enough production code to fulfill that test. There are three important laws to follow:

1. **First Law**: You may not write production code until you have written a failing unit test.
2. **Second Law**: You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
3. **Third Law**: You may not write more production code than is sufficient to pass the currently failing test.

These laws ensure a minimal gap between the testing and coding phases, leading to more cohesive and reliable code development.

## Keeping Tests Clean

### The Importance of Clean Tests

Writing clean tests is as crucial as writing clean production code. Clean tests are expressive, readable, and maintainable. They provide clear documentation for the production code's expected behaviour.

> **If you don’t keep your tests clean, you will lose them.** And without them, you lose the very thing that keeps your production code flexible. Yes, you read that correctly. It is unit tests that keep our code flexible, maintainable, and reusable. The reason is simple. **If you have tests, you do not fear making changes to the code!** Without tests every change is a possible bug. No matter how flexible your architecture is, no matter how nicely partitioned your design, **without tests you will be reluctant to make changes** because of the fear that you will introduce undetected bugs.

**Unit tests play a crucial role in refactoring**. They provide a safety net that allows you to improve the structure of the code with the assurance that you haven’t broken anything.

### Characteristics of a Clean Test

1. **Readable**: Tests should be easy to read and understand.
2. **Reliable**: Tests should produce the same results every time they're run.
3. **Fast**: Tests should be quick to run, encouraging frequent use.
4. **Independent**: Tests should not depend on each other.
5. **Maintainable**: Tests should be easy to maintain alongside the production code.

> The `BUILD-OPERATE-CHECK` pattern is made obvious by the structure of these tests. Each of the tests is clearly split into three parts. The first part builds up the test data, the second part operates on that test data, and the third part checks that the operation yielded the expected results.

## Building Testable Code

A well-designed codebase inherently lends itself to effective testing. It often involves:

- **Modular Design**: Breaking down the code into independent modules or components.
- **Use of Interfaces**: Implementing interfaces to allow for easier testing and mock implementation.
- **Dependency Injection**: Injecting dependencies into a class rather than hard-coding them, which facilitates easier testing.

## Test Coverage

### Ensuring Adequate Coverage

Test coverage measures the amount of production code that's tested by the unit tests. While high-test coverage is desirable, it's also important to focus on the quality of the tests.

### Pitfalls to Avoid

- **Overemphasis on Coverage Metrics**: Striving for 100% coverage might not always be practical. Focus on critical paths and complex logic.
- **Neglecting Edge Cases**: Ensure that tests cover various scenarios, including edge cases and error conditions.

## F.I.R.S.T Principles of Testing

Adhering to the F.I.R.S.T principles helps in creating a robust and maintainable suite of unit tests, which in turn supports overall software quality and reliability.

- **Fast**: Tests should be fast. They should run quickly, allowing them to be run frequently without slowing down the development process. Fast tests give immediate feedback to developers, which is essential for effective troubleshooting and iterative development.

- **Independent**: Each test should be independent of others. Tests should not depend on each other, as dependencies can cause tests to fail in a cascade and make pinpointing the root cause of a failure more difficult. Independent tests ensure that a failure in one test does not impact the execution or result of another.

- **Repeatable**: Tests should be repeatable in any environment. The results of the tests should be the same whether they are run in a local development environment, a continuous integration server, or a production environment. This consistency helps ensure that issues identified are due to the code and not environmental factors.

- **Self-Validating**: A test should have a boolean output: pass or fail. There should be no need for manual interpretation of log files or results to determine whether the test passed.

- **Timely**: Tests should be written in a timely manner, typically before the production code is written (as in Test-Driven Development - TDD). Writing tests first helps ensure that the code is testable and meets the requirements, and it can lead to better designed, more maintainable code.

<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
