---
title: "PGConf.dev 2024 Live-Blog"
datePublished: Thu May 30 2024 17:43:29 GMT+0000 (Coordinated Universal Time)
cuid: clwtjni1m000f09l7c86i02gh
slug: pgconfdev-2024-live-blog
tags: postgresql, databases, developer

---

Live blogging a few sessions at the [PostgreSQL Development Conference](https://2024.pgconf.dev/) in Vancouver, BC.

# Lessons from the Support Desk

*Speaker:* [*Evan D Macbeth*](https://www.linkedin.com/in/evanmacbeth/)

## Surface Area vs. Volume

AREA is the MOST important thing for developers to understand.

Every new release, code patch, feature... expands that area of your application (in this case, PostgreSQL), and every developer is resposnsible for an ever-expanding area of that surface.

And your Support organization is responsible for the VOLUME. Biggest takeaway:

***Even making code better increases the work that your support team has to do.***

"We only want to make things better, not worse" — Thomas Munro

That sounds great in theory!  
What happens when you make things better?

1. You bump the version number
    
    1. There's a new release out in the world!
        
2. How does this impact your Support team and customers?
    

They need to support both users applying the fix AND users who DON'T have the fix (double the work!)

Even reducing code complexity increases support work.

So please keep your users, support engineers, and technical account managers in mind when you're doing coding.

Ther'es nothing you can do to make their jobs LESS work. (Can make it erasier, but not less work.)

When creating a feature or fix, **your utopian case matters!**

## **Detail your assumptions.**

All problems can be diagnosed as a **variance from an assumed state.**

"Why did you do it that way?"

"Why did you assume I wouldn't do it that way?"

Detailing assumptions makes it WAY eaier for support team to know what's going on

* What's it supposed to do?
    
* What did you test it on?
    

Use cases (EXAMPLES)

ALL examples are good examples, with a bit of context.

Why? **Users follow examples before reading documentation.**

## Users don't read your docs, but your SUPPORT team does!

Most Support contracts are paying the Support team to read the docs for them. :roll

(The PostgreSQL docs are excellent!)

ChatDox, helps find where to look,but shoud not rely on answer from chat. (Hallucinations are a thing.)

## No one upgrades :(

March 2024 - A bit of less than half of their servers were running PG11 or below. 6 were running 9.6 or below. :O

It's great that new versions of PostgreSQL have new features! But, most users aren't going to see those benefits.

ONE WEEK AGO:

[https://www.yugabyte.com/blog/yugabytedb-moves-beyond-postgresql-11/](https://www.yugabyte.com/blog/yugabytedb-moves-beyond-postgresql-11/)

Trouble ticket:

***The password you entered is too long. \*\*\*Windows NT\*\*\* will not accept a user password that is longer than 14 characters.***

8 JANUARY 2024! :O

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
    
* Also test assumptions. Ask ChatGPT question you expect it to work the way you think. The answer back may surorise yu! Anf that's what your cutomers will get. ;)