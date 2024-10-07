---
title: What is the Relationship Between Microservices and SOA?
date: 2024-10-07 11:12:00 UTC
categories: [ (CS) Learning Note, Architecture ]
tags: [ software engineering , architecture, microservices ]
pin: false
image:
  path: /assets/img/posts/soa.png
---

**Microservices** include the concept of "service", and **SOA (Service Oriented Architecture)** also has the concept of "service", we will naturally ask: **what is the relationship between microservices and SOA? Why do we still need microservices when we have SOA?**

If you are going to use microservices architecture, it is important to understand the above questions. If you don't understand these questions and just follow the trend of using microservices, it will not be beneficial, but may have negative side effects.

---

<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction to SOA & Microservices](#introduction-to-soa--microservices)
    * [SOA](#soa)
      * [History of SOA](#history-of-soa)
      * [Key Concepts of SOA](#key-concepts-of-soa)
      * [Key Features of SOA](#key-features-of-soa)
    * [Microservices](#microservices)
      * [History of Microservices](#history-of-microservices)
      * [Key Features of Microservices](#key-features-of-microservices)
  * [Different Viewpoints: The Relationship Between Microservices & SOA](#different-viewpoints-the-relationship-between-microservices--soa)
    * [Microservices is a Concrete Implementation of SOA (×)](#microservices-is-a-concrete-implementation-of-soa-)
    * [Microservices is SOA without the ESB (×)](#microservices-is-soa-without-the-esb-)
    * [Microservices and SOA are Essentially Two Different Architectural Concepts. (√)](#microservices-and-soa-are-essentially-two-different-architectural-concepts-)
  * [When to Use SOA vs. Microservices](#when-to-use-soa-vs-microservices)
    * [When SOA is More Suitable](#when-soa-is-more-suitable)
    * [When Microservices is More Suitable](#when-microservices-is-more-suitable)
<!-- TOC -->

---

## Introduction to SOA & Microservices

In the world of software architecture, **Service-Oriented Architecture (SOA)** and **Microservices** are two widely discussed approaches to building scalable, modular, and distributed applications.

### SOA

**SOA (Service-Oriented Architecture)** is an architectural approach where **different components or services of an application are designed to communicate and work together over a network.** The core idea is to create a collection of loosely coupled, reusable services, each responsible for a specific business function, which can be combined and reused across different applications.

#### History of SOA

SOA was born in the 1990s, and the first SOA report was published in 1996 by Roy W. Schulte and Yefim V. Natis, two analysts at Gartner.

The emergence of SOA is mainly to solve the problem of duplication and inefficiency of IT systems within the enterprise. These problems are mainly reflected in:
- **Independent IT Systems**: Each department within an organization may have its own IT system (e.g., HR, finance, sales), which often require dedicated personnel for development and management.
- **Incompatibility**: These IT systems are likely to have been built by different vendors and use varying technologies, making integration or updates challenging.
- **Complexity of Coordination**: As business processes evolve, more systems are required to work together. Without standard methods for integration, such as unified protocols or services (e.g., Java for HR systems, .NET for financial systems, SOAP for communication), developing and coordinating new processes becomes inefficient, leading to low productivity.

SOA was introduced to address these issues by standardizing communication between systems and enabling more efficient system integration and management. In order to do so, SOA proposes the following key concepts.

#### Key Concepts of SOA

1. **Service**
   - In SOA, all business functionalities are considered services. A service represents **the capability to be offered externally**, making it accessible to other systems when needed **without customization**.
   - Services can range from simple to complex. The granularity of services depends on the actual needs of the enterprise.
2. **ESB (Enterprise Service Bus)**
   - ESB is a middleware solution that connects different services within an enterprise, **acting like a bus** in computing that connects various devices. It ensures the integration of services that might be built **using different technologies and standards.**
   - By utilizing an ESB, SOA enables efficient communication between these heterogeneous systems, offering a **unified interface** for various services.
3. **Loose Coupling**
   - Loose coupling **reduces dependencies between services**. In an SOA architecture, services operate independently and can even run without knowing the details of other services or databases.

![](/assets/img/note/architecture/sm1.jpg){: .w-10 .shadow .rounded-10 }
_Typical SOA Architecture Sample_

#### Key Features of SOA

1. **Centralized Governance**: SOA typically emphasizes strong governance with centralized control over services, ensuring compliance with enterprise-wide standards and policies.
2. **Heavy Middleware**: SOA often relies on an **Enterprise Service Bus (ESB)** to manage the communication, orchestration, and integration of services.
3. **High-Level Concept**: SOA architecture is a high-level architectural design concept (enterprise level). In general, we can say that an enterprise has adopted SOA architecture to build its IT systems, but we cannot say that a separate system has adopted SOA architecture. For example, an organisation adopts a SOA architecture and divides the system into ‘HRM service’, ‘time and attendance service’ and ‘financial service’, but the separate system (such as HRM service) are not usually split into further services under the SOA architecture.
4. **Complexity**: SOA solves the problems of duplication and inefficient scaling of traditional IT systems, but introduces more complexity of its own. **one of the most criticised aspects of SOA is the ESB**, which is required to implement protocol conversions, data conversions, transparent dynamic routing, and other functions with various systems. 

> **Designing an ESB in SOA is a last resort.**
> 
> When SOA was introduced, heterogeneous IT systems had already existed for many years. The cost of completely rewriting them or adapting them to a unified standard was very large. The only way to adapt to the heterogeneous systems that already existed was through ESB.
{: .prompt-tip }

> **SOA is more commonly used in traditional industry (e.g., manufacturing, finance, etc.) and is not widely used in the Internet industry.**
> 
> **This is because SOA is a product of specific historical conditions.** It is designed for a variety of heterogeneous and more stable IT systems in traditional enterprises. 
> 
> And the features of the Internet enterprise are **small, new and fast**. SOA architecture generally cannot be quickly scaled, which is not suitable for the Internet enterprise. And many Internet companies are newly created, without so much historical baggage. Therefore, Internet enterprises are more suitable for the microservices architecture.
{: .prompt-tip }

### Microservices

**Microservices** is a more recent architectural style that also focuses on building applications as a collection of small, independent services. Each service in a microservices architecture is designed to be lightweight, highly decoupled, and self-contained, allowing it to be deployed, scaled, and managed independently.

> In short, the microservice architectural style is an approach to developing a single application as a suite of **small** services, each running in its own process and communicating with **lightweight** mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully **automated** deployment machinery.
> 
> -- Martin Fowler

#### History of Microservices

Microservices is a very hot architectural design concept in recent years. Most people think that the concept of microservices was introduced by Martin Fowler in 2014, but in fact, the history of microservices is much earlier. And Martin Fowler didn't create microservices, Martin just explained [microservices](https://martinfowler.com/articles/microservices.html) in a systematic way. However, we can't deny Martin's role in promoting microservices, and he's a big part of the reason why microservices have become so popular.

Here is a brief timeline of the development of microservices:

- **2005**: Dr. Peter Rodgers introduced the concept of "Micro-Web-Services" at the Web Services Edge Conference.
- **2011**: A software architecture team first used the term "microservice" to describe a particular architectural style.
- **2012**: The same team formally adopted "microservice" as a term to represent this architecture.
- **2012**: James Lewis from ThoughtWorks discussed the concept of microservices at QCon San Francisco 2012, gaining more recognition.
- **2014**: James Lewis and Martin Fowler co-wrote an influential article that detailed microservices, further shaping the understanding and adoption of the architecture.

![](/assets/img/note/architecture/sm5.jpg){: .w-10 .shadow .rounded-10 }
_Typical Microservices Architecture Sample_

#### Key Features of Microservices

1. **Decentralized Governance**: Unlike SOA, microservices promote decentralized governance, giving teams the autonomy to choose the best technologies, tools, and standards for each service.
2. **Lightweight Communication**: Microservices typically use lightweight protocols such as **HTTP/REST** or **gRPC** for communication between services.
3. **Fine-Grained Services**: Microservices are designed to handle specific business functions and are smaller in scope compared to SOA services.
4. **Independent Deployment**: Each microservice can be developed, tested, and deployed independently, reducing the risk of dependencies breaking other parts of the system.
5. **Scalability**: Microservices can be scaled independently, which improves resource utilization and makes the system more resilient under heavy load.

## Different Viewpoints: The Relationship Between Microservices & SOA

The relationship and differences between SOA and microservices are roughly divided into the following typical viewpoints:

### Microservices is a Concrete Implementation of SOA (×)

![](/assets/img/note/architecture/sm2.jpg){: .w-10 .shadow .rounded-10 }

This viewpoint considers SOA as an architectural concept and microservices as a concrete implementation of the SOA concept. For example, "Microservices are SOA using the HTTP RESTful protocol for ESBs", "Using SOA to build individual systems is microservices", and "Microservices are SOA at a finer granularity".

### Microservices is SOA without the ESB (×)

![](/assets/img/note/architecture/sm3.jpg){: .w-10 .shadow .rounded-10 }

One of the most widely criticised aspects of traditional SOA architectures is the large, complex and inefficient ESB. So this viewpoint considers removing the ESB from SOA and replacing it with a lightweight HTTP implementation to be microservices.

### Microservices and SOA are Essentially Two Different Architectural Concepts. (√)

![](/assets/img/note/architecture/sm4.jpg){: .w-10 .shadow .rounded-10 }

This viewpoint considers microservices and SOA to be only somewhat similar, but essentially different architectural design concepts. The similarity lies in the fact that both focus on ‘services’, and both solve scalability problems by splitting services. The essential differences lie in some core concepts: ESB or not, granularity of services, architectural design goals, etc.

While SOA and Microservices share common goals, such as modularity, reusability, and loose coupling, they differ in key aspects of their design and philosophy. Let’s examine these differences:

| **Aspect**             | **SOA**                                    | **Microservices**                                  |
|------------------------|--------------------------------------------|----------------------------------------------------|
| **Service Scope**       | Larger, coarser-grained services           | Smaller, fine-grained services                     |
| **Governance**          | Centralized governance and standardization | Decentralized governance, team autonomy            |
| **Communication**       | Often uses heavier protocols like SOAP/ESB | Uses lightweight protocols like REST, gRPC, or MQ  |
| **Data Management**     | Shared data model across services          | Each service manages its own database              |
| **Deployment**          | Services are typically co-deployed         | Services are independently deployed                |
| **Inter-Process Communication** | Relies heavily on ESB for integration | Direct communication, often without an ESB         |
| **Technology Choices**  | Standardized across the enterprise         | Teams can choose their own tech stack per service  |
| **Scaling**             | Horizontal scaling, but often monolithic   | Each service can scale independently               |

So the third viewpoint is correct: So the third viewpoint is correct: **SOA and microservices are essentially two different architectural design concepts** that intersect at the point of ‘service’. **There is no superiority between the two, just different application scenarios.**

> **SOA is about integrating multiple systems, whereas microservices are about taking individual systems apart. The two go in opposite directions.**
{: .prompt-tip }

## When to Use SOA vs. Microservices

### When SOA is More Suitable

- **Large Enterprises with Complex Integration Needs**: SOA is often favored by large organizations that need to integrate a wide variety of services, databases, and legacy systems. The **ESB** acts as a central hub that handles message routing, data transformation, and service orchestration, making it well-suited for complex integrations.
- **Standardized Environments**: If your organization demands strong governance and compliance to standards, SOA’s centralized governance model ensures consistency across the organization.

### When Microservices is More Suitable

- **Agile Development Teams**: Microservices are an excellent choice for teams practicing agile methodologies, where fast iterations and independent deployments are key.
- **Highly Scalable Applications**: Microservices allow for independent scaling of services based on demand. For instance, in an e-commerce system, the service responsible for handling customer searches can be scaled independently from the payment service.
- **Startups or Growing Businesses**: Microservices allow for rapid development and deployment of new features without impacting the entire system. This makes them ideal for startups or businesses that need to innovate quickly.

<br>

---

**Reference:**

- Li, Yunhua (2018) _Learn Architecture from 0_. Geek Time.
- https://medium.com/@adeelsarwarblog/what-is-service-oriented-architecture-9b4406fcedeb
- https://medium.com/microtica/microservices-vs-soa-is-there-any-difference-at-all-2a1e3b66e1be
- https://microservices.io/patterns/microservices
