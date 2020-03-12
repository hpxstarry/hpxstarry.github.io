---
title: "Distributed systems tutorial"
date:  2020-03-10 00:31:10 -0800

categories: [bigdata]
tags: [bigdata]
---

For almost 3 years, I have been using different kinds of distributed systems to solve production problems within my work. I investigated paper, books; researched the documents of distirbuted products, such as Hadoop, Spark, HBase. This gets me to think about one question, can we have a tutorial to distributed systems, introducing the common challenges, the frequently used trade-offs, different products and their relationships. So I wrote this blog. 

## 什么是分布式系统？
A distributed system in its most simplest definition is a group of computers working together as to appear as a single computer to the end-user.

These machines have a shared state, operate concurrently and can fail independently without affecting the whole system’s uptime.

## 为什么需要分布式系统？
Systems are always distributed by necessity. The truth of the matter is — managing distributed systems is a complex topic chock-full of pitfalls and landmines. It is a headache to deploy, maintain and debug distributed systems, so why go there at all?

1.  ``Scalability``. Scalability is the ability of a system, network, or process, to handle a growing amount of work in a capable manner or its ability to be enlarged to accommodate that growth. What a distributed system enables you to do is **scale horizontally**.  Going back to our previous example of the single database server, the only way to handle more traffic would be to upgrade the hardware the database is running on. This is called **scaling vertically**. Scaling vertically is all well and good while you can, but after a certain point you will see that even the best hardware is not sufficient for enough traffic, not to mention impractical to host. Scaling horizontally simply means adding more computers rather than upgrading the hardware of a single one. It is significantly cheaper than vertical scaling after a certain threshold but that is not its main case for preference. Vertical scaling has performance cap while horizontal scaling has no upper bound: vertical scaling can only bump your performance up to the latest hardware’s capabilities. These capabilities prove to be insufficient for technological companies with moderate to big workloads. The best thing about horizontal scaling is that you have no cap on how much you can scale — whenever performance degrades you simply add another machine, up to infinity potentially. Easy scaling is not the only benefit you get from distributed systems. Fault tolerance and low latency are also equally as important.
2. ``Fault Tolerance`` — a cluster of ten machines across two data centers is inherently more fault-tolerant than a single machine. Even if one data center catches on fire, your application would still work.
3. ``Low Latency`` — The time for a network packet to travel the world is physically bounded by the speed of light. For example, the shortest possible time for a request‘s round-trip time (that is, go back and forth) in a fiber-optic cable between New York to Sydney is 160ms. Distributed systems allow you to have a node in both cities, allowing traffic to hit the node that is closest to it.

For a distributed system to work, though, you need the software running on those machines to be specifically designed for running on multiple computers at the same time and handling the problems that come along with it. This turns out to be no easy feat.

# Distributed systems categories

![image](/assets/images/distributed_systems_overview.png)

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

