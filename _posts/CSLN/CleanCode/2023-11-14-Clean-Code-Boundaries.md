---
title: "Clean Code: Boundaries"
date: 2023-11-14 12:12:00 +0530
categories: [(CS) Learning Note, Clean Code]
tags: [software engineering, Clean Code, code]
pin: false
image:
  path: /assets/img/posts/boundaries.jpg
---

>We seldom control all the software in our systems. Sometimes we buy third-party packages or use open source. Other times we depend on teams in our own company to produce components or subsystems for us. Somehow we must cleanly integrate this foreign code with our own.

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Using Third-Party Code](#using-third-party-code)
  * [Exploring and Learning Boundaries](#exploring-and-learning-boundaries)
  * [Learning Tests Are Better Than Free](#learning-tests-are-better-than-free)
<!-- TOC -->

---

## Using Third-Party Code

- **Challenges**: Third-party packages can offer powerful functionality, but they often come with excess baggage or unfamiliar paradigms.
- **Solution**: Create clear interfaces or wrappers around third-party code. This encapsulates the third-party package and minimizes its impact on your code. 
- **Best Practice**: Avoid spreading third-party package calls throughout your code. Instead, isolate them behind an interface or in a specific module. **This way, you don't expose unnecessary interfaces of third-party packages, and you don't need to make extensive changes when third-party packages change.**

```java
public class ThirdPartyAdapter {
    private ThirdPartyPaymentProcessor paymentProcessor;

    public void processPayment(PaymentDetails details) {
        paymentProcessor.initiatePayment(details);
    }
}
```

## Exploring and Learning Boundaries

- **Process**: When using new code or a third-party package, spend time exploring and understanding its boundaries.
- **Implementation**: Write tests, build small implementations, and run experiments to learn how the new code behaves.

## Learning Tests Are Better Than Free

- **Approach**: Write learning tests to understand how the third-party package works. These tests are simple experiments that help you learn the behavior of the third-party code.
- **Benefit**: They provide concrete **documentation on how to use** the third-party package and **alert you if a new version of the package has breaking changes**.

```java
@Test
public void testThirdPartyFunction() {
   ThirdPartyPackage thirdPartyPackage = new ThirdPartyPackage();
   assertEquals(expectedResult, thirdPartyPackage.someFunction());
}
```

<br>

---

**Reference:**

- Martin, R. C. (2009) _Clean code : a handbook of agile software craftsmanship._ Upper Saddle River, NJ: Prentice Hall (Robert C. Martin series).
