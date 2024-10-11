---
title: Best Practice of Microservices Architecture
date: 2024-10-11 12:07:00 UTC
categories: [ (CS) Learning Note, Architecture ]
tags: [ software engineering , architecture, microservices ]
pin: false
---

Currently, microservice architecture is very popular, which also led to many teams to adopt microservices in practice without thinking ( not considering the size of the team, nor the development of the business, nor the support of the underlying technology ). However, there are also many problems after blindly using microservices.

---

<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Pitfalls of Implementing Microservices](#pitfalls-of-implementing-microservices)
    * [Complexity: Over-Segmentation of Services and Complex Relationships](#complexity-over-segmentation-of-services-and-complex-relationships)
    * [Long Call Chains: Performance Degradation and Difficult Error Localization](#long-call-chains-performance-degradation-and-difficult-error-localization)
    * [Difficult to Deliver Quickly without Automation](#difficult-to-deliver-quickly-without-automation)
    * [Service Governance Issues Leading to Management Chaos](#service-governance-issues-leading-to-management-chaos)
  * [Best Practices for Implementing Microservices](#best-practices-for-implementing-microservices)
    * [Service Granularity](#service-granularity)
    * [Decomposition Methods](#decomposition-methods)
    * [Infrastructure](#infrastructure)
<!-- TOC -->

---

## Pitfalls of Implementing Microservices

### Complexity: Over-Segmentation of Services and Complex Relationships

When services are divided into smaller, finer-grained components, the complexity of individual services may decrease, but **the overall system complexity can increase** because microservices shift complexity from within services to the interactions between them. If there are `n` services, the complexity of the system is `n × (n - 1) / 2`, meaning complexity increases significantly as the number of services grows.

![](/assets/img/note/architecture/bm1.jpg){: .w-10 .shadow .rounded-10 }

**Too many services can also lead to a sharp drop in team efficiency.** The word "micro" in microservices may lead some teams to overly fragment services, assuming everything must be broken down into very small components. For instance, a team of five to six people may end up with 30 services, with each team member responsible for managing five or more services. This setup can negatively impact productivity because even simple tasks may require involvement with multiple services. Tasks such as development, testing, and deployment involve dealing with many service interfaces, leading to constant switching between different services.

### Long Call Chains: Performance Degradation and Difficult Error Localization

In microservices, communication between services usually occurs over the network via HTTP or RPC, which **adds latency to each call.** For example, if a business request involves six service calls, with each call taking around 50 milliseconds, the total response time could be around 300 milliseconds. This can be problematic in high-performance scenarios where low latency is crucial.

When systems are broken into multiple microservices, a single request may pass through several services. If any service fails, it can lead to cascading errors, making it difficult to pinpoint the root cause.

![](/assets/img/note/architecture/bm2.jpg){: .w-10 .shadow .rounded-10 }

The above image illustrates a scenario where a slow database query in Service C causes cascading errors. **Although the picture clearly shows the cause of the error, troubleshooting the problem is much more complex in a real project.** (For example, there are many reasons for Service A to fail, and it may take us an hour to find out that it is due to an error returned by Service B.) The root cause is not immediately clear, leading to a time-consuming investigation through multiple layers. Initially, the focus might be on Service A, before moving to Service B, and finally discovering the issue in Service C. **If multiple services encounter different types of failures simultaneously, troubleshooting becomes even more complex**, requiring substantial effort to locate and resolve the underlying issues.

### Difficult to Deliver Quickly without Automation

If there is no **automation for tasks like testing, deployment, and monitoring, managing microservices** becomes highly labor-intensive and inefficient, negating the benefits of adopting microservices.

Examples of challenges without automation:
- Each test requires manual testing of many interfaces.
- Each deployment involves multiple services and machines, with operators executing _shell commands_ manually.
- Troubleshooting requires manually inspecting logs and statuses across numerous services and servers.

### Service Governance Issues Leading to Management Chaos

The design philosophy of microservices often emphasizes being "lightweight". However, as the number of microservices increases, management without proper governance can become problematic.

For example:
- **Service Routing:** With many microservices (e.g., 60 services across 20 servers), determining how dependent services should route requests can be challenging.
- **Service Failure Isolation:** When some nodes go down (e.g., 5 out of 60), figuring out how dependent services should respond to these failures can be difficult.
- **Service Scaling:** As services and nodes are added or removed, managing the configuration (e.g., scaling from 60 to 80 nodes or reducing to 40) without disrupting other services becomes complex.

## Best Practices for Implementing Microservices

In the previous section, I talked about some of the pitfalls of implementing microservices, briefly refined as:

- Microservices are split too fine, overemphasising the **small**.
- Microservices infrastructure is not sound, ignoring the **automated**.
- Microservices are not **lightweight**, and when they get bigger, ‘lightweight’ no longer fits.

Despite the pitfalls, microservices can be implemented effectively by following these best practices:

### Service Granularity

The solution to over-segmentation is to **base the breakdown of services on team size and scale** using the "three-person rule." This principle means that each microservice should be managed and developed by a team of three people. As the business expands and the number of services grows, the number of microservices should be adjusted based on team size. For example, If the team starts with six members, plan for two microservices. As the team grows to 12, consider expanding to four microservices.

- **Why "three-person rule"?**
  - **System Complexity Management**: With three members, the system's complexity is at a level where everyone can understand it thoroughly. More members could lead to inefficiencies and communication issues.
  - **Backup and Maintenance**: Three members create redundancy; if one member is unavailable, two can still manage the service without issues.
  - **Effective Decision-Making**: With three members, there are more perspectives for discussions and design decisions. Two people may struggle with differences of opinion, while four or more can slow down decision-making.

"Three-person rule" is mainly used in the design and development stage of microservices. If the microservices have been developed for a period of time and have become more stable and are **in the maintenance period, then on average 1 person can maintain 1 microservice or even several microservices.** 

### Decomposition Methods

- Decomposition Based on Business Logic:
  - This is the most common approach, where system modules are separated according to business boundaries, with each functional business module treated as an independent service.
  - While straightforward in theory, challenges can arise when team members disagree on how to split services due to differences in understanding business boundaries. For example, breaking a system into "products," "orders," and "transactions" may seem logical, but others may prefer "products," "purchases," "sales," and "shipping."
  - To avoid such disputes, apply the "three-person rule" to calculate an appropriate number of services based on team size, then choose a level of business granularity that suits the team's ability to manage. Larger teams can support finer granularity.
- Decomposition Based on Scalability:
  - This method splits services into **stable** and **frequently changing** components. The stable services are more general and less likely to change, such as "user management," while dynamic services are more specialized.
  - This approach aims to boost project delivery efficiency by keeping frequently changing parts separate from stable core services, thus avoiding disruption to core functions.
- Decomposition Based on Reliability:
  - Services are split according to their criticality. Core and highly reliable services are treated separately from less critical ones. Then focus on ensuring high availability of core services.
  - Core services are prioritized for stability and reliability, while less critical services can be more flexible.

### Infrastructure

Focus on the importance of **automation** rather than just making services "small" and "lightweight."  If proper automation isn't in place, microservices can become unmanageable as the number of services grows. **Compared to SOA, microservices don't reduce complexity, but simply shift it from the ESB to the infrastructure.** 

Building a sound microservices infrastructure is a huge project, and in general, only big companies develop their own microservices infrastructure.  Smaller companies typically use existing microservices infrastructure (e.g. Spring Cloud, Dubbo).

Not every infrastructure is necessary if the number of microservices is not very large. Typically, we need to build the infrastructure according to the following priorities:
1. **Service Discovery, Routing, and Governance**
   - These are the foundational elements, necessary for managing the basic functionality of microservices, such as finding services and ensuring proper communication.
2. **API Gateway and Interface Management**
   - Focuses on improving development efficiency. The API gateway facilitates integration with external services, while interface management ensures smooth connections between services.
3. **Automation Tools**
   - Includes automated testing, deployment, and configuration management to streamline the release process and operational tasks.
4. **Service Monitoring and Security**
   - These elements further enhance operational efficiency.

The above 3 and 4 types of infrastructures will become more and more important as the number of microservice nodes increases. However, when the number of microservice nodes is small, they can be supported manually, which is not very efficient but can basically hold up.


<br>

---

**Reference:**

- Li, Yunhua (2018) _Learn Architecture from 0_. Geek Time.
