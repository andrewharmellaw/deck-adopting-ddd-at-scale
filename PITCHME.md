## **Combatting Near Enemies**
### _Adopting Domain Driven Design at Scale_
#### MuCon 2019
##### Gayathri Thiyagarajan and Andrew Harmel-Law

---

**Andrew Harmel-Law** <br/>
Tech Principal @ ThoughtWorks <br/>
[@al94781](https://twitter.com/al94781)

Note: 

* Java dev (worked on Microservices, CQRS, continuous delivery, and cloud-native computing _at scale_) with DDD under it every time.

---

**Gayathri Thiyagarajan** <br/>
Engineering Lead @ Expedia Group <br/>
[@gaythu-rajan](https://twitter.com/gaythu-rajan)

Note:

* Java Engineer for over 15 years and working on DDD, Microservices, Event Sourcing, CQRS in BigData environments for the past 5 years

---?color=#e49436

![Near Enemy](img/ogre.png)

@quote[*Near Enemies* are counterfeits of what we’re actually aiming for, and they're unhelpful because while the genuine article helps free us, the counterfeit doesn’t.](https://www.wildmind.org/tag/near-enemy)


Note:

## The Near Enemies of Domain Driven Design [AHL]
### (How to Recognise and Defeat Them)

We've often been heard to say "people still don't get DDD". What do we mean?  With the rise of microservices it's being used everywhere right?

Well, not really...

There is a concept in Buddhism called the "near enemy".  It's well described by this quote (read quote).

In software we can spot _many_ near enemies: most notably the adoption of so-called "Agile" (and associated backlash), and more recently in the drive towards "DevOps culture".

DDD, especially at scale is another one of these where near enemies strike frequently.

Why do Near Enemies arise? Because people do not engage fully with a concept.

And frequently its because they ignore the core, fundamental, simple aspects of a concept

For example, they forget the simple four lines of the Agile manifesto, 

Or ignore the DevOps goals of breaking down boundaries and building a culture of learning.  

Instead people get tied up in the complicated details which seem more "valuable" and where the "expertise" lies.

We're going to use this "Near Enemy" lens to tell a story and present a collection of common challenges and associated failure patterns we've experienced doing DDD on a large scale.


Hopefully we can help you avoid falling into many "Near Enemy" traps.

---?image=img/Overlapping-Timelines.png&size=contain

@snap[north span-85]
### "Bringing Criminal Justice into the 21st Century"
@snapend

Note:

[AHL]
Gayathri and I are going to tell you about our most recent project together.


In this story it's important to note that we overlapped very little; just a month.  I (Andrew) inherited a bunch of early artefacts from another DDD expert whom I never met, and mainly handled the continued discovery of the domain for a further 9 months.


[GT]
I (Gayathri) inherited from Andrew - with all the good and bad that came with it 

For 12 months, I largely focussed on implementing what Andrew had, further challenging and changing the assumptions he had made as further domain insight was unearthed.

So what was the project? 

It was the modernisation of core public systems within a Judicial system.

---

## Key Constraints 

@ol

* Modernisation of the end-to-end justice lifecycle (spanning multiple organisations)
* Teams already identified and code already being cut
* CQRS _everywhere_

@olend

Note:

[AHL]
To ensure you have the right picture, we need to make our constraints on this project clear:


1. Our "domain" was co-owned: we were tasked with building a collection of systems which met the needs of two different stakeholder organisations - the State Prosecutor, and the Criminal Courts. What is more, the END-TO-END-PROCESSES spanned further client organisations.


2. When I (Andrew) joined the project this massive piece of work was already being tackled head on. Software delivery was already up and running; the work for (7 or more) feature teams had been allocated and lots of code had already been cut. Consequently some DDD "ideas" had already become entrenched. (We'll get to them in turn later.)


3. Some complex architectural choices had been made (e.g. CQRS for everything) and devs were struggling with them. At the time I (Andrew) arrived this was still proving an impediment rather than a boost to productivity.  The benefits had very much still to pay off.

---

## Incredibly High Stakes 

Note:
[GT]

With all these constraints, it is no surprise that things had got complicated prior to our arrival.  

The stakes were INCREDIBLY HIGH, both in RISKS and BENEFITS.

---

# In The Beginning... 

Note:

When I arrived I set off a number of lines of enquiry, looking always at what was already there; design-, code- and team-org-wise.

I pulled in as many info sources as I could, official and unofficial, trying to avoid value judgements, and always looking for the edges. I wanted to know the full extent of where we found ourselves.

I paid attention to lines of communication, and identified dependencies (both human and technical).

As I did this I tried to make sure I didn't get sucked into too much detail in any one area.  
I needed to avoid getting overwhelmed.


---?image=img/Simple-World-Map-Wikipedia.png&size=contain

Note:

## Where was the Big Picture? [AHL]

I found a LOT, much of it very detailed, and incredibly insightful.


But what was lacking?

Fundamentally, it was the fact that I'd needed to reverse engineer a big picture from the pieces I found.

---?image=img/Simple-World-Map-Wikipedia.png&size=contain

## Problem Summary

@snap[north-west span-40]
@box[bg-white text-black text-left span-80 fragment](No single domain expert with a detailed, end-to-end view)
@snapend

@snap[north-east span-40]
@box[bg-white text-black span-80 fragment](No obvious "Big Picture") @note[within which a team could locate itself in the detailed domain-world.]
@snapend

@snap[south span-40]
@box[bg-white text-black span-80 fragment](The cognitive load was much too high) @note[for those building the software.]
@snapend

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>
Design has been done but it hasn't been laid out in a way that makes it consumable.
@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>
Design has been done but it hasn't been laid out in a way that makes it consumable.

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>
Make sure all your design artefacts are created with the audience in mind.
@snapend

---

# THE CORE MODEL?

Note:

So a key overview aspect was lacking.

My investigations also uncovered a key problem with the existing design too.  

This proved far harder to resolve.


---?image=img/Single-Case-Microservice.png&size=contain

Note:

### "One Case to Rule Them All" [AHL]

While investigating I'd repeatedly come across a core belief embedded in the minds of _everyone_ on the project.


  "a Case is a Case (is a Case)".


When and why this chant arose is unclear (perhaps from the prime directive to "take the justice system into the 21st century").  It is likely the aim was to reduce duplication of effort, software and data.

But by the time I got there it been interpreted to mean:

  there is a single representation of a Case
  shared across all software, 
  and that this single Case model be wrapped in a single microservice.

---?image=img/jedward.jpg&size=auto 100%&position=right

@snap[west span-50]
### Similar,<br/> but Not the Same 
@snapend

Note:
[AHL]

I mentioned the suspicion that "A Case is a Case" arose from a desire to reduce duplication. 

The chosen architecture was definitely one way to achieve that.

and you don't need to be a domain expert to see that on the surface Cases were a candidate for this.


Unfortunately, when it came to it, the simlarities were less than anticipated, and the differences were critical - mainly around shifting Case ownership and function as a Case made it's way through the Criminal Justice System.

Things were similar, but definitely NOT the same.

---

## Domain Generification 

Note:

[AHL]

Lets look at an example: the key people participating in a Criminal Case.

---?image=img/Case-with-Suspect-and-Defendant.png&size=contain

Note:

A Case is not a Case without someone to prosecute.

We mentioned before, _usually_ someone is a Police "Suspect" at the beginning of a Case, becoming a "Defendant" when the Case is moved to the Public Prosecutor. 

---?image=img/Case-with-all-People.png&size=contain

Note:

But it's not just Suspects and Defendants.  As we know from our favourite shows, there are other key actors in a Case: Police, Victims, Witnesses (Expert and otherwise). 

In a DDD world, _if an abstraction serves a purpose_ you would expect to see all this richness explicitly in the model. 

Here we _had_ a purpose, because other key concepts such as Case Materials (e.g. statements, evidence, etc.) had to be associated with these actors in very meaningful ways.

But when we looked in the code, none of this was there.

---?image=img/Case-with-just-People.png&size=contain

Note:

Domain-richness had been sacrificed as the drive for simplification had taken over.

What we did have was a "catch-all" class called "People".  The specific types of people were now only noticable in the _names_ of associations in the Cases Aggregate.

It got worse. 

---?image=img/Case-with-just-People-Separate-BCs.png&size=contain

Note:

Because this People entity was _so_ commonly used, it had been split out into a separate model in a separate Bounded Context.  

The links between key actors, their Case Materials, and the Case itself was increasingly tenuous.


By implementing a core tenent of good software design - being DRY - the implementations had fallen into a trap.


---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Similarities have been spotted, and abstractions made.
But important differences have been lost.

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Similarities have been spotted, and abstractions made.
But important differences have been lost.

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Capture the richness of the domain in the core entities and don't abstract too early.

@snapend

---

# Data Centric

Note:
[GT] 

Fundamentally, this "Case is a case (is a case)" doctrine and further simplification of other key entities had pushed a data-based view, at the expense of a process or behavioural one.

Everything was centered around data and this had inevitably led to a data centered archtecture.

This was seen in the implementation too and resulted in multiple _core_ teams being organised around a single codebase - the Case. 

---?image=img/Competing-teams.png&size=contain

Note: 

This resulted in many merge conflicts between teams trying to change the same single class for their various features. Since Case is core to everything they implemented, you can imagine the merge conflicts this caused. 

The teams had ended up assigning a baton and whoever held the baton were the ones who were allowed to merge, this disrupted and slowed down the release cycles of various teams. 

On the core entities left outside, teams were left to compromise with a diluted model of Defendant & Case Material and unable to add richness that their own context often demanded.

Yet again, prioritising the data and ignoring the rest had made _our_ domain far less explicit.

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

A data-based view has been achieved at the expense of process / behaviour, materialised as code conflicts between teams. 

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

A data-based view has been achieved at the expense of process / behaviour, materialised as code conflicts between teams. 

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Share data and models _only_ where none of the teams involved have high stakes in them. 

@snapend

---

### Problem Summary

@ul

* "One Model to Rule them All"
* Design-decisions made only part of the domain information 
* Similarities identified based solely on names
* Models were about data, behaviour was left out

@ulend

Note:
 [GT]

PROBLEMS:
- "One Model to Rule them All" thinking @note[n.b. bourne of a valid desire not to duplicate data]
- Consequently design-decisions / trade-offs had been made only with a sub-set of the domain information.
- Similarities have been identified based solely on names, attributes and values. 
- Behaviour and relationships / ownership have lost out in the process. Remember, models aren't just about data. 

Hopefully you can see that some very significant results had arisen from a seemingly very simple statement

This conceptual mis-step had subtly given both teams and domain experts the signal to look for _commonality and overlaps in the data_, and to de-prioritise the _differences in the ownership, processing and behaviour_.  This wasn't confined to Cases either.

---

# OWNERSHIP

Note:
[AHL]
Before we move on we need to shift focus and talk a little about ownership.


When I started on the project I was heralded as the "DDD expert".

I'd go into meetings and people would address me as such. I even got called the "DDD Messiah" once.

That's when I really started to get worried.

---?image=img/whiteboard-drawing.jpg&size=contain

## Alone, "Doing the DDD" 

Note:
[AHL]
It was clear that there was not only a general awareness of my arrival, but also an expectation that I would be able to solve a lot of problems; and that DDD would be my tool for doing so.

However, rather than everyone looking for a more general adoption of DDD as an approach and a set of skills, I was there to take things off people's hands.


Worst of all, I wasn't there to deliver any code - I was an "Architect" in the purest sense.  

I wasn't assigned to a particular team and it seemed as if people expected me to be there to do diagrams and definitely NOT write code.

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Hands on modellers aren't _hands on_.   <br/>
They aren't manipulating their models, using them to try and solve real problems.
@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Hands on modellers aren't _hands on_.   <br/>
They aren't manipulating their models, using them to try and solve real problems.

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Everyone manipulates the code. If certain team members can't, get them pairing.

@snapend

---?image=img/other-side.jpg&size=auto 100%&position=right

@snap[west span-50]
### @color[white](The Other Side)
@snapend

Note:
 [GT]
However, the initial build-up around Andrew's arrival had subsided - problems were not going away fast enough, mainly because his focus was in discovering the (at that point non-existent) models. We were still a long way away from solving real problems.

They only truly started to disappear when we started seeing the models implemented in code. This took team effort and definitely not one person's job.

I (Gayathri) realised that DDD was being 'done' because someone had said so, most likely because of it's connection with CQRS. Having said that, many had also experienced a lot of pain from having done it wrong before.

Resulting in DDD being more of a 'must be done' step rather than something which developed organically.

On top of this, there was a strong desire within the Architects team wanting to 'own' the model and  also be its gatekeepers. This had the danger of not only restricting the domain knowledge within a small group, but obstructed innovation and collaboration amongst devs. 

---?color=#e49436
@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Domain Driven Design is being done "to" - rather than "by" - teams.  
@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Domain Driven Design is being done "to" - rather than "by" - teams.  

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Modelling is done "by" the team who own their models. Grow DDD practices organically.

@snapend

---

# BREATHER: The Legal Domain

---?image=img/Chethams_library_interior.jpg&size=auto 100%&position=right

@snap[west span-50]
## Legal Systems are **Necessarily Complex** 
@snapend

Note:
[AHL]

We need to pause a few seconds and ensure one key point is clear.  

While we disagreed with the way things had worked out, we could very much see the valid motivations behind them.  We could relate, because we'd previously been in similar situations ourselves.

Remember, legal systems are complex. They evolve over _significant_ periods of time and they also explcitly represent history and the future in their models (i.e. the law changes, things can expire, things have deadlines).

To operate, they must bring together a great number of independent and probably hostile parties, all of whom have different obligations and needs to be met.

Most importantly, Legal systems operate on a set of core principles like fairness and swiftness in resolving a case against an individual. Principles which MUST NOT be lost in any digital transformation.

Given all this, it's a wonder things were as on track as they were.

---

## Legal Systems are **Ripe** for DDD 

Note:
[GT]
ALL IN ALL, LEGAL SYSTEMS MAKE FOR AN EXCELLENT SET OF CIRCUMSTANCES TO EMPLOY THE TECHNIQUES OF DOMAIN DRIVEN DESIGN.

And we already had some excellent foundations to build on.

---

# DOING THE DOING

Note: 

We've talked about how things were as we found them.

We'd now like to start talking about how we tackled the near enemies which we talked about, and uncovered even more.

We're going to start with the problem of conceptualising how everything could fit together.

---?image=img/Technical-Illustration.jpg&size=auto 100%&position=right

@snap[west span-50]
### How do the Key Pieces Fit Together? 
@snapend

Note:
[AHL]
Knowing about the various models in a large work-programme is important.

But when you're building software as complex as we were; 
when you're building at this scale 
and with many parallel teams, 
knowing how the models inter-relate, interact, and (possibly) overlap is most important_.

We just discussed the unsuccessful attempt to find fundamental architecture pieces - the case of "a Case is a Case".

How might we find a better solution?


Remember; this was a very process-intensive environment, where Cases pass through multiple organisations and multiple owners.

Discovering the "spine" of our solution turned out to be the breakthrough step in solving this.


And the way to find it? Looking *end-to-end* helped us _a lot_.

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Not having any 10,000-foot view when working at scale. 

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Not having any 10,000-foot view when working at scale. 

<br/></br>
![Combat Strategy](img/ninja-trans.png)
<br/>

Just because one structural "big idea" is wrong, doesn't mean you can get away with nothing. <br/>Relationships _between_ models are _always_ key.

@snapend

---

## PROCESS-NOT-DATA<br/>(THE CORE-DOMAIN)

Note:
[AHL]
Our route to the improved "Big Idea" lay in tackling "A Case is a Case (is a Case)" head on.  

This was a multi-step process.

Gayathri mentioned the Case code and the baton before; it was *massive*.

What you saw in this code was a _lot_ of attributes. What you couldn't see clearly was much business logic and process.

---

### _Why Share a Case Model?_

@ul

* Data consistency
* Reporting
* Planning
* Simplified access control
* _What about business domain needs?_ 

@ulend

Note:
 [AHL]

### Tackling "A Case is a Case is a Case" 

Now, we must stress, there _were_ valid reasons to view all Cases as a single Entity:  

* Data consistency
* Reporting
* Planning
* Simplified access control

But these were either technical or operational. 

What about the business domain needs? (We were doing DDD right?)

I went out and listened to the domain experts;  They would know _the full list of activities and business processes that their concepts of a "Case" would need to support_.

They described differences in ownership, different purposes in the Criminal Justice System, and consequently very different lifecycles.  

From a non-technical perspective, it was clear we did need the concept of multiple types of Case.


---?image=img/Diff-Cases-Owners.png&size=contain

Note:

Let's look at a quick example. 

Remember Suspects and Defendants? 

You can see here how one concept comes from the Police and the other from the Public Prosecutor. 

  
The work being done by these two public bodies is _very_ different - one is investigating, one is prosecuting.  Therefore the Case-functions which we would implement were very different too.

But remember, we currently had a shared Case model which meant the code for working with both Suspects and Defendants lived in the same place - on the Case Aggreagte.  That meant it was _really_ hard to see what was going on, and therefore very hard to work on.


How could we square the circle? How could we meet our business-logic while keeping the right elements of the "shared-everything" concept. How could we balance both and maintain the explicit differences? 

(And make it easy for many teams to build their solutions in parallel)?

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Solving one problem at the expense of another. 

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Solving one problem at the expense of another.  

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Don't ignore the tensions between problems.</br> Use DDD tools to make them, and their solutions, explicit.

@snapend

---

# An Abstract Core

Note:
 [AHL]
While the shared generic Case model / microservice was an insufficient solution, 
it _was_ a strong signal from the past.

As a Case goes through it's lifecycle and through various systems, some key aspects of a Case never change. Did this mean we had an abstract core?

---?image=img/Diff-Cases-Owners.png&size=contain

Note:

We saw before how we had our three types of Case - Pre-Charge, Prosecuted, and Simple Justice.  We've talked about the differences, but what did they all share?  


Listening carefully to the language of the domain experts raised this possibility - sometimes they talked about Cases as an abstract concept.  A concept which wasn't a million miles away from our legacy concept of a shared Case.  


---?image=img/Abstract-core.png&size=contain

Note:

They both had some unique other-system ids, investigating authorities and prosecuting authorities, case materials, and either a suspect or a defendant (which was the same person at differeing points on their legal journey - the subject of the case.)

Something like this.

But how to arrive at this abstraction, and avoid falling into the previous trap?  The way to do this is _always_ via the detail of the domain, and the various context-specific implementations.

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Anaemic (rather than focused) abstraction.

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Anaemic (rather than focused) abstraction.

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Don't jump to abstraction.<br/> Distill it from the detail of specific contexts.

@snapend

---?image=img/mind-the-gap.png&size=contain

Note:

### Mind the Gap

 [GT]

At this point, Andrew he had laid a strong foundation for me with an abstract core and atleast three models for a case.

There was still one BIG PROBLEM; I realised that there was a chasm between the models he had identified and their implementation in code.

First and foremost, very few realised that the models thus found had to be translated into code, and even fewer had any idea how to go about it.

At that point we still had in code the big 'Case' model Andrew mentioned, though the teams had now realised they needed to split it out.

---?image=img/Diff-Cases-Owners.png&size=contain

Note:

What was expected was this....

---?image=img/hacked-case.png&size=contain


Note:

What we got was this instead...
With the three different models Andrew had found, the teams roughly went about hacking the existing case (and the microservice it contained) into 3 pieces. 

This was a huge step for the teams, still not enough modelling was done prior to this, which meant the CORE was still missing pieces. 

We saw earlier how a defendant or a suspect should have been part of the CORE. Similarly, Case Materials which includes the Evidence, the Statements which back the Case, was another core entity of a case which had been split out of the core. 

Of course the physical storing of the Case material belonged outside in a document store, but the fundamental association of specific Case Materials to certain people on the case: Victims, Defendants, Witness, Police Officer, Evidence (different for different Suspects / Defendants) should be part of the core model.

i.e. Case was hacked into 3 bits while People, Material which we saw was core to the case model was still left outside. My job now was to bring them together while splitting the model up.  

This was easier said than done. There already was an implementation and then the subsequent hacking, which meant a big-bang approach was not going to be possible even within a single BC.

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Abstract concepts mean little if they are not implemented by the team.

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Abstract concepts mean little if they are not implemented by the team.

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Incrementally step towards the final model; and while incrementing, constantly validate and challenge your model.

@snapend


---?image=img/crack.jpg&size=auto 100%&position=right

@snap[west span-80]
## Splits @color[orange](---->)Silos 
@snapend

  
Note:
[GT]
Following the splitting of models into individual bounded contexts, I found that one of the core teams were dying to split off and be able to do things on their own. 

This new-found freedom was even more dangerous as there was the risk of the models diverging irrevocably. There was a need to distinguish this from the freedom to work independantly i.e. to make changes, release and operate.


---?image=img/split-and-regroup.png&size=contain

Note:

This was key realisation as even though teams should have the freedom to go off and work within their boundaries on their own model, at the end of that process they will have to be able to come back together which means they can't diverge too much from a consistent thread of a model. 

The team relationship was not "Separate Ways" but "Partnership".

This is when I realised that the teams were not aware of the business process outside of their domain - Team building Pre-Charge were not aware of the next stage and so on. The danger was now Silos forming from these splits.

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Splitting into BCs is good; but premature split can lead to silos which are harder to recover from.

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Splitting into BCs is good; but premature split can lead to silos which are harder to recover from.

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Think team relationships when splitting up bounded contexts so that it doesn't get lost through cracks.

@snapend

---

## Icebergs and Icecubes 

Note:
[GT]

Meanwhile, in the absence of any higher-level view which Andrew talked about before, everything at the code level had combined to create a significant set of problems - complexities had been created where there needn't be (significant amounts of complex shared code, lack of domain understanding - in both breadth and depth - amongs the devs) and over-simplifications where the domain actually needed to be far richer. 

We came to refer to these as the "icebergs" and "icecubes".

---?image=img/iceberg.jpg&size=contain

Note:
[GT]

One example of an Iceberg is the prosecution case bundle. What was perceived as a simple service for PDF generation from multiple documents was actually a key stage in the prosecution process particularly for the state prosecutor. This is when the prosecutor collects the case material and sorts the relevant ones according to the suspect/defendant. The second step is when the these are bundled and shared with everyone on the case. The seemingly innocent actvity of pdf generation turned out to have such richness in the domain that failing to capture would have been disastrous.

---?image=img/icecube.jpeg&size=contain 

Note:

The other side of this exists too. What is considered as a big problem sometimes melts into nothing. Simultaneous updates to a case is a great example. When I started there was serious concern amongst domain experts about how to deal with simultaneous updates to a Case. So I was asked to setup a DDD session to find a solution to this problem.

It actually turned out to be a design smell by not defining the boundaries between different models of the case, remember our single, big case model. When we started implementing the different models that Andrew had identified in their own bounded contexts, this problem just disappeared, we literally had to nothing!

Access control is another example - of course access control is super important but separation of models particularly multiple models of the same entity in their own bounded context and worked on by corresponding actors i.e. prosecutor, court admin provideD out of the box access control at the very basic level.

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Pseudo domain complexity. 

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Pseudo domain complexity. 

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Anything that is not inherently complex in the domain should not be complex in code. 

@snapend

---?image=img/Brandolini-Bounded-Context-Archetype.png&size=contain 

# THE END-TO-END-VIEW

Note:
[AHL]

While we leave Gayathri wrestling with splitting out the various types of Case in the code base, I'd like to introduce the next key realisation and part two of our journey towards a new "big-picture".


Having identified our Abstract Core which gave us licence to have multiple models for a case, the question of how these types were related could no longer be avoided.  Solving this problem was going to give us the clear "spine" for our models.

---?image=img/Spine-Components.png&size=contain

Note:

Not only did each distinct Case model exist within its own Bounded Context, but also that there was a clear flow from one BC to another.

In this manifestation, instances of earlier Case types would almost give rise to into subsequent instances.

It seemed like I'd come across something fundamental.  

I looked to the domain experts and there they were: business-level processes (legal ceremonies even) involved in moving cases from one context to the next.  

These moves involved significant conceptual (and data-level) changes.  They had specific criteria, and ownership was typically transferred from one organisation or body to another.

---

## "Seeing" This in Action

Note:
 [GT]
Andrew's discovery was great, next comes the critical part - communicating this to the people implementing it. All we had now was multiple models of a Case with some relations but no way of visualising the connecting transformations of state between these models. 
 
Enter the Context maps. They are an incredible aid to solve many visualisation problems.

---?image=img/state-transformation.png&size=contain 

Note:
  
As we can see visually, a Case that comes in at a Pre-Charge state will transform into Prosecuted case when one of the "Defendant is 'Charged'". Similarly, a simple justice case enters the next state in the cycle when it is referred to higher court. These state changes had to be called out explicitly and this is where the boundary and the contours of your microservice lies. This carries with it only the necesarry attributes required for the state transfer into the next model.
We used Context maps to demostrate visually that there were relationships - and they were creation-level ones. One model could pass control onto a downstream model, and create that downstream model in the process.
  
This was helpful for two other reasons:
1. It became clear to _everyone_ why different models of a case was absolutely _essential_
2. Teams undestood where they were in the big picture.

---

## MODELS->CODE

---?image=img/emerging.jpeg&size=auto 100%&position=right

@snap[west span-70]
## @color[white](The Emerging Implementation)
@snapend

Note:
[GT] 

We have multiple models of a case, we understood that there was a clear and explicit change of state from one to the other. How did we implement this in code?  

There wasn't one correct way of building this - 

1. We could have had an orchestration service which replicates the physical world of sorting out different types of prosecution notices and forward it to appropriate court or 

2. Have the case land in the correct context depending on the type and then let the natural court process take it course as the case goes for referral to higher jurisdiction 

Regardless of the approach, we still embedded the cross-bounded-context-links which we learnt from the domain. 

It is worth remembering that real world != software application. Software world offers so many opportuniites to optimise that leveraging it might even lead to business transformation.

---?image=img/short-sight.jpg&size=auto 100%&position=right

@snap[west span-50]
## Shortsight @color[orange](Vs) Longsight 
@snapend

Note:
[GT]
While the implementation was emerging, there was a different conflict brewing in the background. How much of this was future proofing and how much was discerning the domain?

Former means, you are anticipating these requirements to come up later and building it in advance; requirements and scope can change as there are several synthetic factors like cost, resource that can influence this. 

While the latter means due to the deeper insights gained from the domain, the model will be more robust and less likely to fall over because the real world seldom changes at the same pace as the requirements on which a software application is built.


Also remember that we had to "take the justice system into the 21st century" as we delivered things.

This meant we had to push back against "quick" wins (from which the resulting tactical solutions had incurred a great deal of debt in the code) and instead efficiently find the "real" wins.


---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>
Minimum Viable Product.
@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Minimum Viable Product.

<br/><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Don't constrain yourself by requirements and scope (MVP) when learning about the domain. <BR/>
Once learnt, implement MVP.

@snapend

---?image=img/vicious-cirlce.jpg&size=auto 100%&position=right

@snap[west span-50]
## As-Is<br/>vs<br/>To-Be<br/>Vicious Circle
@snapend

Note:  
 [GT]

There is almost always some "legacy" systems, even in a green field project. 

It's worth keeping in mind that the legacy systems (as-is) don't exactly reflect the domain knowledge and can take you down a rabbit hole sometimes.  
Especially when you are working with the aim to "modernise" a system, you seldom are looking at reprodcuing the same old boring legacy systems. 

We know domain changes more slowly than the system that we are building. You will find that it is more dependable than look at existing systems. Word of warning, most times you might have to filter out the domain expertise which may have come from working on these legacy systems. 


---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Legacy (ways of thinking).

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

Legacy (ways of thinking).

</br><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

Obtain knowledge from the current state of the domain.<br/>Model the To-Be state. 

@snapend

---?image=img/complexity.jpg&size=contain

@snap[west span-80]
## @color[white](Complicated Bits)
@snapend

Note:
[AHL]
We mentioned at at the very top that we had a CQRS-based architecture.

It is more than likely the source of the decision to do DDD across the board.  Not a bad decision at all.

Given the fact we've just given you so much context about where it was being applied, we though it was also worth sharing some pros and cons about this too - as it was also being used at scale.

---

## CQRS - What Suited Us

@ul

* Human-centric way to view Law
* Time and eventual consistency as first-class citizens
* Event-based thinking at its core
* Time + Events = History

@ulend

Note:
 [AHL]
First up lets quickly list why CQRS was a great fit for this project.

Firstly it is a very human-centric way to think of things which is very like law.

Secondly, CQRS has a lot going for it as a design approach.  Not least because it is has both time as a primary citizen and the concept of eventual consistency baked into it.

Thrdly, it also plays _very nicely_ when you tackle things from an event-based perspective.  In fact you NEED to consider things from this perspective in order to get things to work.

Combine events with time and you get history.  Yet again this was a first-class concept that we wanted (needed even?) in our software as it would allow us to do some amazing things and with relatively little technical complexity.

---

## CQRS - Where There Was Friction

@ul

* Aggregates - Similar but not same

* Lack of explicit model

* Read Vs Write model

* Synchronous way of thinking

* Visualisation

@ulend

Note:
@gayathri to slim this down - very wordy

1. CQRS uses the term Aggregate. IMO, CQRS aggregates are similar but not the same as a DDD aggregate. Often, I have found that one muddles the implementation of the other. CQRS of course made the DDD aggregates famous.

1.1  In pure DDD, there can be group of entities as aggregates, but in CQRS most of the times, you will have only one entity as an aggregate root and the rest are value objects. It is mainly because as an entity with it's own lifecycle it would make sense to have to capture events in it's own stream hence a different aggregate. A "root" doesn't make much difference in CQRS aggregate

1.2 Again in DDD,he root is the only way to access the children in an aggregate and that's mostly how you will identify the root. This mostly lead in our project to "Case" being the root all the times! Everything needs to have a case to start with ofcourse. But in CQRS, it meant the other entities can be an aggregate in themselves. E.g. Case, Casematerial, Defendant as you want to capture events in their own streams. Also, the event streams of those entities should be accessible independantly as once after creation we don't need Case to access Defedant for e.g. to amend their accessibility requirements 

2. DDD is all about explicit modelling - In CQRS aggregates, apart from the root entity, the model is not visible. It is in pieces within the events. Although strictly events themselves are not domain models, they are BASED on your domain model (they are too denormalised to be a model - they just capture facts)

3. Read model or write model -> Which of these is your domain model? If you overlay the domain model diagram it would seem like a read model which is a normalised view of domain data is you domain model BUT it is not. It is simple a projection. The richenss of your model is in write side

4. Our mind is trained to look at things in a synchronous(?) way, cause-effect, request-response. With async events flowing all over the place, it is very difficult for the best of devs to wrap their mind around this event driven concept 

6. Visualisation - very difficult at best of times.  It is difficult to capture a synchronised view of the architecture. The closest I got to was to use Sequence diagram to show a handovers and flow of events (instead of method calls)

---?color=#e49436

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

CQRS (everywhere)

@snapend

---?color=#90ee90
@transition[fade]

@snap[north span-100]
![Near Enemy](img/ogre.png)
<br/>

CQRS (everywhere)

</br><br/>
![Combat Strategy](img/ninja-trans.png)
<br/>

CQRS is powerful when used in the right place. <br/>
Use it only if _dictated_ by your domain, and even then only sparingly.

@snapend

---?color=#90ee90

@snap[north span-100]
# Conclusions
![Logo](img/nearenemy-logo.png)
@snapend

---?color=#90ee90

# Conclusions

@ul

* Slow down and listen - especially for differences
* Work with the code - a lot
* Work as a team - DDD is for _everyone_
* Don't dilute - distill
* Investigate puzzles - they have solutions hidden inside
* The domain knows how to split things up already
* Distinguish as-is from to-be

@ulend


Note:

Slow down and listen - especially for differences

Work with the code - a lot

Work as a team - DDD is for _everyone_

Don't dilute - distill

Investigate puzzles - they have solutions hidden inside

The domain knows how to split things up already

Distinguish as-is from to-be


---

# Thankyou
## (What Questions Do You Have?)

---
