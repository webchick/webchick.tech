---
title: "Creating your own ChatGPT app: A Getting Started Guide"
datePublished: Thu Nov 09 2023 07:06:53 GMT+0000 (Coordinated Universal Time)
cuid: cloquix6q000z09johhz4ghw0
slug: creating-your-own-chatgpt-app-a-getting-started-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699513509307/bf81aeac-9a1d-41ee-bb36-e7e4c2f64a07.webp
tags: ai, generative-ai, chatgpt

---

In today's installment of Tech Around And Find Out, we dig into the wild world of Generative AI.

Earlier this week, [OpenAI DevDay](https://devday.openai.com/) took place, and the Internet has been abuzz since with the various [announcements](https://openai.com/blog/new-models-and-developer-products-announced-at-devday) that happened there.

One of those was the new [Assistants API](https://platform.openai.com/docs/assistants/overview) that makes it easier for developers to build their own ChatGPT-powered apps. Check out some [examples](https://platform.openai.com/examples), that range from the useful such as [Spreadsheet Creator](https://platform.openai.com/examples/default-spreadsheet-gen) or [Python Bug Fixer](https://platform.openai.com/examples/default-fix-python-bugs) to the fun such as [Rap Battle Writer](https://platform.openai.com/examples/default-rap-battle) and [Summarize for a 2nd Grader](https://platform.openai.com/examples/default-summarize).

But how can you yourself create such an app? Let's dive in!

# Prototyping in the Playground

*Note: To use the Assistants API, you must a) be a* [*ChatGPT "Plus"*](https://openai.com/chatgpt) *subscriber, and b)* [*paid*](https://platform.openai.com/account/billing/) *for at least $5 in API credits.*

Before diving into the code, it can be helpful to play around with the various options and see the results. Enter the [OpenAI Playground](https://platform.openai.com/playground)!

Head to [https://platform.openai.com/assistants](https://platform.openai.com/assistants) and there you'll find a handy-dandy "Create" button. Once you click that, you'll see an interface that asks for several pieces of information:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699505130106/87382493-9b0a-45b6-9265-ba4bfe211785.png align="center")

Some of these require further explanation, so here's an overview:

* [**Instructions**](https://openai.com/blog/custom-instructions-for-chatgpt): Custom instructions allow you to add preferences or requirements that you’d like ChatGPT to consider when generating its responses. Examples of things you can influence include tone of voice, length of responses, and how it should address you (see also this [FAQ](https://help.openai.com/en/articles/8096356-custom-instructions-for-chatgpt)).
    
* [**Model**](https://platform.openai.com/docs/models): Which version of ChatGPT to use. Options include standard, "turbo" (which allows dealing with massive amounts of text) and "preview" (to show what's coming up next). Generally speaking, the fancier it is, the more recent its dataset, and also the more it [costs](https://openai.com/pricing).
    
    * According to ChatGPT itself btw, the most cost-efficient model as of this writing is **gpt-3.5-turbo-1106**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699507954355/c44de6bd-ff95-403b-a70b-8ad1009be7f4.png align="center")
        
* [**Tools**](https://platform.openai.com/docs/assistants/tools)**:** These give your assistant additional capabilities such as [Code Interpreter](https://platform.openai.com/docs/assistants/tools/code-interpreter) (to read and run code) or [Knowledge Retrieval](https://platform.openai.com/docs/assistants/tools/knowledge-retrieval) to grab data out of user-uploaded [files](https://platform.openai.com/docs/assistants/tools/supported-files). You can also build your own Tools by defining a [Function](https://platform.openai.com/docs/assistants/tools/function-calling). (You can find some nifty ideas in the [OpenAI Cookbook](https://cookbook.openai.com/).)
    

Once you've filled things out as you like, click the **Test** button to see it in action!

# Basic App: Talk Like A Pirate

This one doesn't use any of the special Tools, but instead uses Instructions to modify the way ChatGPT responds.

**Instructions:** *You are a pirate, and you talk like one. This means during dialog, you substitute regular English words with pirate words like "Arrr" and "matey"*

**Result:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699508766186/0e50f3dc-7481-4bff-88c7-f3c16dcdf506.png align="center")

# More Advanced App: Pirate Coder

Now let's try out some more advanced features. Create a new Assistant, and turn on the "Code Interpreter" option. Give it the following **Instructions**:

*A user will paste in some code. You should summarize what it does in plain language. But with a twist: Make sure when you respond, you do so in the most pirate-y way possible. Then re-write the code so any strings are in pirate speak as well.*

Here's the result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699510967309/31284edd-8153-4775-8ad2-a1b769b7bf89.png align="center")

Pretty nifty! :D

# Further Reading

* [Assistants API](https://platform.openai.com/docs/assistants/overview)
    
* [How Assistants Work](https://platform.openai.com/docs/assistants/how-it-works)
    
* [Tools](https://platform.openai.com/docs/assistants/tools)