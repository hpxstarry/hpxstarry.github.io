---
title: Reading nots of "building microservices"
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
* Small - Several factors to consider: 1) time to rewrite the whole; 2) whether it aligns and fits the team structure; 3) no longer feels to be big; 4) trade offs between the benefits and complexities. 
* Autonomous - change independently; decoupled from each other; deployed separately.  

## Q: What is the difference between microservice architecture and service oriented architecture (SOA)?
1) scope - SOA is usually adopted enterprise-wide while microservices are typically used to build individual applications, i.e., to further decompose applications (services) to micro services.
2) reuse - reuse of integrations is the primary goal of SOA while microservices prefers to decoupling and sometimes even copy code or duplicate data to achieve that. 
3) call pattern - SOA usually uses synchronous calls while microservice can have different call patners and asynchronous communication is popular. 
4) date duplication - Usually SOA applications will get hold of or make changes to data directly at its primary source. Microservices may have duplicated local data for decoupling. 

Another way to think of microservices as a specific approach for SOA in the same way that XP or
Scrum are specific approaches for Agile software development.

## Q: What are the pros of microservice architecture?
* Technology heterogeneity - different parts of the system can adopt different tech stacks. We can optimize the performance with different tech separately; it also enables faster adoption of new tech. But it also introduces overhead to use multiple tech stacks. 
* Resilience - With service boundaries being the obvious bulkheads, microservices can help isloate problems and improve resilience. 
* Scaling - Independent scaling. Scale only the services that need scaling while other parts run on smaller, less powerful hardware. 
* Ease of deployment - Independent, small-impact, low-risk, faster deployment. 
* Organization alignment - Allow us to better align architecture with organization. Easier to shift ownership. 
* Composability - Microservices allow for functionality to be consumed in different ways for different purposes. 
* Optimizing for replaceability - With services being small, it is easier to rewrite the whole service or deprecate/kill it when required. 

## Q: What are the cons of microservice architecture?
* Complexity - added complexity to manage distributed systems; need to handle issues related to communication erros, API versioning, etc. 
* Modeling - if not modeled well, changes need to update multiple micro services, which takes more time to develop, test and deploy. 
* Debug - debugging involes multi services and takes more time. 
* DevOps - additional efforts to achive engineering/operation excellence, such as full CI/CD pipelines, metrics/monitoring, etc. 
* Code duplication - microservices usually duplicates shared code in different microservices. 

## Q: Microservice is a way to decomposite systems. What are other ways?
* Shared libraries
* Modules - OSGi in Java. 

## Q: What are the pitfalls?
* Shared database

## Q: What are the best practises?
* Model services using domain driven design (DDD). 

## Q: Patterns of microservice architecture?

## Q: How microservices are integrated? What are the common ways?
* Sync - request/response
* Async - event based

## Q: From a techinical point of view, how to implement microservice architecture?

## Q: How to migrate from monolithic architecture to microservice architecture?

## Q: For further readings, what books to recommend?

# References
* Microservice vs SOA - https://www.ibm.com/cloud/blog/soa-vs-microservices
