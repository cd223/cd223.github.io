---
title: "You build it, you budget it 💰"
date: 2025-07-19
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

Money can be a taboo topic, and can often feel far-removed from an engineers' remit. The reality is, behind staffing costs, hosting costs are one of the biggest line items for a business, and [FinOps](https://www.finops.org/) is one of the few engineering disciplines where you can know your impact on the bottom line within 24 hours. 

A lot of organizations subscribe to the "_[you build it, you **run** it](https://www.thoughtworks.com/en-gb/insights/decoder/y/you-build-it-you-run-it)_" operating model, but this _rarely_ extends to costs. When was the last time your pager went off in the night because a service exceeded its budget?

In this post, we look at what a _"you build it, you **budget** it"_ philosophy looks like and why vendor lock-in isn't always a bad trade. 

{{< imgresize src="shovel-costs.gif" width="450" height="300" alt="Shovelling money into the Cloud" >}}
_A representation of how companies like [37signals](https://basecamp.com/cloud-exit) view cloud provider invoicing..._

### "Frivolous" Figma 🤑
Figma's recent S-1 filing was called out in a [flurry](https://www.infoq.com/news/2025/07/figma-aws-300k-daily-bill/) [of](https://www.datacenterdynamics.com/en/news/design-platform-figma-spends-300000-on-aws-daily/) [headlines](https://news.ycombinator.com/item?id=44462016) this month for declaring a spend of "$300,000 a day" on AWS. At face value, this seems shocking, but immediately becomes a moot point when you hear that they are running with a 91% gross margin and their infrastructure spend is only 12% of their revenue. They have been very public about the [many](https://www.figma.com/blog/the-infrastructure-behind-ai-search-in-figma/) [ways](https://www.figma.com/blog/how-figmas-databases-team-lived-to-tell-the-scale/) they have reduced cloud spend. 

Thankfully, a lot of noise was debunked by prominent voices such as [Corey Quinn](https://www.duckbillgroup.com/blog/figmas-300k-daily-aws-bill-isnt-the-scandal-you-think-it-is/). The reaction is interesting though - do engineers _really know_ what a reasonable cloud bill is at their organization? 

### Shifting Left ⏪
...

- https://docs.datadoghq.com/developers/ide_plugins/idea/
- https://www.infracost.io/
- https://www.apptio.com/products/kubecost/?src=kc-com
- "Platform" Engineering Paradox 🔁

### Locked in? 🔐
...

https://serverlessland.com/content/guides/refactoring-serverless/introduction

### The optimisation taxonomy 📉
In a recent cost optimization effort, we reduced AWS spend by 40%. I would bucket the effective optimizations into a few categories. 

- Compute = (Capacity * Time)
- Storage = (Retention * Storage Tier) + Data Transfer + API calls 
- Logging = (Events * Size)

1. **No-brainers** 🧠: Intelligent tiering, Bucket keys, Graviton
1. **Right-sizing** 🤏: Capacity, serverless 
1. **Availability gamblers** 🎲: Spot compute, middleware, removing failover instances
1. **Spring-cleaning** 🧹: Lifecycle policies, TTLs, job reapers

### The budgeters' philosophy 💼
Let's end on what I see a _"you build it, you budget it"_ philosophy like in practice.

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
