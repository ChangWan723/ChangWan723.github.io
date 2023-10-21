---
title: Introduction to Project Management
date: 2023-10-01 17:55:00 +0530
categories: [ (CS) Learning Note, Software Project Management ]
tags: [ computer science, software engineering, project management ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What Is a Project?](#what-is-a-project)
    * [Project Attributes](#project-attributes)
    * [Project Constraints](#project-constraints)
    * [Project Vs. Operation](#project-vs-operation)
    * [Examples of Projects](#examples-of-projects)
  * [What is Project Management?](#what-is-project-management)
    * [Project Stakeholders](#project-stakeholders)
    * [Project Management Knowledge Areas](#project-management-knowledge-areas)
    * [Project Management Tools and Techniques](#project-management-tools-and-techniques)
  * [Advantages of Using Formal Project Management](#advantages-of-using-formal-project-management)
  * [Some Concepts in Project Management](#some-concepts-in-project-management)
    * [Project Selection](#project-selection)
      * [Quantitative Project Selection - An Example](#quantitative-project-selection---an-example)
    * [Project Charter](#project-charter)
    * [Project Success](#project-success)
  * [Related Blogs](#related-blogs)
<!-- TOC -->

---

## What Is a Project?

- A project is “a **temporary** endeavor undertaken to create a unique **product**, **service**, or **result**”
- Projects end when their objectives have been reached, or the project has been terminated.
- On the other hand, _operations_ is work done to sustain the business.

### Project Attributes

A project:

- Has a unique purpose
- Is temporary
- Drives change and enables value creation
- Is developed using progressive elaboration or in an iterative fashion
- Requires resources, often from various areas
- Should have a primary customer or sponsor
  - The project sponsor usually provides the direction and funding for the project
- Involves uncertainty

**Project managers** work with the project **sponsors**, the project **team**, and the other people involved in a
project to **define**, **communicate**, and meet **project goals**.

### Project Constraints

- Every project is constrained in different ways.
- Some project managers focus on the **triple constraint** (meeting **scope**, **time**, and **cost** goals)
  - **Scope**: What work will be done as part of the project? What unique **product**, **service**, or **result** does
    the **customer** or **sponsor** expect from the project?
  - **Time**: How **long** should it take to complete the project? What is the **timeline**?
  - **Cost**: What should it **cost** to complete the project? What is the project’s **budget**? What **resources** are
    needed?
- Other constraints include **quality**, **risk**, and **resources**

### Project Vs. Operation

| Project                              | Operation (Business as Usual)                                         |
|--------------------------------------|-----------------------------------------------------------------------|
| New payroll system                   | Payroll processing each month                                         |
| New buildings or extensions          | Building maintenance                                                  |
| Designing a new car                  | The car production line                                               |
| Developing a new version of software | Supporting the new software version. e.g., answering support tickets. |

### Examples of Projects

- Construction of a bridge
- Development of software for a new business process.
- Installation of machinery in a factory
- Relief efforts after a natural disaster
- Developing a cloud-based marketing platform for start-ups

## What is Project Management?

> **Project management** is “the application of **knowledge**, **skills**, **tools** and **techniques** to project
> activities to meet project requirements.”
>
> From: Project Management Institute, Inc., The Standard for Project Management, Seventh Edition (2021), p. 4.

### Project Stakeholders

- **Stakeholders** are the people **involved** in or **affected** by project activities
- Stakeholders include:
  - The project sponsor
  - The project manager
  - The project team
  - Support staff
  - Customers
  - Suppliers
  - Opponents to the project

### Project Management Knowledge Areas

- Project **integration management** is an overarching function that coordinates the work of all other knowledge areas.
  - It affects and is affected by all the other knowledge areas.
- Project **scope management** involves working with all appropriate stakeholders to define, gain written agreement for,
  and manage all the work required to complete the project successfully.
- Project **time management** includes estimating how long it will take to complete the work, developing an acceptable
  project schedule given cost-effective use of available resources, and ensuring timely completion of the project.
- Project **cost management** consists of preparing and managing the budget for the project.
- Project **quality management** ensures that the project will satisfy the stated or implied needs for which it was
  undertaken.
- Project **resource management** is concerned with making effective use of the people and physical resources needed for
  the project.
- Project **communications management** involves generating, collecting, disseminating, and storing project information.
- Project **risk management** includes identifying, analysing, and responding to risks related to the project.
- Project **procurement management** involves acquiring or procuring goods and services for a project from outside the
  performing organization.
- Project **stakeholder management** focuses on identifying project stakeholders, understanding their needs and
  expectations, and engaging them appropriately throughout the project.

### Project Management Tools and Techniques

- Project management **tools** and **techniques** assist project managers and their teams in various aspects of project
  management.
- Note that a tool or technique is **more than** just a software package.
- Specific tools and techniques include:
  - **Project charters**, scope statements, and **WBS** (scope)
  - **Gantt charts**, **network diagrams**, **critical path analyses** (time)
  - **Net present value**, cost estimates, and **earned value** management (cost)
  - Agile projects often require product **roadmaps**, **backlogs**, **burndown charts**, **retrospectives**, etc.

## Advantages of Using Formal Project Management

- Better control of financial, physical, and human resources
- Improved customer relations
- Shorter development times
- Lower costs
- Higher quality and increased reliability
- Higher profit margins
- Improved productivity
- Better internal coordination
- Higher worker morale

## Some Concepts in Project Management

### Project Selection

- Projects are chosen using Project Selection Methods.
- Generally, more than one methods are applied. Usually, a mix of qualitative and quantitative.

- Some qualitative criteria:
  1. Brand Image
  2. Complementary Products/services
  3. Extension of existing portfolio of products/services
  4. Competitive Landscape

- To use the quantitative methods, we need to estimate the **cash flows** that the product will **need** and **generate
  ** over a period of time.
- Based on this data we need to calculate the discounted cash flow DCF of those future cash flows in today’s terms and
  see if the returns are greater than the cost of capital.
- For example, if the project will need money to be borrowed from banks at 10%, then the cash flows should generate a
  return that is greater than 10%.
  - Otherwise, the project is going to lose money for the company.

#### Quantitative Project Selection - An Example

---
Let’s assume that the company has estimated the cash flows for this project as given below:

| Year0        | Year1      | Year2      | Year3      |
|--------------|------------|------------|------------|
| -$10 million | $2 million | $4 million | $6 million |

The raw total **cash inflow** is $2 million (-$10 + $2 + $4 + $6)

But we need to discount them to bring them to their current value using a discounting rate which is equal to the cost of
capital.

DCF(Discounted Cash Flow) = Cash flow / (1 + `r`)^`n` (`r` is the cost of capital and `n` is the number of years,
Assuming `r` is 0.1)

| Year0        | Year1          | Year2          | Year3          |
|--------------|----------------|----------------|----------------|
| -$10 million | $1.818 million | $3.306 million | $4.508 million |

If we add the above cash flows the net cash flow of -$0.368 million

The final net cash flow of -$0.368 is called the NPV (Net Present value) of the project.

---

- The NPV (Net Present value) of the project is one of the most important parameters
  looked at when making project selection.
  - The higher the NPV, the better it is from a quantitative point of view.
  - An NPV of at least 0 is required to provide the returns expected by the company.
- A measure similar to NPV is called IRR (Internal Rate of Return) which gives the returns of the project in percentage
  terms.
- A project will make money if the IRR is above the cost of capital.
- For example, if there are two projects: one with an IRR of 15% and the other with an IRR of 20%; and the cost of
  capital is 10% both projects will make money.
  - In such a case if the company wants to select only one project, it should select the second one as it brings in
    greater returns.

### Project Charter

- Once the company selects the projects to be undertaken, it gives authorization for
  those projects.
- A **Project Charter** is providing that authorization for a selected project.
- The project charter is a one-to-two-page document that is issued by the sponsor of the project. It includes:
  - Project Name & Description
  - Business need of the project
  - Justification for starting the project
  - High Level requirements
  - Deliverables & Constraints
  - Assumptions
  - High-level Risks
  - Project Manager & Stakeholders

---
A Sample Project Charter:

| **Field**                   | **Description**                                                                                                                                                                                                                                                                                                                                                                                              |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Project Name**            | R&D Cost Optimization                                                                                                                                                                                                                                                                                                                                                                                        |
| **Project Description**     | This project will identify the areas where costs can be optimized to bring about an overall cost reduction in the R&D department without affecting its operations.                                                                                                                                                                                                                                           |
| **Business Need**           | Due to a market slowdown, it is imperative that we reduce our costs.                                                                                                                                                                                                                                                                                                                                         |
| **Project Justification**   | Our company spends about 25% of its costs on the R&D department. A cost reduction in this department can help us increase our net income by a percentage that is higher than the increase in our revenue after removing the project costs. As per estimates, this project would bring us a cost reduction of about 5% and this would increase our net income by 10% with a 5% increase in revenue this year. |
| **High-level Requirements** | Identify areas of cost reduction in the R&D department. Suggest ways of implementing cost reduction in the R&D department                                                                                                                                                                                                                                                                                    |
| **Deliverables**            | Report on areas of cost reduction & ways of implementing them in the R&D department. High-level implementation schedule                                                                                                                                                                                                                                                                                      |
| **Constraints**             | The project should be completed within 2 months. The total project cost should not exceed $20,000                                                                                                                                                                                                                                                                                                            |
| **Assumptions**             | All required data will be available from the R&D department. The cost reduction will not reduce employee productivity                                                                                                                                                                                                                                                                                        |
| **High-level Risks**        | Unavailability of relevant data. Unwillingness to part with relevant data                                                                                                                                                                                                                                                                                                                                    |
| **Project Manager**         | Lan Pham                                                                                                                                                                                                                                                                                                                                                                                                     |
| **Stakeholders**            | R&D Functional Manager, Marketing Director                                                                                                                                                                                                                                                                                                                                                                   |

---

### Project Success

- There are different ways to define project success:
  - The project provided **value**. Value is “the **worth**, **importance**, or **usefulness** of something.”*
  - The project met **scope**, **time**, and **cost** goals.
  - The project **satisfied** the **customer**/sponsor.
    - One method used to measure customer satisfaction is a **net promoter score**, a number that represents the
      customer’s willingness to recommend a product or service to others.
- The project **produced** the **desired results**.


## Related Blogs

- [Introduction To Agile Project Management](/posts/Introduction-To-Agile-Project-Management/)
- [Project Management Process Groups](/posts/The-Project-Management-Process-Groups/)
