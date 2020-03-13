---
title: Distributed databases - basic concepts
date: 2020-03-10 00:31:10 -0800

categories: [Big Data]
tags: [database]
seo:
  date_modified: 2020-03-12 01:31:28 -0700
---

## CAP 

### What is CAP?
* Consistency - Every read receives the most recent write or an error. To be detailed, it is actually Linearizability.
> If operation B started after operation A successfully completed, then operation B must see the the system in the same state as it was on completion of operation A, or a newer state.

* Availability -  Every request received by ``any`` non-failing node in the system must result in a non-error response. Note that errors are usually by design to achieve consitency. 
* Partition tolerance - The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes

CAP means ``you could only choose 2 of these 3``. Since network partition always happen, you could only choose ``CP`` or ``AP``.  Wiki page for [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem). 

### Why CAP

Let’s say you have replicas of your database in two different datacenters. The exact method of replication doesn’t matter for now – it may be ``single-leader (master/slave), multi-leader (master/master) or quorum-based replication (Dynamo-style)``. The requirement of replication is that whenever data is written in one datacenter, it also has to be written to the replica in the other datacenter. Assuming that clients only connect to one datacenter, there must be a network link between the two datacenters over which the replication happens.

Now assume that network link is interrupted – that’s what we mean with a network partition. What happens?


Clearly you can choose one of two things

1. The application continues to be allowed to write to the database, so it remains fully available in both datacenters. However, as long as the replication link is interrupted, any changes that are written in one datacenter will not appear in the other datacenter. This violates linearizability (in terms of the previous example, Alice could be connected to DC 1 and Bob could be connected to DC 2).

2. If you don’t want to lose linearizability, you have to make sure you do all your reads and writes in one datacenter, which you may call the leader. In the other datacenter (which cannot be up-to-date, due to the failed replication link), the database must stop accepting reads and writes until the network partition is healed and the database is in sync again. Thus, although the non-leader database has not failed, it cannot process requests, so it is not CAP-available.


See ref[1] for the proof of CAP. 
### Why CAP is too narrow?
CAP uses ``narrow definitions``

* ``Consistency`` is actually ``linearizabilitily``, which is a very specific notion of consistency. Nothing to do with C in ACID. 

* ``Availabilty``. It’s not sufficient for **some** node to be able to handle the request: any non-failing node needs to be able to handle it. Many so-called “highly available” (i.e. low downtime) systems actually do not meet this definition of availability.

* ``Partition Tolerance``. (terribly mis-named) basically means that you’re communicating over an asynchronous network that may delay or drop messages. The internet and all our datacenters have this property, so you don’t really have any choice in this matter.


Describes a very specific model

* Single read-write register. ``No transactions``. 

* ``Only fault`` considered is network partition.    

* Says nothing about ``latency``. 

Examples

* A asynchronous replicated relational database with single leader is neither CAP-constent nor CAP-available. 

    + asynchronous replication - not CAP-consistent. 

    + cannot write to slave when network is partitioned - not CAP-available. 

* databases with snapshot isolation/MVCC are intentionally non-linearizable, because enforcing linearizability would reduce the level of concurrency that the database can offer. For example, PostgreSQL’s SSI provides serializability but not linearizability, and Oracle provides neither. Just because a database is branded “ACID” doesn’t mean it meets the CAP theorem’s definition of consistency. <WHY?>

* MongoDB - CAP-available by the argument above. And Kyle recently showed that it allows non-linearizable reads even at the highest consistency setting, so it’s not CAP-consistent either.

* Dynamo derivatives like Riak, Cassandra and Voldemort, which are often called “AP” since they optimize for high availability? It depends on your settings. If you accept a single replica for reads and writes (R=W=1), they are indeed CAP-available. However, if you require quorum reads and writes (R+W>N), and you have a network partition, clients on the minority side of the partition cannot reach a quorum, so quorum operations are not CAP-available (at least temporarily, until the database sets up additional replicas on the minority side).
+ You sometimes see people people claiming that quorum reads and writes guarantee linearizability, but I think it would be unwise to rely on it – subtle combinations of features such as sloppy quorums and read repair can lead to tricky edge cases in which deleted data is resurrected, or the number of replicas of a value falls below the original W (violating the quorum condition), or the number of replica nodes increases above the original N (again violating the quorum condition). All of these lead to non-linearizable outcomes.

