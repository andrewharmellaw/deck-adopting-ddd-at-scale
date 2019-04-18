# Intro

---

## The Near Enemies of Domain Driven Design (and how to recognise and defeat them)

  "The near enemy is a [...] counterfeit of what we’re actually aiming for, and it’s unhelpful because while the genuine article helps free us[...], the counterfeit doesn’t." from https://www.wildmind.org/tag/near-enemy

Note:
Quote: "The traditional term “near enemy” points to some spiritually unhelpful quality or experience that can be mistaken for a helpful quality or experience. The near enemy is a kind of counterfeit of what we’re actually aiming for, and it’s unhelpful because while the genuine article helps free us from suffering, the counterfeit doesn’t." from https://www.wildmind.org/tag/near-enemy

We say "people still don't get DDD". What do we mean?  With the rise of microservices it's being used everywhere right?  Well, not really...

The concept of near enemies should be very familiar to anyone who has worked in software for even a short while - we have _many_ near enemies: in the adoption of so-called "Agile" methodologies, and more recently in the drive towards "DevOps culture".  

The application of DDD is another one of them.

Why do they arise? They arise because people do not engage fully with a concept, and typically this is because they ignore the core, fundamental aspects; which are also typically the most simple.  They forget the simple four lines of the Agile manifesto, or ignore the DevOps goals of breaking down boundaries and building a culture of learning.  Instead get tied up in the complicated details which seem more "valuable" and where the "expertise" lies.

We want to use this lens to present a collection of challenges and failure patterns we saw when using DDD on a large scale.  It's ideal for these purposes (we could argue essential if you want in any way to succeed) but when things get complicated people can easily forget about the core concepts, and that causes problems.  

Hopefully this story will help you avoid falling into that trap.

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

We had to "modernise justice" as we did it, within a publicly funded program of work. Constantly having to battle with business against "quick" wins (from which the resulting tactical solutions had incurred a great deal of debt in the code) and instead efficiently find the "real" wins.

