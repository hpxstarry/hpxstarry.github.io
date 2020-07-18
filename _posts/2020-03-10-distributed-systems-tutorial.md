---
title: Distributed systems tutorial
date: 2020-03-10 00:31:10 -0800

categories: [Big Data, Tutorial]
tags: [bigdata]
seo:
  date_modified: 2020-07-12 23:31:07 -0700
---

For the past 5 years, I have been using different kinds of distributed systems to solve production problems. Have read some books, paper, blogs. Maintained Hadoop, HBase cluster for some time. Now I am writing this blog to summarize for myself. It will act like a tutorial or an indexing for distributed systems. As a disclaimer, distributed systems are complicated and this blog is far less be able to cover all. Any specific section worths being discussed separately in a blog or even a book. 

# Basic FAQs

## What is a distributed system?
To put it simple, a distributed system is a group of computers working together to appear as one single computer to provide some services, such as data storage, computation, etc. 


## Why are distributed systems needed?
Building/maintaining a distributed system is complicated, full of pitfalls and landmines. But nevertheless distributed systems are still required and becoming extermely popular because of serveral reasons. 
1.  ``Scalability``. Scalability is the ability of a system to handle a growing amount of work in a capable manner or its ability to be enlarged to accommodate that growth. Previous tradition way to support this is to  **scale vertically**. For example, purchase a better server with larger memory, more CPU cores, etc. However, it has a physcial limit and also the cost does not increase linerly with the scale. In distributed systems, it **scales horizontally**, where a bunch of cheap servers can be combined togther to support growing needs. With this way, it can easily breaks the physcial limit of vertical scale; the cost spent on servers is also linear. 
2. ``Availability and fault Tolerance`` — Distributed systems also enable higher availability that your application/service will continue to work even some machines failed. Today a lot of distributed systems are built on top of more than two data centers that even one data center catches fire, the applications on top of it still works. 
3. ``Low Latency`` — The time for a network packet to travel the world is physically bounded by the speed of light. For example, the shortest possible time for a request‘s round-trip time (that is, go back and forth) in a fiber-optic cable between New York to Sydney is 160ms. Distributed systems allow you to have a node in both cities, allowing traffic to hit the node that is closest to it.

# Distributed systems categories

![image](/assets/img/blog/distributed_systems_overview.png)

## Distributed computing
**Frameworks**
* MapReduce - Consisting of two stages of map and then reduce. See [link](https://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html) for details. 
* Spark - runs in memory or disk (claims to be 100x faster in memory, 10x faster in disk comparing to Hadoop); not limited to the two-stage paradigm of MapReduce. 
* Streamed processing

**Products**
* Hadoop
* Apache Spark
* Pig, Hive
* Apache Spark Streaming
* Apache Flink
* Apache Storm
* Kafka Streams
* Apache Samza

## Distributed database
**Products**


## Distributed cache

## Distributed file systems

## Distributed messaging

## Distributed ledger
* Blockchain
* Bitcoin

# Concepts
## ``Byzantine fault``
A Byzantine fault (also interactive consistency, source congruency, error avalanche, Byzantine agreement problem, Byzantine generals problem, and Byzantine failure) is a condition of a computer system, particularly distributed computing systems, where components may fail and there is imperfect information on whether a component has failed. The term takes its name from an allegory, the "Byzantine Generals Problem", developed to describe a situation in which, in order to avoid catastrophic failure of the system, the system's actors must agree on a concerted strategy, but some of these actors are unreliable [1]. In a Byzantine fault, a component such as a server can inconsistently appear both failed and functioning to failure-detection systems, **presenting different symptoms to different observers**. It is difficult for the other components to declare it failed and shut it out of the network, because they need to first reach a consensus regarding which component has failed in the first place.

``Byzantine fault tolerance (BFT)`` is the dependability of a fault-tolerant computer system to such conditions.  

[1] https://en.wikipedia.org/wiki/Byzantine_fault
[2] https://academy.binance.com/blockchain/byzantine-fault-tolerance-explained 

# Reading
## Books
* Designing Data-Intensive Application
* Cloud Computing Specialization, University of Illinois, Coursera — A long series of courses (6) going over distributed system concepts, applications ?
* Jepsen — Blog explaining a lot of distributed technologies (ElasticSearch, Redis, MongoDB, etc)

## Papers
[https://github.com/papers-we-love/papers-we-love/tree/master/distributed_systems](https://github.com/papers-we-love/papers-we-love/tree/master/distributed_systems)

# References
1. https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html
2. Designing data-intensive applications. 
3. https://blog.yugabyte.com/how-does-consensus-based-replication-work-in-distributed-databases/
4. RAFT - [https://raft.github.io/](https://raft.github.io/)
5. Consitency slide - [http://www.cs.cmu.edu/~srini/15-446/S09/lectures/10-consistency.pdf](http://www.cs.cmu.edu/~srini/15-446/S09/lectures/10-consistency.pdf)
6. Lamport papers - http://lamport.azurewebsites.net/pubs/pubs.html
7. Distributed systems for fun - http://book.mixu.net/distsys/single-page.html
8. Time and order - https://www.microsoft.com/en-us/research/uploads/prod/2016/12/Time-Clocks-and-the-Ordering-of-Events-in-a-Distributed-System.pdf
9. https://en.wikipedia.org/wiki/Byzantine_fault
10. Distributed systems cheat sheet
http://dimafeng.com/2016/12/04/distributed-systems/
11. A Thorough Introduction to Distributed Systems - https://www.freecodecamp.org/news/a-thorough-introduction-to-distributed-systems-3b91562c9b3c/
12. Distributed systems theory for the distributed systems engineer - https://www.the-paper-trail.org/post/2014-08-09-distributed-systems-theory-for-the-distributed-systems-engineer/

