---
title: Software Testing
date: 2024-01-20 17:07:00 UTC
categories: [(CS) Learning Note, Automated Software Verification]
tags: [software engineering, software verification]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Main Types of Testing](#main-types-of-testing)
    * [Black-Box Testing](#black-box-testing)
      * [Advantages](#advantages)
      * [Disadvantages](#disadvantages)
    * [White-Box Testing](#white-box-testing)
      * [Advantages](#advantages-1)
      * [Disadvantages](#disadvantages-1)
    * [Grey-box Testing](#grey-box-testing)
      * [Advantages](#advantages-2)
      * [Disadvantages](#disadvantages-2)
  * [Coverage Criteria for White-box Testing](#coverage-criteria-for-white-box-testing)
    * [Statement Coverage](#statement-coverage)
    * [Branch Coverage](#branch-coverage)
    * [Condition Coverage](#condition-coverage)
    * [Branch + Condition Coverage](#branch--condition-coverage)
    * [Modified Condition/Decision Coverage (MC/DC)](#modified-conditiondecision-coverage-mcdc)
  * [Regression Testing](#regression-testing)
  * [Fuzz Testing](#fuzz-testing)
    * [Mutation-Based Fuzzing](#mutation-based-fuzzing)
    * [Generation-Based Fuzzing](#generation-based-fuzzing)
    * [Grey-Box Fuzzing](#grey-box-fuzzing)
<!-- TOC -->

---

## Main Types of Testing

- **black-box testing**: does the system behave according to its specification?
- **white-box testing**: are all aspects of the code covered by the tests?
- **grey-box testing**: uses a combination of both specification and knowledge of the internal workings of the software.

### Black-Box Testing

- In black-box testing, we can treat our system as a “black box”, without looking at its internal structure.
- In a black-box test one:
  - **passes an input** to the system,
  - **records the output** produced by the system,
  - **compares it to the expected output** of the system.
- Test cases are derived from the _specification_.
  - A specification may be formal or informal.
  - If there is **no specification**, then any behaviour is deemed correct.

- Experience has shown that programmers often make mistakes on **edge cases** of specification.
  - This motivates so-called **boundary value analysis** to derive test case data for black-box testing.
  - The idea is to consider the boundaries of the equivalence classes.

#### Advantages

1. **No Need for Internal Knowledge**: It does not require knowledge of the internal code structure. This allows testers to objectively test the software, focusing on inputs and outputs without any bias related to the internal code.
2. **User Perspective**: It simulates the end-user perspective, ensuring the software is examined for real-world use cases.
3. **Flexibility**: Testers do not need to be programmers, making it more accessible for various testers.
4. **Efficient for Large Code Bases**: Ideal for large, complex applications where understanding every aspect of the codebase is impractical.

#### Disadvantages

1. **Limited Coverage**: It might miss certain “hidden” functionalities, as it only tests what the software is supposed to do and not how it does it.
2. **Inefficient for Algorithm Testing**: Not suitable for algorithm testing as it cannot check the internal workings of the software.
3. **Potential Redundancy**: Without insight into the code, tests may be redundant or insufficient in covering certain aspects.
4. **Dependent on Requirements**: Heavily reliant on the documentation and requirements. If these are not clear, testing may not be effective.

### White-Box Testing

- In white-box testing, we have complete knowledge of the code.
  - But we are more concerned with **code coverage**, i.e. the derivation of test data sets is **based on the analysis of source code**.


#### Advantages

1. **Thorough Testing**: Allows for a thorough testing of the application as it covers all possible paths, including branches, loops, and conditions within the code.
2. **Optimization**: Helps in optimizing the code by identifying redundant paths and unreachable code.
3. **Early Bug Detection**: Can detect issues early in the development phase.
4. **Better Integration**: Facilitates more integrated testing when combined with black-box testing, leading to a more comprehensive test coverage.

#### Disadvantages

1. **Requires Strong Knowledge**: Testers need to have a strong understanding of the internal workings of the application, which can be complex and time-consuming.
2. **Time-Consuming and Costly**: Creating and maintaining white-box tests can be more time-consuming and expensive than black-box tests.
3. **Not Suitable for User Interface Testing**: Does not focus on usability or the user interface; it is more about internal functionality.
4. Potential Bias: Testers’ knowledge of the code can introduce bias, potentially overlooking errors or user experience issues.

### Grey-box Testing

- Grey-box testing combines aspects of both black-box and white-box testing.

#### Advantages

1. **Balanced Approach**: Provides a good balance between internal workings (as in white-box testing) and external functionality (as in black-box testing).
2. **Efficient Test Design**: Allows testers to design test scenarios more effectively by using both high-level (black-box) and detailed (white-box) perspectives.
3. **Increased Test Coverage**: Can uncover different types of issues – both from the user's perspective and from the system internals.
4. **Improved Communication**: Facilitates better communication between developers and testers, as it requires understanding both functional specifications and code structure.

#### Disadvantages

1. **Limited Depth in Both Perspectives**: Might not be as thorough as pure white-box testing in uncovering deep technical issues or as effective as pure black-box testing in evaluating user experience and usability.
2. **Potential for Overlooking Errors**: There's a risk of overlooking certain types of errors that might be caught by a more focused black-box or white-box approach.
3. **Complexity in Test Design**: Designing grey-box tests can be more complex, as it requires an understanding of both the external behavior and some aspects of the internal structure of the application.

## Coverage Criteria for White-box Testing

- There are a number of coverage criteria for white-box testing:
  - Statement coverage
  - Branch coverage
  - Condition coverage
  - Branch + Condition coverage
  - Modified Condition/ Decision Coverage

### Statement Coverage

- **Definition**: Measures whether each statement in the program's source code has been executed.
  - The most widely used coverage criterion.


### Branch Coverage

- **Definition**: Ensures that each branch of every control structure (like if-else statements) is executed.
  - Full branch coverage does not guarantee that a failure will be found.
  - branch coverage **subsumes** statement coverage.


### Condition Coverage

- **Definition**: Checks whether each boolean sub-expression evaluated both to true and false.
  - Condition coverage does **not subsume** branch coverage.

### Branch + Condition Coverage

- **Definition**: Branch + Condition Coverage combines both branch coverage and condition coverage. It ensures that every branch (as in branch coverage) and each condition within a decision (as in condition coverage) are evaluated both to true and false.
  - This combination obviously **subsumes** Branch Coverage and Condition Coverage.


### Modified Condition/Decision Coverage (MC/DC)

- **Definition**: MC/DC is a criterion used in high-integrity systems (like avionics software). It requires that each condition in a decision affects that decision’s outcome independently. MC/DC ensures that test cases explore scenarios where each condition can independently affect the overall decision's outcome.
  - **Main idea**: conditions should independently affect the decision outcome.
  - MC/DC **subsumes** Branch and Condition Coverage

## Regression Testing

- When software is modified, new test cases are typically added to test new code.
- However, there is a danger that the new changes have introduced a fault, perhaps broken previously tested code.
  - Such changes are called regressions.
- **Regression testing** is applied when code is modified; essentially it involves running old tests on the new code.
  - This can be very expensive.
- The main idea is to select only a subset of tests that are relevant to the modifications and only run those.
- Some possible criteria for regression test selection:
  - **Code-based**: only run test cases that execute the modified code.
  - **Control flow-based**: only run test cases that execute modified control flow nodes.

## Fuzz Testing

- Fuzzing is an example of negative testing.
- Fuzz supplied **random inputs** to command line tools, looking for exploitable security bugs.

---

- In fuzz testing, the first step is **input generation**. 
- One way to create inputs is to generate them randomly.
- In practice, this doesn’t work very well because obviously the program rejects invalid inputs easily
- The main idea behind fuzzing is to observe a program’s behaviour on inputs that are almost valid.
- There are two common approaches:
  - Mutation-based fuzzing
  - Generation-based fuzzing

### Mutation-Based Fuzzing

- In mutation-based fuzzing, one starts with a well-formed seed input, and mutates it to generate new inputs.
- A seed input can be supplied manually, but if a test suite for the program is available, the test inputs can be used as seeds.
  - It Does not require any knowledge of the input format.
  - However, the mutated inputs tend to be rejected early because they vary too much from what is expected by the program.
  - Typically, it gives low-code coverage.

### Generation-Based Fuzzing

- A generation-based fuzzer needs to know the grammar of the input format in order to generate inputs.
  - Typically, it gives much better code coverage because inputs are much more plausible.
  - However, requires knowledge of the input format.
- Generation-based fuzzing gives better code coverage but requires more effort.

### Grey-Box Fuzzing

- An interesting more recent approach to fuzzing seeks to
  - use conventional mutation-based fuzzing (requiring a seed input)
  - use “lightweight” coverage information
  - obtain coverage information by instrumenting the program to monitor the control flow,
  - save those generated inputs that resulted in new coverage and use them for future re-fuzzing.
- Perhaps surprisingly, this approach has been highly successful at finding security vulnerabilities in practice.
