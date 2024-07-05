---
title: "High Performance Architecture: Caching"
date: 2024-07-05 19:55:00 UTC
categories: [ (CS) Learning Note, Architecture ]
tags: [ software engineering , architecture]
pin: false
---

Caching is a vital technique used in software architecture to enhance the performance and scalability of applications. By storing frequently accessed data in a temporary storage area (cache), applications can significantly reduce access times and server load. 

---
<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [Introduction to Cache Architecture](#introduction-to-cache-architecture)
    * [Benefits of Caching](#benefits-of-caching)
    * [Types of Caching](#types-of-caching)
      * [Client-Side Caching](#client-side-caching)
      * [Server-Side Caching](#server-side-caching)
      * [Distributed Caching](#distributed-caching)
      * [Database Caching](#database-caching)
  * [Cache Policies](#cache-policies)
    * [Cache Invalidation](#cache-invalidation)
    * [Cache Eviction](#cache-eviction)
  * [Challenges in Cache Architecture](#challenges-in-cache-architecture)
    * [Cache Penetration](#cache-penetration)
      * [Causes of Cache Penetration: Non-existent Data](#causes-of-cache-penetration-non-existent-data)
      * [Causes of Cache Penetration: Large Amount of Data](#causes-of-cache-penetration-large-amount-of-data)
    * [Cache Avalanche](#cache-avalanche)
      * [Causes of Cache Avalanche](#causes-of-cache-avalanche)
      * [Mitigation Strategies](#mitigation-strategies)
    * [Cache Stampede](#cache-stampede)
      * [Causes of Cache Stampede](#causes-of-cache-stampede)
      * [Mitigation Strategies](#mitigation-strategies-1)
<!-- TOC -->

---

## Introduction to Cache Architecture

Cache architecture refers to the design and organization of cache systems within an application or network. A cache temporarily stores copies of data or computations to serve future requests more quickly. Effective cache architecture can lead to significant improvements in application responsiveness and efficiency.

### Benefits of Caching

1. **Performance Improvement**: Reduces data access time by storing frequently used data closer to the application.
2. **Reduced Load on Backend Systems**: Decreases the number of direct requests to databases or other backend services.

### Types of Caching

#### Client-Side Caching

Client-side caching stores data on the client-side, such as in the browser or on the user's device. This type of caching is useful for reducing server load and improving the user experience by loading data locally.

- **Example**: Browser caching of web assets like HTML, CSS, and JavaScript files.

#### Server-Side Caching

Server-side caching stores data on the server. It can be implemented at different layers, including the application server, database server, and proxy server.

- **Example**: Application-level caches, such as in-memory caches (Redis, Memcached).

#### Distributed Caching

Distributed caching involves spreading the cache across multiple servers or nodes, providing a scalable solution for large-scale applications.

- **Example**: Using a distributed caching system like Apache Ignite or Amazon ElastiCache to store session data or application data.

#### Database Caching

Database caching stores query results or frequently accessed data at the database level. This can significantly reduce the load on the database and improve query performance.

- **Example**: MySQL query cache or Redis as a caching layer for frequently accessed database queries.

## Cache Policies

### Cache Invalidation

Cache invalidation is the process of **removing outdated data from the cache to keep the data up-to-date. It usually occurs when data is out of date.** There are three primary strategies for cache invalidation:

- **Time-Based Invalidation**: Entries are invalidated after a specific time-to-live (TTL) period.
- **Event-Based Invalidation**: Entries are invalidated based on specific events or triggers, such as data updates.
- **Manual Invalidation**: Entries are invalidated manually by the application or administrator.

### Cache Eviction

Cache eviction refers to the **removal of entries from the cache to make room for new data. It usually occurs when the cache is out of space.** Common eviction policies include:

- **Least Recently Used (LRU)**: Removes the least recently accessed entries first.
- **First In, First Out (FIFO)**: Removes the oldest entries first.
- **Least Frequently Used (LFU)**: Removes the least frequently accessed entries first.

## Challenges in Cache Architecture

Improper cache implementation can lead to issues such as cache avalanche, cache penetration, and cache stampede. They are common issues that can arise in caching systems, leading to degraded performance and increased load on backend systems.

### Cache Penetration

**Cache penetration means that the cache is not working for some reason.** 

Cache penetration occurs when requests bypass the cache and go directly to the backend data source, **usually because the requested data does not exist in the cache and the backend.** This can lead to a significant load on the backend.

#### Causes of Cache Penetration: Non-existent Data

In general, if there is no data in the storage system, the corresponding data will not be stored in the cache. Thus, **when querying for data that does not exist, the corresponding data is not found in the cache, and each time it has to go to the storage system and query again to confirm that the data does not exist.** (Because in the cache, there's no way to determine whether the data doesn't exist or isn't cached)

---

**Mitigation Strategies:**
1. **Bloom Filters**: Use a [Bloom filter](/posts/Bit-Map/) to quickly check for the existence of data.
2. *Cache Null Results**: If the data is not found, a default value (either `Null` or a specific value) is set into the cache. This way the second time it queries for the same data, it will know that this data does not exist and will not continue to access the storage system.


1. **Non-existent Keys**: Repeated requests for non-existent data.
2. **High Query Rate**: A large number of queries that miss the cache.

#### Causes of Cache Penetration: Large Amount of Data

 **When there is too much data to cache, we cannot cache all of it. And generating cached data may take a long time or consume a lot of resources.** This may cause caching to not take effect. And it causes access pressure to be concentrated on the storage system.

---

For example, if we select "mobile phone" as a category on an e-commerce platform, we can't cache all the data due to the huge data. We can only cache by paging. Since it is difficult to predict exactly which pages a user will visit, the simplest thing to do is to generate a page cache each time a page is clicked. This way pages that are frequently clicked on by users are cached.

Normally, this implementation is basically satisfying the requirements. However, if it is traversed by a competitor using a crawler, problems may arise. This situation does not have a good solution, because the crawler will traverse all the data, and there is no regularity. One of the solutions is to identify crawlers and disable access, but this may affect SEO and promotion. Another solution is to do a good monitoring and deal with the problem in time after finding it. Because the crawler is not an attack, it will not carry out violent damage, the impact on the system is gradual, and the monitoring has time to deal with the problem when it is found.


### Cache Avalanche

Cache avalanche is a situation when **a large number of caches are invalidated (expired) at the same time** causing a sharp drop in system performance.

Cache avalanche occurs when a large number of cache entries expire simultaneously, causing a sudden surge of requests to the backend data source. This can overwhelm the backend, leading to performance degradation or even system failure.

#### Causes of Cache Avalanche

1. **Simultaneous Expiry**: Setting the same expiration time for a large number of cache entries.
2. **High Traffic Load**: High traffic applications where many requests hit expired cache entries at the same time.

#### Mitigation Strategies

1. **Randomized Expiry**: Add a random factor to the cache expiration time to prevent simultaneous expiry.
2. **Cache Warm-Up**: Pre-populate the cache with frequently accessed data during low traffic periods.
3. **Rate Limiting**: Implement rate limiting to control the number of requests hitting the backend when the cache expires.

### Cache Stampede

Cache stampede occurs when multiple threads or processes simultaneously request a cache entry that is not present or has expired. This can lead to multiple requests hitting the backend data source at the same time, overwhelming it.

#### Causes of Cache Stampede

1. **Simultaneous Cache Misses**: High concurrency environments where multiple requests miss the cache simultaneously.
2. **High Traffic Peaks**: Sudden spikes in traffic leading to simultaneous cache misses.

#### Mitigation Strategies

1. **Mutex Locks**: Use mutex locks to ensure that only one process can refresh a cache entry at a time.
2. **Early Expiration and Lazy Loading**: Set an early expiration time and refresh the cache entry before it fully expires.


<br>

---

**Reference:**

- Li, Yunhua (2018) _Learn Architecture from 0_. Geek Time.

- https://philosophyotaku.medium.com/a-complete-beginner-guide-for-cache-penetration-stampede-avalanche-ecadd7f16009
