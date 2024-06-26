---
title: "PGConf.dev 2024 Live-Blog"
datePublished: Thu May 30 2024 17:43:29 GMT+0000 (Coordinated Universal Time)
cuid: clwtjni1m000f09l7c86i02gh
slug: pgconfdev-2024-live-blog
tags: postgresql, databases, developer

---

Live blogging a few sessions at the [PostgreSQL Development Conference](https://2024.pgconf.dev/) in Vancouver, BC

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717092967812/afd02fa9-0b27-4e8d-bc95-f880b7b27348.jpeg align="center")

.

# Lessons from the Support Desk

*Speaker:*[*Evan D Macbeth*](https://www.linkedin.com/in/evanmacbeth/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717093018794/4d6411e0-59d7-41cf-9d56-46221f21803a.jpeg align="center")

## Surface Area vs. Volume

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717093029034/cebc7796-39cf-4425-9dba-87e684c72a2c.jpeg align="center")

**AREA is the MOST important thing for developers to understand.**

Every new release, code patch, feature... expands that area of your application (in this case, PostgreSQL), and every developer is now responsible for an *ever-expanding area of that surface*.

And your Support organization? They're responsible for the VOLUME. Biggest takeaway:

***Even making code better increases the work that your support team has to do.***

## What happens when you ship a fix?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717093152630/bcc90ba7-b9b9-4a09-88d0-9b4a1920fd52.jpeg align="center")

"We only want to make things better, not worse" — Thomas Munro

That sounds great! ... in theory.  
What happens when you make things better?

1. You bump the version number
    
2. Now there's a new release in the wild!
    
3. **You just doubled your Support team's work! :O** (They need to support both the users who upgraded, AND the ones who didn't!)
    

**Even reducing code complexity increases support work.**

So please keep your users, support engineers, and technical account managers in mind when you're doing coding.

**There's nothing you can do to make their jobs LESS work.** (Can make it easier, but not less work.)

## **Detail your assumptions.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717093497570/c6911feb-6eb0-4168-bf77-b8233a3db21b.jpeg align="center")

When creating a feature or fix, **your utopian case matters!**

All problems can be diagnosed as a **variance from an assumed state.**

* "Why did you do it that way?"
    
* "Why did you assume I *wouldn't* do it that way?"
    

Detailing assumptions makes it WAY eaier for support team to know what's going on:

* What's it supposed to do?
    
* What did you test it on?
    
* Use cases (EXAMPLES!)
    

ALL examples are good examples, with a bit of context.

Why? **Users follow examples before reading documentation.**

## Users don't read your docs, *but* your SUPPORT team does!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717093528918/c43a3959-553f-4b22-972e-937c2038ac7a.jpeg align="center")

Most Support contracts are paying the Support team to read the docs for them. 🤣

So have your Support team read your docs *before* release!

(The PostgreSQL docs are excellent!)

Cautionary tale with ChatDox: It's OK to help users find where to look, but should not rely on an answer from AI. (Hallucinations are a thing.)

## No one upgrades :(

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717093606787/4c2ad8e9-571a-4400-9fb9-91f945932755.jpeg align="center")

March 2024 - One particular customer, a bit of less than half of their servers were still running PostgreSQL 11 (EOL Nov 2023) or below. *6 were running 9.6* (EOL Nov 2021) or below. :O

**It's great that new versions of PostgreSQL have new features! But, most users aren't going to see those benefits.**

An example from a well-known company from ONE WEEK AGO:

