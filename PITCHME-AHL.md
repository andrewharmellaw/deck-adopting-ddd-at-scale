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

# Intro

---

## The Near Enemies of Domain Driven Design (and how to recognise and defeat them)

  "The near enemy is a [...] counterfeit of what we’re actually aiming for, and it’s unhelpful because while the genuine article helps free us[...], the counterfeit doesn’t." from https://www.wildmind.org/tag/near-enemy

Note:
Quote: "The traditional term “near enemy” points to some spiritually unhelpful quality or experience that can be mistaken for a helpful quality or experience. The near enemy is a kind of counterfeit of what we’re actually aiming for, and it’s unhelpful because while the genuine article helps free us from suffering, the counterfeit doesn’t." from https://www.wildmind.org/tag/near-enemy

We say "people still don't get DDD". What do we mean?  With the rise of microservices it's being used everywhere right?  

Well, not really...

The concept of near enemies should be very familiar to anyone who has worked in software for even a short while - we have _many_ near enemies: great examples can be seen in the adoption of so-called "Agile" methodologies, and more recently in the drive towards "DevOps culture".  

In our opinion, the application of DDD, especially at scale is another one of them.

Why do Near Enemies arise? They arise because people do not engage fully with a concept. 

Typically this is because they ignore the core, fundamental aspects; which are also typically the most simple.  They forget the simple four lines of the Agile manifesto, or ignore the DevOps goals of breaking down boundaries and building a culture of learning.  Instead get tied up in the complicated details which seem more "valuable" and where the "expertise" lies.

We want to use this lens to present a collection of challenges and failure patterns we experienced when using DDD on a large scale.  It's ideal for these purposes (we could argue essential if you want in any way to succeed) but when things get complicated people can easily forget about the core concepts, and that causes problems.  

Hopefully this story will help you avoid falling into that trap.

!!!!!! We need to make clear at every point how the core got forgotten and things got lost !!!!!!

---

## Modernising the English and Welsh Criminal Justice System

!!!!!! @andrewharmellaw added this on top of the agreed sections !!!!!!

Note:
We're going to share the story of our most recent project together.

We have first-hand experience of seeing what DDD looks like on a large scale. 

We have seen in detail how pseudo-DDD is the near enemy[1] of real DDD, and that when it strikes it can make the adoption job all the harder.

In this story it's important to note that while we worked on the same project, we overlapped very little.  I (Andrew) inherited a bunch of early artefacts from another DDD expert whom I never met, and mainly handled the discovery of the domain.

Just as Andrew had inherited a legacy from those who went before him, I (Gayathri) inherited from him (with all the good and bad that that brings).  I (Gayathri) was largely focussed on delivering what Andrew had found (and challenging the assumptions he had made).

So what was the project? It was the transformation and modernisation of some core public systems within the UK Judicial system.

@gaythu-rajan and @andrew to alternate on each slide
 
---

## Our Constraints

  * Lots of code had already been cut
  * We were supporting the full justice-lifecycle, end to end, across multiple organisations
  * Significant scale - many teams, already working in parallel
  * CQRS _everywhere_
  * There was an efficiency-finding "modernising" agenda to serve
  * Existing tech legacy cast a _long_ shadow over domain experts

Note: 
When I (Andrew) joined the project things were already up and running and lots of code had already been cut. 

Consequently some DDD "ideas" had already become entrenched. 

@gaythu-rajan made further changes as it was still more object based split.


We had to support a full-lifecycle view - justice end-to-end. 

Not only that, the "domain" was co-owned: we were tasked with building a collection of systems which met the needs of two different stakeholder organisations - the State Prosecutor, and the Courts System - AND the END-TO-END-PROCESSES spanned even more client organisations. 

Note: @andrew mentions "No one domain expert had the end-end view", but even when they did it was never communicated to the those who are wrtiting the code. Head of BPOs was brought in but still that end-end view was stuck within a group of domain experts.


This massive piece of work was being tackled head on. 

When I (Andrew) started, software was being built by multiple (7?) teams in parallel.


Complex Architectural choices had been made (e.g. CQRS for everything) and devs were struggling with them. 

At the time I (Andrew) arrived it was almost always an impediment rather than a boost 

