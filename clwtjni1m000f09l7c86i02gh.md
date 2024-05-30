---
title: "PGConf.dev 2024 Live-Blog"
datePublished: Thu May 30 2024 17:43:29 GMT+0000 (Coordinated Universal Time)
cuid: clwtjni1m000f09l7c86i02gh
slug: pgconfdev-2024-live-blog
tags: postgresql, databases

---

Live blogging a few sessions at the [PostgreSQL Development Conference](https://2024.pgconf.dev/) in Vancouver, BC.

# Lessons from the Support Desk

*Speaker: Evan D Macbeth*

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