[https://www.yugabyte.com/blog/yugabytedb-moves-beyond-postgresql-11/](https://www.yugabyte.com/blog/yugabytedb-moves-beyond-postgresql-11/)

Another example: trouble ticket from January 2024:

***The password you entered is too long. \*\*\*Windows NT\*\*\* will not accept a user password that is longer than 14 characters.***

\[\[ scream face \]\]

Reality: Most of the support things they're dealing with isn't because of new features.

That's not what's keeping your support team / customers awake at night. This old stuff is!

**Versions matter.**

Give me the specific version numbers. Give me an SBOM with the dependencies.

**Backward copatibility is critical (and testing that it works!)**

Give me a matrix.

This release has been tested / validated on these versions.

Especially in "ship constantly" era.

Test on the older stuff!

Give us roadmaps!

Ansible announcements: 5 pages of changes coming to the project, but tells me nothing. :(

PostgreSQL, on the other hand, PostgreSQL 17 beta release notes, available for review!

Give me clear roadmaps.  
Let us know where things are going.

Then w can tell customers when interacting with them what to exoect when. they upgrade.

Because eventually...

## Everyone\* Upgrades

(Just not on the timeframe you expect!)

PostgreSQL release cycle is 3 months.

If an organization releases every 6 months, they can't take every minor release, so we can't expect them to.

So. DOCUMENT and talk about what changed and why.

Especially comapatibility deprtecations / assumptions.

If dropping support for something, BOLD and at the TOP of the release notes.

Don't assume! That just because RedHat 6 is EOL you no longer support it. Call it out explicitly.

10 release window? It's great!

But it's going to create an EXTRAORDINARILY large amount of work for Support team. Backward Compatibility is no longer guaranted.

It creates incentives to upgrade... but also creating a lot of anxiety for them.

But!  
COmmunity at PostgreSQL let me know this was coming.

That's great! Let us know.

**Release notes are your Support team's best friend. &lt;3**

Please put ALL the details in there! We read them cover-to-cover.

Take the lesson from PostgreSQL for your own projects. Make your release notes as detailed and high-quality as theirs, and your support team will be very happy. ;)

## Everyone Hates Downtime

How many people have been in a meeting with a customer who wants zero downtime? (Lots of people)

How many people believe there is "zero downtime" (no hands :D)

There are only two types of downtime: planned and unplanned. ;)

Users are not patient. They never upgrade, but they're not patient.

**Set and manage expectations for changes.**

I bet in the PostgreSQL 17 talk they didn't say how long an upgrade from PostgreSQL 16 -&gt; 17 is going to take. ;)

"We can't do that! There are so many variables!"

True! So document your assumptions. I have 100GB database, moving from 16 -&gt; 17, and it took XXX minutes.

Backwards compatibiity SUPER critica

**But PLEASE test.**

And not just the immediate previous version to the new version.

Most customers are running something 6-7 vrsions back.

The more you test, the better off your support team and customers are going to be. :)

This is a lot of work, and a trade-off.

At minimum, test from every major supported version to the latest.

Multiple success paths: give us many ways of successfully completing an upgrade.

Example:

* pg\_upgrade, PostgreSQL dump/restore
    
* "rolling" upgrades, buld in flexibiltiy as to what rolls when
    

## Recovery

Backups, restores very important. Why talking to developers about this? **I want you to try it.**

You built a new fix, a new feature, it works! Super great, yay!

Now, back up the system and try a recovery with your new code in it. ;)

Maybe recovery takes a lot longer now? Something to think about...

If yuor support team is not doing restores from backup all the time, that's a problem. Should be part of standard toolset, muscle memory.

Support team, Customer, even developers!

Why can upgrades take so long? For example, Federal customers. They can't "certify" PostgreSQL because it's open source software so needs to be thoroughly tested and certified themselves.

Can automation help?

## PostgreSQL Users

The most important audience not in the room. :)

**"There are only two industries that call their customers "users" — illegal drugs and software."** — Edward Tufte

Language matters. There's an underlying assumption of "taking" versus being involved in the process.

Open source users a bit different.

Goldfish? They have no memory.

One of the things that's very frustrating for Support but very true...

* They're not going to learn
    
* They're not going to remember things
    

Not because they're bad people.

There's turnover. Lost institutional memory.

So important to remember: they won't necessarily know what they knew before.

But there is a degree to which they are all the same and interchangeable... when they forget things, they revert to a state of commonality.

**Remember: YOU are a User, too!**

Every single person in the room uses PostgreSQL, so you have a perspectve on this. Imagine how frustrated you get when a tool isn't doing te thing the way you want it to dot it! Congrats, you now have user exprience. :) Hold onto that. Because...

## Your Users Are Not Like You.

"The median voter is a 50-something white person who didn't go to college" — the people making the decisions aren't like him.

In a similar fashion, we do not know who our POstgreSQL users are!

This is a big deal. A blind spot.

Timescale has tried to address this, they have a survey it's great.

That survey had 888 respondents.

That is not a statistically significant sample.

Estimated Oracle users is 70 million.

WE DON'T KNOW WHO OUR USERS ARE

So we can't assume they're like us!

But they **need** what you're building!

And your support team **needs** your participation/attention!

That helps them understand: Where were you coming from and why?

Suggestion; Give it a try for a week!

Promise: Support team will say yes! ;D

Take a week, field tickets, answer calls... get a feel for experience youi're putting your support team and users through. You'll be a better coder for it!

## YOU can build a team like YOUR users

You have some influence on the team you're on.

