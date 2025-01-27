---
title: "Why OpenAI Operator is pretty cool... but will not be coming for anyone's jobs anytime soon. ;-)"
datePublished: Mon Jan 27 2025 07:00:10 GMT+0000 (Coordinated Universal Time)
cuid: cm6ep8cps000l08l58ft9g6c3
slug: openai-operator
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/8gr6bObQLOI/upload/5ffd98ceb9e4a30afdfaa6f6296e0b48.jpeg
tags: ai, automation, openai, agentic-ai

---

A few days ago, OpenAI announced [Operator](https://openai.com/index/introducing-operator/), a research preview of an agent that can use its own browser to perform tasks for you.

The *possibilities* of tech like this are very interesting, essentially allowing you to automate away any tedious tasks that could be done by a person sitting in front of a web browser for long enough. And in fact, when you first log in, the [home screen](https://operator.chatgpt.com/) presents you with several *possibilities*, ranging from booking dinner reservations to finding you a hotel in NYC to aggregating the latest political news.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737917574161/8e763478-fb5f-4cdd-a8e7-fcebb6d1393c.png align="center")

However, it’s always a good idea to test out claims yourself before believing the hype, especially in any over-hyped industry a $1 trillion market cap such as Generative AI. ;P

# Use case: Make a post including links to jobs on LinkedIn

Of course, I’m skipping right past all of those sample ideas, because those have probably all been battle-tested for this preview to make it look awesome. I want to instead see how it reacts to a “real-world” scenario, where someone just asks it to do something that’s on their mind, and I happen to have a request at the ready.

The past couple of years have been rough for folks across many industries, but particularly so for those in the DevRel / Community space. The job market however seems to be picking up in early 2025, and I recently posted a few jobs that sounded interesting to my LinkedIn.

That [post](https://www.linkedin.com/posts/webchick_devrel-community-opensource-activity-7287178283773841409-glAJ), as the kids say, “did numbers,” so clearly folks out there are hungry for this kind of information. But as one commenter—[Chris Ward](https://www.linkedin.com/in/chrischinchilla/)—pointed out, ‘Hiring is back, but sadly so much of it back to "US only"‘.

So let’s test Operator to see if it can make a post that highlights a few DevRel roles that are available in Europe.

# How OpenAI Operator works

Before we get into what happened with that request though, let’s talk a bit about how OpenAI Operator works.

Essentially, OpenAI Operator is a model based on ChatGPT-4, that runs in a virtual machine with access to the [Chromium](https://www.chromium.org/Home/) web browser. (Your Operator conversations are kept separate and distinct from the rest of your ChatGPT conversations.)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737952405461/c72eee9f-6a53-447c-83a8-2d5f7c4c47bd.png align="center")

It analyzes your prompts to determine how best to respond. If it’s a task that involves online activities like browsing websites, filling out forms, or interacting with web applications, it uses Chromium. If the task can be completed through conversation or doesn't require internet access, it is handled within the chat interface like a “normal” ChatGPT chat.

When in browser mode, it performs the tasks “live” through a series of screenshots taken at regular intervals. This allows you to see the progress and actions being taken in the virtual machine in real-time. (You can also share the sequence of screenshots it took afterwards as a video containing all steps.)

Example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737957163463/5462846a-7404-4447-8ab1-fdf8951cac78.gif align="center")

(There’s also an option to get an in-browser notification when it finishes, since certain tasks could take a long time.)

Above the browser window, it shows a bit of info about how it’s thinking about the task / what it’s trying to do, as well as adjustments along the way. Example:

> Worked for 2 minutes:
> 
> Searching LinkedIn for DevRel jobs
> 
> Filtering results to show jobs
> 
> Adjusting location filter to Europe
> 
> Clearing field, entering "Europe" location
> 
> Selecting European Union for jobs
> 
> Filtering results by recent postings
> 
> Applying past week filter for jobs
> 
> Compiling recent EU job listings
> 
> Reviewing job listings, preparing summary

When it encounters specific situations, such as encountering a CAPTCHA, needing to confirm sensitive actions, or when input of personal information is required (e.g. username / password), it will pause what it’s doing and seek human input to ensure accuracy and security. (You can also at any time “Take control” of the browser and get hands on keys/mouse.)

After making manual edits, you then “return control” to the Operator, along with a note of what you did (since it stops recording at this point).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737952960640/b85c6b17-4df0-4c49-bd99-c6a1098f985f.png align="center")

If you’re happy with the results of an Operator, you can “Save” the task and, in a similar way to [creating your own GPTs](https://webchick.tech/creating-your-own-gpts-a-getting-started-guide), specify a default prompt and website(s) to go along with it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737955651715/e8d840cf-a272-435e-943e-85524e655cfa.png align="center")

These then show up as “Pinned” on your home page, so are good for things you want to run frequently.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737955792248/1ed2a759-7974-4c19-a165-65f8f3f853e4.png align="center")

Things Operator *cannot* do?

* It has no knowledge of persistent state between chats; each one is its own fresh universe.
    
* Further, there seems to be some sort of a time cut-off (several hours) at which point the chat box will say “Conversation closed” and you’re not allowed to type in it anymore.
    
* Except, ironically, it also has no knowledge of time, so for example you can’t ask it to check a value on a website for you hourly.
    

# So how did OpenAI Operator do?

There doesn’t seem to be a way to export the chat from Operator, so I’ll do my best to give the play-by-play. (See also the [video](https://youtu.be/gr0gnMNP3NE) of browser activity.)

Starting prompt:

> **Post an update to LinkedIn that contains a list of jobs available in the DevRel space in Europe this week.**

At first, things went pretty smoothly:

* ✅ Interpreted from the prompt that it should start on Linkedin.com
    
* ✅ Figured out it would need to log in in order to do anything further, and prompted me to take control to enter username/password.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737952867967/08e37a72-db03-422c-9acf-a85aee9e27fb.png align="center")
    
    * Note: At this point, LinkedIn prompted me to enter a code from my email because it said I was acting suspicious. Which is probably fair, because I was logged in on my laptop at whatever IP at the same time. :)
        
    * Note #2: Because this required human intervention, it was *not* recorded in the video.
        
* ✅ [~0:04](https://youtu.be/gr0gnMNP3NE?t=4): Navigated to the [LinkedIn Jobs list](https://www.linkedin.com/jobs/), and fiddled with the search words and filters there to find “DevRel jobs in Europe” in location “European Union” that had a Date Posted of the Past Week.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737958026274/55f277dd-b551-46e8-b51b-d548dfa0f74a.png align="center")
    
    .
    
* ✅ Having done this, reported back to the chat with a summary of what it had found, and asked for a quality control check.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737956471072/b994cc6a-8794-4d56-8521-3965bcb36c72.png align="center")
    
    Next prompt:
    

> **That is sufficient. Could you please craft a LinkedIn message that contains links to each of those jobs, but prompt me to manually approve it before it is posted.**

Here’s where things got a bit “interesting”…

* ✅ ~[0:35](https://youtu.be/gr0gnMNP3NE?t=35): Navigated to the home page and opened the post window.
    
* ✅ ~[0:40](https://youtu.be/gr0gnMNP3NE?t=40): Inserted the above text, plus some LinkedIn greeting cruft, plus “\[Link\]” placeholders next to each job
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737957456431/1aa0e710-1790-4943-a9b5-f236d41c896d.png align="center")
    
* ❌ ~[0:41](https://youtu.be/gr0gnMNP3NE?t=41) Attempted to replace \[Link\] placeholders with URLs to jobs and got **stuck in an infinite loop** of highlighting text and failing to replace it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737957554681/9db03361-bc20-4ce6-8673-bbf378e36eee.png align="center")
    
    (I’m honestly not sure what exactly happened here… it’s like it’s trying to highlight only “\[Link\]” and ends up accidentally highlighting a lot more \[maybe because the first part of the message is off-screen and it lost its way-finding?\], then gets confused about why that happens, then tries again, over and over.)
    

Anyway, after several minutes of this, I manually intervene. Prompt:

> **Hi, you seem to be stuck at this step. Is there something I can do to help?**

It responds by **asking me to manually copy/paste** the Markdown into the text area for it??

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737957717486/a299b9e2-5d26-474c-a402-ebc883db1e38.png align="center")

❌ ~[1:33](https://youtu.be/gr0gnMNP3NE?t=93): Ok, now replacing URLs has worked a bit better, but… it’s pretty sloppy. You can see that *some* links are `https://…` (as intended) others are `[https://…` or `[Lhttps://…` and there’s even a VERY special `ttpss://` :P

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737958420157/2f0a5e31-1f76-44f8-8968-f8d6fc17ffc9.png align="center")

❌ I try various tricks to get it to fix these links, including attempting to instruct it directly, and asking it to do automated verification itself. **It was *confidently wrong* every single time. :P** (For example, assuming job postings from 5 minutes ago were “no longer available” vs. that it screwed up the URLs.)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737958607467/ede71146-1ccd-4daf-b138-d37e0cda3b67.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737958595881/a4208b8a-1a9c-4fd9-8600-a00ea44cc88c.png align="center")

Finally I give up and try a different approach. Prompt:

> **Hm. I would like all jobs in this post to be:**
> 
> **1) jobs that are currently available**
> 
> **2) open to candidates living/working in Europe**
> 
> **3) contaning proper, valid URLs connecting people reading this post to said jobs**
> 
> **Is it possible we need to start the process over, or do you think the post can be fixed with only minor adjustments?**

