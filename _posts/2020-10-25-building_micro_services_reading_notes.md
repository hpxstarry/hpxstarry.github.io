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


## Q: What are the pros of microservice architecture?

## Q: What are the cons of microservice architecture?

## Q: What are the best practises?

## Q: Traditional patterns of microservice architecture?

## Q: From a techinical point of view, how to implement microservice architecture?

## Q: How to migrate from monolithic architecture to microservice architecture?

## Q: For further readings, what books to recommend?

# References
* Microservice vs SOA - https://www.ibm.com/cloud/blog/soa-vs-microservices
