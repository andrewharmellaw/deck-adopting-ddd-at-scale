# Adopting Domain Driven Design at Scale
## MuCon 2019
### Gayathri Thiyagarajan and Andrew Harmel-Law

---

# Hello
(Who we are)

---

## Agenda

---

## The Challenge

People _still_ don't get DDD
But its the best way that we know of to get large teams around large codebases
Whether you're doing Microservices, or a Modular Monolith

---

## Our Story

MoJ (and some other bits before and after)

We have first hand experience of seeing what failed DDD looks like on a very large scale. We have seen in detail how pseudo-DDD is the near enemy[1] or real DDD, and that when it strikes it can make the adoption job all the harder, and make the journey towards shaping a success even more effort.

---

# Part 1: Failure States
(Patterns?)

---

## Kill misconceptions:
* There is only one model (that there is only one of anything is a risky view in DDD)
* There is a blessed team responsible for modelling and "the domain model"
* The model doesn't need to be explicit in the code

Also
* Models have to be in UML (the real one is in the code).

---


## It's in the frikkin' Blue book

* All the (DDD) things! Also known
* Are layers a bad thing?

* Work with the teams
* Work with the domain experts
* Work with the code
* Iterate

---

### The "Blue Book" and the "Red Book"

---

You're just trying to split your hard problem, into smaller problems, 
and trying to get as many people understanding and working on the problem as possible

---

# Part 2: The Journey Towards Success

---

## Everyone get modelling

We're _all_ doing design
Draw pictures!
C4 is good for this (Simon Brown has training for Developers too)
Find champions (junior folks can actually be good for this)

---

## Find the model in the code

FEEL the code

---

## It's not your model, it's everyone's

Use tools to generate your models that everyone can use to edit
N.b. folks need to be confident in these tools, not just have access to them.
You need to over-communicate and over-share
You need to work with others to find it

---

## Find the Bounded Contexts

Event Storming is good for this, 
But Conway's Law is also a good bet

---

## Context Map

(I used to think yiou found this via doing models)
(Now I've seen Event Storming at scale I realise there are other ways)

---

## Strategic Patterns

Start to point out the Strategic Patterns (teams succeeding might already be doing this)

---

### End-to-End Flows

Do Event Storming
It's in the ThoughtWorks Tech Radar
It's great for the obvious reasons
But you also get Business and Tech working together
And _everyone_ is modelling

---

### You _can_ copy data

---

## This is best seen in Alberto Brandolini's ()->|()->() diagram

---

### Pick your battles

Don't spread yourself too thin
Don't waste time trying to convince everyone - some folks will come round to the idea, especially when they see it working

---

## Domain Vision

---

## It's in the frikkin' book

* Work with the teams
* Work with the domain experts
* Work with the code
* Iterate

---

# Stage 3: Applications in Other DDD-Derived Areas (E.g. CQRS)

---

## Consolidate / Fight

---

## Beware close enemies

---

## Core domain

---

## Generic Sub Domain
Lose some battles

---

## It's in the frikkin' book

* Work with the teams
* Work with the domain experts
* Work with the code
* Iterate

---

# Conclusion

* Don't get waylaid
* Have confidence - you're finding and iterating, and training
* You're the guide to the DDD Theme Park