Even as an IC, make suggestions about your team

Help build/influence a team that looks like your user community.

Makes your team stronger!

Add people who are ike.

37% pf IS population not-white

35% of all STEM employees women in 2021.

27% of STEM graduates were women

is your team a quarter women? Is it a quarter non-white?

If not, is your team reflecting your user community? No?  
**WHY NOT?**

**Variety of perspectives leads to better solutions.**

Study from Kellogg School of Management. Task, find the murderer. The more diverse the team, the better off their chances.  
BUT.

Also less confident that they had the right answer.

Less diverse teams HYPER-condident! Even if they're wrong. ;) (AI Hallucinations, anyone? ;))

So, PLEASE think of your users when you write code. :)

## Coda: AI

AI as a user (users submitting erquests bassed on advice / answers given by AI)

AI as a developer

AI — "Best" practice

* It can make doc writing better! (Clearer, more understandable)
    
* Declarative / short statements are very yseful, and hard to do
    
* Also test assumptions. Ask ChatGPT question you expect it to work the way you think. The answer back may surprise you! And that's what your customers will get. ;)
    

---

# Making PostgreSQL Hacking More Inclusive

Speakers:

[**Amit Langote**  
**Masahiko Sa**](https://www.pgevents.ca/events/pgconfdev2024/schedule/speaker/48-amit-langote/)[**wada**  
**Melanie Plage**](https://www.pgevents.ca/events/pgconfdev2024/schedule/speaker/20-masahiko-sawada/)[**man**  
**Robert H**](https://www.pgevents.ca/events/pgconfdev2024/schedule/speaker/8-melanie-plageman/)[**aas**](https://www.pgevents.ca/events/pgconfdev2024/schedule/speaker/27-robert-haas/)

## The PostgreSQL community is amazing! :D But...

* So,etimes, judge people on things other than quality of their work
    
* Sometimes, we extend opportunites to people who are more like us
    
* Sometimes, we behave in ways that are mre problematic for some groups of people than others.
    

**Unfairness is a problem.**

* Looks bad for the project
    
* Drive away potential new contributors (and we *need* them!)
    
* Drive away / demoralize *existing* contributors, contributes to burnout.
    
* Make hacking on PostgreSQL less enjoyable
    

## Possible reasons for Inequality of Opportunity

* Demographics (race, skin colour, national origin...)
    
* Neurodiversity
    
* Fluency in Engish
    
* ...
    

## Amit Langote's Story

Going to share some of the experiences that had a lot of impact on me personally psychologically, kept me engaged for 11 years.

Hoping someone with similar background / similar personality might find this relevant or helpful.

I'm not planning to talk for *everyone* who's like me, sharing *my* experience, to bring some benefit to discussion.

### Maintaining Two "Personas" as a PostgreSQL Contributor

* Many of us communicate differently in our personal lives (indirect, nuanced communication) vs. how we need to be successful in PostgreSQL discussions (direct, assertive style).
    
    * Maintaining two personas can be draining at times.
        
* Inability to be direct and assertive may result in being overlooked or dismissed. People have let me know that this is limiting; I could be more successful if i made certain points in a more direct/assertive manner. Many others can face this same issue. They "have" to be more direct, but they can't... because of their personality or where they are in their journey.
    
* Recommendation: Be more understanding / aware there are people with differnt experiences here.
    

### Challenges of Non-Native English Speakers

* Email comunication strucggles
    
    * Difficulty expressing complex thoguhts in email as non-native English speaker
        
    * Many folks speak very differently in-person vs. in written communication.
        
    * Time-consuming drafting process to sound coherent (especially for "high stakes" conversations), potentially leading to perceived disengagement.
        
    * Non-native speakers leading discussions may face reduced engagement / disappearing from community. — it's not that, it's that it takes time to put a response together.
        
* What can be done?
    
    * **Have Patience**: Allow non-native speakers time to express themselves.
        
    * **Use Clear Language**: Avoid jargon and idiomatic expressions (and e.g. sarcasm) for clarity.
        
    * **Ask for Clarifications**: Request explanations or provide summaries when needed. (Instead of dismissal.)
        

### On Giving a Chance

When you first start out, you are nervous, don't know if you'll be taken seriously.

**Entrusting newcomers with important tasks**

* Example: In 2024 Robert, Alvaro, others encouraged me, a relative newcomer, to work on a cricual project (table partitioning) in the commmuity.
    
    * This was crucial in my sustained involvement.
        
    * Give other newcomers this chance, and we have more folks becoming specialists!
        
* Their support, along with backing from in-house managers and colleagues, fueld my enthusiasm for contributing to Postgres hacking.
    

**Diversifying Community Energy**

* Encouraging newcomers
    
* ...
    

Flipside

* ON the Flipside, when newcomers aim for leadersip roles, experienced members may hesitate, fearing it could ompede project success, which may hinder recruitment of other experienced contributors.
    
* Confidende in newcomers' abilities has to be. balanced swith support and mentorship from experienced members.
    

"Trust, but verify" :)

