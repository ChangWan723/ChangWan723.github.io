---
title: State Machine Diagrams in UML
date: 2023-10-21 19:44:00 +0530
categories: [(CS) Learning Note, Software Modelling]
tags: [computer science, software engineering, UML, State Machine Diagrams]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is a State Machine Diagram?](#what-is-a-state-machine-diagram)
  * [Key Components of a State Machine Diagram](#key-components-of-a-state-machine-diagram)
  * [Notation Elements of a State Machine Diagram](#notation-elements-of-a-state-machine-diagram)
  * [Sequence of actions](#sequence-of-actions)
  * [How to Create a State Machine Diagram](#how-to-create-a-state-machine-diagram)
  * [Examples of State Machine Diagrams](#examples-of-state-machine-diagrams)
    * [Simple Digital Watch](#simple-digital-watch)
    * [Back ATM](#back-atm)
  * [Advantages of State Machine Diagrams](#advantages-of-state-machine-diagrams)
<!-- TOC -->

---


When it comes to understanding the behavior of a system or an object within a system, State Machine Diagrams in Unified Modeling Language (UML) are an indispensable tool. 

## What is a State Machine Diagram?

- A state diagram is a graph in which nodes correspond to states and directed arcs correspond to transitions labelled with event names.
- A state diagram combines states and events in the form of a network to model all possible object states during its life cycle, helping to visualise how an object responds to different stimuli.

## Key Components of a State Machine Diagram

1. **States**: These represent the different conditions or situations of an object. A state is depicted by a rounded rectangle. A state can be defined as the duration of time during which an object is doing an activity.

2. **Transitions**: These are arrows that connect states, representing the shift from one state to another.

3. **Events**: These are external triggers that cause the transition from one state to another. An event occurs at a time point and transmits information from one object to another.

4. **Activity**: An activity is an operation with certain duration that can be interrupted by another event. For example, a bulb in the “On” state is doing a continuous activity of “illumination” and this operation can be interrupted by another event like “switch off”.

5. **Actions**: These are operations or activities that result from a transition. An action occurs in response to an event and cannot be interrupted.
 
6. **Initial and Final States**: The initial state is where the object begins its lifecycle, represented by a filled circle. The final state, represented by a circle surrounding a smaller filled circle, shows where the lifecycle ends.

7. **Guard**: A guard is a logical condition placed before a transition that returns either a true or a false. A guarded transition occurs only if the return value is true.

## Notation Elements of a State Machine Diagram

![](https://i.postimg.cc/VLVT6gR4/smd1.png){: .w-100 .shadow .rounded-10 }


- Final state
  - A real state
  - Object can remain in that state forever
- Terminal state
  - Pseudo state
  - Object is destroyed
- Decision Node
  - Pseudo state
  - Used to model alternative transitions


## Sequence of actions

- Guard is tested **while in state** (**before exist** action)
- Transition action **after exit** action

**For example:**

---

![](https://i.postimg.cc/NjbBDM3L/smd2.png){: .w-50 .shadow .rounded-10 }

1. Enter state S1, `x=4`
2. Event `e` occurs and `x==4` then execute exit action `x=5`
3. Followed by the transition action `x*2=10`
4. S2 is entered and entry is `x++` then `x=11`

---


## How to Create a State Machine Diagram

1. **Identify the States**: Start by listing the different states that the object can be in during its lifecycle.

2. **Determine the Events and Transitions**: Identify the events that trigger transitions between states.

3. **Specify Actions**: Define any actions that result from transitions between states.

4. **Draw the Diagram**: Use the UML notation to draw the diagram, connecting states with transitions and labeling them with the respective events and actions.

## Examples of State Machine Diagrams

### Simple Digital Watch

A simple digital watch has a **display** and two **buttons** to set it, the **A button** and the **B button**. The watch has two **modes of operation**, **display time** and **set time**. In the display time mode, **hours and minutes** are displayed, separated by a flashing colon. The **set time mode** has two **sub-modes**, **set hours** and **set minutes**. The A button is used to select modes. Each time A is pressed, the mode advances in sequence: display, set hours, set minutes, display etc. Within the **sub-modes**, the B button is used to advance the hours or minutes once each time it is pressed. Buttons must be released before they can generate another event. Prepare a state diagram of the watch.

![](https://i.postimg.cc/ZqQq4nK0/smd4.png){: .w-75 .shadow .rounded-10 }
_State Machine Diagram of Digital Watch_

### Back ATM

- The ATM was initially turned **off**. After the power is turned on, ATM performs startup action and enters **Self Test** state.
- If the **test** fails, ATM goes into **Out of Service** state, otherwise there is **triggerless transition** to the **Idle** state. In this state ATM waits for customer interaction.
- The ATM state changes from **Idle** to **Serving Customer** when the customer **inserts** debit or credit card in the ATM's card reader.
- On entering the **Serving Customer** state, the entry action **readCard** is performed. Note, that transition from **Serving Customer** state back to the **Idle** state could be triggered by **cancel** event as the customer could cancel transaction at any time.
- **Serving Customer** state is a **composite state** with sequential substates **Customer Authentication**, **Selecting Transaction** and **Transaction**.
- **Customer Authentication** and **Transaction** are composite states by themselves which is shown with hidden decomposition **indicator icon**.
- **Serving Customer** state has **triggerless transition** back to the **Idle** state after transaction is finished.
- The state also has **exit** action **ejectCard** which releases customer's card on leaving the state, no matter what caused the transition out of the state.


![](https://i.postimg.cc/44z0T0WT/smd3.png){: .w-75 .shadow .rounded-10 }
_State Machine Diagram of Back ATM_

## Advantages of State Machine Diagrams

1. **Clarity**: They provide a clear and comprehensive visualization of the different states and transitions.

2. **Ease of Understanding**: They simplify the understanding of complex behaviors.

3. **Effective Communication**: They act as a valuable communication tool within development teams.

4. **Facilitates Testing**: They clearly outline the different states and transitions, making it easier to test the system.

- State diagrams are mostly used in reactive/event driven systems/components
- State diagrams are also useful in modeling concurrent or parallel behavior by allowing multiple states to exist simultaneously.
- This is helpful in modeling systems with multiple threads or concurrent processes.

