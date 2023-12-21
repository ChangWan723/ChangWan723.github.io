---
title: Principles in Refactoring
date: 2023-12-21 18:24:00 UTC
categories: [(CS) Learning Note, Refactoring]
tags: [software engineering, Refactoring, code]
pin: false
---


---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [The Two Hats](#the-two-hats)
  * [The Rule of Three](#the-rule-of-three)
    * [Understanding the Rule of Three](#understanding-the-rule-of-three)
      * [The Essence of the Rule](#the-essence-of-the-rule)
    * [Example the Rule of Three in Practice](#example-the-rule-of-three-in-practice)
  * [Other Principles of Refactoring](#other-principles-of-refactoring)
<!-- TOC -->

---


## The Two Hats

- The metaphor about the Two Hats comes from Kent Beck. The **Two Hats** mean **Adding Function** and **Refactoring** (you need to divide your time between these two different activities).
- The point is: **you can only wear one hat at a time.**
   - When adding functions, you're only adding new functions and shouldn't be thinking about refactoring.
   - When refactoring, you should only be restructuring the code only and should not be thinking about adding features.
     And don't add any UT (unless you find something missing or a necessary interface change)

---

- During your actual development, you may find yourself needing to **switch hats frequently**. 
   - You start trying to add a new function, and then realise that it would be much easier if the code was structured differently. So, you switch hats and start refactoring.
   - Once the code structure becomes better, you switch hats again and add the new function.
- All of this may happen often, or even happen in a brief period of time. But during that time, **you should always be aware of which hat you are wearing**.
   - If you're not sure which hat you're wearing, you may get confused and ride the fence.

## The Rule of Three

### Understanding the Rule of Three

The Rule of Three in refactoring is a concept that suggests **waiting until you have three instances of similar patterns or code** before you make the decision to refactor. **The principle is applied to keep code clean and avoid over-designing** (However, some obvious errors and defects should be refactored without a delay). 

#### The Essence of the Rule

1. **First Time**: You write the code for the first time, and it's new and unique.
2. **Second Time**: You encounter a similar pattern or requirement. You duplicate the code with slight modifications, recognizing the similarity.
3. **Third Time**: When the same pattern emerges again, it’s time to refactor. Now you have enough examples to understand the general pattern, making your refactoring more informed and effective.

### Example the Rule of Three in Practice

Consider a scenario where you're developing a web application, and you write a function to validate user input on a form. Later, you write a similar function for a different form. According to the Rule of Three, you would wait until you need a similar function for a third form before you refactor these functions into a single, more generic one.

> When I worked at Huawei, our team had a project for verifying use cases: 
>    - At first, there was only one use case to verify, and the functionality was simple, so no design was made. 
>    - Then the number of use cases increased to two, and my colleague simply added an `if-else` branch to handle it. This is still acceptable. 
>    - But then the number of use cases increased to twelve, colleagues still simply add `else` branch to handle. At this time, the code became really ugly.
> 
> Then, we couldn't tolerate such code any more. So, I used Strategy Pattern with Static Factory Pattern to refactor it.
>    - Actually, according to **The Rule of Three**, it should be refactored on the third time of adding use cases. It would have saved much trouble if that had been done.
{: .prompt-tip }


## Other Principles of Refactoring

- **Defining Clear Goals**
   - Refactoring should have specific objectives, like improving readability, reducing complexity, or preparing the code for new features.

- **Ensuring Behavior Preservation**
   - A cardinal rule in refactoring is to preserve the existing behaviour. The output before and after refactoring should remain the same.

- **Taking Small Steps**
   - Refactoring is best done in small, incremental steps rather than large, sweeping changes. This minimises the risk of introducing errors.


- **Enhancing Performance Indirectly**
   - While refactoring isn't primarily about improving performance, it often leads to more optimised code by clarifying the underlying structure.

- **Not a Substitute for Design**
   - Refactoring is not about fundamentally redesigning the system. It's about making improvements within the existing design framework. We also still need to do pre-design.


<br>

---

**Reference:**

- Fowler, M. and Beck, K. (1999) _Refactoring : improving the design of existing code._ Reading, MA: Addison-Wesley (The Addison-Wesley object technology series).