### Off-List Dynamics

* Off-list collaboration can be very effective:
    
    * Strategic planning and sensitive disucssions may require confidentiality.
        
    * Building personal relationships and trust through one-on-one interactions.
        
    * Addressing urgent matters promptly without the delay od group discussions.
        
* However, it may lead to some folks feeling excluded:
    
* * Business-level discussions may delay patch acceptance, affecting contributor morale
        
        * Be transparency about that to the textnent possible
            
        * Help people understand how decisions were mde. Otherwise, can lead to people feeling demoralized.
            
    * Engineers investing in patches feel undervalued when decisions rely on off-list interactions that don't involve them.
        
        * Cite off-list discussion whenever possible. for transprency.
            

## Masahiko Sawada

Sharing both my experience and experience of other Japenese hackers' experiences that Iv'e heard of.

* For some, no clear solutions exist.
    

Not intended as complaints / accusations

### Difficulties with English

* English is a prerequisite
    
* Most Japneses ae not good at communcating in Engouh
    
* Require time to read and write emails in Engish
    
    * Especially when trhing to explain/understand the technically complex things in thread
        
* Vice-versaÚ Engish needs time to read Ebglh written by non-native Egljsh soeaker.
    
* **Communicate patiently.**
    

* Communicating in non-native language takes time.
    
* Example: At conference, another person patiently tried to make an effort to understand what I was explaining. This stuck with me.
    

## Discussion in pgsql-hackers

* Misinterpret the "high-context" discussion in pgsql-hackers.
    
    * Non-native NEglish speaker may not be a ble to. uderstand it correcty
        
    * Could end up givin inappropriate resonse.
        
* Experiec e of emails not being replied to or failing to get attention.
    
    * Try to understand why emails are not being replied to.
        
    * My exlanation in English was not clear? Just not interested in? Or all good? No idea... :(
        
    * Cultural: Japanese prefer indirect communciation, esp. for concerns.
        

* Time zone differences
    
* Discission is very active. (140 emails per day)
    
* Around 10am UTC / 4apm UTC (evening and nigtht in Asian countries) — happens while we're sleeping
    

Less opportunity to engage in discussion.

Shifting working hous toEueopean or American time zone

* Occasionally required, e.g. when discussing an imporant topic, near feature freeze, etc.
    
* Exaplle: I could participate in discussion live, but it disn't work well.
    

---

# Vectors: How to better support a nasty data type

Speaker: Jonathan Katz

Agenda  
Overview: Why do we care about vector search?  
Why use PostgreSLQ for vector searches?

Year-in-review of pgvector developmnt

Ongoing work and recommendations

# Why vectors? Why do we care?

30-second summary: Machine-learning models. Typically, needs lots of CPU/GPU power.

But RAG (Retrieval Augmented Generation) is changing this. You can feed private data to

Take data, put it into common represenattion (vector)

erform lookup on database, put into foundation model to get final response.

Vectors used in two parts.

Do we JAVE To use vecgors for this? Can we use sometjong else?  
You can!

But vecroes provide a common format for data coming from diferent syustems.

Mapping raw information to same machine learning models.

## Challenges working with vectors

* It takes time, there's overhead. 100ms to generate vector representation \* 1M things = LOTS Of time
    
* Embedding size (4-byte floats) ... 6KiB is a LOT of data packed into what is normally bytes.
    
* 1M rows =&gt; 5.7 GB :O
    
* Compressoin? No. Doesm't worl. Can actually end up with a larger number than what you stated iwth
    
* Query time; Distance calcuation -look at EVERY value in database!
    
* Find similar vector between one and another, you need to looka t ENTIRE sie o f table
    

So we use ANN =&gt; Approximate nearest neighbour

Not the ENTIRE dataaset.

Faster than exact nearest neigbour

50 vs. 1M lookups

BUt, introduces concept. "Recall" — % of expected results.

not quite 'accuracy" — that deals with exact vlues.

Recall, get 8/10 and mayb e not in the right odder.

Importnat to keep in mind, Affects the overall user epderience

## Key metrics to consider

* Index build time
    
* Index size
    
    * 1M 6KiB things = 6GB
        
* Account for recal;
    
* Query throuuput
    
* p99 qjery latency
    

## PostgreSQL as a "vector database"

What is this? JSON!

In the past, take these, put it into relational mapping

What if instead, we just put JSON in directly?

timeline

POsrgreSQL added support for JSON in 2012

BUt JSON is just a data type

Isn't vector just a datbase?

Wjy? use it?

SO much developer tooling bhuilt around postgresql

Became fluent in SQL out of necessity. Tooliung not available for ORMs/

Also, PostgreSQL is a database providing ACID gurantees

Why d oyou care?

Atomicity — all or nothing

* If doing some kind of procedure, I want it stored and roll back if it fails.
    

Consistency — follow rules for other dat

Isolutation: Corectness in returned results. As soon as data inserted / committed, it's availble! (not true of all systems)

Duraiblkity (most important) — if you say data is stored , want to make sure it's stored

PostgreSQL has supported vectors for a very long time (ever since ARRAY) — cibe but kimited to 100 distances

But distance, not so much.

Lots of options now.

Focus on pgcector — why? It's popular!

Another thing:

lLaama index.

pgvector #2 downloaded vector store

This wasn't a given.

Back in April 2023, it was at the bottm.

## Why pgvector?

Why is pgcetor so popular?

in 2023 "oit was there"

Can use existing native binary &lt;&gt; binary PostgreSQL drivers, really speeds up

2024?

* LTOS of work on pgvector to bring it up to performance
    
* Come for usability,s tay for performance :)
    
