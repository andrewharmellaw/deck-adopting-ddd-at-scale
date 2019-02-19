# Adopting Domain Driven Design at Scale
## MuCon 2019
### Gayathri Thiyagarajan and Andrew Harmel-Law

---

# Hi
(Who we are)

* Andrew Harmel-Law ([@al94781](https://twitter.com/al94781))
  * Tech Principal @ ThoughtWorks
  * Seen Microservices, CQRS, CI/CD, and cloud-native computing _at scale_.
* Gayathri Thiyagarajan
  * TBD (@gaythu-rajan)

---

## Agenda

---

## The Challenge

* People _still_ don't get DDD
* But it's _still_ the best way that we know of to get large teams around large codebases
* Whether you're doing microservices, or a modular monolith

---

## Our Story

Our project together (and some other bits before and after)

We have first hand experience of seeing what failed DDD looks like on a very large scale. We have seen in detail how pseudo-DDD is the near enemy[1] or real DDD, and that when it strikes it can make the adoption job all the harder, and make the journey towards shaping a success even more effort.

There was a LOT of Tech (Design) Debt.  

---

## Our Goal

* Prioritize what areas we were focussing to those which maximising value for the business AND developers
* Make teams independent (as opposed to tightly coupled) so they could build and release independently.

---

Do we need to explain what a near enemy is?

---

# Part 1: Where we Started / Failure States / Our Challenges
(Patterns?)

---

## Discovery

TBC @andrewharmellaw

---

## Delivery

TBC @gaythu-rajan

---

## Kill misconceptions:
* Lots of people just think it's "names".
* Near Enemy: And grasping the theory is easy, but putting it into practice is harder.
* Domain experts don't know best
* Ubiquitous language needn't be ubiquitous, nor does it have to give us clues
* There is only one model (that there is only one of anything is a risky view in DDD)
* There is a blessed team responsible for modelling and "the domain model"
* The model doesn't need to be explicit in the code
* The model doesn't need to change once you "find" it

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

## Challenges

NOTE: LOTS OF THIS IS THE SOLUTION BUT WE CAN PULL THAT DOWN TO LOWER SECTIONS LATER

* Discovering boundaries - this was a very process-intensive environment, where things (cases) _seemed_ to pass through a lot of organisations and hands.

* The "domain" was co-owned (courts and prosecutor)  The PROCESS spanned multiple organisations

* Complex Architectural choices - devs getting drowned by them. It was almost always an impediment rather than a boost.

* The scale - EVERYTHING was CQRS (EVERYTHING) and Microservices, plus it was being built by multiple teams in parallel, staffed from multiple partners. (Different roles thought in different ways - e.g. Devs, BAs, Data Architects, Software Architects, etc.  Find something which ties all this together (-> DOMAIN VISION))

* Embrace change - a lot of people needed to let go of things, but without knowing excatly where we were going (trust the DDD)

* Constant desire to "future-proof" - this is not the same as building on a supple model.

* Cost - the cost of lots of people is _enourmous_, so prepare, define the problem statement, and get the right people but no more. (A lot of vague things will get thrown at you, and you will be invited to a lot of meetings as "the domain expert".  SOME PROBLEMS WERE PHANTOM PROBLEMS - e.g. "simultaneous updates to a case" only occurs when you have one case to rule them all.)

* (Not allowed to "train" the folks)

* Finding the icebergs - how big / important is something?

---

# Part 2: The Journey Towards Success

Action: Decide what our three big topics for "Journey" are.

There is an order to do things...

---

## Discovery

TBC @andrewharmellaw

---

## Delivery

TBC @gaythu-rajan

---

## Process
Design Retro - speak to K and G and ... team (first implementers)

---

## Tools
Draw out the entire architecture - showing all the BCs and microservices - Context map
(WARNING: Don't make the context map do too much! - Use layers on top if it you need this)

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

## Discovery

TBC @andrewharmellaw

---

## Delivery

TBC @gaythu-rajan

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

* We didn't fix everything - this isn't a fairy story.  

* Don't get waylaid
* Have confidence - you're finding and iterating, and training
* You're the guide to the DDD Theme Park
