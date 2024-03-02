---
title: "Avoiding common pitfalls when first contributing to open source"
datePublished: Tue Feb 13 2024 07:36:52 GMT+0000 (Coordinated Universal Time)
cuid: clsk1v94500070ajv0zwhgtnm
slug: avoiding-common-pitfalls-contributing-to-open-source
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707809698699/a4982bf5-13dd-4430-8187-d0bc140e589f.jpeg
tags: github, python, opensource, community

---

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><strong>UPDATE 2023-03-01:</strong> This blog post got <a target="_blank" rel="noopener noreferrer nofollow" href="https://developers.slashdot.org/story/24/02/29/0730233/avoiding-common-pitfalls-when-first-contributing-to-open-source" style="pointer-events: none">Slashdotted</a>, and as a result of a comment by <a target="_blank" rel="noopener noreferrer nofollow" href="https://slashdot.org/~firewrought" style="pointer-events: none">firewrought</a>, there's now better clarity below on the <a target="_blank" rel="noopener noreferrer nofollow" href="https://webchick.hashnode.dev/avoiding-common-pitfalls-contributing-to-open-source#heading-so-uh-wait-what-are-the-actual-pitfalls-were-avoiding-again" style="pointer-events: none">specific pitfalls you're avoiding</a> by following this advice. :)</div>
</div>

It has been a **LONG** time (we don't need to get into quite *how* long ;)) since I was new to contributing to open source, but I was asked for some advice on how to get started. Here's what I came up with, but I'd **love** to hear what others have to say, as well!

# Start with your interests

While open source is amazing, and you can learn SO much and meet SO many wonderful people... let's face it, it can *also* be a bit frustrating/discouraging at times, so it can be greatly beneficial to have a solid personal reason to tough it out. ;)

Here are some questions to help guide you towards a first project:

* What are open source projects you *already* use?
    
* What programming languages are you strongest in, or want to learn?
    
* What problem space / use cases do you find fascinating and want to dig in more?
    

In this particular person's case, they are interested in learning more about AI/ML, are strongest in Python, and are familiar with [Pandas](https://github.com/pandas-dev/pandas/), so that is a great combination right there. For me, I was into making websites, and I knew PHP really well, so [Drupal](https://www.drupal.org/) made a lot of sense.

# Find a welcoming project

Sometimes, the [vibe](https://lkml.iu.edu/hypermail/linux/kernel/2401.3/04208.html) of a given open source project precedes it, and you have a pretty good idea what you're about to be walking into. But not always. Here are some things you can look for to try and suss out whether a project is likely to welcome new contributors:

* **Do they have a** [**Code of Conduct**](https://www.contributor-covenant.org/version/1/4/code-of-conduct/)**?** This is normally referenced in their README.md or CONTRIBUTING.md file. A Code of Conduct is generally an indicator of a project striving to be inclusive and welcoming.
    
* **Does their issue tracker have tags such as \[**[**help wanted**](https://github.com/search?q=label%3Ahelp-wanted&type=issues)**\], \[**[**good first issue**](https://github.com/search?q=label%3Agood-first-issue&type=issues)**\], \[**[**first-timers-only**](https://github.com/search?q=label%3Afirst-timers-only&state=open&type=Issues)**\]?** This is indicative of a community doing some form of "triage" to help make their project more accessible to newcomers.
    
* **Do they participate in programs geared toward newer contributors**, such as [Google Summer of Code](https://summerofcode.withgoogle.com/), [Outreachy](https://www.outreachy.org/), or [Hacktoberfest](https://hacktoberfest.com/)? This can indicate a higher tolerance for new folks and getting started questions.
    
* **Do they highlight ways to contribute *beyond* just code?** For example, documentation, issue triage, user support? This can indicate a project that takes a more holistic view toward what contribution entails.
    

# Community, *before* code

It can be tempting to get super excited, immediately roll up your sleeves, look at a list of [good first issues](https://goodfirstissue.dev/), filter by your language of choice, and go to town.

Instead, look around for a place where they talk about their "Community." This could be mailing lists, Slack/Discord servers, Reddit/StackOverflow communities, Meetups, Forums, and more. Whatever it is, join up and spend a bit of time lurking. You can pretty quickly get a sense of how they prefer to work, who the major decision-makers are, how receptive they are to newcomers, etc. so you don't end up wasting time in both directions.

In the case of Pandas, for example, they hold a [New Contributor Meeting](https://pandas.pydata.org/docs/development/community.html#new-contributor-meeting) on the 3rd Wednesday of the month, specifically to answer newcomer questions. Drupal has a [First Time Contributor Workshop](https://www.youtube.com/watch?v=0K0uIgKaVNQ) at their conferences, recorded for posterity. Both projects have online Slack communities you can join to meet the people behind the projects.

# Start with the Docs

You might not know it yet, but as a newcomer to an open source project, you have this AMAZING superpower: you are often-times the *only* one in that **whole** project capable of reading the documentation through *new* eyes. Because I can *guarantee*, the people who *wrote* that documentation are **not** new. :-)

So take time to read the docs and file issues (or better yet, pull requests) for anything that was unclear. This lets you get a "feel" for contributing in a project/community without needing to go **way** down the deep end of learning coding standards and unit tests and commit signing and whatever other bananas things they're about to make you do. :) Also, people are more likely to take time to help *you*, if you've helped *them* first!

# So, uh, wait... what are the actual pitfalls we're avoiding, again?

**Fair enough! :D** If you follow this advice, you avoid blissfully waltzing into an open source project...

* **...without sufficient *context***: Open source sometimes has a bad rap for ignoring new contributors / contributions, but I find this tends to happen in large part because folks are working on the "wrong" things: things the project isn't currently prioritizing, things that actively work *against* the stated goals or scope of the project, etc. If you take the time to first understand something about the world you're about to enter *before* you begin working on a PR, you're more likely to save headaches in all directions, and avoid a common problem of "I posted a PR and nobody cared."
    
* **...without sufficient *trust***: Almost every open source maintainer out there is stressed out, over-worked, and many are completely burnt out. This can unfortunately negatively colour their default assumptions (and tone) when they see a new face in their issue queue. By putting a helpful foot forward with a tangible, useful contribution, you demonstrate *through your actions* that you're one of the "good ones" that is there to help vs. there to demand instantaneous free support, for example.
    
* **...without sufficient *relationships***: Normally in order for changes to be made in open source projects, it takes coordination and collaboration of multiple individuals or teams (and certainly the bigger the open source project, the more likely this is to be true). Getting to know *who* those people are, figuring out where they meet (and joining in), what *problems* they are concerned about, etc. will help you be better equipped to know how to get things going again should they stall.
    

This is not to say everything's guaranteed to be sunshine and rainbows in your open source journey, but these are all certain precautions you can take which can go a long way to not wasting your time on a project that doesn't want you. :)

# What are *your* tips/advice?

I'm curious what others would recommend to a new prospective contributor trying to get started on their open source journey? Spout off in the comments! :D

*Cheers to the* [*https://vancouver.dev/*](https://vancouver.dev/) *Discord for prompting this question.*