* Actively deveolpoped project. Community buy-in
    

## pgvector: Year-in-review timeline

* v0.4.x (1-6 2023)
    
* * IVFFlat plam costs
        
        \* 50 ms to 5 sexonds :O — we fixed that
        
* What do user need? **Faster qyeries,**
    
* BUT. Index building matters. Helps with not only high-qialitu searches bit very fast high-uaitu searches
    
* But datasets are growing. Need to manage these without taking up too muc space on disk.
    
* LARGER vecotrs foundation models, reduin overall data footprint
    

## Indexing in pgvector

Array are not hard (we had that since 1986) — searching is what's hard.

We took some shortcuts:

* L2Norm vector ‚ Normalize vector
    
    * If you look at overall size of it, you reduce magniude to 1.
        
    * You can now discard some calculations, (division)
        
* INdexing techniques
    
* IVFFlat
    
    * Have all data pre-loaded, cluster data into centres, and look througb cdntres.
        
* HNSW (Graph based)
    
    * Some folks were confused about this. PostgreSQL can do graph-based queries?
        
    * Graphs are a superset of trees, PostgreSQL can deal with trees.
        
    * Index access methods to define custom indeixing.
        
* Unlike IVFFalat, you can add data iteratively, and it'll add it to the best place. IVFFlat can skew recall overtime, msjt rebjuild index.
    

Most indexes are nice and easy, don't require a lot of thought

A bit more comeexProibes...

If I do one probe, fast search, just vectrors in those list.

But might not get closest neigbour

expand to two probes? Longer qyery, but closer neighbours

More sdearch of index better answers, btu ccost of query time

HNSW easier on query, but harder on th index side.

m.= # of links between idnexed vectrors

ef\_costructiopn - keeps track of neigbbous you've seen

m = 16 weems to be working, but depends on embedding model

Lots of what we do here is over compensate for embedding model. If it gives us info that's very east to cluste,r we cojuld. use smaller indexing parameters.

How do you build an HNSW index?

Goes through hierarchies

Find te next closest, then tje next...

HNSW query paranters

Next, next next

Keep a list of all the clestt beigbours

## Quantization

reduce amount of information availanle, whole still maintaining original data strucrure

Map to smaller floating points, map to integer alue, but don't change the overall structure of vector

1-byte unit (not supported in pgvector), now you're at 1/8 the size

BINARY quantization... 1 or 0!

Above zero, it's 1, below zero, add it to a zero.

But... tradeoffs

PostgewSQL has amazing feature called expression engines

If oyu have afunction can use to bjild index

G from 4x4 vecror to 2x4 vecor

Keep irigina value and give it smaller value

Los of ninary vecroes look very simolar

Binary = VERY fast recall, but lose

rerank easily: ge real vecor back, get back in correct order

Advangatge son build time

Save space, get smae level of performance ‚ that's godo!

