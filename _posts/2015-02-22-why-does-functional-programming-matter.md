---
layout: post
title: "Why does functional programming matter?"
modified:
categories: 
excerpt: Like any other missing feature in any programming language imperative programming languages address these problems by making more libraries with complex interfaces. Likewise any built-in language supported feature can result in code clarity, elegance and maintainability and leave the responsibility of optimization and other concerns to programming language in order to have programmers focus on their problems. 
tags: [functional programming]
image:
  feature: sample-image-3.jpg
date: 2015-02-22T20:10:39-05:00
---
<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->


## Overview
As software constructs are getting more complicated it’s evident that programming languages must come up with new techniques for modularity, separation of concerns to improve maintainability. Like any other missing feature in any programming language imperative programming languages address these problems by making more libraries with complex interfaces. Likewise any built-in language supported feature can result in code clarity, elegance and maintainability and leave the responsibility of optimization and other concerns to programming language in order to have programmers focus on their problems. 

## No side effects
Emergence of vast diverse type of dependency injection frameworks is the evidence that all in conventional programming languages there’s a more need for separation of primitive language types, which are primarily classes and objects. Not only existence of global variables and static variables in conventional programming languages makes program hard to debug and maintain they made dependency between software constructs too transparent so it’s hard to justify if a particular module of program is modular enough. In pure functional programming languages it’s guaranteed that every function can be tested and verified in isolation of rest of program so software bugs can be replicated and resolved in function resolution.  

## Lazy-evaluation 
Having hardware support for features like “Page Faults” in MMU in even hardware level it are apparent this lazy-evaluation features must exist as first-class constructs in programming languages. Lazy-evaluation is important not only because of saving some more CPU cycles but its significance can be viewed as a facility to add more layers of abstraction without developing more performance concerns. Most software engineering practices advocate the usage of abstraction throughout different levels of abstraction but the trade-off to keep modules as general as possible and performance wise at the sometime is challenging. Mainly lower levels libraries have no clear idea that what evaluations and operations might be needed later by high-level applications. 
Parameterizing library interfaces, to specify the exact requirements (which makes library interface even more complicated) or sacrificing performance seem to be the only solution to this issue in conventional programming languages. 

## High order functions
Higher-order functions and lambda expressions allow making structures regardless of control flow of that structure. One example might condition to verify certain element of a list must be iterated can be isolated from iteration algorithm itself. This feature like lazy-evaluation can contribute to layered software design as higher levels of software can still maintain control flow flexibility with no need to sacrifice performance or modularity by passing the required control flow as a parameter to lower levels.

## Emergence of new hardware platforms
We have seen emergence of more multicore processors due to the fact that semiconductors companies are reaching to processors speed limit to avoiding power consumption problem by scaling processor frequency and other problems. Meanwhile graphic processor manufactures claim their products have much more potential for general-purpose computing than any other type of processors.  On the other hand, recent studies show that FPGA can outperform specific tasks easily.

No-side effect of functional languages ideal for parallel computing as function constructs are stateless there won’t be any race conditions anymore and consequently no locking costs. Immutability of data in functional programming languages allows sharing data easily across core in general-purpose processors and graphic processors without having concurrency concerns.

Taking into account embedding feature of domain-specific languages into account and the fact all hardware description languages are merely another representation of mathematical functions. Functional meta-programming languages seem to be ideal candidate for embedding hardware description languages. They also certainly seem to be potentially a worthy candidate to be a cross-hardware-platform for computation intensive problems as they capture abstract-enough definition of problem and this leaves a lot of room for optimizations and platform migration by programming language and provided libraries. 

## Lambda-expression Parsing
Capability of parsing lambda-expression parsing in multi-paradigm languages like C# enables framework developers to parse or modify lambda-expressions at runtime. This allows end-developers to benefit from single programming language for programs that interoperate with variety of systems with different programming language input. In this case end-programmer leaves the job of translation from source language to target languages to framework. An example would be LINQ feature in C# 3.0 which can dynamically construct query statements for different type of databases at runtime only providing required lambda expression. This reduces software construct complexity, as there’s no need to mix different type of languages together, it also benefits to compile-time checking and even optimization for query statements instead of passing to target database as string literals which their content makes no sense to original programming language. It also allows more tight integration query statements with program data structures. All supported as first-class feature in a functional and multi-paradigm programming language.

The growing demand for server-side scalability in era of internet of things resulted in requirement to have services even more scalable. We can see the concept of scalability and being stateless are tightly coupled in RESTfull related technologies even. 
