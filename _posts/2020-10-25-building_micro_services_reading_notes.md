---
title: Bbuilding microservices - reading notes
date: 2020-10-24 00:31:10 -0800

categories: [microservices]
tags: [design]
seo:
  date_modified: 2020-10-24 23:40:26 -0800
---
>

# FAQ
## Q: What is microservice? 
Microservices are ``small``, ``autonomous`` services that work together. 
1. Small - Several factors to consider: 1) time to rewrite the whole; 2) whether it aligns and fits the team structure; 3) no longer feels to be big; 4) trade offs between the benefits and complexities. 
2. Autonomous - change independently; decoupled from each other; deployed separately.  

## Q: What is the difference between microservice architecture and service oriented architecture (SOA)?
1. scope - SOA is usually adopted enterprise-wide while microservices are typically used to build individual applications, i.e., to further decompose applications (services) to micro services.
2. reuse - reuse of integrations is the primary goal of SOA while microservices prefers to decoupling and sometimes even copy code or duplicate data to achieve that. 
3. call pattern - SOA usually uses synchronous calls while microservice can have different call patners and asynchronous communication is popular. 
4. date duplication - Usually SOA applications will get hold of or make changes to data directly at its primary source. Microservices may have duplicated local data for decoupling. 

Another way to think of microservices as a specific approach for SOA in the same way that XP or
Scrum are specific approaches for Agile software development.

## Q: What are the pros of microservice architecture?
1. Technology heterogeneity - different parts of the system can adopt different tech stacks. We can optimize the performance with different tech separately; it also enables faster adoption of new tech. But it also introduces overhead to use multiple tech stacks. 
1.  Resilience - With service boundaries being the obvious bulkheads, microservices can help isloate problems and improve resilience. 
1.  Scaling - Independent scaling. Scale only the services that need scaling while other parts run on smaller, less powerful hardware. 
1.  Ease of deployment - Independent, small-impact, low-risk, faster deployment. 
1.  Organization alignment - Allow us to better align architecture with organization. Easier to shift ownership. 
1.  Composability - Microservices allow for functionality to be consumed in different ways for different purposes. 
1.  Optimizing for replaceability - With services being small, it is easier to rewrite the whole service or deprecate/kill it when required. 

## Q: What are the cons of microservice architecture?
1.  Complexity - added complexity to manage distributed systems; need to handle issues related to communication erros, API versioning, etc. 
1.  Modeling - if not modeled well, changes need to update multiple micro services, which takes more time to develop, test and deploy. 
1.  Debug - debugging involes multi services and takes more time. 
1.  DevOps - additional efforts to achive engineering/operation excellence, such as full CI/CD pipelines, metrics/monitoring, etc. 
1.  Code duplication - microservices usually duplicates shared code in different microservices. 

## Q: Microservice is a way to decomposite systems. What are other ways?
``Shared libraries`` - breakdown code base into multiple libraries. 

Drawbacks
  + Lost technology heterogeneity - library usually is used by same language. 
  + Reduced ability to scale parts independently
  + Reduced ability to deploy parts independently
  + Shared code used to communicate becomes a point of coupling
  + Everything in the lib can be potentially used, causing the lib hard to change
  + Lack obvious seams around which to erect architectual safty measures to ensure system resiliency 

Notes
  + Breaking down code base into libraries is a regular practice to decompose an existing monolithic service into microservices. 

``Modules`` - Provided by some languages for modual decomposition that go beyonds simple libraries. Allow for lifecycle management of the modules so that it can be deployed to a running process without taking it down. 
+ OSGi in Java - emerged as a framework to allow plugins in eclipse. 
+ Java 9 module. Difference between OSGi and Java 9 module - https://www.infoq.com/articles/java9-osgi-future-modularity/
+ Erlang support module - impressive support for module. 
Module address the independently deployable concern of libraries

Drawbacks 
  - OSGi tries to enforce lifecycle management without good support from language itself
  - Without clear boundary, easier to fall into the trap of overly coupled modules. 
  - Same problem for technology heterogeneity with library
  - Same problem for scale parts independently with library
  - Same problem for resiliency

  
## Q: How microservices are integrated? What are the common ways?
* Synchronous vs Asynchronous 
  + Request/response - a client initiates a request and waits for a resonse.
    + Mostly used for synchronous communication. 
    + Can also be used for asynchronous communication. Client can kick off an operation and register a callback. Examples are facebook APIs 
  * Event based - one party produces events, other parties listen to events and take actions. Asynchronous; highly decoupled.
* Orchestration vs Choreography - a process that stretch across the boundary of individual services; usually consists of multiple steps of invocation.
  + Orchestration - rely on a central brain to guide and drive the process of a flow. Usually work with services with synchronous model. 
    + Pros: easy to understand, monitor and track
    + Cons: the orchestration flow acts as a god father and may introduce additional coupling 
  + Choreography - inform each part of the system the job and let it work out the details. Works in a distributed way that each part (service) act separately based on the request or event it receives. Usually depend on that the services collaborates with aynchronous events. 
    + Pros: more loosely coupled, more flexible and amendble to change. 
    + Cons: the process or flow is implicit. Needs additional work to monitor and track. 
* RPC - remote procedure call. Implementations include SOAP (HTTP+XML). Usually relies on having an interface definition (SOAP, Thrift, protocol buffer) while java RMI does not rely on it. Web Service Definition Language (WSDL) can help generate client. Can run on top of different protocols with different serialization/deserialization techniques. 
    + Cons: technical coupling (for example, RMI); remote call is not like local call; brittleness to add/remove fields. 
* REST - REST (REpresentational State Transfer) is an architectual style for building web service interfaces. Mostly commonly used over HTTP.
    + Pros: default choice for service-to-service integration
    + Cons: cannot easily generate client stub; some web server frameworks don't support all the HTTP verbs well; performance may also be an issue (HTTP overhead might be a concern for low-latency requirements)
* Implementing event-based collaboration
  + Technical choices - middeware like RabbitMQ (handle subscriptions, even handle states of consumers), events over HTTP (ATOM), message broker. 

## Q: What are the pitfalls?
* Bad integration pattern - use shared database as integration point. Large blast radius; hard to change; tied to specific technology choice. 
* Microservices not modeling well around domain boundaries. 

## Q: What are the best practises?
* Model services using domain driven design (DDD). 

## Q: Patterns of microservice architecture?

## Q: Technical frameworks/services to implement microservice architecture?
* ECS
* EKS
* Kafka

## Q: How to migrate from monolithic architecture to microservice architecture?

# References
* Microservice vs SOA - https://www.ibm.com/cloud/blog/soa-vs-microservices
* REST - https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm
* Enterprise integration patterns 