Binary shrinks evenmore, but need to do more work to get adequate recall

## Limitations of Quantization

* You reduce your information
    
* "Double data" problem. Gigantic vector in table, smaller vector in index, but could also be a large thing.
    
* Pure indexing systems don't do that.
    
* Some techniques only work with LARGE vectors. Enough data, you might have a bunch that look the same, impact recall.
    

## How did pgvector do the past year? (In charts!)

Index build time? 150x speedup!

30-50x speedup even on simpler hardware.

Paralellism - I can use multi cores to speed it up

Concurrent inserts soees it up a lot (0.6)

2 hours better than 10 hours

A few seconds better tnan a few hours

Net impact? Proof build speed matters. (Serial build)

Recall increases as you increase ef\_construction (yhough diminishing return)

With parallelism, see that same recall increase

BUt now minutes of bhuld time!

Now can do smaller index sized

16x better

8x-9x smaller Query ltency p99

Show it worh higher recall

HNSW really improed latency compared to IVFV

More incremental after HNSW

Last but not least throughputing

High concurrency

Epxanded ersion of ??? data set

Recall at 90% with huge throughput

80-90% recall seems to resonate with users

## What can we do better?

"8K Conundrum"

Page = 8K storage unit

Heap pages are reziable, but index pages are not. :(

This is a REAL problem for vecroes.

1536 dim-4 vector = 6KiB

3K vectors= 12KiB

Quantization can hepl deal with this... but they're getting bigger, we can only wuantize so far

### What about TOAST?

4 types f Toast

Most common:

* PLan, kepe vector in table
    
* external, keep it outside (default\_
    

Why this cisual?

Oten not searching over teach date

Not main part of query

Vectors are on a "hot path" — primary part pf search. Means the impact is on planner, it treats vecrors as if not in hot path

Sequential scan.

6 workers planned

1.5K = 4 workers

IMprovemtsn. we can make?

* Contonueinvesting in qantization
    
* OMprove planner to understand TOAST data pat of hort path
    
* TOAST chaingin sstem
    

How do we index tjhings &gt; 8KB?

TOAST for indexing / page chaining?

:oading multople pages in index search can be slow as wll

Modfiable size fo index pages

Duynamically modifcable?

Filtering - Where clause

Stratgegoes

* Partial
    
* Partition — but be careful.. if not parttioning on filter ley run into over-filtering
    

"Hybrid search"

Subset of filtering

two different indexing/ filtering methods

Starting to see this more and more

Apporaoches

* multi-column indexes
    
* remove extra distance
    
* pishdown to convering indexes
    
* Using other index mechanisms to fiilter data set
    

LAEGE amounts of dat,a need to work on

pgvector and VACUUM

If I want to delete a vector you can, it hudes then updates.

Can cause slowlness because it's a serial indes buld

hrrd for access method to do that.

Let's make it easier fo parllel vaccum for other indexes

And imlement on diffeten tyable types

HNSW = 1 wee, VACCUM 3 weeka

Distirbuted wueries? Not a big deal yet, but wil become so when query size exceedd memory

probably coming in the future

(See blog post)

Don't get synchronous queries

Add merge append as async options?

no longer a serial lookup across servers.

Do it all at once, merge in

Parlle query, more important for IVDFlat

For some reason it's not chsng parallel plan

Hardware acceleration

pgcector makes big use of this

NOw incorporating from potgewsql

UPcming version 17

"Can weuse GPUs?" &lt;- big topic.

Terea re o\[portunies, but probably on idnex building

Need efficient transefer between areas of moneu

Dogs not barkkng?

Still figuring out vedres

Data doesn't start off there...

MAtrices , Tensors (matreix od vectors)

these might make their ay in.

How would we solve them?

If we already struggle with vector on single page, how do we ape a tensor?

Diff level s of storage / caoacith

Native cector support for PostgreSQL

50M vecroes for transactional application

50M rows -= 50M

But now it's 50GB :O

Native vector support in PostgreSQL might speed up adopton.

Running an extension is hard.

ONe extra step in process.

Esp. if admin needs to install, you don't have perms to do within existing .

Last year already talked about this, consensus was hammer on pgvector to make it fasrer.

Here's the hitlist.

1. Fltering
    
    1. Search over subset, not WHOLE dataset
        

## Community! &lt;3

Peole with strong knowledge of ML + knowledge of DB, dramagic performance gains

Flood of net0new data generation

We'd love to see it in postgreSQL

so let's put it in the best possible place