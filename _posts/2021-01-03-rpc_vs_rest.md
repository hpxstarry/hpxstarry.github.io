---
title: RPC vs REST
date: 2021-01-04 00:31:10 -0800
published: true

categories: [microservices]
tags: [design]
seo:
  date_modified: 2021-01-04 23:40:26 -0800
---
>

Services (or applications, micro-services) need to interact/integrate with each other to deliver a business functionality. 

There are two patterns for service to service interaction. 
1. ``Synchronous`` - a call is blocked until the operation completes
    * Easy to reason about
    *  Easy to implement
2. ``Asynchronous`` - a call is not blocked
    *  Servers not need to respond immediately - good for IO bound activities, long-running or long-polling jobs, service proxies
    *  Clients are not blocked - good UX for websites, phone apps
    * Loosely couping - service and client no need to be available on the same time

``Request-reply`` is one of the most popular styles. 
1. Synchronous - in most cases, request-reply is used for synchronous interaction. 
2. Asynchronous
      + StartAsyncTask, GetTaskStatus, GetResultFromTask 
      + Server calls back when task finishes 

**What are the challengs of service to service interaction/integration and what matters?** 

Fundamental Challenges
 1. Network are unreliable and slow. 
 2. Any two applications are different. 
 3. Change is inevitable. 

What matters
1. Loosely coupling between applications
1. Strong cohesion within an application 
1. Easy to change - hide internal implementation details
1. Avoid breaking changes
1. An application is simple to use for consumers
1. Technology agnostic

**What is RPC?**
RPC stands for Remote Procedure Call
  1.  Running remote procedure calls like local calls
  1.  Requires a client stub
  1.  Can be on top of HTTP, TCP, UDP
  1.  Request/response will be serialized (marshal) to wire formats

![image](/assets/img/blog/rpc.png)

**What is REST?** 
REpresentational State Transfer - an architectural style of HTTP with below \hreff{https://en.wikipedia.org/wiki/Representational_state_transfer}{6 principles/constraints}
  1.  Uniform interface
    \begin{itemize}
      1.  Resource identification in requests
      1.  Resource manipulation through representations
      1.  Self-descriptive messages
      1.  Hypermedia as the engine of application state (HATEOAS)
    \end{itemize}
  1.  Client-server architecture
  1.  Statelessness
  1.  Cacheability
  1.  Layered system
  1.  Code on demand

## REST vs RPC
RPC
  1.  Operation-centric (more operations required for resource CRUD)
  1.  Use protocols including HTTP, TCP, UDP (able to achieve higher efficiency)
  1.  With HTTP, usually uses GET, POST verb only 
  1.  Cache - good cache support in some frameworks

REST 
  1.  Resource-centric (concise, consistent if designed well)
  1.  HTTP only (may not be appropriate for latency sensitive applications)
  1.  Use GET, POST, PUT, DELETE HTTP verbs
  1.  Cache - mostly for GET, HTTP cache support


## Implementations
### RPC implementations
Popular frameworks for RPC
  1.  Amazon coral framework
  1.  \hreff{https://grpc.io/docs/what-is-grpc/introduction/}{gRPC} - developed by google, open source. 
  1.  SOAP (Simple Object Access Protocol) 
  1.  \hreff{https://thrift.apache.org/}{Apache Thrift} - developed by Facebook, open source. 
  1.  RPyC

Amazon coral framework
1.  First-class Java support. 
1.  Apollo/Brazil internal integration. 
1.  Endpoint - Bobcat, JLBRelay/CDORelay, Netty, Lambda, ...
1.  Wire format agnostic, support multiple formats/protocols, Coral-RPC, AWS JSON, HttpBinding, ... 
1.  Client generation in Java, Ruby, Python, ... 
1.  interface definition language - Coral Model, Smithy. 
1.  Powerful tooling such as Metrics, Diver, Throttling, ... 
1.  Streaming support for both request/response (streaming support is still new in Coral). 
1.  Async support with Continuation Activity


gRPC
![image](/assets/img/blog/grpc.png)
1.  Protocl Buffers as both the wire format and IDL
1.  HTTP/2 by default
1.  Streaming support 
1.  Build-in timeout support
1.  Rich lanaguage support - C\#, C++, Go, Java, Objective-C, ...
1.  Async support

REST implementations
  1.  Amazon ARest
  1.  Amazon Coral w/t HTTP endpoint binding
  1.  OpenAPI (Swagger)
  1.  JAX-RS


Interface definition language - IDL
  1.  Smithy
  1.  OpenAPI
  1.  WSDL - usually used together by SOAP
  1.  Protocol Buffer
  1.  Thrift


**Further readings**
1. HTTP protocol