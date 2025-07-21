---
title: "You build it, you budget it 💰"
date: 2025-07-22
tags: ["aws", "cloud", "finops"]
showToc: true
draft: true
TocOpen: false
hidemeta: false
comments: true
disableHLJS: true
disableShare: false
hideSummary: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: true
UseHugoToc: true
---

Figma's recent S-1 filing was called out in a [flurry](https://www.infoq.com/news/2025/07/figma-aws-300k-daily-bill/) [of](https://www.datacenterdynamics.com/en/news/design-platform-figma-spends-300000-on-aws-daily/) [headlines](https://news.ycombinator.com/item?id=44462016) this month for declaring a spend of _"$300,000 a day"_ on AWS. At face value, that number seems shocking, but perhaps the industry _reaction itself_ is the main thing worth examining.  

Many organizations subscribe to the "_[you build it, you **run** it](https://www.thoughtworks.com/en-gb/insights/decoder/y/you-build-it-you-run-it)_" operating model, but this ownership _rarely_ extends to costs. When was the last time your pager went off in the night because a service experienced an unusual spike in costs? ☎️🧑‍🚒

Money can be a taboo topic, and can often feel far-removed from an engineers' remit. The reality is, behind staffing costs, hosting costs are one of the biggest line items for a business, and [FinOps](https://www.finops.org/) is one of the few engineering disciplines where you can know your impact on the bottom line within 24 hours.

In this post, we look at what a _"you build it, you **budget** it"_ philosophy might look like.

{{< imgresize src="shovel-costs.gif" width="450" height="300" alt="Shovelling money into the Cloud" >}}
_Companies like [37signals](https://basecamp.com/cloud-exit) have been vocal about their cloud exit, presumably feeling like this when it came to paying the invoice._

{{< callout type="note" title="\"Frivolous\" Figma 🤑" collapse="false" >}}
Figma's reported daily spend immediately becomes a moot point when you hear that they are running with a 91% gross margin and their infrastructure spend is only 12% of their revenue. They have been very public about the [many](https://www.figma.com/blog/the-infrastructure-behind-ai-search-in-figma/) [ways](https://www.figma.com/blog/how-figmas-databases-team-lived-to-tell-the-scale/) they have reduced cloud spend.
Thankfully, a lot of the noise was debunked by prominent voices such as [Corey Quinn](https://www.duckbillgroup.com/blog/figmas-300k-daily-aws-bill-isnt-the-scandal-you-think-it-is/). The reaction is interesting though - do engineers _really know_ what a reasonable cloud bill is at their organization, or what _gross-margin_ is?
{{< /callout >}}

### Availability (💥) > Costs (💸) 
It is understandable why many organizations implicitly prioritise availability over costs in their definition of "owning" a production system.
1. **Visibility**: The former is immediately visible to clients, so does not carry as much immediate reputational damage.
1. **Complexity**: It is easier to reason about. An SLA is a static target. Costs are dynamic - each part of the system's spend may correlate with different factors (e.g. scheduled bursts or spikes due to system activity).
1. **Maturity**: Startups desperately need market fit before they can set up a rigid FinOps strategy.
1. **Cost**: The ironic one - engineers are expensive, so having them purely focus on this is not a differentiator.

The key caveat to all of this, is many meaningful opportunities arise in the **intersection** of what Product and Platform Engineering teams can achieve alone.

Many organizations choose to divide teams into Product and Platform responsibilities as a way of creating abstraction. As Conway's Law describes, by doing this you end up in a state where developers shipping features do not understand the infrastructure that their code runs on. Greater freedom at the infrastructure level may mean less scrutiny on hosting costs for developers who aren't operating at that level.

### Optimisation Hunting 🤠
In a series of efforts spanning a few Quarters, we managed to reduce our company AWS spend by 40%. This was no mean feat, but now it's done, I can look back and bucket the different optimizations into a few categories.

{{< callout type="note" title="No-brainers 🧠" collapse="true" >}}
Settings which should arguably be defaults. Once enabled, they are immediately effective.

**Examples**: Intelligent tiering, Bucket Keys, Graviton

**Difficulty**: Low

**Ownership**: Platform
{{< /callout >}}

{{< callout type="note" title="Spring-cleaning 🧹" collapse="true" >}}
...

**Examples**: Lifecycle policies, TTLs, job reapers

**Ownership**: Platform

{{< /callout >}}

{{< callout type="note" title="Right-sizing 🤏" collapse="true" >}}
...

**Examples**: Unused services, Capacity, serverless

**Ownership**: Platform
{{< /callout >}}

{{< callout type="note" title="Availability gamblers 🎲" collapse="true" >}}
...

**Examples**: Spot compute, middleware, removing failover instances

**Ownership**: Platform
{{< /callout >}}

{{< callout type="note" title="Application changes 🧩" collapse="true" >}}
...

**Examples**: Caching, network chatter, database access patterns, logging

**Ownership**: Platform
{{< /callout >}}

What should become clear is that _every single one of these_ optimisations require some level of communication between Platform and Product to gather data, get buy-in and keep teams in the loop in case of outages.

### Shifting Left ⏪
Let's look at some practical ways that Engineers could take greater ownership of costs. 

1. Tooling:
- https://docs.datadoghq.com/developers/ide_plugins/idea/
- https://www.infracost.io/
- https://www.apptio.com/products/kubecost/?src=kc-com

1. Tooling:


- 
1. AI assistants:

### Locked in? 🔐
A lot of the scrutiny of Figma's figures came from their $500m multi-year commitment to AWS, admitting their reliance on a sole provider. 

What many fail to realise is the opportunity cost of not doubling down on that commitment.
https://serverlessland.com/content/guides/refactoring-serverless/introduction

### The budgeters' philosophy 💼
Let's end on what I see a _"you build it, you budget it"_ philosophy like in practice.

{{< callout type="note" title="Mental Model 💲" collapse="false" >}}
- Compute = (Capacity * Time)
- Storage = (Retention * Storage Tier) + Data Transfer + API calls
- Logging = (Events * Size)
{{< /callout >}}

- Soft quotas
- Cost anomalies
- Cost incidents: same attention as outages.

### Summary 🧵
In this post, ...

In future posts, I may dive into some niche cloud cost-saving measures. Here are a few podcast recommendations in the meantime:
- 🎧 [Screaming in the Cloud (Last Week in AWS)](https://www.lastweekinaws.com/podcast/)
- 🎧 [Cloud Masters (DoIt)](https://www.doit.com/podcasts/cloud-masters/)

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