(We'll come back to this in the final section. For now, suffice it to say that it made the adoption of the DDD even harder)


We had to "modernise justice" as we delivered things. 

This meant we had to push back against "quick" wins (from which the resulting tactical solutions had incurred a great deal of debt in the code) and instead efficiently find the "real" wins.


Finally it's useful to raise the issue that Domain experts were stuck in the legacy way of thinking or worse paper based. In courts, traditionally, the prosecutors, defence and courts will fill in the same form alternately and the expectation was to translate that literally onto the software application. 

---

### Incredibly High Stakes

With all this in mind it is no surprise that things had got complicated prior to our arrival.  The stakes were INCREDIBLY HIGH, both RISKS and BENEFITS.

---

# Where things were when Andrew started? //when "we" started rather?

---
	
## BIG PICTURE: 

Note:
GROKK-ABILITY, 
END-TO-END-VIEW 
"Where is the big picture?" [AHL] - INTRO TO THIS PART

---

### Where was the Big Picture? [AHL]

Note:
I take a very "I'm the noob and I'm keeping the beginners mind as long as I can to get as deep an understanding as possible" style of approach to DDD.

When I first started I had to look at what was already there design-wise, including how it had manifest already in the team structures, lines of communication, dependencies (human and code), and codebases and artefacts.  

I needed to reverse engineer a big picture from the pieces I could find.  
 
As I did this I tried to make sure I didn't get sucked into too much detail in any one area.  At this stage I needed to avoid getting overwhelmed by any one thing.

I began by setting off a number of lines of enquiry - I had a vague idea of the domain, having spent a long time delivering software in the Scottish Legal system.  

As Scots will remind you, things there are distinctly different, but it allowed me to compare things and ask "North of the border they have to do this?  Is there an equivalent?" or question "In Scotland this is owned by a person who works for department X, is something similar needed here, and of so, who does it?"

I pulled in as many info sources as I could, official and unofficial, trying to avoid value judgements, and always looking for the edges. I wanted to know the full extent of where we found ourselves.

What did I find?

As we said earlier things here had been running for a while already.

There was a bunch of designs already in existence, and a significant amount of code already written.  There was also an architect who had done a bunch of the early work, but they had since moved on - we never overlapped. 

This is what I found. But what was lacking? 

LACKING: 
- THERE WAS NO WAY IN. 
- THERE WAS NO BIG PICTURE WITHIN WHICH TO LOCATE YOUR MORE DETAILED WORLD.  
- CONSEQUENTLY THE COGNITIVE LOAD WAS TOO HIGH ON INDIVIDUAL TEAM MEMBERS.  
- THERE WASN'T EVEN A SINGLE DOMAIN EXPERT WITH AN END-TO-END VIEW.

NEAR ENEMY: Design had been done. A lot of it in fact.  But it hadn't been laid out in a way that made it consumable by those who needed it the most - the Domain Experts and the Development Teams.

---
	
## CORE MODEL: 

Note:
DATA-NOT-PROCESS, 
MODELS
"one model to rule them all", [AHL]
"data focussed" [GT]

### "One Model to Rule Them All" [AHL]

Note:

Not only were there core aspects lacking. I uncovered problems with what _had_ stuck from the design efforts too.  These proved far more hard to resolve.

As I investigated, I slowly uncovered a few core tenents which had embedded themselves in the minds of everyone on the project. 

The most prevalent was a oft-repeated phrase that "a case is a case (is a case)".  


This had been interpreted to mean there should be a single representation of a case that made its way through the criminal justice system. 

It had also been decided that this Case representation be handled via a single "Case" microservice / datastore. 


Further investigation revealed that this had come into being via a (noble) desire to reduce data copying and hold central case records.  In itself, no bad thing.  

The issue was, this had accidentally pushed a data-centric view, at the expense of a process / behavioural one.  


Despite this being a CQRS shop, these didn't even really manifest in domain events.

(The domain events, such as they were weren't even very fleshed out, having mainly fallen back into the realm of CRUD operations.)

This wasn't evident in itself specifically - there was simply a lot of the former, and a significant absense of the latter. 


What did this mean? 

Most fundamentally, this core tenent had subtly given teams and domain experts the signal to look for _commonality and overlaps in the data_, and to de-prioritise the _differences in the ownership, processing and behaviour_.  This wasn't just confined to Cases either.

PROBLEM: 
- "ONE MODEL TO RULE THEM ALL" THINKING HAD BUBBLED UP,
- BOURNE OF A DESIRE NOT TO DUPLICATE DATA.
- CONSEQUENTLY DESIGN DECISIONS / TRADE-OFFS HAD BEEN MADE WITH ONLY A SUB-SET OF THE DOMAIN INFORMATION.

NEAR ENEMY: Domain Driven Design is about the data, and not the behaviour, or if it is both, then the data has more weight, and the behaviour is of secondary importance.  (I actually think it's the other way around.)


(@gaythu-rajan to elaborate with the defendant model and people context; mention how @andrewharmellaw comes up with the idea and how it was implemented)

---

### Data Focused [GT]

// @gaythu-rajan - this is nice, and gives more detail to the general point I make half way down the slide above.  I suggest we split that slide in two, and move this up into the gapo between them.

As mentioned the models were identified not based on behaviour/actors but purely object based which brought everything centered around the data. Object-centric split leads to data centered archtecture.

To give an example - A Case is not a case without someone being prosecuted. That someone could be a suspect at the beginning of a case and then become a defendant when the case is brought to the court. This is when the offence is indictable (you could go to prison for). In summary only offence, you enter the system as a defendant. As objects, these must have started as a suspect or defendant but there are other actors in a case such as police, victims, witnesses. This gave away to a more genric "catch-all" object called "People" - and the data captured in this object lived in a single place outside of the core contexts.

What's wrong with that? 

 a. First the realisation that Defendant/Suspect, are THE CORE of a case. They should live where the case model lives. 
 b. Reconciling the states in case of failures becomes easier. 
 c. There is no access control concerns over the data - who is able to access suspect information (very limited number of people). 
 d. Freedom to add richness to your own model of defendant depending on the context. No corruption of your model.

---

## (Pull "lifecycle", "object-based-split" from Constraints slide under here) [GT]  

// !!!!!! not sure it fits here. !!!!!!
// AGREED - I THINK WE CAN DROP THIS.

We had to support a full-lifecycle view - justice end-to-end. The "domain" was co-owned, we were tasked with building a collection of systems which met the needs of two different stakeholders - the State Prosecutor, and the Courts System - AND the PROCESSES entailed spanned even more organisations than that. 

Note: @andrew mentions "No one domain expert had the end-end view", but even when they did it was never communicated to the those who are implementing. Head of BPOs was brought in but still that end-end view was stuck within a group of domain experts.

We had to "modernise justice" as we did it, within a publicly funded program of work. Constantly having to battle with business against "quick" wins (from which the resulting tactical solutions had incurred a great deal of debt in the code) and instead efficiently find the "real" wins.

---
	
## OWNERSHIP

Note: 
Alone,  "Doing the DDD" [AHL]
"Ownership" [GT]

---

### Alone, "Doing the DDD" [AHL]

Note:
When I landed I was heralded as the "DDD expert".  

I'd go into meetings and people would address me as such. I even got called the "DDD Messiah" once.  

That's when I really started to get worried.

It was clear that there was not only a general awareness of my arrival, but also an expectation that I would be able to solve a lot of problems; and that DDD would be my tool for doing so.  

However, rather than everyone looking for a more general adoption of DDD as an approach / set of skills, I was there to take things off people's hands.

Worst of all, I wasn't there to deliver any code - I was an "Architect" purest sense.  It seemed as if people expected me to be there to do diagrams and definitely NOT write code.

PROBLEMS: 
- I WAS THERE TO SOLVE ALL THE PROBLEMS,
- AND I OWNED THE DESIGN. 
- DOMAIN EXPERTS AND DEVELOPERS WERE EXCLUDED. 
- I WAS GOING TO TELL EVERYONE WHAT TO DO,
- BUT WITHOUT HANDS ON.

NEAR ENEMIES: 
- Domain Driven Design isn't done "to" teams, it's done "by" teams.  Ubiquitous language needs to be _ubiquitous_.  
- Hands on modellers need to be _hands on_.  
- Domain Driven Design isn't for governance and _control_, it's a tool to _enable_.  People need to be trusted and helped to use it.

---

### Ownership [GT] <<<<<< TO COME from @gaythu-rajan

Architects wanted to not only 'own' the model, they also wanted to be its gatekeepers. -> I need to say something about people, desire to control which curtails the innovation in model 

@gaythu-rajan to add more bits here

@andrewharmellaw Again I think this fits really nice as a follow-up to my slide above, or as a topic sliced into it.  Actually, having read the slide below I think we could chop this up a little (i.e. put the slide boundaries in different places.)

---

## GROKK-ABILITY 

Note:
Perception @Scale [GT]

---

### Perception @ Scale [GT] <<<<<< TO COME from @gaythu-rajan

I (Gayathri) also realised that DDD was being 'done' because someone said so. 

Very few teams had realised the actual benefits of doing it but many were experiencing a lot of pain from doing it wrong.

This lack of awareness about DDD was a big problem. It was seen as 'someone' else's problem, teams were not clear about whose responsibility it was to do DDD, more often than not it was seen as a directive from the top, seen as a 'must be done' step rather than something which developed organically.

Having burnt their hand once, everyone was keen not to repeat the same mistake again. Which is all good only they didn't realise what the mistake was (not doing modelling enough and not iterating on it). Everyone now wanted to get it right and get it right the first time (well second time, anyway). So the business architects were constantly at me asking about the governance (i.e ring fence the model with tight governance so that noone can mess around with it!) and also expecting guarantees from me that this is the "correct" model!

We will see again and again that people are the making or breaking factor for any adoption at this scale be it Agile, DevOps or DDD. We had to deal with a good many sceptics, critics and some who point blank refused that DDD is useful. I stopped explaining why they should DDD but resolved to show them its merits in practice instead.

---

## BCs (Naming Teams) [GT]

@andrewharmellaw - I think we'd need to give too much context to the audience to make this point in the time we have.  What do you reckon?

Teams named after the part of business process they were working on (which would change and grow) like C2I, I2T etc. rather than named from contexts - Prosecution/Defence/Courts/SJP etc. which would create teams specialised in that part of the legal system. 

Wrong names/contexts were used by the wrong teams. Scheduling was something used by ATCM which created SJP session.

---

# BREATHER: The Legal Domain

---

## Legal Systems are **Complex** [BOTH]

Note:
We need to pause a few seconds and state what might be obvious.

It's no wonder that things had got confused in the places they had in the ways that they had.

Legal systems are complex.  

They have evolved over _significant_ periods of time, and they contain TIME itself as a significant Domain consideration (i.e. the law changes, things can expire, things have deadlines).  

They bring together a great number of (by the very nature of the adveserial system, hostile) parties, all who have their views on the system, and obligations / needs to be met.  

Most importantly, they must contain within themselves a great deal of flexibility, while still balancing against this an incredible formality; seemingly small details can make large differences, and have VERY SERIOUS, real-world outcomes.  

---

## Legal Systems are **Ripe** for DDD [BOTH]

ALL IN ALL, THEY MAKE FOR AN EXCELLENT SET OF CIRCUMSTANCES TO EMPLOY THE TECHNIQUES OF DOMAIN DRIVEN DESIGN.

---

# DOING

---

## GROKK-ABILITY / END-TO-END-VIEW

Note:
If we can't grokk it, how can anyone else?
"How do the Key Pieces Fit Together?" [AHL]


---

### How do the Key Pieces Fit Together? [AHL]

Note:

@andrewharmellaw: WHAT WENT IN THIS SECTION? PERHAPS THE FOLLOWING?

Knowing about all the various models is one thing. 

When you're doing work this complex, at this scale, knowing how they inter-relate, interact, and (possibly) overlap is the _big_ thing.  

We've discussed a little about the unsuccessful attempt to distill out a core - the case of Case.


Remember; this was a very process-intensive environment, where our things (Cases) pass through a lot of organisations and hands.

Discovering the spine / the armature of the domain as a whole turns out to be fundamental in this. 


You don't need to do this all bottom-up.  You can start from the top, or take value-stream slices. 

Going *end-to-end* helped us _a lot_.  

(This is a great use case for Event Storming, and one reason why it has proved so popular.)

(There is a paradox here - I needed to investigate this first, in order to find the concrete elements, which then allowed me to pull back out to see how everything joined together into the whole, bigger picture.)

NEAR ENEMY: When modelling, don't lose the bigger picture. 

---

## DATA-NOT-PROCESS, CORE-DOMAIN

Note:
"A Case is a case is a case" [AHL]
"Shared Kernels and the Abstract Core" [AHL], 
"Mind the Gap" [GT]

---

### "A Case is a Case is a Case" [AHL]

Note:
The route into everything was to try and tackle the "case is a case (is a case)" issue.

I could see where it had come from; the idea was to modernise the criminal justice system, and to remove some of the unnecessary complexity.  

!DATA!DATA!DATA! ADD SOMETHING ABOUT DATA (AND TRYING NOT TO HAVE TOO MUCH OF IT) HERE. 

@gaythu-rajan to pull this into the data section.

One way to do this was to find things which where similar and to treat them in the same way.  From some angles, there was a lot to suggest that fundamentally, cases were a candidate for this.  The problem was, the simlarities were less than anticipated, and the differences were critical - mainly in the regards to who owned the cases and how they were handled as they made their way through the system.


NEAR ENEMY: When exploring the domain, listen for difference, rather than look for similarity.  Don't abstract too early.


How to prove one way was right, and the other wrong however?

The problem became painfully evident when looking at the existing Case Aggregate - it was *massive* and had tons of attributes.  It also had a significant amount of contributors - it was a *very* hot piece of code. Everyone wanted to add their stuff to it.  

I began by apportioning each of the attributes and functions to the team which had added them. Perhaps they'd just failed to communicate about what they needed and ended up duplicating things?  It's a common problem.

In parallel I went out to sit with the teams themselves, predominantly their domain experts;  They would be the ones who knew what was needed, and more importantly, the activities and business processes that the concept of a "Case" would need to support in their area.  

It was abundantly clear very early on, that there were many types of case, which served different purposes in the criminal justice system.  

But not only that, they were owned by different stakeholders, meeting differing purposes, and undergoing very different lifecycles.  

At this level of detail, there were quite clearly many types of case, which were related (more on that later) but were also very different.

This is where the tensions arose.  How to square the circle? How could I reconcile the pull in these two opposed directions?  To keep the shared concept (which at some level wa correct - a case was a case from some perspectives) but balance it with the need for explicit differences.


NEAR ENEMY: Don't solve one problem at the expense of another.  Embrace all tensions, and use the tools of DDD to make them and the solution to reconciling them explicit.


I went back to DDD; and there was something to help me out: Shared Kernels and the Core Domain.

---

### Shared Kernels and the Abstract Core [AHL]

Note:
While I disagreed that "a case was always a case" because this lost too much detail in abstraction, it was also the signal that there was highly likely to be a common core - in DDD parlance a shared kernel.  

[BRING IN THE DDD DIAGRAM AND DEFINITIONS HERE]

The flow of cases through the criminal justice system _is_ a collaborative one. There is a fixed number of ways for cases to come into being, and there is a very strict set of protocols governing how they change from one type to another.  

There is space at this point to bring in one more concept. Beneath everything, there was something which, on it's own was never enough to be a case in its own right, but that could be considered an "Abstract Case" from which all concrete types of case could inherit.

(Example: Go into this with an example of A PCD Case and a MagistratesCourtCase - showing the example of Suspects and Defendants.)

---

### Mind the Gap [GT] <<<<<< TO COME from @gaythu-rajan

When I took over from Andrew, I realised that there was a chasm between the models he had identified and their implementation in code. 

First and foremost, very few realised that the model had to be translated into code, and even fewer had any idea how to go from there.

At that point we still had the big 'Case' model Andrew mentioned, and the teams had realised they needed to split it out. 

Andrew had identified at least three different models for a case. So they roughly went about hacking the case into 3 pieces.

Beware the pseduo DDD experts. Advocating for a literal translation of real world paper based process to software. This brings service orchestration into the equation and thus single point of failure.

@andrewharmellaw - the above paragraph jumps in out of nowhere.  How does it link into what goes before it?

I mentioned the implementation of the new models before - it was not an easy job. There already was an implementation which cannot be changed in a big-bang approach even within a single BC. 

Incremental changes towards the final model; and while incrementing constantly validating and challenging the model was important.

---

## THE END-TO-END-VIEW 

Note: 
"()->|()->()" [AHL]
"The Domain is Talking to You"  [AHL] 
"Visualisation" [GT]


### ()->|()->() [AHL]

Note:
While we leave Gayathri wrestling with the tough task of actually splitting out the various types of case in the code base, I'd like to introduce the next concept.

This one *isn't* explicitly brought out in the (Blue) DDD book.  

Alberto Brandolini had however identified it, and if I'd know that when I started I might have been a lot more confident in what I uncovered.

Having pulled out the shared kernel of cases, and having identified how this was manifest in various contexts to solve various problems and support various activities the question of how these were related could no longer be avoided.  

It was clear that not only did each distinct case model exist within its own bounded context, but also that there was a clear flow from one manifestation to another:

()->|()->()

But despite this breakthrough, I was nervous.  I was nervous about the nature of the relationships between these contexts.  

I knew relationships between bounded contexts was significant - I am a big fan of the strategic design patterns and the clarity they gave - but what I had here felt like a different form.  

Instances of earlier case types would almost transmogrify into subsequent instances.  

These relationships between bounded contexts represented a flow of execution and data and ownership (over a significant period of time, but a flow nontheless). 

It seemed like I'd come across something fundamental.

With hindsight this seems obvious, but which made me nervous at the time, 

@gaythu-rajan to provide the sketch of this

### The Domain is Talking to You  [AHL] 

!!!!!! ADDED THIS AS IT FELT LIKE A LEAP WITHOUT IT !!!!!!!

I went back to the domain experts.  What I thought I could see in the model was right there in the domain in their heads. 

It was clear very rapidly that there were business-level processes (ceremonies even) involved in moving cases from one context to the next.  These moves involved significant conceptual (and data-level) changes.  They had specific criteria, and ownership was typically transferred from one organisation or body to another.

This discovery felt good, a real modelling breakthrough, mainly because it was corellated strongly to the domain reality. 

A year or so later, in a workshop with Alberto Brandolini, he introduced his archetype.  When I saw it I could immediately recognise it for what it was, and realised there were *many* manifestations.  I felt satisfied.  

There were relationships - and they were creation-level ones. One model could pass control onto a downstream model, and create that downstream model in the process.

I turns out that this is entirely valid.

It also turned out that I'd not brought the development teams along with me.

NEAR ENEMY: The greatest modelling breakthroughs are worthless if they don't end up down in the code.

---

### Visualisation [GT] <<<<<< TO COME from @gaythu-rajan

@andrewharmellaw - I think this could actually go _after_ the "Icebergs and Icecubes" slide.

Context maps can be drawn in various ways - I used them to even show the end to end process flow with the bounded contexts clearly marking the point where the responsibility is handed over to another party. This made it easier for the teams to undestand to see where they are in the big picture.

These modelling sessions brought out new bounded contexts like Defence into the picture, merged contexts such as Mags and crown which were separate legacy systems but nonethless the same business process. Because of the two legacy system they had pretty much diverged in the real world as well (but no reason why they should be different in fact). Potential to change the real business process as a result.

NEAR ENEMY: Purity in delivery of DDD artefacts can make them difficult to consume for teams.  They are just tools - the code is the real model, so work to make it 

---

## Bounded Contexts

Note:
"Icebergs and Icecubes" [GT], 
"Splits vs Silos" [GT]

---

### Icebergs and Icecubes [GT] <<<<<< TO COME from @gaythu-rajan

At the code level, all this combined to create a significant set of problems - complexities had been created where there needn't be any (significant amounts of complex shared code, lack of domain understanding - in both breadth and depth - in the devs) and over-simplifications where the domain actually needed to be far richer. We came to refer to these as the "icebergs".

(To illustrate this we need to provide a lightning intro to the dynamics of the domain we're talking about.) - TODO - Simplified pictorial rep of domain here?

Sometimes requirements and reduced scope can diguise a key process as a simple straight forward one. The real magnitude of it can only be obtained by looking into the actual domain.

Therefore, do not constrain yourself by requirements and scope (MVP) when learning about the domain. MVP is another near enemy! Once the actual process is learnt, distill the bits not within scope and what remains is implemented but at least you know the true size of it and confident that the model can expand as the scope gets bigger.

One such example is the IDPC. What was perceived as a simple service for PDF generation from multiple documents was actually a key stage in the prosecution process particularly one main prosecutor (the Crown Prosecution Service). As you will hear later, while implementing this feature I personally learnt the above lesson of not underestimating the size based on just the MVP.

The other side of this exists too. What is considered as a big problem (Ice cubes?) sometimes fizzles into nothing. Simulataneous updates to a case is a good example. When I started there was serious apprehension amongst domain experts about how to deal with simultaneous updates to a case. So I was asked to setup a DDD session to find a solution to this problem.

It actually turned out to be a design smell by not defining the boundaries between different models of the case. When we started implementing the different models in their own bounded contexts, this problem just went away.

Access control is another example - of course it is important but delineation of models particularly multiple models of the same entity in their own bounded context and operated on by corresponding actors provides out of the box access control at the very basic level.

---

### Splits vs Silos [GT] <<<<<< TO COME from @gaythu-rajan

One of the teams were dying to split off and be able to do things on their own. This new-found freedom was even more dangerous as there was the risk of the models diverging irrevocably. There was a need to distinguish this from the freedom to work independantly make changes, release and operate.

In the legal system, different parties go off on their own to work on the case file - collect evidence, witnesses, putting together documents, case material and then COME TOGETHER for the next phase of hearing, sentencing. 

Not realising this was a big failure. I.e. Even though teams should have the freedom to go off and work within their boundaries on thier own model, at the end of that process, they will have to be able to come back together which means they can't diverge too much from a consistent thread of a model. (Knowing the strategic pattern andthe team relationship was important here - as it was "Separate Ways" here but "Partnership")

So my job was to make sure that the teams were made aware that this is not the chance to break free. This is when I realised that the teams were not aware of the business process outside of their domain - Team building Pre-Charge were not aware of the next stage and so on. The other danger was from avoiding Silos forming from these splits.

@gaythu-rajan pull this to the place where @andrew talks about independant teams

---
	
## MODELS->CODE - 

Note: "Looking through the crystal ball" [GT], 
"Shortsight vs longsight" [GT],
"[Generic Sub Domain]" [AHL]

---

### Looking through the crystal ball [GT]

There are many ways to skin a cat - what you build may not be the perfect way of building, but as long it is one of the ways that is based on a domain model, then it is unlikely to fall over design wise. It is a WIN! 

E.g. We could have had an orchestration service which replicates the physical world of sorting out different types of prosecution notices and forward it to appropriate court or have the case land in the correct context depending on the type and then let the natural court process take it course as the case goes for referral to higher jurisdiction atcm->mag->crown.

It is worth remembering that real world != software application. Software world offers so many opportuniies to optimise that leverage it even if it means that performing business differently.

---

### Shortsight vs longsight [GT] 

Another sign of failure is failing to realise the difference between learning the domain beyond what the 'requirements' captured vs future proofing. The former means due to the deeper insights gained from the domain the model will be more robust and less likely to fall over because the real world seldom changes at the same pace as the requirements on which a software application is built. While the latter means, you are anticipating these requirements to come up later and building it in advance. Constantly having to battle with businesss quick wins and resulting tactical solutions incurred so much debt in code.

---

### When is Something NOT a Generic (Technical) Subdomain? [AHL]

@andrewharmellaw - I THINK WE CAN DROP THIS TO SAVE TIME. WE MIGHT WANT TO PULL SOME SPECIFIC BITS OUT OF IT HOWEVER.  

(Such as the bits for "Domain Experts - Good" below)

---

## DOMAIN EXPERTS

Note:
Good - ( from "When is Something NOT a Generic (Technical) Subdomain?") [AHL]
and Bad -  "Distill... the noise" [GT], 
"Driver for change" [GT]

---

### Domain Experts - Good [AHL]. (from "When is Something NOT a Generic (Technical) Subdomain?") 

Scheduling in Courts seemed initially to be the opportunity for an off-the-shelf product, perhaps with a little wrapping up to expose it in a meaningful way to consuming parties (other BCs).  I'm going to talk a little now about how listening to domain experts led me away from this conclusion.

The seam I mined was based around the edge cases - when the scheduling was a complex matter, when it changed, when it was significantly sized.  It turned out that these circumstances weren't universal in this Criminal Justice System. Luckily we had domain experts who had a wide range of experience.  By asking about the biggest jurisdictions, and the circumstances when things were the hardest / most comoplicated, we eventually settled on a model which could represent the real richness of this complex task.  

Along the way we'd discovered that there were individuals who had this scheduling task as their sole responsibility, and that there was frequently a great deal of intuition, insight, and discretion that they applied.  This was beyond mere slot-filling.  These people were applying a great deal of local knowledge, and awareness of many upstream feeding-factors about which they could only have learned through experience.

NEAR ENEMIES: Think you know better than a Domain Expert.  Thinking that all Domain Experts are the same and will all agree all the time.

---

### Distill... the noise [GT]

Learning to recognise what is core to your domain, to your business context, to your aggregate is important.

Domain distillation e.g. ATCM - overly complex solution of what is supposed to be a simple process. this is because the team had no visibility beyond their part of the process. This is because they implemented what turned out to be a typical Process Manger's job into their core process. It became very difficult to untangle from it, at one point we even considered scrapping the whole thing and build it from the start.

---

### Driver for change [GT]

A lot of people needed to let go of things, but without knowing exactly where we were going. Domain experts or in this case end users needed to unlearn a lot of things that they is ingrained in them throughlegacy systems. Our application is not going to be around for years, it will be legacy one day but as long as it had managed to capture the essence of the actual business process which doesn't change, the future is safe.

---

# TRANSFORMATION

---

## Iterate

---

### Method: Model -> Share -> Question -> Repeat [AHL]

@andrewharmellaw - DID WE WANT THIS ONE HERE? (I'M HAPPY TO DROP IT)  We could put any bits we want to keep up in other slides.
YOU HAD SOMETHING ABOUT THE MODELLING WHIRLPOOL.

Note:
Draw lots of pictures - try and find what is "comfortable". Being able to draw something on a sheet of A3, or a standard whiteboard is a good sign that the level of detail is correct.

Go back to the book. The "pattern style" that it is written in means it is very easy to find your problem already described.  Then simply follow the solution.  

Find the *armature* - it sometimes seems to me that this part of the process is a lot like discovering the model's armature.

Share these pictures constantly.  Adopt a beginners mind.  Articulate when something doesnt feel comfortable (though be willing to accept a minor amount of discomfort, not everything will fit elegantly into the model you need.)  Get the help of others - specifically the domain experts.  Gather round the board and ask questions of your models and see when they break.

At a meta level, it was exciting to come at DDD from another angle. It meant I had to re-read Eric's book, and find value in other parts which I'd previously skimmed. I was amazed (yet again) at how relevant and applicable and valuable these concepts were.

---

## IDEAS LEGACY - (DOMAIN VISION STATEMENT++, multiple models of the same thing, actors coming together, process-centric, etc.) 

@andrewharmellaw - It feels like we could drop this entire section to save time.  If any elements are key points we don't want to drop we could re-home them.

---

### Articulate the Domain Vision [AHL]

Note:
By the time we got to this point, there was a LOT of detail - even in the Context Map. I needed something simpler to show key stakeholders and people beginning their journey into the domain. It turns out, yet again, DDD had something for me - the Domain Vision statement.

---

### Why have a Domain Vision Statement?

- the critical aspects of a Domain may span multiple bounded contexts
- but you can't structure them to show their common focus
- write something (a single page) to bring this out and keep the team headed in a common direction

---

### What's in a Domain Vision Statement?

- Paragraph One: The key entities
- Paragraph Two: The key roles / activities / events 
- Paragraph Three: The key integrations

In _each case_, include _why_ these elements are important.  

Note:

DETAIL: Describe how we used it. (Do you cover this @gaythu-rajan? I think I saw that you did...)

---

### Multiple models of the same thing, actors coming together, process-centric, etc.

I think these are all yours @gaythu-rajan. Right?

---

## CONTEXT MAP (TO-BE)

---

### The Resulting Context Map [AHL]

Note:

@andrewharmellaw - this next para is a repeat.  Also you talk about Context Maps higher up.

I used to think you only discovered Bounded Contexts from modelling lower-level concerns and then using the concept to split your models.  We had in some respects short-circuited this.  We did it by paying attention to Conways Law and studying organisations, departments, actors and jobs-to-be-done.

(Event Storming is also good for this and another short-cut.)

We could now draw our context map.

[BRING IN THE DDD DIAGRAM AND DEFINITION HERE]

[Rough sketch of the context map - @Gayathri, do you have a memory of this which might help?] - yup, @andrew to say this is how it started and @gaythu-rajan 

[Describe the map]

This map, with it's representations of the spine, ... all in the ubiquitious language was a very useful artefact.  It served exactly the purpose stated in the blue book.  it served to orient, to scope, to show relationships (and flow).

[Allude to the relationships, and the direction and their nature (all partnership / shared kernel?)]

---

## Talking to Domain Experts

@andrewharmellaw - We have a bunch of stuff on Domain Experts about 5 slides above this.  Do we want to merge? (I think we should.)

---

### _Loads_ of Lovely Domain Experts - Listen [AHL]

Note:
This unified "Case" construct came into direct conflict with the fact that there were many teams, working with their own individual domain experts, on different services, with different release plans; all of whom had to play in this shared "Case" space.

The existence of the domain experts, embedded 3 out of 5 days with each team was a boon. (I've seen _many_ DDD projects fail due to a lack of this.)  This involvement must have been incredibly difficult to plan, set up and finance, and as such it needs to be explicitly called out as a win.

GOOD THING: HAVING DOMAIN EXPERTS AROUND ALL THE TIME IS A MUST.  

There was a problem however. In many teams, the domain experts weren't being used to their full potential.  I kept coming across the worrying signs that the technical people didn't agree with their embedded Crown Prosecution rep. And not just on which version of a java library to use. No, I heard people saying that they were wrong when they described how their job worked.

---

### _Loads_ of Lovely Domain Experts - Listen [AHL]

NEAR ENEMIES: 
- NOT _LISTENING_ TO THE DOMAIN EXPERTS. 
- UNWRITTEN TENET: DOMAIN EXPERTS **DON'T** KNOW BEST.

Note:
A little later I stumbled upon something which might have been the root cause of the above lack of shared domain understanding.  Almost a myth, most likely born of misunderstanding / misinterpretation than anything else - it was that "diagrams can't be drawn".  And despite the fact that a few guerilla diagrams were in existence, this ghost-dictat had largely been adhered to.  

What this was saying to me was "ubiquitous language needn't be ubiquitous, nor does it even have to give us clues".

Worse still, it was stopping developers playing with the language of the domain in order to grasp it more deeply, and consequently arrive at modelling breakthroughs.
@Andrew - make this and then next one into single slide?

---

## Process, Tools and Methods

---

### Process [GT]

---

#### Before [GT]

Governance - the G word; architects love it; engineers hate it! But there is some advantages to it. At such a scale it brings consistency and discipline across board, if it doesn't look like it is going to emerge organically, then a bit of process helps you get there. So we introduced a process by which when the increments go for gate review (for approval to resource, time and money) the teams present the outcome of modelling and if applicable the domain mdoel & add the models to the design document - model thus presented is not set in stone, could continue to evolve as increment goes on but this made sure that there was some modelling discussion that happened before the work kicked off and there was a good justification for the time and money being requested.

---

#### After [GT]

Design Retro - Find out the good, bad and the ugly. Make sure it is incorporated in the subsequent design sessions. One of the best retro feedback for myself was to pay extra attention to multi-step process which could seemingly look like a single step. E.g. Case Material and IDPC - I failed to realise early on that this is a two step process particularly for CPS where in step 1-> they get ALL the material from police, sort it according to each defendant AND step 2 -> then put them together in IDPC. we did not model the first step in code meaning, when the sort and allocatino process happens we were not storing the association of materials to defendant (only at the case level) but jumped straight into IDPC bundling process. WE COULD GET INTO TROUBLE IF I SAID THIS, I AM SURE)

---

### Tools [GT]

@andrewharmellaw - we talk about this earlier, but I think it's better dealt with in this section.

Draw out the entire architecture - showing all the BCs and microservices 

Context map: Context Map and I had few versions of it is an excellent tool to show the enterprise architecture with all the microservices, their relationship at a high level. I drew another one to show how they came together as part of the process or journey. 
I also had smaller versions for the core teams made out which showed their BC at the centre and the other BCs they actively interact with, this filtered out the noise of the big picture which to Tom, Dee and Hari as devs is not as important as their own world. CONTEXT MAP IS A POWERFUL TOOL.

(WARNING: Don't make the context map do too much! - Use layers on top if it you need this)

---

### Methods [GT]

---

#### Modelling Whirlpool [GT]

Where a strawman model is just what everyone needs to get things kicked off instead of a blank wall. Remember the cost as well, can you afford to coup people in a room for the whole day? How can you make things go faster.

---

#### Event Storming [GT]

By far the best method to find aggregates and document events. It doesn't have to be a day long full blown exercise. Small, iterative sessions are helpful for solutioning too. It is a good method to document event driven contexts too.

---

# Complicated Bits [GT] <<<<<< TO COME from @gaythu-rajan

---
	
## CQRS good - history and replayable In (core domains)

@andrewharmellaw - I can put some things in here...

---

## CQRS bad - end-to-end!!! devs don't think like this

Challenge in documenting a CQRS architecture.

CQRS is a paradox of DDD

CQRS uses the term Aggregate. IMHO, CQRS aggregates are similar but not the same as a DDD aggregate. Often, I have found that one muddles the implementation of the other. CQRS ofcourse made the DDD aggregates famous.

DDD is all about explicit modelling - In CQRS aggregates, apart from the root entity, the model is not visible. It is in pieces within the events. Although strictly events themselves are not domain models, they are BASED on your domain model (they are too denormalised to be a model - they just capture facts)

In pure DDD, there can be group of entities as aggregates, again I beleive in CQRS most of the times, you will have only one entity as an aggregate root and the rest are value objects. It is mainly because as an entity with it's own lifecycle it would make sense to have to capture events in it's own stream hence a different aggregate.

Strict definition of DDD Aggregate does not apply in CQRS -> for e.g. DDD aggregate mentions that the root is the only way to access the children in an aggregate and that's mostly how you will identify the root. This mostly lead in our project to "Case" being the root all the times! Everything needs to have a case to start with ofcourse. But in CQRS, this only means that the stream-id is caseId but the other entities can be an aggregate in themselves. E.g. Case, Casematerial, Defendant. They are separate CQRS aggregates as you want to capture events in their own streams but they all have the same streamId. (@GT to elaborate this a bit more to make it clear)

Read model or write model -> what is your domain model. If you overlay the domain model diagram it would seem like a read model which is a normalised view of domain data is you domain model BUT it is not. It is simple a projection. The meat of your model is in write side

Visualisation - very difficult at best of times. Our mind is trained to look at things in a synchronous(?) way, cause-effect, request-response. With async events flowing all over the place, it is difficult to capture a synchronised view of the architecture. The closest I got to was to use Sequence diagram to show a handovers and flow of events (instead of method calls)

CQRS Vs Rest Vs DDD - @gaythu-rajan to elaborate this

---

# Conclusions

---
	
## Modelling is not cheap [GT] 

One practical challenge at this scale was the cost. Cost of failing - yes (@Andrew touched on this before?) but also the cost of pulling people together to do modelling. Therefore, define the problem statement ahead, and get the right people but no more. (A lot of vague things will get thrown at you, and you will be invited to a lot of meetings as "the domain expert". Beware of the PHANTOM PROBLEMS.

---

## As-is / to-be vicious circle [GT]

Obtain knowledge of the domain from the As-Is state. Model the To-Be state. Domain changes more slowly than the system that we are building. Beware the legacy systems - they don't exactly reflect the domain knowledge.

---

## You _can_ copy data - look to the Process

Matthias Verraes: “Don’t Repeat Yourself” was never about code. It’s about knowledge. It’s about cohesion. If two pieces of code represent the exact same knowledge, they will always change together. Having to change them both is risky: you might forget one of them. On the other hand, if two identical pieces of code represent different knowledge, they will change independently. De-duplicating them introduces risk, because changing the knowledge for one object, might accidentally change it for the other object.

