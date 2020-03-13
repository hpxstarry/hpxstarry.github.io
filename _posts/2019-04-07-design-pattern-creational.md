---
title: Desgin patterns - creational design patterns
date: 2019-04-17 00:31:10 -0800

categories: [Design Pattern]
tags: [design pattern]
seo:
  date_modified: 2020-03-12 23:31:07 -0700
---

# Introduction
In this blog, we are going to talk about creational design patterns, such as Abstract Fatory, Builder. With this blog, you would be able to answer questions such as
* What is the difference between Builder, Abstract Factory, Factory?

# Creational design patterns
## Abstract factory

## Factory method

## Builder

The Builder design pattern describes how to solve such problems:

* Encapsulate creating and assembling the parts of a complex object in a separate Builder object.
A class delegates object creation to a Builder object instead of creating the objects directly.
A class (the same construction process) can delegate to different Builder objects to create different representations of a complex object.


## Prototype
## Singleton

# Descrption of Factory and Builder

They are both design patterns

https://stackoverflow.com/questions/757743/


# Differences
what-is-the-difference-between-builder-design-pattern-and-factory-design-pattern

Gamma design patterns 1995.

From Wikipedia:

Builder focuses on constructing a complex object step by step. Abstract Factory emphasizes a family of product objects (either simple or complex). Builder returns the product as a final step, but as far as the Abstract Factory is concerned, the product gets returned immediately.

Builder often builds a Composite.

Often, designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed.

Sometimes creational patterns are complementary: Builder can use one of the other patterns to implement which components get built. Abstract Factory, Builder, and Prototype can use Singleton in their implementations.

Wikipedia entry for factory design pattern: http://en.wikipedia.org/wiki/Factory_method_pattern

Wikipedia entry for builder design pattern: http://en.wikipedia.org/wiki/Builder_pattern

# When to use constructor, factory, builder?

# References
* Gamma, design patterns, 1995
* https://en.wikipedia.org/wiki/Builder_pattern
