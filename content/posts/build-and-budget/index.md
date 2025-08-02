---
title: "You build it, you budget it? 💰"
date: 2025-08-02
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

Figma's recent S-1 filing was called out in a [flurry](https://www.infoq.com/news/2025/07/figma-aws-300k-daily-bill/) [of](https://www.datacenterdynamics.com/en/news/design-platform-figma-spends-300000-on-aws-daily/) [headlines](https://news.ycombinator.com/item?id=44462016) for declaring a spend of _"$300,000 a day"_ on AWS. At face value, that number seems shocking, but perhaps the industry _reaction itself_ is the main thing worth examining.  

Many organizations subscribe to the "_[you build it, you **run** it](https://www.thoughtworks.com/en-gb/insights/decoder/y/you-build-it-you-run-it)_" operating model, but this ownership _rarely_ extends to costs. When was the last time your pager went off in the night because a service experienced an unusual spike in costs? ☎️🧑‍🚒

Money can be a taboo topic, and can often feel far-removed from an engineers' remit. The reality is, behind staffing costs, hosting costs are one of the biggest line items for a business, and [FinOps](https://www.finops.org/) is one of the few engineering disciplines where you can know your impact on the bottom line within 24 hours.

In this post, we look at what why costs are a shared responsibility and what developers (and tooling providers) can do to help own them. 

{{< imgresize src="shovel-costs.gif" width="450" height="300" alt="Shovelling money into the Furnace" >}}
_Companies like [37signals](https://basecamp.com/cloud-exit) have been vocal about their cloud exit, presumably feeling like this when it came to paying the invoice._

{{< callout type="note" title="\"Frivolous\" Figma 🤑" collapse="false" >}}
Figma's reported daily spend immediately becomes a moot point when you hear that they are running with a 91% gross margin and their infrastructure spend is only 12% of their revenue. They have been very public about the [many](https://www.figma.com/blog/the-infrastructure-behind-ai-search-in-figma/) [ways](https://www.figma.com/blog/how-figmas-databases-team-lived-to-tell-the-scale/) they have reduced cloud spend.
Thankfully, a lot of the noise was debunked by prominent voices such as [Corey Quinn](https://www.duckbillgroup.com/blog/figmas-300k-daily-aws-bill-isnt-the-scandal-you-think-it-is/). The reaction is interesting though - do engineers _really know_ what a reasonable hosting cost is at their organization, or what _gross-margin_ is?
{{< /callout >}}

### Availability often trumps Costs (🧑‍🚒 > 💸) 
It is understandable why many organizations implicitly prioritise availability over costs in their definition of "owning" a production system.
1. **Visibility**: The former is immediately visible to clients, so does not carry as much immediate reputational damage.
1. **Complexity**: It is easier to reason about. An SLA is a static target. Costs are dynamic - each part of the system's spend may correlate with different factors (e.g. scheduled bursts or spikes due to system activity).
1. **Maturity**: Startups desperately need market fit before they can set up a rigid FinOps strategy. If growth figures are healthy, costs are less of a concern. 
1. **Cost**: The ironic one - engineers are expensive, so having them purely focus on this is not a differentiator.

### Conway's Law: A limiting factor? ⚖️
Many organizations choose to divide teams into Product and Platform responsibilities as a way of creating abstraction. As [Conway's Law](https://en.wikipedia.org/wiki/Conway%27s_law) describes, the system architecture becomes a representation of the organization structure.  This results in situations where developers shipping features often do not understand the infrastructure that their code runs on. Greater abstraction means freedom at the infrastructure level, but also means less scrutiny on hosting costs for developers who aren't operating at that level of the stack.

The key trade-off in these team boundaries, is that many meaningful cost optimization opportunities arise in the **intersection** of what Product and Platform Engineering teams can achieve alone.

{{< imgresize src="platform-product-venn.png" width="890" height="477" alt="The Platform-Product Venn diagram" >}}
_A simplified model - responsibilities will vary by org, with impactful efforts sitting in the overlap._

### Optimisations require partnership 🤝
In a series of project spanning a few quarters, we managed to reduce our AWS spend by 40%. This was no mean feat, but the main takeaway was that _every optimisation_ required communication between Platform and Product teams. Whether this was in gathering data, getting buy-in or keeping teams in the loop in case of outages.

{{< callout type="note" title="Infrastructure settings ⚙️" collapse="true" >}}
Settings which are low-effort to change, and should arguably be defaults. Once enabled, they are immediately effective.

**e.g.**: Intelligent tiering, Bucket Keys, Graviton
{{< /callout >}}

{{< callout type="note" title="Spring-cleaning 🧹" collapse="true" >}}
...

**e.g.**: Unused services, Lifecycle policies, TTLs, job reapers
{{< /callout >}}

{{< callout type="note" title="Right-sizing 🤏" collapse="true" >}}
...

**e.g.**: Capacity, serverless
{{< /callout >}}

{{< callout type="note" title="Re-architecting 🎲" collapse="true" >}}
...

**e.g.**: Spot compute, middleware, removing failover instances
{{< /callout >}}

{{< callout type="note" title="Application changes 🧩" collapse="true" >}}
...

**e.g.**: Caching, network chatter, database access patterns, logging
{{< /callout >}}

### Shifting left ⏪
Not every developer needs to take on large optimisation projects to impact costs. Let's look at some practical ways that Engineers could take greater ownership. 

#### Dashboards 📊
Cost explorer

#### Tooling 🛠️
- https://docs.datadoghq.com/developers/ide_plugins/idea/
- https://www.infracost.io/
- https://www.apptio.com/products/kubecost/?src=kc-com

#### Designs 🎨
ADRs

#### Artificial Intelligence 🤖
AI assistants:
Kiro, Claude.md, CodeRabbit

### Locked in? 🔐
A lot of the scrutiny of Figma's figures came from their $500m multi-year commitment to AWS, admitting their reliance on a sole provider. Many fail to consider the opportunity cost of not doubling down on that commitment.
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
- ADRs

### Summary 🧵
This post tried to cover a lot of ground. Here are my main takeaways:

1. 💸 Costs are a **shared responsibility**, like availability, with a more immediate ROI. Delegating responsibility to a single platform/FinOps team leaves many optimisations off the table.
1. 🔐 Lock-in and cloud commitments get a bad reputation, because it's harder to quantify the **opportunity cost** of not going "all-in". 
1. 💻 Developer tooling and AI **shifts a lot of effort left**. Producing code will become less of bottleneck as more of this is delegated to machines. However, understanding how that code impacts system reliability and costs will only matter more. 

In future posts, I may dive into some cost-saving measures I have seen in the wild. In the meantime, here are a few podcast recommendations:
- 🎧 [Screaming in the Cloud (Last Week in AWS)](https://www.lastweekinaws.com/podcast/)
- 🎧 [Cloud Masters (DoIt)](https://www.doit.com/podcasts/cloud-masters/)

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
