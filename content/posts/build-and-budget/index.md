---
title: "You build it, you budget it? 💰"
date: 2025-08-06
tags: ["aws", "cloud", "finops"]
showToc: true
draft: false
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

In this post, we look at:
1. Why costs are a **shared responsibility**.
1. What developers (and tooling providers) can do to help own them **early on**.
1. The vendor "lock-in" **trade-off**.

> _This post was largely inspired by SigNoz's post: ["Observability isn't just for SREs"](https://signoz.io/blog/why-observability-isnt-just-for-sres/)._

### FinOps 💰
Cost management can often feel far-removed from an engineer's remit. The reality is, behind staffing costs, hosting costs are one of the biggest line items for a business, and [FinOps](https://www.finops.org/) is one of the few engineering disciplines where you can know your impact on the bottom line within 24 hours.

{{< imgresize src="shovel-costs.gif" width="450" height="300" alt="Shovelling money into the Furnace" >}}
_Companies like [37signals](https://basecamp.com/cloud-exit) have been vocal about their cloud exit, presumably feeling like this when it came to paying the invoice._

{{< callout type="success" title="\"Frivolous\" Figma 🤑" collapse="false" >}}
Figma's reported daily spend immediately becomes a moot point when you hear that they are running with a 91% gross margin and their infrastructure spend is only 12% of their revenue. They have been public about the [many](https://www.figma.com/blog/the-infrastructure-behind-ai-search-in-figma/) [ways](https://www.figma.com/blog/how-figmas-databases-team-lived-to-tell-the-scale/) they have reduced cloud spend.
Thankfully, a lot of the noise was debunked by prominent voices such as [Corey Quinn](https://www.duckbillgroup.com/blog/figmas-300k-daily-aws-bill-isnt-the-scandal-you-think-it-is/). The reaction is interesting though - do engineers _really know_ what a reasonable hosting cost is at their organization, or what _gross-margin_ is?
{{< /callout >}}

### Availability often trumps Costs (🧑‍🚒 > 💸) 
It is understandable why many organizations implicitly prioritise availability over costs in their definition of "owning" a production system.
1. **Visibility**: The former is immediately visible to clients, so does not carry as much immediate reputational damage.
1. **Complexity**: It is easier to reason about. An SLA is a static target. Costs are dynamic - each part of the system's spend may correlate with different factors (e.g. scheduled bursts or spikes due to system activity).
1. **Maturity**: Startups desperately need market fit before they can set up a rigid FinOps strategy. If growth is sufficiently high in the early stages, costs are less of a concern. 
1. **Cost**: The ironic one - engineers are expensive, so having them purely focus on this is sometimes not viable.

Despite feeling like orthogonal concerns, several concepts we use to describe availability could also carry over into the FinOps space.

{{< callout type="note" title="Parallels ↔️" collapse="false" >}}

| Availability 🧑‍🚒 | FinOps 💸                                            |
|--------------------|------------------------------------------------------|
| **SLA**            | Target spend - a fixed $ value, or % of revenue.     |
| **Alert**          | A budget breach or anomaly alarm.                    |
| **MTTD**           | Mean time (duration) to _detect_ a cost spike.       |
| **MTTR**           | Mean time (duration) to _recover_ from a cost spike. |
| **Incident**       | An investigation into an unexplained cost.           |
| **Observability**   | Cost and usage reports/dashboards.                   |
{{< /callout >}}

### Conway's Law: A limiting factor? ⚖️
Many organizations choose to divide teams into Product and Platform responsibilities as a way of creating abstraction. As [Conway's Law](https://en.wikipedia.org/wiki/Conway%27s_law) describes, a system architecture will become a representation of the organization structure.  This results in situations where developers shipping features often do not understand the infrastructure that their code runs on. Greater abstraction means freedom at the infrastructure level, but also means less scrutiny on hosting costs for developers who aren't operating at that level of the stack.

The key trade-off in these team boundaries, is that many meaningful cost optimization opportunities arise in the **intersection** of what Product and Platform Engineering teams can achieve alone. If the responsibility to optimise costs lies with a central team, the goal becomes a moving target as micro-level decisions elsewhere slowly negate the impact of planned work. Efforts significantly reduce if a culture of awareness/ownership exists across teams. 

{{< imgresize src="platform-product-venn.png" width="890" height="477" alt="The Platform-Product Venn diagram" >}}
_A simplified model - responsibilities will vary by org, with impactful efforts sitting in the overlap._

### Optimisations require partnership 🤝
In a series of projects spanning a few quarters, we managed to reduce our AWS spend by 40%. This was no mean feat, but a key lesson was that _every optimisation_ required communication between Platform and Product teams. Whether gathering data, getting buy-in or keeping teams in the loop in case of unexpected outages.

Life is also made significantly easier if Product-focused teams can readily help explain _ongoing cost changes_ (e.g., a new client onboard, a recent feature rollout etc.). If revenue increases proportionally, it becomes less of a concern and budgets can be adjusted to the new baseline.

Let's look at some common types of optimisation, and the level of their cross-team dependencies. These are placed in order of **increasing dependency** on Product context, to squeeze the most value out of each optimisation.  Click to expand/collapse each one.

{{< callout type="note" title="Settings ⚙️" collapse="true" >}}
Settings which are low-effort to change, and should arguably be defaults. Once enabled, they are immediately effective.

**e.g.**: Using [intelligent tiering](https://aws.amazon.com/s3/storage-classes/intelligent-tiering/), [bucket encryption keys](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-key.html), different architectures (e.g. [Graviton](https://docs.aws.amazon.com/prescriptive-guidance/latest/optimize-costs-microsoft-workloads/net-graviton.html)), log [classes](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CloudWatch_Logs_Log_Classes.html).

**Dependencies**: Co-ordination is needed during testing and rollout to minimise impact on production environments.
{{< /callout >}}

{{< callout type="note" title="Cleanup 🧹" collapse="true" >}}
Reducing the footprint of compute services and managing the lifetime of data.

**e.g.**: Removing unused services, adding [lifecycle policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html), [TTLs](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html), [job timeouts](https://docs.aws.amazon.com/batch/latest/userguide/job_timeouts.html).

**Dependencies**: Much like [Hyrum's law](https://www.hyrumslaw.com/) for APIs, it is almost never clear which service or data is relied upon until it is deleted. Product teams can provide context on which service/data is valuable and for which initiatives/clients far quicker than metrics would alone. Metrics tell you the current state of the world - not what to expect in the near future.
{{< /callout >}}

{{< callout type="note" title="Right-sizing 🤏" collapse="true" >}}
Matching the reserved capacity of compute services as closely to their usage as possible.   

**e.g.**: Changing CPU and memory (statically or dynamically), removing redundant instances, adopting serverless.

**Dependencies**: If embracing serverless, there are fundamental limitations (e.g. memory, timeouts) that Product teams need to know about when shipping code. Right-sizing might mean use of horizontal or vertical scaling, which means choosing a sensible scaling strategy (e.g. scheduled, on-demand). This all requires crucial Product context.
{{< /callout >}}

{{< callout type="note" title="Re-architecting 🎲" collapse="true" >}}
Changing the operating model or system architecture of a service, accepting a reasonable trade-off (e.g. performance, availability) for a significant cost reduction. 

**e.g.**: Embracing event driven architecture ([EDA](https://aws.amazon.com/what-is/eda/)), removing middleware (e.g. queues/load balancers/proxies), using [Spot compute](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html).

**Dependencies**: Adopting EDA might add integration latency at key points in a customer workflow. Using interruptible batch jobs could delay critical outputs if there is no checkpointing in use when the job restarts. Metrics can help guide decisions on how often middleware services add value, but Product context is needed to assess whether they are needed long-term. What might seem overkill for today's scale might be perfectly sensible for an upcoming initiative.  
{{< /callout >}}

{{< callout type="note" title="Code changes 🧩" collapse="true" >}}
Modifying the behaviour of application code to alter its usage of resources (e.g., databases, storage, APIs).

**e.g.**: Caching, "pushing down" data filtering, changing storage/API access patterns, reducing logging.

**Dependencies**: Often the hardest optimisations for Platform teams to spot if relying on infrastructure metrics alone. An isolated measure of CPU/memory usage or database accesses will not tell you whether there is _room to meaningfully optimise behaviour_. This is where an observability stack of Logs, Metrics and Traces matters. Everyday code changes can introduce large changes in the cost-profile of a service. _Shifting left_ is even more important at this level (discussed below).
{{< /callout >}}

### Shifting left ⏪
So far, we have only touched on _optimisations_ once costs are already a problem. With greater ownership across teams, we can shift a lot of these concerns "left" earlier in the development cycle, to reduce the size of future problems. Not every developer needs to take on large, multi-week optimisation projects to be seen as "owning" costs. 

A sad irony is that getting visibility into costs itself carries a cost (through additional services and SaaS subscriptions), but the payoff is often worthwhile.

#### Observability 📊
Giving teams _visibility_ of their baseline costs is the first step.  If using a cloud provider, a lot of these primitives are provided:
1. **Tagging**: Label infrastructure by team/project. Regularly monitor Cost Explorer dashboards (e.g. [AWS](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/)/[GCP](https://cloud.google.com/stackdriver/docs/costs/optimize-costs)/[KubeCost](https://www.apptio.com/products/kubecost/)) and schedule reports.
1. **Alerting**: Set up budgets and anomaly detection, with integrations to the communication platforms (e.g. Slack & incident.io).
1. **Dependencies**: Monitor usage metrics for each third-party provider / service / API that has its own pricing model.

Once observability is in place, let's look at some practical methods that enable cost ownership earlier on in development. 

#### Designs 🎨
During the design of a new service or feature, ADRs (Architectural Decision Records) could explicitly consider the cost impact of decisions - forcing early discussion. Whilst it is tricky to provide exact dollar estimates, a "back of the envelope" calculation is made far easier by cloud providers' [Pricing Calculators](https://calculator.aws/#/). In the age of AI and LLMs with [spiralling costs there](https://ethanding.substack.com/p/ai-subscriptions-get-short-squeezed), there are even [token calculators](https://pricepertoken.com/)!

> _A mental model I like to use for Cloud costs is:_
> - `Compute = (Capacity * Time)`
> - `Storage = (Retention * Data Size) + Data Transferred`
> - `Logging = (Retention * Event Count * Event Size)`

#### Tooling 🛠️
A range of tooling exists to target the IDE and Pull Request workflows, which developers can use to estimate and reduce cost impact before code is shipped.

For infrastructure changes, tools like [Infracost](https://www.infracost.io/) offer comparisons in the IDE and PR reviews. At the application layer, I've had some success using [Datadog's IDEA plugin](https://docs.datadoghq.com/developers/ide_plugins/idea/) to remove noisy logs and optimise frequently executed code. There is room for vendors to go further in this space, and bring cost awareness to the IDE for application code. 

{{< imgresize src="infracost.webp" width="1000" height="433" alt="Viewing costs inside a pull request diff" >}}
_*Image credit: [Infracost](https://www.infracost.io/products/)*_

#### Artificial Intelligence 🤖
As AI tooling like [Claude Code](https://www.anthropic.com/claude-code) and [CodeRabbit](https://www.coderabbit.ai/) start to integrate into CLI/IDE and VCS software, there is a natural space to ensure costs are considered with every prompt. 

Amazon's [Kiro](https://kiro.dev/) is an interesting proposition here. Providing "spec" documents and breaking tasks down like a human before code is generated would naturally lend itself to feeding in ADRs like those described above.  If a file exists in the repository describing the system's tenancy model, budget and priorities as a system prompt, then the code these tools generate could reflect that. 

### "Lock-in": Friend or foe? 🔐
The final topic we will touch on here is vendor _"lock-in"_. A lot of the scrutiny on Figma's IPO filings came from their $545m-per-year _multi-year_ commitment to AWS. By admitting their reliance on a sole provider and solidifying plans to spend across a long-term horizon, it was seen by many as a big _concentration risk_. 

As [Corey Quinn](https://www.duckbillgroup.com/blog/figmas-300k-daily-aws-bill-isnt-the-scandal-you-think-it-is/) points out, that size of commitment may be risky for a company hosting "lifted and shifted" VMs where compute costs come at a premium, but Figma's technical stack is deeply ingrained in AWS ecosystem already. Once you are far enough along the adoption curve of a particular cloud provider, it leaves a lot of money on the table if you **do not** make commitments. This could be explicit commitments via Savings Plans/reserved capacity, or implicit ones like moving ["glue code" to the infrastructure layer](https://serverlessland.com/content/guides/refactoring-serverless/introduction). The latter can save many Engineering hours, in return for greater dependence on a specific provider's primitives.

{{< callout type="note" title="Serverless Refactoring ☁️" collapse="false" >}}
One of my go-to talks from recent AWS re:Invent conferences is about _Serverless Refactoring_, which blurs the line between application and infrastructure concerns.

> _**TL;DW (Too Long; Didn't Watch)**_  
> _The next time you find yourself writing code to integrate two pieces of infrastructure, it's worth questioning if a different primitive exists instead._

{{< youtube id="bIu8XZZROw4" start=0 loading="lazy" autoplay=false >}}
{{< /callout >}}

### Summary 🧵
This post tried to cover a lot of ground. Here are my main takeaways:

1. 💸 Costs are a **shared responsibility** across development teams, like availability, with a more immediate ROI. Delegating responsibility to a single platform/FinOps team leaves many optimisations off the table, and may elongate projects.
1. 💻 Developer tooling and AI can **shift a lot of effort left**. Producing code will become less of bottleneck as more of this responsibility is delegated to machines. However, understanding how that code impacts system reliability and costs will only matter more over time. 
1. 🔐 _"Lock-in"_ and cloud commitments get a bad reputation, because it's harder to quantify the **opportunity cost** of not going "all-in" on providers' offerings.

As always, context matters, so the next time we see a headline about an organization's hosting costs, it's worthwhile treating it with the nuance it deserves, rather than being outraged by the headlines.

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).

In future posts, I may dive into some neat cost management measures I have seen in the wild. In the meantime, here are a few podcast recommendations:
- 🎧 [Screaming in the Cloud (Last Week in AWS)](https://www.lastweekinaws.com/podcast/)
- 🎧 [Cloud Masters (DoIt)](https://www.doit.com/podcasts/cloud-masters/)
