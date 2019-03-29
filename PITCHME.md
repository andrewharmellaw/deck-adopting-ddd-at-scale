# Adopting Domain Driven Design at Scale
## MuCon 2019
### Gayathri Thiyagarajan and Andrew Harmel-Law

---

# Hi
(Who we are)

* Andrew Harmel-Law ([@al94781](https://twitter.com/al94781))
  * Tech Principal @ ThoughtWorks
  * Worked on Microservices, CQRS, continuous delivery, and cloud-native computing _at scale_.
* Gayathri Thiyagarajan
  * Tech Lead @ Expedia Group (@gaythu-rajan)
  * Worked on Microservices, Event Sourcing, CQRS in BigData environments

---

## Agenda

---

## Where We Find Ourselves

* People _still_ don't get DDD
* But it's _still_ the best way to solve complex problems in software
* and the best way that we know of to get teams around codebases
* Whether you're doing microservices, or a modular monolith
* And worst of all, it gets harder the bigger the problem you're trying to solve

---

## Our Story

Our project together (and some other bits before and after)

We have first hand experience of seeing what failed DDD looks like on a very large scale. We have seen in detail how pseudo-DDD is the near enemy[1] or real DDD, and that when it strikes it can make the adoption job all the harder, and make the journey towards shaping a success even more effort.

There was a LOT of Tech (Design) Debt. (We'll get to why in a little bit.) 

---

## Our Goals

* Solve the right problems and build the right software
* Make teams independent (as opposed to tightly coupled) so they could build and release independently (and therefore more quickly).
* Prioritize the areas we focussed which maximised value for the client AND developers

--- 

## Or More Simply...

We're just trying to split the hard problem, into smaller maximally independent problems, 
and trying to get as many people understanding and working on those problems as possible

---

# Part 1: Where we Started / Failure States / Our Challenges

(Patterns?)

---

## The Near Enemies of Domain Driven Design (and how to recognise and defeat them)

  "The traditional term “near enemy” points to some spiritually unhelpful quality or experience that can be mistaken for a helpful quality or experience. The near enemy is a kind of counterfeit of what we’re actually aiming for, and it’s unhelpful because while the genuine article helps free us from suffering, the counterfeit doesn’t." from https://www.wildmind.org/tag/near-enemy

Note:
The concept of near enemies should be very familiar to anyone who has worked in software for even a short while - there are _many_ near enemies in the adoption of so-called "Agile" methodologies, and more recently in the drive towards "DevOps culture".  There are smaller-scale versions in many other places.  DDD is one of them.

Why do they arise? Fundamentally, they appear because people do not engage fully with a concept, and typically this is because they ignore the core, fundamental aspects; which are also typically the most simple.  They forget the simple four lines of the Agile manifesto, or ignore the DevOps goals of breaking down boundaries and building a culture of learning. 

Instead get tied up in the complicated details which seem more "valuable" and where the "expertise" lies.

We want to use this lens to present a collection of challenges and failure patterns we've seen when using DDD at a large scale.  It's ideal for these purposes (we could argue essential if you want in any way to succeed) but when things get complicated people reach for the power tools, and that causes problems.  We want to help you avoid falling into that trap.
 
---

## Our Constraints

Things were already up and running - some ideas had already become entrenched

The "domain" was co-owned (courts and prosecutor)  AND the PROCESS spanned multiple organisations *****

The scale - it was a massive piece of work, being built by multiple (how many?) teams in parallel, staffed from multiple partners. (Different roles thought in different ways - e.g. Devs, BAs, Data Architects, Software Architects, etc. Find something which ties all this together (-> DOMAIN VISION))

Complex Architectural choices had been made (e.g. CQRS for everything) and devs were getting drowned by them. It was almost always an impediment rather than a boost - We'll come back to this in the final section. For now, suffice it to say that it made the adoption of the DDD even harder)

---

## Existing Failure Patterns / Challenges

(DDD skills were in short supply - We were not allowed to "train" folks)

(Models have to be in UML or some other "architect-only" notation (the real one is in the code). - DISCO / DELI)

(Red Book and not the Blue Book - DISCO)

---

## Discovery

TBC @andrewharmellaw

(Tell the story - what were the key points / milestones in this?)

When I landed I was heralded as the "DDD expert".  I'd go into meetings and people would address me as such. It was clear that there was not only a general awareness of my arrival, but also an expectation that I would be able to solve a lot of problems, and that DDD would be my tool to do so.  PROBLEM: I WAS TO SOLVE THE PROBLEMS, AND I OWNED THE DESIGN. DOMAIN EXPERTS AND DEVELOPERS WERE EXCLUDED. 

I began by setting off a number of lines of enquiry - I had a vague idea of the domain, having spent a long time delivering software in the Scottish Legal system.  I knew things here had been running for a while already, and that there was a bunch of designs already in existence on the confluence wiki, and a significant bunch of code already written.  There was talk of an architect who had done a bunch of the early work, but they had since moved on.  I had to look at what was there, and how it had manifest in the team structures and codebases.  I had to reverse engineer a big picture from the pieces I could find.  PROBLEM: THERE WAS NO WAY IN. THERE WAS NO BIG PICTURE WITHIN WHICH TO LOCATE YOUR MORE DETAILED WORLD.  THE COGNITIVE LOAD WAS TOO HIGH.  THIS WAS EVIDENCED IN TEH FACT THAT NO ONE DOMAIN EXPERT HAD AN END-TO-END VIEW.

There were additionally an over-focus on the data, and an under-emphasis on the behaviour / workflow / jobs to be done.  PROBLEM: DESIGN DECISIONS / TRADE-OFFS HAD BEEN MADE WITH ONLY A SUB-SET OF THE DATA.

I quickly came across a few core tenents which had embedded themselves in the psyche of everyone on the project. (I take a very "I'm the noob and I'm keeping the beginners mind as long as I can to get as deep an understanding as possible" approach.) The most prevalent was the dictum that "a case is a case (is a case)", by which was meant that there should be a single representation of a case making its way through the criminal justice system, most likely mastered by a single microservice / datastore. PROBLEM: "ONE MODEL TO RULE THEM ALL" THINKING HAD BUBBLED UP, BOURNE OF A DESIRE NOT TO DUPLICATE DATA.

What did this mean? Most findamentally, there was only one model of a case which tried to be all cases (that there is only one of anything is a risky view in DDD).

This came into direct conflict with the fact that there were teams working with different domain experts, on different services, with different release plans; all of whom had to play in this unified "case".  GOOD THING: HAVING DOMAIN EXPERTS AROUND ALL THE TIME IS A MUST.  BAD THING / FAILURE: Not listening to the domain experts. Domain experts don't know best. 

The second tenent was actually more like a myth, most likely born of misunderstanding / misinterpretation than anything else - it was that "diagrams can't be drawn".  And despite the fact that a few guerilla diagrams were in existence, this ghost-dictat had largely been adhered to.  PROBLEM: TECHNICAL TEAM MEMBERS HAD NO WAY OF GRAPPLING WITH THE DOMAIN, NO WAY OF TESTING THEIR UNDERSTANDING OF THE UBIQUITOUS LANGUAGE, AND NO WAY OF MAKING MODELLING BREAKTHROUGHS.  FAILURE: Ubiquitous language needn't be ubiquitous, nor does it have to give us clues.

All this combined to create a significant problem - complexities had been created where there needn't be any (significant amounts of complex shared code, lack of domain understanding - breadth and depth - in the devs) and over-simplification where the domain actually needed to be far richer.  We came to refer to these as the "Icebergs".  To evidence how this is we need to provide a quick intro to the doimain we're talking about.

Legal systems are complex.  They have evolved over _significant_ periods of time, and contain TIME itself as a significant factor (i.e. the law changes, things can expire, things have deadlines).  They bring together a great number of (hostile) parties, all who have their views on the system, and obligations / needs to be met.  Most importantly, they must contaim within themselves a great deal of flexibility, while still balancing against this an incredible formality; seemingly small details can make large differences, and have VERY SERIOUS, real-world outcomes.  

ALL IN ALL, IT IS AN EXCELLENT SET OF CIRCUMSTANCES TO EMPLOY THE TECHNIQUES OF DOMAIN DRIVEN DESIGN.

Given all this, things were harder still for the following reasons:

 * we were tasked with building a collection of systems which met the needs of two different stakeholders - the State Prosecutor, and the Courts System
 * we had to support a full-lifecycle view - justice end-to-end
 * and we had to "modernise justice" as we did it

With this in mind it is no surprise that things had got complicated prior to our arrival.  The stakes were INCREDIBLY HIGH, as were the potential RISKS and BENEFITS.

ACTION: Deal explicitly with finding the Icebergs - how big / important is something? - DISCO / DELI (and the opposite - red herrings)

ACTION: AHL TO SUMMARISE - WHERE WERE WE AT THIS POINT?  WHAT SPECIFICALLY ARE THE NEAR ENEMIES WHAT WE'VE IDENTIFIED?

---

## Delivery

TBC @gaythu-rajan

FAILURE MODE: DESIGN CONTINUES DURING DELIVERY -IT'S PRACTICAL, NOT THEORETICAL

The model doesn't need to change once you "find" it - DELI *****

Constant desire to "future-proof" - this is not the same as building on a supple model - DISCO / DELI

Lots of people just think DDD is "just names" - DELI

There is a blessed team responsible for modelling and "the domain model" - DELI

The model doesn't need to be explicit in the code - DISCO / DELI  *****

Grasping the theory is easy, but putting it into practice is harder - practice builds up pattern recognition, gut instincts and muscle memory - DELI

Finding the Icebergs - how big / important is something? - DELI **** (and the opposite - red herrings - e.g. simultaneous updates to cases)

---

In summary: Solve the business problems. Work with the domain experts. Work with the teams. Work with the code. Iterate.

---

# Part 2: The Journey Towards Success

Action: Decide what our three big topics for "Journey" are.

Andrew's might be: 

 * Establish a Domain Vision 
 * Find the AS-IS bounded contexts - you can start from the top, or take value-stream slices, going *end-to-end* helps a lot
    * Context Map
    * Copying data
    * Alberto Brandolini's ()->|()->() diagram
    * Warning! - SubDomains
    * Core Domain, and other Strategic design patterns
 * _Everyone_ does the modelling
 	* Running "awareness" sessions to engage the business and allow their language to carry weight
 

There is an order to do things...

(Have some common slide headings / topics for both @Gaythri and @Andrew to cover)

---

## Discovery

TBC @andrewharmellaw

BIG TOPIC ONE: Discovering boundaries - this was a very process-intensive environment, where things (cases) seemed to pass through a lot of organisations and hands. - DISCO


As the Discovery phase began to wind up and I began to start _doing_ more I realised my focus would be in three areas:

  * finding what's most important 
  * finding the big picture and breaking it into smaller pieces
  * articulating how the pieces fit together 

While I addressed them more in an interleaved fashion, I'll speak about them each in turn for clarity.

---

### What is Most Important?

[everyone modelling -> domain vision]

Note: what it prioritised and of highest value?  Where does (should?) the control / the power / the centre of gravity sit?

---

#### Domain Vision ***** (AHL)

---

### Finding the Big Picture, and Breaking it Up

[Context Mapping and Core Domain]

I used to think you only discovered Bounded Contexts from modelling lower-level concerns and then using the concept to split your models.  

When working on this, I realised that you could also profitably see them from the top down (although this is more a blunt-instrument approach it has a lot of value)

---

#### Find the Bounded Contexts ***** (AHL)

Event Storming is good for this, 
But Conway's Law is also a good bet - sometimes: focus on actors and jobs-to-be-done rather than organisations.  Everyone is doing things to a shared model all the way through a process.

#### Context Map **** (AHL)

(I used to think yiou found this via doing models)
(Now I've seen Event Storming at scale I realise there are other ways)

---

### How Things Fit Together

(both at implementation-time and run time) [Alberto's: ()->|()->(), and Strategic Patterns]

---

### End-to-End Flows ***** (AHL)

Do Event Storming.
It's in the ThoughtWorks Tech Radar
It's great for the obvious reasons
But you also get Business and Tech working together
And _everyone_ is modelling

--- 

#### (Strategic Patterns)

Start to point out the Strategic Patterns (teams succeeding might already be doing this)
This would have been the next step

---

## Delivery

TBC @gaythu-rajan

Driving change - a lot of people needed to let go of things, but without knowing exactly where we were going (trust the DDD) - DELI

Managing Cost - the cost of lots of people is enourmous, so prepare, define the problem statement, and get the right people but no more. (A lot of vague things will get thrown at you, and you will be invited to a lot of meetings as "the domain expert". SOME PROBLEMS WERE PHANTOM PROBLEMS - e.g. "simultaneous updates to a case" only occurs when you have one case to rule them all.) - DELI

---

## Process
Design Retro - speak to K and G and ... team (first implementers)

---

## Tools and Methods
Draw out the entire architecture - showing all the BCs and microservices - Context map
(WARNING: Don't make the context map do too much! - Use layers on top if it you need this)

Modelling Whirlpool - Where a strawman model is just what everyone needs to get things kicked off instead of a blank wall

Event Storming - by far the best method to find aggregates and document events. It doesn't have to day long full blown exercise. Small, iterative sessions are helpful for solutioning too.

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
## Ownership

Team collectively owns the model. 
Everyone has some important insight and perspective to add to the model.
Collective ownership stimulates collective responsibility in implementation. 

---

## AS-IS <-> TO-BE vicious circle **** (GT)

Obtain knowledge of the domain from the As-Is state. Model the To-Be state. 
Domain changes more slowly than the system that we are building. 
Beware the legacy systems - they don't exactly reflect the domain knowledge.

---

### You _can_ copy data ***** (AHL/GT)

Matthias Verraes : “Don’t Repeat Yourself” was never about code. It’s about knowledge. It’s about cohesion. If two pieces of code represent the exact same knowledge, they will always change together. Having to change them both is risky: you might forget one of them. On the other hand, if two identical pieces of code represent different knowledge, they will change independently. De-duplicating them introduces risk, because changing the knowledge for one object, might accidentally change it for the other object.

---

### Pick your battles ***** (GT)

Don't spread yourself too thin
Don't waste time trying to convince everyone - some folks will come round to the idea, especially when they see it working

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

---

# Appendixes

https://twitter.com/ntcoding/status/1097139309642158080
