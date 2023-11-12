---
title: "Creating your own GPTs: A Getting Started Guide"
datePublished: Sun Nov 12 2023 23:46:57 GMT+0000 (Coordinated Universal Time)
cuid: clow4kk9s000209jsbq38hbba
slug: creating-your-own-gpts-a-getting-started-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699832811335/ab8e2bdf-8099-4373-a422-bcb89beb69a7.png
tags: app-development, ai, machine-learning, openai, gpt

---

So it appears the [previous tutorial](https://webchick.tech/creating-your-own-chatgpt-app-a-getting-started-guide) I wrote, uh, less than a week ago, is now out of date. 😅 Late last week, Open AI rolled out [GPTs](https://openai.com/blog/introducing-gpts) which are custom versions of ChatGPT that can be created by regular folk like you and me, *without* writing any code required. 🤯

Let's dive in and see how to use this new capability in practice.

*Note: You'll need to sign up for the* [*ChatGPT Plus*](https://openai.com/chatgpt) *plan ($20/month) to get access to GPT-4 and the custom GPT functionality.*

# First, what is a "GPT"?

GPT stands for [Generative Pre-training Transformer](https://en.wikipedia.org/wiki/Generative_pre-trained_transformer), and it's a type of artificial intelligence that can understand and generate human-like text.

Imagine GPT like a really smart robot in a library. This robot has read almost every book, article, and website in the library. Now, when you ask it a question or tell it to write something, it remembers all the things it has read and uses that knowledge to answer your question or write something new. It's like if you could remember every story or fact you've ever heard and use them to tell your own new stories or answer questions. That's what a GPT does, but with a lot more information!

"GPTs" in this context you can think of kind of like "apps" that are running copies of ChatGPT but with special instructions that you provide to change how it works.

# Overview of GPT Editor

From the ChatGPT interface, go to **Your Name &gt;** [**My GPTs**](https://chat.openai.com/gpts/discovery) (and/or head to [https://chat.openai.com/gpts/discovery](https://chat.openai.com/gpts/discovery))

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699829271385/e0129924-11ae-4b4d-9772-de61f23cc761.png align="center")

From here you can see a list of both "official" GPTs from OpenAI, as well as any you've created. Click on **Create a GPT** (or head to [https://chat.openai.com/gpts/editor](https://chat.openai.com/gpts/editor)).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699829372400/48bbfbe5-8445-461a-9e48-d4d28cc0462e.png align="center")

The editor has two panes: on the left you give it instructions and configuration options, on the right it shows a preview of what the GPT you've created looks like.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699828969119/de18db03-dcfd-4906-b884-594025c439df.png align="center")

Under the **Configure** sub-tab, you'll see some basic options such as "Name" and "Description" as well as the ability to tweak its capabilities, upload additional files to expand the knowledge of ChatGPT, and the ability to add "Actions" (essentially a function call to pull data from *outside* ChatGPT such as the current weather).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699829121153/1ddd455f-e92f-4eb4-98ac-49ca83379441.png align="center")

Let's get started with a couple of examples.

# Let's Build: "Kindergarten Explainer" GPT

There's a [Reddit community](https://www.reddit.com/r/EILI5/) (ELI5) where the goal is for people to explain complex topics using everyday language such that a child would understand. I would like this same capability, but without having to deal with people on Reddit. ;) Let's re-create this idea as a GPT.

Initial prompt:

*Make a kindergarten teacher who's really good at taking deeply complex, technical topics and explaining them so that the kids in their class can understand.*

Waiting...

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699829692318/df704f40-4cb3-4fb5-a1f6-2628d77d8347.png align="center")

After a few seconds, it tweaks some settings on its own and suggests a name, as well as some sample questions you might want to start with. :O

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699829763455/8efc235f-9129-496c-a746-a3e484cbd7d7.png align="center")

I affirm the name sounds good to me, and it continues working for a few seconds:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699829856560/072b6bfc-5ff4-4692-bb67-7cacfd7fc2fb.png align="center")

Bam. Now it has a profile picture that it used [DALL-E](https://openai.com/dall-e-2) to automatically generate based on the name. The preview pane is automatically updated with the image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699830364005/5fe1a760-d53e-489a-a0d4-65baa1357828.png align="center")

It also asks for a bit more detail on the context:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699830405683/a46f5291-cf9b-4981-b60e-1beca55de297.png align="center")

Let's pause here and check out the "Configure" tab. You can see that it's automatically set a bunch of different options:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699830509740/34f5a04b-0adc-454c-a243-2e3117182660.png align="center")

Ok, back to the questions on the **Create** tab. Let's answer them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699830784381/1a505a09-9431-46e9-99c4-8782ea7e93e6.png align="center")

"Interesting" results on the image re-generation. ;)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699830835598/949ddc29-9508-43cb-8846-9fb0fec1191b.png align="center")

Here's what it came up with from my more detailed prompt:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699830887937/21cc175b-0171-46c1-a339-d6bd2a9e7a4a.png align="center")

And here's what it now has for "instructions" on the Configure tab:

*Kindergarten Explainer, portrayed as a female kindergarten teacher of color, is adept at making complex, technical topics simple and understandable. It uses real-world examples over theoretical explanations, making learning relatable and practical. When facing questions that require a deeper understanding, it explains the foundational concepts needed first, offering users a choice on which topic to delve into more deeply. The GPT approaches controversial topics without avoidance, providing balanced, age-appropriate explanations. It maintains a sense of humor, frequently incorporating dad jokes to make learning more enjoyable and engaging. The GPT avoids technical jargon, is patient and encouraging, and always aims to educate in a friendly, accessible manner. Its responses are infused with storytelling or playful language, ensuring explanations are clear, comprehensible, and fun.*

ChatGPT also helpfully created a few sample prompts ("Conversation Starters") to get started. These also appear in the preview pane.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699831155092/7d7b41a6-ddfc-4132-b739-d391a8f9450e.png align="center")

Ok, let's do it!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699831077421/63e25ef1-8891-4564-9827-810b86515ff4.png align="center")

Here's the new preview:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699830931638/33075a34-8761-4c3e-a567-ae24bdc60e15.png align="center")

Let's try it with having it describe how AI works:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699831224912/082edd74-2c46-4b0e-b17f-affb44aa9bbf.png align="center")

Not bad! :)

# Publishing your GPT

When you've tested a few times and are happy with the output, it's time to show your work off to the world (or not).

In the upper right corner of the Editor interface there's a Save button that gives you a few options:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699831773030/9395f932-f3da-463b-8605-c27d2fe86591.png align="center")

Similar to Google Docs, you can make the feature available privately, only to people with a link, or to the general public (requires creating a valid Builder Profile first). It'll pull your Name from your billing details, and you can optionally validate a domain as well, by adding a custom TXT record to the DNS.

You can find Kindergarten Explainer here [https://chat.openai.com/g/g-MdcS7UzmV-kindergarten-explainer](https://chat.openai.com/g/g-MdcS7UzmV-kindergarten-explainer)

What will *you* build next? :)