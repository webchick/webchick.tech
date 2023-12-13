---
title: "How to get an open source AI chatbot (Mixtral) running on your local machine in about 10 minutes"
datePublished: Wed Dec 13 2023 08:48:22 GMT+0000 (Coordinated Universal Time)
cuid: clq3j4dhk000008ieft2m48w1
slug: how-to-get-an-open-source-ai-chatbot-mixtral-running-on-your-local-machine-in-about-10-minutes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702457158423/3504249e-a1f1-45d6-8df0-511ee4768997.png
tags: ai, opensource, ollama, mistral

---

# This Week in Open Source AI...

Big news this week in AI-land, [Mistral AI](https://mistral.ai/)'s new model was [announced](https://mistral.ai/news/mixtral-of-experts/), and the AI folk are all a-flutter about it.

What's the big deal?

* It was first subtly released as a [torrent file](https://twitter.com/MistralAI/status/1733150512395038967) before the marketing post was ready. ;)
    
* It uses a Sparse [Mixture of Experts](https://en.wikipedia.org/wiki/Mixture_of_experts) (SMoE) model — meaning instead of training one super-smart expert model that knows everything about everything, it instead has smaller, specially trained models that are experts on a variety of topics and routes prompts to the appropriate one(s). This allows for more efficient learning and better handling of complex tasks with diverse sub-tasks.
    
* It supports 7 Billion+ *parameters*, which are settings or values that a machine learning model uses to help it learn and make accurate predictions.
    
* Thus, it outperforms GPT3.5 and Llama 2 in most [benchmarks](https://mistral.ai/images/news/mixtral-of-experts/overview.png).
    
* It's natively multilingual (supports English, French, Italian, German and Spanish)
    
* It's [open source](https://github.com/mistralai/mistral-src) (licensed under Apache 2.0)
    
* And finally, when a developer [complained](https://twitter.com/far__el/status/1734341328685896157) about their open source-iness conflicting with a part of their [terms of use](https://mistral.ai/terms-of-use/), the CEO just... [changed it](https://twitter.com/arthurmensch/status/1734470462451732839).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702454516844/79bb680e-3ab7-4278-9b89-22afcfacdf51.png align="center")

# Cool! So how do I try it?

A quick and easy way to try it in your browser is to find them on [Hugging Face](https://huggingface.co/) (which is kinda like GitHub for Large Language [Models](https://huggingface.co/models)), for example, [Mixtral-8x7B-Instruct-v0.1](https://huggingface.co/mistralai/Mixtral-8x7B-Instruct-v0.1) and use the little "Inference API" text box off to the side to type in your prompt.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702456064841/4d5ee311-2919-443a-9422-e4310cef3ac7.png align="center")

However, if you want to play around with it locally, and you don't have a bunch of fancy-bananas GPUs just lying around, there's a great little open source project for that: [Ollama](https://ollama.ai/)!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702455301464/ab38137d-f9c1-4427-a8c6-7df5d6342560.png align="center")

With it, you can choose from any number of supported models and get it up and running locally, lickety-split. (You can also [create and customize your own models](https://github.com/jmorganca/ollama#customize-your-own-model), but I promised a 10-minute tutorial. ;))

# Step by Step

1. Follow the instructions at Ollama's [Download](https://ollama.ai/download) page for your operating system, or grab the [Docker](https://hub.docker.com/r/ollama/ollama) image (esp. if on Windows).
    
2. From the command line, type:  
    `ollama run mistral`
    
3. <div data-node-type="callout">
    <div data-node-type="callout-emoji">💡</div>
    <div data-node-type="callout-text">If you want to try out a different model, check their <a target="_blank" rel="noopener noreferrer nofollow" href="https://ollama.ai/library" style="pointer-events: none">library</a> and use the <code>ollama run</code> command listed on the <a target="_blank" rel="noopener noreferrer nofollow" href="https://ollama.ai/library/llama2" style="pointer-events: none">model detail page</a>.</div>
    </div>
    
4. The first time this command is run, it'll download the model, which looks something like this:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702456691267/69c58354-ad23-47b3-b5e6-5adb70fcaef4.png align="center")
    
5. Thereafter, as well as immediately after completing the download, you'll jump straight into the prompt and can start chatting! 😎
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702456888957/b6bba82b-3290-4db5-9c45-b0b5f7c99e34.png align="center")
    
6. To get out, either type `/bye` or use `Ctrl+D`.
    

# Where can I learn more?

* Read Mistral AI's [announcement](https://mistral.ai/news/announcing-mistral-7b/), or, if you're feeling exceptionally fancy, their [research paper](https://arxiv.org/abs/2310.06825).
    
* Join the [Mistral AI Discord community](https://discord.gg/mistralai).