The scale - it was a massive piece of work that was being tackled head on. Software was being built by multiple (how many?) teams in parallel, staffed from multiple partners. (Different roles thought in different ways - e.g. Devs, BAs, Data Architects, Software Architects, etc. 

Complex Architectural choices had been made (e.g. CQRS for everything) and devs were  drowning in them. It was almost always an impediment rather than a boost - (We'll come back to this in the final section. For now, suffice it to say that it made the adoption of the DDD even harder)

Domain experts were stuck in the legacy way of thinking or worse paper based. In courts, traditionally, the prosecutors, defence and courts will fill in the same form alternately and the expectation was to translate that literally onto the software application. 

---

### Incredibly High Stakes

With all this in mind it is no surprise that things had got complicated prior to our arrival.  The stakes were INCREDIBLY HIGH, both RISKS and BENEFITS.

---

# Where things were when Andrew started

---
	
## BIG PICTURE: GROKK-ABILITY, END-TO-END-VIEW - ("Where is the big picture?") INTRO TO THIS PART

---

### Where was the Big Picture? [AHL]

Note:
I take a very "I'm the noob and I'm keeping the beginners mind as long as I can to get as deep an understanding as possible" approach.

I began by setting off a number of lines of enquiry - I had a vague idea of the domain, having spent a long time delivering software in the Scottish Legal system.  That's very different, but it allowed me to compare things and ask "North of the border they have to do this?  Is there an equivalent?" or question "In Scotland this is owned by a person who works for department X, is something similar needed here, and of so, who does it?"

I pulled in as many info sources as I could, official and unofficial, trying to avoid value judgements, and always looking for the edges. I wanted to know the full extent of where we found ourselves.

I knew things here had been running for a while already, and that there was a bunch of designs already in existence on the programme wiki, and a significant amount of code already written.  There was talk of an architect who had done a bunch of the early work, but they had since moved on.  

I had to look at what was there, and how it had manifest already in the team structures and codebases.  

I had to reverse engineer a big picture from the pieces I could find.  
 
I tried to make sure I didn't get sucked into too much detail in any one area.  At this stage I needed to avoid getting overwhelmed by any one thing.

PROBLEMS: 
- THERE WAS NO WAY IN. 
- THERE WAS NO BIG PICTURE WITHIN WHICH TO LOCATE YOUR MORE DETAILED WORLD.  
- THE COGNITIVE LOAD WAS TOO HIGH.  
- NO SINGLE DOMAIN EXPERT HAD AN END-TO-END VIEW.

---
	
## CORE MODEL: DATA-NOT-PROCESS, MODELS - ("one model to rule them all", "data focussed")

### "One Model to Rule Them All" [AHL]

Note:
I quickly came across a few core tenents which had embedded themselves in the psyche of everyone on the project. The most prevalent was the dictum that "a case is a case (is a case)", by which was meant that there should be a single representation of a case making its way through the criminal justice system, most likely mastered by a single "Case" microservice / datastore. 

From a DDD perspective, this meant an over-focus on the data (@gaythu-rajan to elaborate with the defendant model and people context; mention how @andrew comes up with the idea and how it was implemented), and an under-emphasis on the behaviour / workflow / jobs to be done.  

It didn't even really manifest in domain events  

This wasn't evident in itself specifically - there was simply a lot of the former, and a significant absense of the latter. 

(The domain events, such as they were weren't even very fleshed out, having mainly fallen back into the realm of CRUD operations.)

What did this mean? Most fundamentally, there was only one model of a case which tried to be all cases (that there is only one of anything is a risky view in DDD).

PROBLEM: 
- "ONE MODEL TO RULE THEM ALL" THINKING HAD BUBBLED UP,
- BOURNE OF A DESIRE NOT TO DUPLICATE DATA.
- CONSEQUENTLY DESIGN DECISIONS / TRADE-OFFS HAD BEEN MADE WITH ONLY A SUB-SET OF THE INFO.

---

### Data Focused [GT] <<<<<< TO COME from @gaythu-rajan

---

## (Pull "lifecycle", "object-based-split" from Constraints slide under here) [GT] <<<<<< TO COME from @gaythu-rajan

---
	
## OWNERSHIP - (Alone doing...), ("Ownership")

---

### Alone, "Doing the DDD" [AHL]

Note:
When I landed I was heralded as the "DDD expert".  

I'd go into meetings and people would address me as such. I even got called the "DDD Messiah" once.  That's when I got worried.

It was clear that there was not only a general awareness of my arrival, but also an expectation that I would be able to solve a lot of problems; and that DDD would be my tool for doing so.  

However, rather than everyone looking for a more general adoption of DDD as an approach / set of skills, I was there to take things off people's hands.

PROBLEMS: 
- I WAS THERE TO SOLVE ALL THE PROBLEMS,
- AND I OWNED THE DESIGN. 
- DOMAIN EXPERTS AND DEVELOPERS WERE EXCLUDED. 
- I WAS GOING TO TELL EVERYONE WHAT TO DO.

---

### Ownership [GT] <<<<<< TO COME from @gaythu-rajan

---

## GROKK-ABILITY (Perception @Scale) 

---

### Perception @ Scale [GT] <<<<<< TO COME from @gaythu-rajan

---

## BCs (Naming Teams)

---

# BREATHER: The Legal Domain

---

## Legal Systems are **Complex** [BOTH]

Note:
We need to pause a second and make some things clear.  

Legal systems are complex.  They have evolved over _significant_ periods of time, and contain TIME itself as a significant factor (i.e. the law changes, things can expire, things have deadlines).  

They bring together a great number of (by the very nature of the adveserial system, hostile) parties, all who have their views on the system, and obligations / needs to be met.  

Most importantly, they must contain within themselves a great deal of flexibility, while still balancing against this an incredible formality; seemingly small details can make large differences, and have VERY SERIOUS, real-world outcomes.  

---

## Legal Systems are **Ripe** for DDD [BOTH]

ALL IN ALL, IT IS AN EXCELLENT SET OF CIRCUMSTANCES TO EMPLOY THE TECHNIQUES OF DOMAIN DRIVEN DESIGN.

---

# DOING

---

## GROKK-ABILITY / END-TO-END-VIEW - if we can't grokk it, how can anyone else?

---

### WHAT WENT IN THIS SECTION?

---

## DATA-NOT-PROCESS, CORE-DOMAIN - (Case is a case is a case, Shared Kernels and the Abstract Core, Mind the Gap)

---

### "A Case is a Case is a Case" [AHL]

Note:
The route into everything was to try and tackle the "case is a case (is a case)" issue.  I could see where it had come from; the idea was to modernise the criminal justice system, and to remove some of the unnecessary complexity.  

!DATA!DATA!DATA! ADD SOMETHING ABOUT DATA (AND TRYING NOT TO HAVE TOO MUCH OF IT) HERE. @gaythu-rajan to pull tihs into the data section

One way to do this was clearly to find things which where similar and to treat them in the same way.  There was a lot to suggest that fundamentally, cases were a candidate for this.  The problem was, the simlarities were less than anticipated, and the differences were critical - mainly in the regards to who owned the cases and how they were handled.

The problem became painfully evident when looking at the existing Case Aggregate Root - it was *massive* and had tons of attributes.  It also had a significant amount of contributors - it was a *very* hot piece of code. Everyone wanted to add their stuff to it.  

I began by apportioning each of the attributes and functions to the team which had added them. Perhaps they'd just failed to communicate about what they needed and ended up duplicating things?  It's a common problem.

In parallel I went out to sit with the teams themselves, predominantly their domain experts;  They would be the ones who knew what was needed, and more importantly, the activities and business processes that the concept of a "Case" would need to support in their area.  

This is where the tensions arose. It was abundantly clear very early on, that there were many types of case, which served different purposes in the criminal justice system.  Not only that, they were owned by different stakeholders, meeting differing purposes, and undergoing very different lifecycles.  At this level of detail, there were quite clearly many types of case, which were related (more on that later) but were also very different.

How to square the circle? How could I reconcile the pull in these two opposed directions?  

I went back to the DDD book.  Yet another time, there was something there to help me out: Shared Kernels and the Core Domain.

---

### Shared Kernels and the Abstract Core [AHL]

Note:
While I disagreed that "a case was always a case" because this lost too much detail in abstraction, it was also the signal that there was highly likely to be a common core - in DDD parlance a shared kernel.  

[BRING IN THE DDD DIAGRAM AND DEFINITIONS HERE]

The flow of cases through the criminal justice system _is_ a collaborative one. There is a fixed number of ways for cases to come into being, and there is a very strict set of protocols governing how these change from one type to another.  

There is space at this point to bring in one more concept. Beneath everything, there was something which, on it's own was never enough to be a case in its own right, but that could be considered an "Abstract Case" from which all concrete types of case could inherit.

(Example: Go into this with an example of A PCD Case and a MagistratesCourtCase - showing the example of Suspects and Defendants.)

---

### Mind the Gap [GT] <<<<<< TO COME from @gaythu-rajan

---

## END-TO-END-VIEW - "()->|()->()", "Visualisation", 


### ()->|()->() [AHL]

Note:
This brings us onto a concept which *isn't* explicitly brought out in the (Blue) DDD book and which I arrived at on my own prior to discovering it detailed in Alberto Brandolini's Context Map Archetypes.  

Having pulled out the shared kernel of cases, and having identified how this was manifest in various contexts to solve various problems and support various activities the question of how these were related came up.  It was clear that not only did each one exist in its own bounded context, but also that there was a flow from one manifestation to another:

()->|()->()

What now seems obvious, but which made me nervous at the time, was the relationship between these contexts.  There was almost a flow of execution and data and ownership (over a significant period of time, but a flow nontheless).  I knew relationships between bounded contexts was significant - I was a big fan of the strategic design patterns and the clarity they gave, but this seemed to be a different form.  It seemed like I'd come across something fundamental.

@gaythu-rajan to provide the sketch of this

---

### Visualisation [GT] <<<<<< TO COME from @gaythu-rajan

---

## BCs - ("Icebergs and Icecubes", "splits vs silos")

---

### Icebergs and Icecubes [GT] <<<<<< TO COME from @gaythu-rajan

---

### Splits vs Silos [GT] <<<<<< TO COME from @gaythu-rajan

---
	
## MODELS->CODE - ("Looking through the crystal ball", "shortsight vs longsight", "[Generic Sub Domain]")

---

### Looking through the crystal ball [GT] <<<<<< TO COME from @gaythu-rajan

---

### Shortsight vs longsight [GT] <<<<<< TO COME from @gaythu-rajan

---

### When is Sometihng NOT a Generic (Technical) Subdomain? [AHL]

I THINK WE CAN DROP THIS TO SAVE TIME. WE MIGHT WANT TO PULL SOME SPECIFIC BITS OUT OF IT HOWEVER.  

(Such as the bits for "Domain Experts - Good" below)

---

## DOMAIN EXPERTS (good - ("[Andrew]") and bad -  "Distill... the noise", "driver for change")

---

### Domain Experts - Good [AHL]. (from "When is Sometihng NOT a Generic (Technical) Subdomain?") 

Scheduling in Courts seemed initially to be the opportunity for an off-the-shelf product, perhaps with a little wrapping up to expose it in a meaningful way to consuming parties (other BCs).  I'm going to talk a little now about how listening to domain experts led me away from this conclusion.

The seam I mined was based around the edge cases - when the scheduling was a complex matter, when it changed, when it was significantly sized.  It turned out that these circumstances weren't universal in this Criminal Justice System. Luckily we had domain experts who had a wide range of experience.  By asking about the biggest jurisdictions, and the circumstances when things were the hardest / most comoplicated, we eventually settled on a model which could represent the real richness of this complex task.  

Along the way we'd discovered that there were individuals who had this scheduling task as their sole responsibility, and that there was frequently a great deal of intuition, insight, and discretion that they applied.  This was beyond mere slot-filling.  These people were applying a great deal of local knowledge, and awareness of many upstream feeding-factors about which they could only have learned through experience.

---

### Distill... the noise [GT] <<<<<< TO COME from @gaythu-rajan

---

### Driver for change [GT] <<<<<< TO COME from @gaythu-rajan

---

# TRANSFORMATION

---

## Iterate

---

### Method: Model -> Share -> Question -> Repeat [AHL]

DID WE WANT THIS ONE HERE? (I'M HAPPY TO DROP IT)

YOU HAD SOMETHING ABOUT THE MODELLING WHIRLPOOL.

Note:
Draw lots of pictures - try and find what is "comfortable". Being able to draw something on a sheet of A3, or a standard whiteboard is a good sign that the level of detail is correct.

Go back to the book. The "pattern style" that it is written in means it is very easy to find your problem already described.  Then simply follow the solution.  

Find the *armature* - it sometimes seems to me that this part of the process is a lot like discovering the model's armature.

Share these pictures constantly.  Adopt a beginners mind.  Articulate when something doesnt feel comfortable (though be willing to accept a minor amount of discomfort, not everything will fit elegantly into the model you need.)  Get the help of others - specifically the domain experts.  Gather round the board and ask questions of your models and see when they break.

At a meta level, it was exciting to come at DDD from another angle. It meant I had to re-read Eric's book, and find value in other parts which I'd previously skimmed. I was amazed (yet again) at how relevant and applicable and valuable these concepts were.

---

## IDEAS LEGACY - (DOMAIN VISION STATEMENT++, multiple models of the same thing, actors coming together, process-centric, etc.) 

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

---

### _Loads_ of Lovely Domain Experts - Listen [AHL]

Note:
This unified "Case" construct came into direct conflict with the fact that there were many teams, working with their own individual domain experts, on different services, with different release plans; all of whom had to play in this shared "Case" space.

The existence of the domain experts, embedded 3 out of 5 days with each team was a boon. (I've seen _many_ DDD projects fail due to a lack of this.)  This involvement must have been incredibly difficult to plan, set up and finance, and as such it needs to be explicitly called out as a win.

GOOD THING: HAVING DOMAIN EXPERTS AROUND ALL THE TIME IS A MUST.  

There was a problem however. In many teams, the domain experts weren't being used to their full potential.  I kept coming across the worrying signs that the technical people didnt agree with their embedded Crown Prosecution rep. And not just on which version of a java library to use. No, I heard people saying that they were wrong when they described how their job worked.

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

## Per-Team Context Maps ("Process - Before and After")

---

### Process - before and after [GT] <<<<<< TO COME from @gaythu-rajan

---

## Tools and Methods

---

### Tools and Methods [GT] <<<<<< TO COME from @gaythu-rajan

---

# Complicated Bits [GT] <<<<<< TO COME from @gaythu-rajan

---
	
## CQRS good - history and replayable (core domains)

---

## CQRS bad - end-to-end!!! devs don't think like this

---

# Conclusions

---
	
## Modelling is not cheap [GT] <<<<<< TO COME from @gaythu-rajan

---

## As-is / to-be vicious circle [GT] <<<<<< TO COME from @gaythu-rajan

---

## You _can_ copy data - look to the Process

Matthias Verraes: “Don’t Repeat Yourself” was never about code. It’s about knowledge. It’s about cohesion. If two pieces of code represent the exact same knowledge, they will always change together. Having to change them both is risky: you might forget one of them. On the other hand, if two identical pieces of code represent different knowledge, they will change independently. De-duplicating them introduces risk, because changing the knowledge for one object, might accidentally change it for the other object.

