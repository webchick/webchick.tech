---
title: "PostHog: Figuring out what the heck your users are doing on your product"
datePublished: Sat May 11 2024 09:00:45 GMT+0000 (Coordinated Universal Time)
cuid: clw1vm2xm00030ajv5ngg14ci
slug: posthog-figuring-out-what-the-heck-your-users-are-doing-on-your-product
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/RbN8pwcYCyM/upload/bf07bbce2c695b3fb22c2f978379c575.jpeg
tags: javascript, opensource, product, posthog

---

## What is PostHog?

[PostHog](https://posthog.com/) is an [open-source](https://github.com/PostHog/posthog) platform that helps teams analyze, test, observe, and deploy new features. They predominantly target [Product Engineers](https://posthog.com/handbook/who-we-are-building-for), but aim to make their tools accessible to everyone on the Product team. They use [ClickHouse](https://clickhouse.com/) on the backend and thus can log bazillions of things.

![Screenshot of PostHog Product Analytics](https://posthog.com/static/a31f7db2abf56ba7e82e88b0d47ea0be/b4d27/screenshot-product-analytics.png align="left")

PostHog offers a number of very useful features for Product teams, including:

* [**Product Analytics**](https://posthog.com/docs/product-analytics): Captures user behaviour in-depth through [Events](https://posthog.com/docs/product-analytics/capture-events) as your users interact with your product. You can then create [Insights](https://posthog.com/docs/product-analytics/insights) to visualize what's happening, and collect those visualizations into [Dashboards](https://posthog.com/docs/product-analytics/dashboards) for easy reference. (And if you're stuck for ideas on Dashboards, there are several [Templates](https://posthog.com/templates) available.)
    
* [**Session Replay**](https://posthog.com/docs/session-replay): Captures and replays for you *exactly* what a user was doing while interacting with your product, including where their mouse went, what they clicked on, etc. This is great for discovering things like your customer journey, as well as the "why" of things you notice in Dashboards.
    
* Various things to help with product testing, such as [Feature Flags](https://posthog.com/docs/feature-flags) (to roll new things out to a subset of users), [A/B Testing](https://posthog.com/ab-testing) (experiment with different features to find what works best), and [Surveys](https://posthog.com/surveys) (collect user feedback from within your product).
    

If you prefer fancy videos, here's their demo:

%[https://youtu.be/2jQco8hEvTI?si=7IMk60tPT66BM-vb] 

If you want to see what's cookin' up next, here's their [roadmap](https://posthog.com/roadmap).

## Sounds cool! How do I get started with PostHog?

PostHog has a [Getting Started tutorial](https://posthog.com/docs/getting-started/install), but it unfortunately seemed to lack some necessary elements to actually get... started. :\\

So here's what worked for me, playing around with a stock copy of [Drupal](https://www.drupal.org/):

1. Once you go through PostHog's signup flow, on the main admin page, you'll see a selection of things to try. Select **Product analytics**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715406778171/840fd5e5-8d01-47c5-a06d-2f83dcec5604.png align="center")
    
2. This takes you to an onboarding flow with 4 steps. At **Install**, choose **HTML snippet**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715410302109/e176e66c-6990-4028-b0c0-2b2b4653ac61.png align="center")
    
3. This will give you a chunk of JavaScript barf similar to the following:
    
    ```html
    <script>
        !function(t,e){var o,n,p,r;e.__SV||(window.posthog=e,e._i=[],e.init=function(i,s,a){function g(t,e){var o=e.split(".");2==o.length&&(t=t[o[0]],e=o[1]),t[e]=function(){t.push([e].concat(Array.prototype.slice.call(arguments,0)))}}(p=t.createElement("script")).type="text/javascript",p.async=!0,p.src=s.api_host.replace(".i.posthog.com","-assets.i.posthog.com")+"/static/array.js",(r=t.getElementsByTagName("script")[0]).parentNode.insertBefore(p,r);var u=e;for(void 0!==a?u=e[a]=[]:a="posthog",u.people=u.people||[],u.toString=function(t){var e="posthog";return"posthog"!==a&&(e+="."+a),t||(e+=" (stub)"),e},u.people.toString=function(){return u.toString(1)+".people (stub)"},o="capture identify alias people.set people.set_once set_config register register_once unregister opt_out_capturing has_opted_out_capturing opt_in_capturing reset isFeatureEnabled onFeatureFlags getFeatureFlag getFeatureFlagPayload reloadFeatureFlags group updateEarlyAccessFeatureEnrollment getEarlyAccessFeatures getActiveMatchingSurveys getSurveys onSessionId".split(" "),n=0;n<o.length;n++)g(u,o[n]);e._i.push([i,s,a])},e.__SV=1)}(document,window.posthog||[]);
        posthog.init('phc_XXXXX',{api_host:'https://us.i.posthog.com'})
    </script>
    ```
    
4. Stick this code just before the closing `</head>` tag in your website's HTML.
    
    <div data-node-type="callout">
    <div data-node-type="callout-emoji">💡</div>
    <div data-node-type="callout-text">In the case of Drupal, I just snuck this snippet into my theme's <code>html.html.twig</code> template file. The "right" way to do it involves grokking <a target="_blank" rel="noopener noreferrer nofollow" href="https://www.drupal.org/docs/develop/creating-modules/adding-assets-css-js-to-a-drupal-module-via-librariesyml" style="pointer-events: none">Drupal's Library System</a>, but that was quite too much for me at midnight. ;) Also, since it's Drupal and all, if you try this, make sure you remember to <a target="_blank" rel="noopener noreferrer nofollow" href="https://drupalize.me/tutorial/user-guide/prevent-cache-clear" style="pointer-events: none">clear the cache</a>, this and any other time you are even <em>breathing</em> near your site's HTML. 🤣</div>
    </div>
    
5. The bottom of this page has a **Check installation** button. If you click it, you'll most likely be notified that no events have been received yet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715410466517/cca3220c-367b-4774-9bd7-3de39471530f.png align="center")
    
6. Not to worry. Go back to your website and start clicking around on things, then come back and try again. It should now read "Installation complete." If it doesn't, see [Troubleshooting and FAQs](https://posthog.com/docs/product-analytics/troubleshooting).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715410812735/cf9d1290-4e61-4ca5-a8c9-6622ba31a36a.png align="center")
    
7. Click **Next** and/or **Skip** through the remaining steps. Among other things, this will turn on [Autocapture](https://posthog.com/docs/product-analytics/autocapture), which automatically logs things like page views, clicks, input changes, etc.
    
8. When finished, you should be at a screen showing some amount of activity from the clicking around on your website that you just did. This is an example of an [**Insight**](https://posthog.com/docs/product-analytics/insights), and you'll be making quite a few of these over time to make sense of all of the data PostHog is capturing.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715411435700/6592250b-dd6c-4754-a24b-9bc4b1ae8ab4.png align="center")
    
9. Click **Save** and you've now got your very first Insight — a **Pageview count**! From here, you can choose to add it to a [Dashboard](https://posthog.com/docs/product-analytics/dashboards), or—if you're feeling *extra* fancy and want to embed these sort of charts dynamically into a document—a [Notebook](https://posthog.com/docs/notebooks).
    
10. You can now check the **Activity** screen to see a running list of *all* the events that are being captured in real-time.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715412876846/c402179c-dff4-4b48-b11d-c916eca1c965.png align="center")
    

## Stay tuned!

I'm out of time for now, but will be digging into this tool a lot more in the coming weeks thanks to the new Growth gig at [Aiven](https://aiven.io/), and hope to write some more of these soon. :)