Apparently, Operator agrees with me that starting over is best. ;)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737958831702/a340e011-34fd-4a52-9d0e-21dd30acd23d.png align="center")

* ✅ ~[2:14](https://youtu.be/gr0gnMNP3NE?t=134) Attempt #2 goes better. It seems to better understand what it’s being asked to do, and drafts the post with the links already inside.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737959126456/00dec4ff-0167-4840-87a1-f1bf54d018ee.png align="center")
    
* ✅ As before, it asks me to confirm prior to posting.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737959070762/52cdb5a8-63c9-43e2-b209-107de0d6f2bc.png align="center")
    
* ✅ Success! You can read the post that OpenAI Operator posted on my behalf here: [https://www.linkedin.com/feed/update/urn:li:activity:7289360004195700737/](https://www.linkedin.com/feed/update/urn:li:activity:7289360004195700737/)
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737959246052/108ad926-75d2-4714-9c64-82c5aa983730.png align="center")
    

# BONUS: How could this have gone better? Let’s Ask!

The prior example highlights the importance of [Prompt Engineering](https://www.promptingguide.ai/), so your request is clear and the bot doesn’t have to guess. Adding a new requirement mid-stream (not only a list of jobs but ALSO links to said jobs) seems to have flummoxed it.

Anywho, snark aside, I decided to do some “meta” prompting to ask what I should’ve asked instead:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737959402476/3e069db2-b5eb-4b16-9790-505c71a6850a.png align="center")

