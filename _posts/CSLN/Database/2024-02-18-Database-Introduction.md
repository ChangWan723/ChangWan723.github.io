---
title: Understanding Databases
date: 2024-02-18 16:14:00 UTC
categories: [ (CS) Learning Note, Database ]
tags: [ software engineering, Database ]
pin: false
---

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction to Databases](#introduction-to-databases)
    * [A Brief History of Databases](#a-brief-history-of-databases)
    * [What is the Difference Between DB, DBS and DBMS?](#what-is-the-difference-between-db-dbs-and-dbms)
  * [What are the major DBMSs?](#what-are-the-major-dbmss)
    * [SQL vs NoSQL](#sql-vs-nosql)
  * [Long-lived languages: SQL](#long-lived-languages-sql)
    * [DDL & DML & DCL & DQL](#ddl--dml--dcl--dql)
  * [Why Do We Need to Learn and Understand about Databases?](#why-do-we-need-to-learn-and-understand-about-databases)
    * [Writing SQL is Easy, but Writing efficient SQL is Hard!](#writing-sql-is-easy-but-writing-efficient-sql-is-hard)
    * [SQL Syntax is Simple and Clear, and It Can be Used as a Communication Tool](#sql-syntax-is-simple-and-clear-and-it-can-be-used-as-a-communication-tool)
<!-- TOC -->

---

## Introduction to Databases

At its core, a **database** is a collection of data organized in a manner that facilitates easy access, management, and
update. Databases are designed to store vast amounts of information in a way that allows for quick searches,
transactions, and analytics. They can range from simple, single-table databases used for small tasks to complex,
multi-tiered database architectures employed by large organizations and web applications.

### A Brief History of Databases

The journey of databases begins in the early 1960s with the advent of the first navigational databases, such as the
hierarchical database model (IBM's IMS) and the network model (CODASYL). These models were characterized by their rigid
structures and complex data relationships.

The 1970s marked a significant turning point with the introduction of the relational database model by Edgar F. Codd.
This model, based on set theory and predicate logic, allowed for data to be stored in tables (relations) with rows (
records) and columns (attributes), revolutionizing the way data was organized and accessed. The relational database
model paved the way for **Structured Query Language (SQL)**, which became the standard language for managing and
querying relational databases.

In the following decades, we saw the emergence of Object-Oriented Databases in the 1980s, which aimed to align database
technology with the growing adoption of object-oriented programming languages. The late 1990s and early 2000s witnessed
the rise of NoSQL databases, such as document stores, key-value stores, wide-column stores, and graph databases,
designed to address the scalability and flexibility needs of modern web-scale applications. .

### What is the Difference Between DB, DBS and DBMS?

- **DB** is Database. Database is a collection of stored data, you can understand it as multiple data tables.
- **DBMS** is DataBase Management System, it can manage multiple databases, so you can understand
  that `DBMS = multiple databases (DB) + hypervisor`. For example, `Oracle` and `MySQL`.
- **DBS** is DataBase System. It is a bigger concept which includes DB, DBMS, DBA(database administrator) and so on. A
  DBS represents the entire environment or ecosystem dedicated to managing database data effectively.

## What are the major DBMSs?

The following table shows the ranking of DBMSs published by [DB-Engines](https://db-engines.com/en/ranking) in February
2024 (the rankings are updated regularly):

| No. | Database Management System (DBMS) | Database Type |
|-----|-----------------------------------|---------------|
| 1   | Oracle                            | Relational    |
| 2   | MySQL                             | Relational    |
| 3   | Microsoft SQL Server              | Relational    |
| 4   | PostgreSQL                        | Relational    |
| 5   | MongoDB                           | Document      |
| 6   | Redis                             | Key-Value     |
| 7   | Elasticsearch                     | Search Engine |
| 8   | IBM DB2                           | Relational    |
| 9   | Snowflake                         | Relational    |
| 10  | SQLite                            | Relational    |
| 11  | Microsoft Access                  | Relational    |
| 12  | Cassandra                         | Wide Column   |

- As we can see from the rankings, **relational** databases are definitely the dominant DBMS, with Oracle, MySQL and SQL Server being the most used DBMSs.
  - A relational database (RDBMS) is a database built on a relational model, and **SQL** is the query language for relational databases.
- Compared to **SQL**, **NoSQL** broadly refers to non-relational databases and includes the Key-Value databases, Document databases, Search Engines and Wide Column stores on the list, besides which Graph databases are also included.
  - **Key-Value** databases store data by means of Key-Value, where Key and Value can be simple or complex objects. 
    - Key as a unique identifier, **the advantage is fast search speed**, in this regard is clearly superior to relational databases. 
    - Meanwhile the disadvantages are obvious. It cannot be as relational databases are free to use conditional filtering (such as `WHERE`). If you do not know where to look for the data, you have to traverse all the keys, which consumes a lot of computations. 
    - A typical use case for key-value databases is as Cache. Redis is the most popular key-value database.
  - **Document** database is used to manage documents. A document is the basic unit of information processing in a database, and a document is equivalent to a record. 
    - MongoDB is the most popular document-based database.
  - **Search Engine** is also an important application in database retrieval, common full-text search engine Elasticsearch, Splunk and Solr. 
    - Although relational databases use indexing to improve retrieval efficiency, but for the full-text indexing efficiency is low. The advantage of the search engine is the use of full-text search technology, the core principle is "inverted index".
  - **Wide Column** databases are relative to row-based databases. 
    - Oracle, MySQL, SQL Server and other databases use row-based storage, while columnar databases store data in columns, which has **the advantage of greatly reducing system I/O** and is suitable for distributed file systems, with the **disadvantage of relatively limited functionality**.
  - **Graph** databases, which make use of a graph as a data structure store the relationships between entities (objects). 
    - The most typical example is the relationships between people in social networks.
    - The data model is mainly implemented in terms of nodes and edges (relationships). It is characterised by its ability to solve complex relational problems efficiently.

### SQL vs NoSQL

**SQL** here refers to **relational databases**, while **NoSQL** refers to **non-relational databases** (e.g., Key-value, Document, Search engines etc. as mentioned above). 

Even though NoSQL includes many types of databases, it's still SQL that has more weight in the DBMS rankings. Four of the top 5 most influential DBMSs are relational databases. So, it is essential to know SQL well.

Since SQL has always dominated DBMSs, many people wondered if there was a database technology that could stay away from SQL, and so NoSQL was born. **But as it evolved, it became more and more SQL-like**, and so far all DBMSs in the NoSQL camp have implemented SQL-like functionality. 

**NoSQL is a great complement to SQL.** The following is a list of interpretations of the term "NoSQL" over time, and the evolution of NoSQL functionality can be seen in these changes in interpretation:
- 1970: NoSQL = We have no SQL
- 1980: NoSQL = Know SQL
- 2000: NoSQL = No SQL!
- 2005: NoSQL = Not only SQL
- 2013: NoSQL = No, SQL!

## Long-lived languages: SQL

In 1974, an IBM researcher published a paper unveiling database
technology, "[SEQUEL: A structured English query language](https://dl.acm.org/doi/10.1145/800296.811515)". Until today
this structured query language has not changed much, and compared to other languages, **SQL's lifespan can be said to be
very long**. There are two important standards for SQL, SQL92 and SQL99, which represent the SQL standards promulgated
in 1992 and 1999. The SQL language we use today still follows these standards.

### DDL & DML & DCL & DQL

We can divide the SQL language into the following 4 parts according to its function:

1. **DDL(Data Definition Language)**. which is used to define our database objects including databases, data tables and
   columns. By using DDL, we can create, delete and modify database and table structures.
2. **DML (Data Manipulation Language)**. we use it to manipulate the records related to database like adding, deleting
   and modifying the records in the data table.
3. **DCL (Data Control Language)**. we use it to define access rights and security levels.
4. **DQL (Data Query Language)**. We use it to query the records we want, and it is the most important part of the SQL
   language. In real business, we deal with queries in the vast majority of cases.

## Why Do We Need to Learn and Understand about Databases?

### Writing SQL is Easy, but Writing efficient SQL is Hard!

- Although technical people use SQL to a greater or lesser extent, different people write SQL with different levels of
  efficiency. A good SQL execution plan, for example, minimises I/O operations, which are the most bottlenecked area of
  a DBMS. **A large amount of time in database operations is spent on I/O.**
- In addition, you also need to consider how to reduce the amount of CPU computation, the use of `GROUP BY`, `ORDER BY`
  and other statements in the SQL statement will consume a lot of CPU computing resources, so we need to start from the
  global perspective, not only need to consider the I/O performance of the database, but also need to **consider the CPU
  computation, memory usage and so on**.
  - For example, `EXIST` and `IN` can get the same result in some cases, but which one is more efficient in specific
    execution?
    - If one of the two tables is smaller and the other is larger, use `EXIST` for the larger sub-query table and `IN`
      for the smaller sub-query table. (`EXIST` uses the index on the table of the sub-query, whereas `IN` uses the
      index on the table of the main-query.) But notice that this is not always true, depending on the database
      optimisation.

### SQL Syntax is Simple and Clear, and It Can be Used as a Communication Tool

SQL statements are so intuitive that you can guess what they mean even if you don't have a basic knowledge of SQL. In
addition to this, **the need to understand data tends to be high-frequency for most computer practitioners**, so getting
to grips with SQL on your own is essential in practice.

**As technology and Internet professionals, we always want to find a language that is versatile, relatively unchanged,
and relatively easy to learn, and SQL is one of the few languages that meet all three of these criteria.** Whether
you're a product manager, an operator, a developer, or a data analyst, you can use the SQL language. It's like a sword
that can expand your work horizons in addition to increasing your productivity.


<br>

---

**Reference:**

- Chen, Yang (2019) _What you must know about SQL_. Geek Time. 
