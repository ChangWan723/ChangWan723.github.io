---
title: Cost Estimation (Query Processing) in Databases
date: 2024-04-08 20:00:00 UTC
categories: [ (CS) Learning Note, Database ]
tags: [ computer science, Database ]
pin: false
---

Cost estimation provides the foundation for query optimization by estimating the resource requirements and execution time of different query execution plans. Query optimization uses these cost estimates to select the most efficient plan, leading to faster query processing and better overall system performance.

- At this stage, no commitment to a particular physical plan
  - Estimate the “cost” of each operator in terms of **the size relation(s) on which it operates**
  - Choose a logical query plan that **minimises the size of the intermediate relations** (= minimises the cost of the plan)
- Assumption: system catalogue stores statistics about each relation

---

- **Statistics**:
  - `T(R)`: Number of tuples in relation `R` (cardinality of `R`)
  - `V(R, A)`: Number of distinct values for attribute `A` in relation `R`
  - Note: for any relation `R`, `V(R, A) ≤ T(T)` for all attributes `A` on `R`

- **Scan**:
  - Operation of reading all tuples of a relation
  - `T(scan(R))=T(R)`
  - For all `A` in `R`, `V(scan(R),A)=V(R,A)`

- **Product**:
  - `T(RxS)=T(R)T(S)`
    - For all `A` in `R`, `V(RxS,A)= V(R,A)`
    - For all `B` in `S`, `V(RxS,B)=V(S,B)`

- **Projection**
  - `T(πA(R))= T(R)`
  - `V(πA(R)),A) = V(R,A)`
    - Assumption: projection does not remove duplicate tuples (value counts don’t change)

- **Selection (attr=val)**:
  - `T(σ A=c (R)) = T(R) / V(R, A)`
  - `V(σ A=c (R),A) = 1`
    - Assumption: all values of `A` appear with equal frequency
  - Conjunction: `T(σ A=c1⋀B=c2 (R))= T(R) / V(R, A) V(R, B)`
  - Disjunction: `T(σ A=c1∨B=c2 (R))= T(R) / V(R, A) + T(R) / V(R, B)`
    - This overestimates the number of tuples. Alternatively, `T(σ A=c1∨B=c2 (R))= T(R) (1 - 1 / V(R, A)) (1 - 1 / V(R, B))`

- **Selection (attr=attr)**:
  - `T(σ A=B (R)) = T(R) / max(V(R, A), V(R, B))`
  - `V(σ A=B (R), A)= V(σ A=B (R),B) = min(V(R, A),V(R, B))`
    - Assumption: all values of `A` appear with equal frequency. And all values of `B` appear with equal frequency

- **Join**:

![](https://i.postimg.cc/TY3nzCst/qp2.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/m2p7B7fB/qp3.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/G3QkgZXB/qp4.png){: .w-10 .shadow .rounded-10 }

![](https://i.postimg.cc/DzbBHnZQ/qp5.png){: .w-10 .shadow .rounded-10 }

