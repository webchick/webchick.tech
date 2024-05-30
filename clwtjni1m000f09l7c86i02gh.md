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

**Detail your assumptions.**

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