We should stop putting datastores into the “AP” or “CP” buckets, because:
* Within one piece of software, you may well have various operations with different consistency characteristics.
* Many systems are neither consistent nor available under the CAP theorem’s definitions. However, I’ve never heard anyone call their system just “P”, presumably because it looks bad. But it’s not bad – it may be a perfectly reasonable design, it just doesn’t fit one of the two CP/AP buckets.
* A huge amount of subtlety is lost by putting a system in one of two buckets. There are many considerations of fault-tolerance, latency, simplicity of programming model, operability, etc. that feed into the design of a distributed systems. It is simply not possible to encode this subtlety in one bit of information. For example, even though ZooKeeper has an “AP” read-only mode, this mode still provides a total ordering of historical writes, which is a vastly stronger guarantee than the “AP” in a system like Riak or Cassandra – so it’s ridiculous to throw them into the same bucket.
* Even Eric Brewer admits that CAP is misleading and oversimplified. In 2000, it was meant to start a discussion about trade-offs in distributed data systems, and it did that very well. It wasn’t intended to be a breakthrough formal result, nor was it meant to be a rigorous classification scheme for data systems. 15 years later, we now have a much greater range of tools with different consistency and fault-tolerance models to choose from. CAP has served its purpose, and now it’s time to move on.

### Conclusion 
 CAP theorem in most cases is a high-level abstraction that can’t be applied to the systems you write or use but can be a starting point for understanding more complex cases.

## Consistency
### What is consistency and why we need consistency?

Consistency is an agreement between clients and data.

### Consistency model

* Strict consistency - All writes are instantaneously visble to all proceses. Relies on ``absolute global time``. 
* Linearizability/ Atomic consistency
    + weaker than strict consistency, stronger than sequential consistency
    +  operations are assumed to receive a timestamp with a global available clock that is loosely synchronized
    + In addition, if tsop1(x) < tsop2(y), then OP1(x) should precede OP2(y) in this sequence.“ [Herlihy & Wing, 1991]
* Sequential consistency - the result of any excution is the same as if the read and write operations by all processes were executed in some sequential order.  Any valid interleaving is legal but all processes must see the same interleaving.
* Causal consistency - writes that are potentially causally related must be seen by all processes in the same order. Concurrent writes may be seen in a different order on different machines.
* FIFO consistency - Necessary Condition: Writes done by a single process are seen by all other processes in the order in which they were issued, but writes from different processes may be seen in a different order by different processes.

## Replication
### Why replication? What is the motivation?
* Performance enhancement
* Enhanced availability
* Fault tolerance
* Scalability

Tradeoff between benefits of replication and work required to keep replicas consistent


### What requirements does replicaiton should satisfy?
* Consistency - depends on application
* Replica transparency - desirable for different applications

## Partitioning (sharding)

* Consistent hashing - https://www.toptal.com/big-data/consistent-hashing 

## Consensus

### What is Consensus?

Consensus typically arises in the context of ``replicated state machines``, a general approach to building ``fault-tolerant`` systems. Each server has a state machine and a log. The state machine is the component that we want to make fault-tolerant, such as a hash table. It will appear to clients that they are interacting with a single, reliable state machine, even if a minority of the servers in the cluster fail.


``Log -> state machine``:  Each state machine takes as input commands from its log. In our hash table example, the log would include commands like set x to 3. A consensus algorithm is used to agree on the commands in the servers’ logs. The consensus algorithm must ensure that if any state machine applies set x to 3 as the nth command, no other state machine will ever apply a different nth command. As a result, each state machine processes the same series of commands and thus produces the same series of results and arrives at the same series of states.





``Why consensus?``
* replicated state machines are used to solve a wide range of fault tolerance problemsn in distributed systems. 
* Examples, GFS/HDFS uses it to manage leader selection and store configuraiton information that must survive leader crash. 

### Raft algorithm
Featuress
* Single leader. 

Properties of consesus algorithms

## Time and order
When we have a sequence of events occurred in a distributed system, it’s important to know in what order they came. We can’t rely on physical clocks because it’s always not perfectly synchronized. That’s why people came up with logical clocks.

Logical clocks are not about actual time, it’s about an order of events, it’s also called a partial ordering. In this model, all events are connected by happens-before relation. There are two implementations of this model:

* Lamport timestamps - https://amturing.acm.org/p558-lamport.pdf

* Vector Clocks - https://en.wikipedia.org/wiki/Vector_clock



How you decide whether an event happened before another event in the absence of any shared clock. This means Lamport clocks and their generalisation to Vector clocks, but also see the Dynamo paper.



## Failure modes

The (partial) hierarchy of failure modes: crash stop -> omission -> Byzantine. You should understand that what is possible at the top of the hierarchy must be possible at lower levels, and what is impossible at lower levels must be impossible at higher levels.


## Broadcast

Difference between atomic broadcast and consensus
* In practical terms, Atomic Broadcast discussions explicitly talk about sending multiple messages in an agreed-upon order, where Consensus discussions have historically talked about agreeing on only one value, and then abstracting that to multiple messages (



# Next steps
* What is quorum read/writes? R+W > N
* What is ``Byzantine conditions``?
https://en.wikipedia.org/wiki/Byzantine_fault