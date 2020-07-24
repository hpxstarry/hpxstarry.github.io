---
title: A map for distributed systems
date: 2020-03-10 00:31:10 -0800

categories: [Big Data, Tutorial]
tags: [bigdata]
seo:
  date_modified: 2020-07-12 23:31:07 -0700
---

For the past 5 years, I have been using different kinds of distributed systems to solve production problems. Have read some books, paper, blogs. Maintained Hadoop, HBase cluster for some time. Now I am writing this blog to summarize for myself. It will act like an indexing of different blogs, books, paper, links. As a disclaimer, distributed systems are complicated and this blog is far less able to cover all.

Github already has a similar page that listed related resources for distributed systems.
* https://github.com/theanalyst/awesome-distributed-systems 

# Tutorials
## Blogs
* [Distributed systems for fun](http://book.mixu.net/distsys/single-page.html)
* [A Thorough Introduction to Distributed Systems](https://www.freecodecamp.org/news/a-thorough-introduction-to-distributed-systems-3b91562c9b3c/)
* [Distributed systems theory for the distributed systems engineer](https://www.the-paper-trail.org/post/2014-08-09-distributed-systems-theory-for-the-distributed-systems-engineer/)
* [Distributed system cheetsheet](http://dimafeng.com/2016/12/04/distributed-systems/)

# Overall Resources
## Books
* Designing Data-Intensive Application
* Jepsen — Blog explaining a lot of distributed technologies (ElasticSearch, Redis, MongoDB, etc)
* [No SQL database](http://www.christof-strauch.de/nosqldbs.pdf)
* https://leanpub.com/distributed-systems-for-practitioners

## Paper
* [papers we love - distributed systems]](https://github.com/papers-we-love/papers-we-love/tree/master/distributed_systems)
* [Lamport paper](http://lamport.azurewebsites.net/pubs/pubs.html)

## Courses
* Cloud Computing Specialization, University of Illinois, Coursera — A long series of courses (6) going over distributed system concepts, applications ?


# Distributed systems categories

![image](/assets/img/blog/distributed_systems_overview.png)

# Concepts
## Failing mode
* ``Byzantine fault modle`` - Comes from the Byzantine generals problem invented by Lamport. To put it simple, some of the nodes within a cluster may not be reliable that they may **present different symptoms to different observers** to cause the failure of reaching a concensus among the cluster.  

See more
* https://en.wikipedia.org/wiki/Byzantine_fault
* https://academy.binance.com/blockchain/byzantine-fault-tolerance-explained 

* ``crash-recovery failure model`` - In practice, most systems assume a crash-recovery failure model: that is, nodes can only fail by crashing, and can (possibly) recover after crashing at some later point.

## Consensus

Frameworks
* [RAFT](https://raft.github.io/)

## Consistency

* [CMU Consitency slide](http://www.cs.cmu.edu/~srini/15-446/S09/lectures/10-consistency.pdf)

## Replication

Blog
* https://blog.yugabyte.com/how-does-consensus-based-replication-work-in-distributed-databases/


Replication - Theory and Practice - effective replication is the heart of modern distributed systems and this theme is covered well in this book.
Introduction to Distributed Algorithms: Gerard Tel: 9780521794831: Amazon.com: Books - this book has very deep theoretical explanation of classical distributed algorithms.


## Partition


* Consistent Hash Rings Explained Simply • Ax's Findings
* Consistent hashing, a guide & Go implementation – Senthil – Medium

## Time and order

* [Blog](https://www.microsoft.com/en-us/research/uploads/prod/2016/12/Time-Clocks-and-the-Ordering-of-Events-in-a-Distributed-System.pdf)

## CAP
* https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html


