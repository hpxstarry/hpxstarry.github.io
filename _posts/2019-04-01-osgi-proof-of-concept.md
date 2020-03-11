---
layout: post
title:  OSGi - quick introduction & investigation
date:   2019-04-01 11:15:15 -0800
categories: osgi
---

# Introduction
This blog is going to talk about OSGi. Target of this blog aims to help people
* Get an overall understanding of OSGi.
* Evaluate whether OSGI is a good alternative to solve their problems.


# FAQ
## What is OSGI?
OSGi (Open Service Gateway Initiative) is a Java framework for developing and deploying modular software programs and libraries.

OSGi has two parts. The first part is a specification for modular components called bundles, which are commonly referred to as plug-ins. The specification defines an infrastructure for a bundle's life cycle and determines how bundles will interact.  The second part of OSGi is a Java Virtual Machine (JVM)-level service registry that bundles can use to publish, discover and bind to services in a service-oriented architecture (SOA).

The work behind OSGi began in 1999 when embedded systems vendors and networking providers came together to create a set of standards for a Java-based service framework that could be managed remotely. OSGi was originally conceived to be a gateway for managing smart appliances and other Internet-enabled devices in the home. The gateway consisted of a Java software framework embedded in a hardware platform such as a cable modem or set-top box. The framework acted as the central message broker for the device on the home's local area network (LAN). The goal, in essence, was to create a standardized middleware for smart devices and make managing cross-dependencies easier for software developers.

## How micro-service is supported?
Code deployment?
In the same process?

Package conflicts? Dependencies?
https://enroute.osgi.org/FAQ/200-resolving.html

classloader

https://dzone.com/articles/osgi-bundle-communication

## What features does OSGI provide?

## What limitations does OSGI have?

## What the pros and cons of OSGI, comparing to docker, Amazon ECS?


## Any good examples?


# References
* https://www.osgi.org/
* https://www.osgi.org/developer/where-to-start/