Ok… let’s try that! Prompt:

> **Please find and compile a list of Developer Relations jobs available in Europe this week. Draft a LinkedIn post with the job titles, companies, locations, and links, ensuring the links are correctly formatted. Share the draft with me for review before posting.**

This one is fascinating, because it takes a *totally* different approach. Instead of starting with LinkedIn, it searches Bing for Developer Relations jobs and starts clicking into websites like [https://devrelcareers.com/](https://devrelcareers.com/) and [https://www.remoterocketship.com/](https://www.remoterocketship.com/)

As before, it compiles a summary (this time with links!) and asks for input:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737959903564/83e4a12a-46ef-453c-9710-f1730fb426a0.png align="center")

Looking great!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737959937127/9facdbb5-77fa-49c4-b40f-9d2d6c9fd884.png align="center")

Great, now just one last step… post it for me!

**Aaaaand… NO! 🤣**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737959974869/227a0ff5-88d0-45eb-96b9-091482d6a020.png align="center")

A couple things that could be going on here:

1. The capabilities of OpenAI Operator truly changed within the 12 hours of these attempts and it no longer supports posting things to websites (seems doubtful).
    
2. This feature’s getting popular and therefore expensive, so they’ve made it dumber on purpose to cut down on costs (would not be the first time OpenAI has done this).
    
3. The subtle shift in the prompt, from “Post an update to LinkedIn” to “Draft a LinkedIn post” turned off some inner capability in support of keeping costs down.
    

# So what’s the deal, is OpenAI Operator gonna put me out of a job?

To its credit, OpenAI Operator *did* successfully automate several tasks with minimum direction:

* Searching for jobs from numerous sources
    
* Figuring out how to filter those jobs appropriately (by location, by time frame)
    
* Compiling a summary of research
    
* Asking for the human to review said research
    
* Drafting LinkedIn copy
    
* Posting LinkedIn updates (once a human has manually supplied their credentials).
    

What it did NOT do great on, though:

* It didn’t deal well with instructions changing mid-stream.
    
* It doesn’t seem to know when it’s stuck repeating the same instructions and getting nowhere.
    
* It seems to be incapable of checking its own work.
    
* When it *thinks* it’s checked its own work, it’s wrong.
    
* It confidently lies about its correctness, even after repeatedly pointing out its wrongness.
    

In other words, you can’t just set this thing off to do things without you watching it carefully (which, in fairness, is pointed out in the text below the Operator chat box). Sometimes you even need to roll your sleeves up to get it manually unstuck.

Also, real talk: If adding a requirement (links to jobs) midstream thew it for such a loop, it essentially means that OpenAI Operator is currently incapable of doing work for ***actual clients*** because they *never* know what they want up front. ;-)

So it feels we are still *quite* a ways off from delegating any and all knowledge work to agents like this. (The 2 minute video is a bit misleading, as it only captures browser screen frames in rapid succession; the task overall took about an hour whereas “DIY” it would’ve taken about 10 minutes.)

On the other hand, it seems like a very interesting tool to play around with, because the promise of being able to automate, even to a limited extent, “anything you can do in a browser” is pretty fascinating.

What would / will YOU build with this tool? 👀