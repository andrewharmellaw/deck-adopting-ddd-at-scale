# Adopting Domain Driven Design at Scale
## MuCon 2019
### Gayathri Thiyagarajan and Andrew Harmel-Law

---

# Hi

* Andrew Harmel-Law ([@al94781](https://twitter.com/al94781))
  * Tech Principal @ ThoughtWorks
  * Java dev (worked on Microservices, CQRS, continuous delivery, and cloud-native computing _at scale_).
* Gayathri Thiyagarajan
  * Tech Lead @ Expedia Group (@gaythu-rajan)
  * Worked on Microservices, Event Sourcing, CQRS in BigData environments

---

## Agenda

  * Intro - Near Enemies
  * Part 1: Existing Constraints and High Stakes
  * Part 2: Journey Towards Success
  * Part 3: Applications in Other DDD-Derived Areas (E.g. CQRS)
  * Conclusions

Note:
Alternate discovery and delivery for each section.
@andrew to draw models/pictures and @gaythu-rajan to write code

---

## Where We Find Ourselves

* Many people _still_ don't get DDD
* But it's _still_ the best way to solve complex problems in software
* And the best way that we know of to get teams around codebases
* Whether you're doing microservices, a -modular monolith-, or whatever we end up doing in the future

---

## The Near Enemies of Domain Driven Design (and how to recognise and defeat them)

  "The near enemy is a [...] counterfeit of what we’re actually aiming for, and it’s unhelpful because while the genuine article helps free us[...], the counterfeit doesn’t." from https://www.wildmind.org/tag/near-enemy

Note:
Quote: "The traditional term “near enemy” points to some spiritually unhelpful quality or experience that can be mistaken for a helpful quality or experience. The near enemy is a kind of counterfeit of what we’re actually aiming for, and it’s unhelpful because while the genuine article helps free us from suffering, the counterfeit doesn’t." from https://www.wildmind.org/tag/near-enemy

We say "people still don't get DDD". What do we mean?  With the rise of microservices it's being used everywhere right?  Well, not really...

The concept of near enemies should be very familiar to anyone who has worked in software for even a short while - there are _many_ near enemies in the adoption of so-called "Agile" methodologies, and more recently in the drive towards "DevOps culture".  

There are smaller-scale instances of this story in many other places.  The application of DDD is one of them.

Why do they arise? They arise because people do not engage fully with a concept, and typically this is because they ignore the core, fundamental aspects; which are also typically the most simple.  They forget the simple four lines of the Agile manifesto, or ignore the DevOps goals of breaking down boundaries and building a culture of learning.  Instead get tied up in the complicated details which seem more "valuable" and where the "expertise" lies.

We want to use this lens to present a collection of challenges and failure patterns we saw when using DDD on a large scale.  It's ideal for these purposes (we could argue essential if you want in any way to succeed) but when things get complicated people can easily forget about the core concepts, and that causes problems.  

Hopefully this story will help you avoid falling into that trap.

---

# Part 1: Our Story Begins: Existing Constraints & High Stakes

Note:
We're going to share the story of one of our most recent projects together (and some other bits before and after)

We have first hand experience of seeing what DDD looks like on a large scale. We have seen in detail how pseudo-DDD is the near enemy[1] of real DDD, and that when it strikes it can make the adoption job all the harder, and make the journey towards shaping a success even more difficult.

While we worked on the same project but we overlapped very little.  I (Andrew) inherited a bunch of early artefacts from another DDD expert whom I never met, and mainly handled the discovery of the domain.

Just as Andrew had inherited a legacy from those who went before him, I (Gayathri) inherited from him (with all the good and bad that that brings).  I (Gayathri) was largely focussed on delivering what Andrew had found (and challenging the assumptions he had made)

So what was the project? It was the transformation and modernisation of the core public systems within the UK Judicial system.

@gaythu-rajan and @andrew to alternate on each slide
 
---

## Our Constraints

  * Lots of code had already been cut
  * We were supporting the full justice-lifecycle, end to end, across multiple organisations
  * There was an efficiency-finding "modernising" agenda to serve
  * Significant scale - many teams, already working in parallel
  * CQRS _everywhere_
  * Existing tech legacy cast a _long_ shadow over domain experts

Note: 
(Things were already up and running - some ideas had already become entrenched. Bounded Contexts were not there, "Domains and sub-domains" were identified at object level than by the model - E.g. Case, People, Material. The SPLIT was wrong)
@gaythu-rajan made further changes as it was still more object based split.

We had to support a full-lifecycle view - justice end-to-end. The "domain" was co-owned, we were tasked with building a collection of systems which met the needs of two different stakeholders - the State Prosecutor, and the Courts System - AND the PROCESSES entailed spanned even more organisations than that. 
Note: @andrew mentions "No one domain expert had the end-end view", but even when they did it was never communicated to the those who are implementing. Head of BPOs was brought in but still that end-end view was stuck within a group of domain experts.

We had to "modernise justice" as we did it, within a publicly funded program of work. Constantly having to battle with businesss against "quick" wins (from which the resulting tactical solutions had incurred a great deal of debt in the code) and instead efficiently find the "real" wins.

The scale - it was a massive piece of work that was being tackled head on. Software was being built by multiple (how many?) teams in parallel, staffed from multiple partners. (Different roles thought in different ways - e.g. Devs, BAs, Data Architects, Software Architects, etc. 

Complex Architectural choices had been made (e.g. CQRS for everything) and devs were  drowning in them. It was almost always an impediment rather than a boost - (We'll come back to this in the final section. For now, suffice it to say that it made the adoption of the DDD even harder)

Domain experts were stuck in the legacy way of thinking or worse paper based. In courts, traditionally, the prosecutors, defence and courts will fill in the same form alternately and the expectation was to translate that literally onto the software application. 

---

### Incredibly High Stakes

With all this in mind it is no surprise that things had got complicated prior to our arrival.  The stakes were INCREDIBLY HIGH, both RISKS and BENEFITS.

---

## Our Goals

  * Solve it right, build it right
  * Maximally indepenent teams
  * Prioritise value for _everyone_
  * Pick our battles

Note:
As Senior Developers, all projects we work on share some common goals.  This project was no different:
@gaythu-rajan to state the goals and pull this into conclusion section

* Solve the right business problems and build the software right
* Make teams independent (as opposed to tightly coupled) so they could build and release independently (and therefore more quickly).
* Prioritize the areas we focussed which maximised value for the client AND developers
* Pick the right battle - there are so many things that you can make perfect, pick the ones that add most value.

--- 

## Or More Simply...

We're just trying to split the hard problem, into smaller maximally independent problems, 

and trying to get as many of the right people understanding and working on the right problems as possible.

---

## Discovery

Note:
I (Andrew) arrived first.  
I (Gayathri) arrived second.  We overlapped a little, but not much.

With hindsight, we both followed similar meta-approaches.  Starting with our own "discovery" phases, and then moving on to "delivery" work. - IS THIS HOW WE'VE STRUCTUED IT? I'M NOT SURE IT IS, BUT TO LOSE THIS WOULD BE FINE IMHO.

@andrew to draw a timeline of @gaythu-rajan (a year and half) and @andrew's (9mo) time there

---

@snap[north]
### Alone, "Doing the DDD" [AHL]
@snapend

Note:
When I landed I was heralded as the "DDD expert".  

I'd go into meetings and people would address me as such. I even got called the "DDD Messiah" once.  That's when I got worried.

It was clear that there was not only a general awareness of my arrival, but also an expectation that I would be able to solve a lot of problems, that DDD would be my tool to do so.  

However, rather than everyone looking for a more general adoption of DDD as an approach / set of skills, I was there to take things off people's hands.

---

@snap[north]
### Alone, "Doing the DDD" [AHL]
@snapend

PROBLEMS: 
- I WAS THERE TO SOLVE ALL THE PROBLEMS,
- AND I OWNED THE DESIGN. 
- DOMAIN EXPERTS AND DEVELOPERS WERE EXCLUDED. 
- I WAS GOING TO TELL EVERYONE WHAT TO DO.

---

### Where was the Big Picture? [AHL]

Note:
I take a very "I'm the noob and I'm keeping the beginners mind as long as I can to get as deep an understanding as possible" approach.

I began by setting off a number of lines of enquiry - I had a vague idea of the domain, having spent a long time delivering software in the Scottish Legal system.  It's very different, but it allowed me to compare things and ask "North of the border they have to do this?  Is there an equivalent?" or question "In Scotland this is owned by a person who works for department X, is something similar needed here, and of so, who does it?"

I pulled in as many info sources as I could, official and unofficial, trying to avoid value judgements, and always looking for the edges. I wanted to know the full extent of where we were now.

I knew things here had been running for a while already, and that there was a bunch of designs already in existence on the programme wiki, and a significant amount of code already written.  There was talk of an architect who had done a bunch of the early work, but they had since moved on.  I had to look at what was there, and how it had manifest already in the team structures and codebases.  I had to reverse engineer a big picture from the pieces I could find.  
 
I tried to make sure I didnt get sucked into too much detail in any one area.  I needed to avoid getting overwhelmed at this stage.

---

### Where was the Big Picture? [AHL]

PROBLEMS: 
- THERE WAS NO WAY IN. 
- THERE WAS NO BIG PICTURE WITHIN WHICH TO LOCATE YOUR MORE DETAILED WORLD.  
- THE COGNITIVE LOAD WAS TOO HIGH.  
- NO SINGLE DOMAIN EXPERT HAD AN END-TO-END VIEW.

---

### "One Model to Rule Them All" [AHL]

Note:
I quickly came across a few core tenents which had embedded themselves in the psyche of everyone on the project. The most prevalent was the dictum that "a case is a case (is a case)", by which was meant that there should be a single representation of a case making its way through the criminal justice system, most likely mastered by a single microservice / datastore. 

From a DDD perspective, there was an over-focus on the data (@gaythu-rajan to elaborate with the defendant model and people context; mention how @andrew comes up with the idea and how it was implemented), and an under-emphasis on the behaviour / workflow / jobs to be done.  It didnt even really manifest in domain events  This wasn't evident in itself specifically - there was simply a lot of the former, and a significant absense of the latter. (The domain events, such as they were weren't even very fleshed out, having mainly fallen back into the realm of CRUD operations.)

What did this mean? Most fundamentally, there was only one model of a case which tried to be all cases (that there is only one of anything is a risky view in DDD).

---

### "One Model to Rule Them All" [AHL]

PROBLEM: 
- "ONE MODEL TO RULE THEM ALL" THINKING HAD BUBBLED UP,
- BOURNE OF A DESIRE NOT TO DUPLICATE DATA.
- CONSEQUENTLY DESIGN DECISIONS / TRADE-OFFS HAD BEEN MADE WITH ONLY A SUB-SET OF THE INFO.

---

### _Loads_ of Lovely Domain Experts - Listen [AHL]

Note:
This unified "Case" construct came into direct conflict with the fact that there were many teams, working with their own individual domain experts, on different services, with different release plans; all of whom had to play in this "Case" space.

The existence of the domain experts, embedded 3 out of 5 days with each team was a boon. (I've seen _many_ DDD projects fail due to a lack of this.)  This involvement must have been incredibly difficult to plan, set up and finiance, and as such it needs to be explicitly called out.

GOOD THING: HAVING DOMAIN EXPERTS AROUND ALL THE TIME IS A MUST.  

There was a problem however. In many teams, the domain experts weren't being used to their full potential.  I kept coming across the worrying signs that the technical people didnt agree with their embedded Crown Prosecution rep. And not just on which version of a java library, no. I heard people saying that they were wrong when they described how their job worked.

---

### _Loads_ of Lovely Domain Experts - Listen [AHL]

PROBLEM: 
- NOT _LISTENING_ TO THE DOMAIN EXPERTS. 
- UNWRITTEN TENET: DOMAIN EXPERTS **DON'T** KNOW BEST.

Note:
A little later I stumbled upon something which might have been the root cause of the above lack of shared domain understanding.  Almost a myth, most likely born of misunderstanding / misinterpretation than anything else - it was that "diagrams can't be drawn".  And despite the fact that a few guerilla diagrams were in existence, this ghost-dictat had largely been adhered to.  

What this was saying to me was "ubiquitous language needn't be ubiquitous, nor does it even have to give us clues".

Worse still, it was stopping developers playing with the language of the domain in order to grasp it more deeply, and consequently arrive at modelling breakthroughs.
@Andrew - make this and then next one into single slide?

---

### _Loads_ of Lovely Domain Experts - Listen [AHL]

PROBLEM: 
- TECHNICAL TEAM MEMBERS HAD NO WAY OF GRAPPLING WITH THE DOMAIN, 
- NO WAY OF TESTING THEIR UNDERSTANDING OF THE UBIQUITOUS LANGUAGE, 
- AND NO WAY OF MAKING MODELLING BREAKTHROUGHS.  

---

### Legal Systems are **Complex** [AHL]

Note:
We need to pause a second and make some things clear.  

Legal systems are complex.  They have evolved over _significant_ periods of time, and contain TIME itself as a significant factor (i.e. the law changes, things can expire, things have deadlines).  

They bring together a great number of (by the very nature of the adveserial system, hostile) parties, all who have their views on the system, and obligations / needs to be met.  

Most importantly, they must contaim within themselves a great deal of flexibility, while still balancing against this an incredible formality; seemingly small details can make large differences, and have VERY SERIOUS, real-world outcomes.  

---

### Legal Systems are **Ripe** for DDD [AHL]

ALL IN ALL, IT IS AN EXCELLENT SET OF CIRCUMSTANCES TO EMPLOY THE TECHNIQUES OF DOMAIN DRIVEN DESIGN.

Segue into GT's delivery after this

---

## Delivery

---

### Mind the Gap! [GT]
When I took over from Andrew, I realised that there was a chasm between the models he had identified and their implementation. First and foremost, very few realised that the model had to be translated into code, and even fewer had any idea how to go from there. 

At that point we had a big 'Case' model which the teams had realised they needed to split. But Andrew had identified at least three different models for a case. So they roughly went about hacking the case into 3 pieces. 

Beware the pseduo DDD experts. Advocating for a literal translation of real world paper based process to software. This brings service orchestration into the equation and thus single point of failure. 

I mentioned the implementation of the new models before - it was not an easy job. There already was an implementation which cannot be changed in a big-bang approach even within a single BC. Incremental change towards the final model and while incrementing also constantly validating and challenging the model was important. 

---

### Icebergs and Icecubes [GT]

All this combined to create a significant set of problems - complexities had been created where there needn't be any (significant amounts of complex shared code, lack of domain understanding - in both breadth and depth - in the devs) and over-simplifications where the domain actually needed to be far richer.  We came to refer to these as the "icebergs".  

(To illustrate this we need to provide a lightning intro to the dynamics of the domain we're talking about.) - TODO - Simplified pictorial rep of domain here?

Sometimes requirements and reduced scope can diguise a key process as a simple straight forward one. The real magnitude of it can only be obtained by looking into the actual domain. 

Therefore, do not constrain yourself by requirements and scope (MVP) when learning about the domain. MVP is another near enemy! Once the actual process is learnt, distill the bits not within scope and what remains is implemented but at least you know the true size of it and confident that the model can expand as the scope gets bigger.

One such example is the IDPC. What was perceived as a simple service for PDF generation from multiple documents was actually a key stage in the prosecution process particularly one main prosecutor (the Crown Prosecution Service). As you will hear later, while implementing this feature I personally learnt the above lesson of not underestimating the size based on just the MVP.

The other side of this exists too. What is considered as a big problem (Ice cubes?) sometimes fizzles into nothing. Simulataneous updates to a case is a good example. When I started there was serious apprehension amongst domain experts about how to deal with simultaneous updates to a case. So I was asked to setup a DDD session to find a solution to this problem. 

It actually turned out to be a design smell by not defining the boundaries between different models of the case. When we started implementing the different models in their own bounded contexts, this problem just went away. 

Access control is another example - of course it is important but delineation of models particularly multiple models of the same entity in their own bounded context and operated on by corresponding actors provides out of the box access control at the very basic level.

---

### Perception @Scale [GT]

I also realised that DDD was being 'done' because someone said so. Very few had realised the actual benefits of doing it but lot of pain from doing it wrong. 

Lack of awareness about DDD was a big problem. It was seen as 'someone' else's problem, teams were not clear about whose responsibiiility it was to do DDD, more often than not it was seen as a directive from the top, seen as a 'must be done' step rather than something which developed organically. 

Having burnt their hand once, everyone was keen not to repeat the same mistake again. Which is all good only they didn't realise what the mistake was (not doing modelling enough and not iterating on it). Everyone now wanted to get it right and get it right the first time (well second time, anyway). So the business architects were constantly at me asking about the governance (i.e ring fence the model with tight governance so that noone can mess around with it!) and also expecting guarantees from me that this is the "correct" model! 

We will see again and again that people are the making or breaking factor for any adoption at this scale be it Agile, DevOps or DDD. We had to deal with a good many sceptics, critics and some who point blank refused that DDD is useful. I stopped explaining why they should DDD but resolved to show them its merits in practice instead. 

---

### Split != Silos [GT]

One of the teams were dying to split off and be able to do things on their own. This new found freedom was even more dangerous as there was the risk of the models diverging irrevocably. There was a need to distinguish this from the freedom to work independantly make changes, release and operate. 

In the legal system, different parties go off on their own to work on the casefile - collect evidence, witnesses, putting together documents, case material and then COME TOGETHER for the next phase of hearing, sentencing. Not realising this was a big failure. I.e. Even though teams should have the freedom to go off and work within their boundaries on thier own model, at the end of that process, they will have to be able to come back together which means they can't diverge too much from a consistent thread of a model.
(Knowing the strategic pattern andthe team relationship was important here - as it was "Separate Ways" here but "Partnership")

So my job was to make sure that the teams were made aware that this is not the chance to break free. This is when I realised that the teams were not aware of the business process outside of their domain - Team building Pre-Charge were not aware of the next stage and so on. The other danger was from avoiding Silos forming from these splits. 

@gaythu-rajan pull this to the place where @andrew talks about independant teams 

---
### Data focussed [GT]

@gaythu-rajan to talk about that data centricity and pull this to the place where @andrew talks about it above

+
+
+
+
+
+
+
+


---

### Shortsight Vs Longsight [GT]

Another sign of failure is failing to realise the difference between learning the domain beyond what the 'requirements' captured vs future proofing. The former means due to the deeper insights gained from the domain the model will be more robust and less likely to fall over because the real world seldom changes at the same pace as the requirements on which a software application is built. While the latter means, you are anticipating these requirements to come up later and building it in advance. 
Constantly having to battle with businesss quick wins and resulting tactical solutions incurred so much debt in code.

### Naming teams

Teams named after the part of business process they were working on (which would change and grow) like C2I, I2T etc. rather than named from contexts - Prosecution/Defence/Courts/SJP etc. which would create teams specialised in that part of the legal system. Wrong names/contexts used by the wrong teams. Scheduling was something used by ATCM which created SJP session.

---

### Ownership

Team collectively owns the model. 
Everyone has some important insight and perspective to add to the model.
Collective ownership stimulates collective responsibility in implementation. 
architects wanted to 'own' the model and be the gatekeepers.  -> I need to say something about people, desire to control which curtails the innovation in model - DDD requires the best skills from everyone: architects on oversight/practice, domain experts on language and domain knowledge, developers on the model implemnentation : THIS is the success of DDD, it implictly brings the whole team together. 

---

In summary: Solve the business problems. Work with the domain experts. Work with the teams. Work with the code. Iterate.

---

# Part 2: The Journey Towards Success

Note:
Andrew isn't yet talking enough about:
	* Copying data
		* Link this back in when we talk about the "()->|()->()" archetype?

Andrew / Gayathri might talk more about:
	* _Everyone_ does the modelling
 		* Running "awareness" sessions to engage the business and allow their language to carry weight
 
There is an order to do things...

(Have some common slide headings / topics for both @Gaythri and @Andrew to cover)
@gaythu-rajan and @andrew to talk Discovery and then Delivery 

---

## Discovery

---

### Focussing the Effort [AHL]

Note:
As the first, listening, phase began to wind up and I (Andrew) began to start _doing_ I slowly realised my focus would be in three areas:

  * stating clearly what's most important - the domain vision
  * finding the big picture and breaking it into smaller pieces - context mapping
  * discovering how the key pieces fit together  - value streams / archetypes

While I addressed them more in an interleaved fashion, I'll speak about them each in turn for clarity.  Counter-intutively I'll start with the last bullet first.

---

### How do the Key Pieces Fit Together? [AHL]

Note:
Knowing about all the various models is one thing. Knowing how they relate, interact, and (possibly) overlap is the _big_ thing.  

Discovering the spine / the armature of the domain as a whole turns out to be fundamental in this. Remember; this was a very process-intensive environment, where our things (Cases) pass through a lot of organisations and hands.

You don't need to do this all bottom-up.  You can start from the top, or take value-stream slices. Going *end-to-end* helps a lot.  (This is a great use case for Event Storming, and one reason why it has proved so popular.)

(There is a paradox here - I needed to investigate this first, in order to find the concrete elements, which then allowed me to pull back out to see how everything joined together into the whole, bigger picture.)

---

#### "A Case is a Case is a Case" [AHL]

Note:
The route into everything was to try and tackle the "case is a case (is a case)" issue.  I could see where it had come from; the idea was to modernise the criminal justice system, and to remove some of the unnecessary complexity.  

!DATA!DATA!DATA! ADD SOMETHING ABOUT DATA (AND TRYING NOT TO HAVE TOO MUCH OF IT) HERE. @gaythu-rajan to pull tihs into the data section

One way to do this was clearly to find things which where similar and to treat them in the same way.  There was a lot to suggest that fundamentally, cases were a candidate for this.  The problem was, the simlarities were less than anticipated, and the differences were critical - mainly in the regards to who owned the cases and how they were handled.

The problem became painfully evident when looking at the existing Case Aggregate Root - it was *massive* and had tons of attributes.  It also had a significant amount of contributors - it was a *very* hot piece of code. Everyone wanted to add their stuff to it.  

I began by trying to apportion each of the attributes and functions to the team which added them. Perhaps they'd just failed to communicate about what they needed and ended up duplicating things?  It's a common problem.

In parallel I went out to sit with the teams themselves, predominantly their domain experts;  They would be the ones who knew what was needed, and more importantly, the activities and business processes that the concept of a "Case" would need to support in their area.  This is where the tensions arose. It was abundantly clear, very early on, that there were many types of case, which served different purposes in the criminal justice system.  Not only that, they were owned by different stakeholders, meeting differing purposes, and undergoing very different lifecycles.  At this level of detail, there were quite clearly many types of case, which were related (more on that later) but were also very different.

How to square the circle? How could I reconcile the pull in these tweo diretions?  I went back to the DDD book.  Yet another time, there was something there to help me out: Shared Kernels and the Core Domain.

#### Shared Kernels and the Abstract Core [AHL]

Note:
While I disagreed that "a case was always a case" because this lost too much detail in abstraction, it was also the signal that there was highly likely to be a common core - in DDD parlance a shared kernel.  

[BRING IN THE DDD DIAGRAM AND DEFINITIONS HERE]

The flow of cases through the criminal justice system _is_ a collaborative one. There is a fixed number of ways for cases to come into being, and there is a very strict set of protocols governing how these change from one type to another.  

There is space at this point to bring in one more concept. Beneath everything, there was something which, on it's own was never enough to be a case in its own right, but that could be considered an "Abstract Case" from which all concrete types of case could inherit.

(Example: Go into this with an example of A PCD Case and a MagistratesCourtCase - showing the example of Suspects and Defendants.)

#### ()->|()->()

Note:
This brings us onto a concept which *isn't* explicitly brought out in the (Blue) DDD book and which I arrived at on my own prior to discovering it detailed in Alberto Brandolini's Context Map Archetypes.  Having pulled out the shared kernel of cases, and having identified how this was manifest in various contexts to solve various problems and support various activities the question of how these were related came up.  It was clear that not only did each one exist in its own bounded context, but also that there was a flow from one manifestation to another:

()->|()->()

What now seems obvious, but which made me nervous at the time, was the relationship between these contexts.  There was almost a flow of execution and data and ownership (over a significant period of time, but a flow nontheless).  I knew relationships between bounded contexts was significant - I was a big fan of the strategic design patterns and the clarity they gave, but this seemed to be a different form.  It seemed like I'd come across something fundamental.
@gaythu-rajan to provide te sketch of this

#### The Domain is Talking to You

I went back to the domain experts.  What I thought I could see in the model was right there in the domain. It was clear that there were business-level processes (ceremonies even) involved in moving from one context to the next.  These moves involved significant conceptual (and data-level) changes.  They had criteria, and ownership was transferred.

I felt good about this discovery, mainly because it was corellated strongly to the domain reality. A year or so later, in a workshop with Alberto Brandolini, he introduced his archetype.  When I saw it I could immediately recognise it for what it was, and realised there were *many* manifestations.  I felt satisfied.  

There were relationships - and they were creation-level ones. One model could pass control onto a downstream model, and create that downstream model in the process.

I turns out that this is entirely valid.

---

### Finding the Big Picture, and Breaking it Up [AHL]

Note:
Now that I had the spine of bounded contexts identified I could begin work on fleshing out all the others which hung off it.  This proved relatively simple once I took into account a few rules of thumb:

 * look for generic (technical) subdomains
 * pay attention to the jobs being done and the ways they were structured from an organisation perspective

---

#### When is Sometihng NOT a Generic (Technical) Subdomain? [AHL]

[BRING IN THE DDD DIAGRAM AND DEFINITION HERE]

Note:
The obviously generic technical subdomains were the easiest to spot - things like reporting, access management, etc. Taking these out of the picture early cleared the decks for the focus on the remainder.  These were the ones where there might well be some above-and-beyond value being added.  

As per the Blue book, I went back and forward on some areas where initial engagement with the domain experts indicated that something was a very generic component, but later, typically guided by the richness of the language used to describe something, my thoughts changed, and I realised they were describing something bespoke.

This specific example brings us on to the second point which was also crucial - a lot of domain driven design requires the suspension fo disbelief. It is my experience that eventually, you will find the one or two facts which indicate to you that your model is correct. In my case, it was around whether the scheduling of cases into courts and court rooms (called "listing" in the domain parlance) was a specific use case atop a generic scheduling system, or something far more bespoke and unique.  

I mentioned above that scheduling in courts seemed initially to be the opportunity for an off-the-shelf product, perhaps with a little wrapping up to expose it in a meaningful way to consuming parties (other BCs).  I'm going to talk a little now about the things which led me away from this conclusion.

The seam I mined was based around the edge cases - when the scheduling was a complex matter, when it changed, when it was significantly sized.  It turned out that these circumstances weren't universal in this Criminal Justice System. Luckily we had domain experts who had a wide range of experience.  By asking about the biggest jurisdictions, and the circumstances when things were the hardest / most comoplicated, we eventually settled on a model which coudl represent the real richness of this complex task.  Along the way we'd discovered that there were individuals who had this scheduling task as their sole responsibility, and that there was frequently a great deal of intuition, insight, and discretion that they applied.  This was beyond mere slot-filling.  These people were applying a great deal of local knowledge, and awareness of many upstream feeding-factors about which they could only have learned through experience.  

It also turned out to be a major source of possibility for achieving the goal of "modernising justice".  Getting cases and their hearings scheduled rapidly, and in the near future, and the information about this scheduling disseminated to the various parties (of whom there were a not insignificant amount) was key.  

There is however a caveat.  The "modernising justice" remit had been taken to heart by some domain experts.  They were using this as an excuse to self-censor; only talking about the "core" or "common" use cases.  This meant they were already pre-judging the outcome and not allowing themselves to go into all the detail which they were party to.  To work this out with them took a building up of trust.  It had to be stated that just because we modelled it didn't mean we were going to build it.  But in order to make this decision we needed to know the full extent of what we were dealing with - then, and only then, would we decide what to build / automate, what we would enable, and what we would target to simply do away with altogether.  This seemed to work.

We now had our two indicators - value add, and rich domain language to describe it (to the extent there were in some cases specific job roles).

---

#### The Resulting Context Map [AHL]

Note:
I used to think you only discovered Bounded Contexts from modelling lower-level concerns and then using the concept to split your models.  We had in some respects short-circuited this.  We did it by paying attention Conways Law and studying organisations, departments, actors and jobs-to-be-done.

(Event Storming is also good for this and another short-cut.)

We could now draw our context map.

[BRING IN THE DDD DIAGRAM AND DEFINITION HERE]

[Rough sketch of the context map - @Gayathri, do you have a memory of this which might help?] - yup, @andrew to say this is how it started and @gaythu-rajan 

[Describe the map]

This map, with it's representations of the spine, ... all in the ubiquitious language was a very useful artefact.  It served exactly the purpose stated in the blue book.  it served to orient, to scope, to show relationships (and flow).

[Allude to the relationships, and the direction and their nature (all partnership / shared kernel?)]

---

### Given All This, What is _Most Important?_ [AHL]

Note:
What it prioritised and of highest value?  Where does (should?) the control / the power / the centre of gravity sit?

In wrestling with the cases flow, and discovering the core bounded contexts which encapsulated it, I'd uncovered many of the fundamental aspects of the domain.  

I'd then taken our focus out and dug into other key aspects of the domain - the places where the processing, and the moving of the Case elements through the system took place.

In doing so we'd also fleshed out a bunch more detail which wasn't super-important, but did perform a function.

This gave us a problem: when looking at all this detail, the important parts they quickly became lost in amidst the other detail of their surroundings.  

---

#### Articulate the Domain Vision [AHL]

Note:
By the time we got to this point, there was a LOT of detail - even in the Context Map. I needed something simpler to show key stakeholders and people beginning their journey into the domain. It turns out, yet again, DDD had something for me - the Domain Vision statement.

---

#### Why have a Domain Vision Statement?

- the critical aspects of a Domain may span multiple bounded contexts
- but you can't structure them to show their common focus
- write something (a single page) to bring this out and keep the team headed in a common direction

#### What's in a Domain Vision Statement?

- Paragraph One: The key entities
- Paragraph Two: The key roles / activities / events 
- Paragraph Three: The key integrations

In _each case_, include _why_ these elements are important.  

Note:

DETAIL: Describe how we used it. (Do you cover this @gaythu-rajan? I think I saw that you did...)

---

### Method: Model -> Share -> Question -> Repeat [AHL]

Note:
Draw lots of pictures - try and find what is "comfortable". Being able to draw something on a sheet of A3, or a standard whiteboard is a good sign that the level of detail is correct.

Go back to the book. The "pattern style" that it is written in means it is very easy to find your problem already described.  Then simply follow the solution.  

Find the *armature* - it sometimes seems to me that this part of the process is a lot like discovering the model's armature.

Share these pictures constantly.  Adopt a beginners mind.  Articulate when something doesnt feel comfortable (though be willing to accept a minor amount of discomfort, not everything will fit elegantly into the model you need.)  get the help of others - specifically the domain experts.  Gather round the board and ask questions of your models and see when they break.

At a meta level, it was exciting to come at DDD from another angle. It meant I had to re-read Eric's book, and find value in other parts which I'd previously skimmed. I was amazed (yet again) at how relevant and applicable and valuable these concepts were.

---

## Delivery

### Target the low-hanging fruit

This is a winning approach for various reasons - you have shown success quickly, demonstrated the benefits to various stakeholders, you gain confidence, good practices and principles starts from something small

Everyone needs to see/feel the value of doing "real" DDD - Lot of it was plain old solutionising and common sense but as I used models to explain and demonstrate this, the teams were able to relate the implementation to the abstract concepts. They were slowly warming up to it. These were also sessions where they can think aloud. Allow mistakes to be made, challenge assumptions, accept compromises. Flexibility is another winning secret of DDD. Remember Eric Evans and Alberto - the design doesn't have to perfect, doesn't have to neat. Note: GT to find quote

### Things that cannot be compromised! 

1. Language & Names - even if temporarily; I would rather have an ugly name because it forces me to think it over; early incorporation embeds these into the team for good or bad
2. Boundaries - beware of violating boundaries 
3. 

### Distill ... The noise. 

Learning to recognise what is core to your domain, to your business context, to your aggregate is important.

Domain distillation e.g. ATCM - overly complex solution of what is supposed to be a simple process. this is because the team had no visibility beyond their part of the process. This is because they implemented what turned out to be a typical Process Manger's job into their core process. It became very difficult to untangle from it, at one point we even considered scrapping the whole thing and build it from the start. 

### Looking through the crystal ball

There are many ways to skin cat - what you built may not be the perfect way of building, but as long it is one of the ways that is based on a domain model, then it is unlikely to fall over design wise. It is a WIN! E.g. We could have had an orchestration service which replicates the physical world of sorting out different types of prosecution notices and forward it to appropriate court or have the case land in the correct context depending on the type and then let the natural court process take it course as the case goes for referral to higher jurisdiction atcm->mag->crown.

It is worth remembering that real world != software application. Software world offers so many opportuniies to optimise that leverage it even if it means that performing business differently.

### Visualisation

Context maps can be drawn in various ways - I used them to even show the end to end process flow with the bounded contexts clearly marking the point where the responsibility is handed over to another party. This made it easier for the teams to undestand to see where they are in the big picture. 

These modelling sessions brought out new bounded contexts like Defence into the picture, merged contexts such as Mags and crown which were separate legacy systems but nonethless the same business process. Because of the two legacy system they had pretty much diverged in the real world as well (but no reason why they should be different in fact). Potential to change the real business process as a result.

### Driver for change 

A lot of people needed to let go of things, but without knowing exactly where we were going. Domain experts or in this case end users needed to unlearn a lot of things that they is ingrained in them throughlegacy systems. Our application is not going to be around for years, it will be legacy one day but as long as it had managed to capture the essence of the actual business process which doesn't change, the future is safe.

### Modelling is not cheap

One practical challenge at this scale was the cost. Cost of failing - yes (@Andrew touched on this before?) but also the cost of pulling people together to do modelling.
Therefore, define the problem statement ahead, and get the right people but no more. (A lot of vague things will get thrown at you, and you will be invited to a lot of meetings as "the domain expert". Beware of the PHANTOM PROBLEMS.

---

## Process
### Before

Governance - the G word; architects love it; engineers hate it! But there is some advantages to it. At such a scale it brings consistency and discipline across board, if it doesn't look like it is going to emerge organically, then a bit of process helps you get there. So we introduced a process by which when the increments go for gate review (for approval to resource, time and money) the teams present the outcome of modelling and if applicable the domain mdoel & add the models to the design document - model thus presented is not set in stone, could continue to evolve as increment goes on but this made sure that there was some modelling discussion that happened before the work kicked off and there was a good justification for the time and money being requested.

---

### Ownership

Team collectively owns the model. 
Everyone has some important insight and perspective to add to the model.
Collective ownership stimulates collective responsibility in implementation. 

---

### After
Design Retro - Find out the good, bad and the ugly. Make sure it is incorporated in the subsequent design sessions. One of the best retro feedback for myself was to pay extra attention to multi-step process which could seemingly look like a single step. E.g. Case Material and IDPC - I failed to realise early on that this is a two step process particularly for CPS where in step 1-> they get ALL the material from police, sort it according to each defendant AND step 2 -> then put them together in IDPC. we did not model the first step in code meaning, when the sort and allocatino process happens we were not storing the association of materials to defendant (only at the case level) but jumped straight into IDPC bundling process. WE COULD GET INTO TROUBLE IF I SAID THIS, I AM SURE)

---

## Tools and Methods
Draw out the entire architecture - showing all the BCs and microservices - Context map: Context Map and I had few versions of it is an excellent tool to show the enterprise architecture with all the microservices, their relationship at a high level. I drew another one to show how they came together as part of the process or journey. I also had smaller versions for the core teams made out which showed their BC at the centre and the other BCs they actively interact with, this filtered out the noise of the big picture which to Tom, Dee and Hari as devs is not as important as their own world. CONTEXT MAP IS A POWERFUL TOOL.
 
(WARNING: Don't make the context map do too much! - Use layers on top if it you need this)

Modelling Whirlpool - Where a strawman model is just what everyone needs to get things kicked off instead of a blank wall. Remember the cost as well, can you afford to coup people in a room for the whole day? How can you make things go faster. 

Event Storming - by far the best method to find aggregates and document events. It doesn't have to be a day long full blown exercise. Small, iterative sessions are helpful for solutioning too. It is a good method to document event driven contexts too. 

---

## Everyone get modelling

We're _all_ doing design; challenge again at scale is there are advocates and sceptics; DDD may not be bought in by everyone, this is fine as long as it doesn't become an impediment, a healthy scepticism is good for design. Find allies of DDD who can help you sell it.

Draw pictures!
C4 is good for this (Simon Brown has training for Developers too)
Find champions (junior folks can actually be good for this)
@gaythu-rajan to pull this into the right section of hers

---

## AS-IS <-> TO-BE vicious circle **** (GT)

Obtain knowledge of the domain from the As-Is state. Model the To-Be state. 
Domain changes more slowly than the system that we are building. 
Beware the legacy systems - they don't exactly reflect the domain knowledge.

@gaythu-rajan to pull into her sectino where appropriate

---

### You _can_ copy data ***** (AHL/GT)

Matthias Verraes : “Don’t Repeat Yourself” was never about code. It’s about knowledge. It’s about cohesion. If two pieces of code represent the exact same knowledge, they will always change together. Having to change them both is risky: you might forget one of them. On the other hand, if two identical pieces of code represent different knowledge, they will change independently. De-duplicating them introduces risk, because changing the knowledge for one object, might accidentally change it for the other object.

@andrew to pull this into his sectino on copuying data

---

### Pick your battles ***** (GT)

Don't spread yourself too thin
Don't waste time trying to convince everyone - some folks will come round to the idea, especially when they see it working
@andrew to talk about this in concliusion

---

# Stage 3: Applications in Other DDD-Derived Areas (E.g. CQRS)

---

## Discovery

TBC @andrewharmellaw

---

## Delivery

Challenge in documenting a CQRS architecture. 

CQRS is a paradox of DDD 

CQRS uses the term Aggregate. IMHO, CQRS aggregates are similar but not the same as a DDD aggregate. Often, I have found that one muddles the implementation of the other. CQRS ofcourse made the DDD aggregates famous. 

1. DDD is all about explicit modelling - In CQRS aggregates, apart from the root entity, the model is not visible. It is in pieces within the events. Although strictly events themselves are not domain models, they are BASED on your domain model (they are too denormalised to be a model - they just capture facts) 
2. In pure DDD, there can be group of entities as aggregates, again I beleive in CQRS most of the times, you will have only one entity as an aggregate root and the rest are value objects. It is mainly because as an entity with it's own lifecycle it would make sense to have to capture events in it's own stream hence a different aggregate. 
3. Strict definition of DDD Aggregate does not apply in CQRS -> for e.g. DDD aggregate mentions that the root is the only way to access the children in an aggregate and that's mostly how you will identify the root. This mostly lead in our project to "Case" being the root all the times! Everything needs to have a case to start with ofcourse. But in CQRS, this only means that the stream-id is caseId but the other entities can be an aggregate in themselves. E.g. Case, Casematerial, Defendant. They are separate CQRS aggregates as you want to capture events in their own streams but they all have the same streamId. (@GT to elaborate this a bit more to make it clear)
4. Read model or write model -> what is your domain model. If you overlay the domain model diagram it would seem like a read model which is a normalised view of domain data is you domain model BUT it is not. It is simple a projection. The meat of your model is in write side
5. Visualisation - very difficult at best of times. Our mind is trained to look at things in a synchronous(?) way, cause-effect, request-response. With async events flowing all over the place, it is difficult to capture a synchronised view of the architecture. The closest I got to was to use Sequence diagram to show a handovers and flow of events (instead of method calls)
6. CQRS Vs Rest Vs DDD - @gaythu-rajan to elaborate this

---

# Conclusion

* We didn't fix everything - this isn't a fairy story.  

* Don't get waylaid
* Have confidence - you're finding and iterating, and training
* You're the guide to the DDD Theme Park

---

# Appendixes

https://twitter.com/ntcoding/status/1097139309642158080
