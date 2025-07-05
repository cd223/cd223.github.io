---
title: "Just Use Postgres 🐘"
date: 2025-07-05
tags: ["postgres", "databases"]
showToc: true
draft: true
TocOpen: false
hidemeta: false
comments: false
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

A common adage for any developer choosing a database technology is _"just use Postgres"_. Whilst this advice is well-intended, it needs revisiting in 2025 in light of recent innovations. In this post, we dissect what it means today, at a time when Postgres providers are behaving like JavaScript frameworks of the 2010s (a new one to consider every 6 months).

This means that once someone has settled on Postgres, there is an _entirely new decision tree_ they need to follow before they can launch their system. 🌳

{{< callout type="note" title="" >}}
**TL;DR**: The answer is always _"it depends"_, but this post signposts exactly what those deciding factors are. ⚖️ 
{{< /callout >}}

{{< imgresize src="elephant-sanctuary.jpg" width="700" height="500" alt="Thailand elephant sanctuary" >}}
_A good excuse to reminisce on my March 2025 trip to Krabi, Thailand_ 🇹🇭

### Postgres Renaissance 🎨
The saying [_"just use Postgres"_](https://mccue.dev/pages/8-16-24-just-use-postgres) is deliberately simplistic, intended to reduce analysis paralysis at a critical point in a system's lifetime. Postgres is the "boring" choice because it has been battle-tested in production for decades by thousands of companies. Being [open-source](https://github.com/postgres/postgres) and [extensible](https://medium.com/agedb/introduction-to-postgresql-extensions-770e37f3fae1), it has a [thriving community](https://www.postgresql.org/community/). There is very little to gain by choosing a less-proven technology, or one with restrictive licensing, or adopting several solutions with their own cost models. It closes the fewest number of doors when a project's uncertainty is at its highest. 

Recent Postgres versions and extensions (e.g [`pgvector`](https://github.com/pgvector/pgvector)) have introduced native support for JSON/vector data, which makes it even harder to justify starting with a specialised store when you can have a stack that supports both. Extensions like [`pg_duckdb`](https://github.com/duckdb/pg_duckdb) support column-oriented, analytical workloads inside a row-oriented, transactional system. [Many](https://www.tigerdata.com/blog/how-to-collapse-your-stack-using-postgresql-for-everything) [articles](https://dev.to/shayy/postgres-is-too-good-and-why-thats-actually-a-problem-4imc) exist on the versatility of Postgres. Some even go as far as stating you can host a full REST API with [PostgREST](https://docs.postgrest.org/en/v13/) (though I haven't come across Production examples).

In the recent times, database technologies derived from Postgres have exploded in number and seen rapid success. In the last few months alone:
- [Databricks acquired Neon](https://www.databricks.com/company/newsroom/press-releases/databricks-agrees-acquire-neon-help-developers-deliver-ai-systems), a serverless Postgres provider.
- [Snowflake acquired Crunchy Data](https://www.crunchydata.com/blog/crunchy-data-joins-snowflake), a hosted Postgres provider.
- [AWS Aurora DSQL](https://aws.amazon.com/blogs/aws/amazon-aurora-dsql-is-now-generally-available/) was released.
- PlanetScale expanded on its MySQL foundation, to offer a [Postgres alternative](https://planetscale.com/blog/planetscale-for-postgres).

Below is a _non-exhaustive_ list of technologies derived from Postgres.

{{< callout type="note" title="Notable systems (Click to expand/collapse)" collapse="true" >}}

| Technology                                                                                                  | Description                                                                                                                                                         |
|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **[Neon](https://neon.com/)**                                                                               | Serverless, fully-managed instances with autoscaling and branching.                                                                                                 |
| **[Nile](https://www.thenile.dev/)**                                                                        | Serverless, fully-managed instances for multi-tenant applications (e.g. B2B SaaS).                                                                                  |
| **[Supabase](https://supabase.com/database)**                                                               | Open-source Firebase alternative - either managed or self-hosted.                                                                                                   |
| **[TigerData (TimescaleDB)](https://www.tigerdata.com/)**                                                   | Optimized for time-series and real-time analytics - either managed or self-hosted.                                                                                  |
| **[CockroachDB](https://www.cockroachlabs.com/)**                                                           | Distributed SQL with Postgres compatibility - either managed or self-hosted.                                                                                        |
| **[PlanetScale Postgres](https://planetscale.com/blog/planetscale-for-postgres)**                           | Managed instances, emphasizing performance and scalability based on [NVMe SSDs](https://planetscale.com/blog/announcing-metal).                                     |
| **[Prisma](https://www.prisma.io/postgres)**                                                                | Opinionated, managed instances with a TypeScript [ORM](https://www.prisma.io/docs).                                                                                                           |
| **[YugabyteDB](https://www.yugabyte.com/)**                                                                 | Distributed SQL with Postgres compatibility - either managed or self-hosted. [Zero-downtime](https://www.yugabyte.com/blog/postgresql-upgrade-framework/) upgrades. |
| **[Crunchy Data](https://www.crunchydata.com/)**                                                            | Fully-compatible Postgres instances for Enterprise - either managed or self-hosted.                                                                                 |
| **[Heroku](https://www.heroku.com/postgres/)**                                                              | Managed instances integrated into the Heroku platform (PaaS).                                                                                                       |
| **AWS [RDS](https://aws.amazon.com/rds/) / [Aurora](https://aws.amazon.com/rds/aurora/)**                   | Managed instances integrated into the AWS platform - provisioned or serverless.                                                                                     |
| **Google [Cloud SQL](https://cloud.google.com/sql) / [AlloyDB](https://cloud.google.com/products/alloydb)** | Managed instances integrated into the Google Cloud platform - provisioned or serverless.                                                                            |
| **[Azure Database](https://azure.microsoft.com/en-us/products/postgresql)**                                 | Managed instances integrated into the Azure platform - provisioned or serverless.                                                                                   |

{{< /callout >}}

{{< imgresize src="postgres-everything.png" width="475" height="350" alt="Using Postgres for everything" >}}
_Image credit: [TigerData](https://www.tigerdata.com/blog/how-to-collapse-your-stack-using-postgresql-for-everything)_

### Cautionary Tales ⚠️
This decision to adopt Postgres over other relational database systems doesn't always go to plan. Uber famously [switched](https://www.uber.com/en-GB/blog/postgres-to-mysql-migration/) to MySQL after facing slowness during writes, favouring the way MySQL handles index updates. Other systems have [faced issues](https://www.cs.cmu.edu/~pavlo/blog/2023/04/the-part-of-postgresql-we-hate-the-most.html) such as table bloat due to the MVCC (and vacuum) model Postgres adopts in favour of locks.
This is a good opportunity to preach the lessons from [_Designing Data Intensive Applications_](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/). Without understanding the underlying storage and retrieval technology these databases rely on, you are likely to face surprises in Production.

### Recent Trends 🔨
In this section we go over the main innovations that have emerged in recent years, causing the explosion in providers with unique offerings. 

Bare-metal Postgres is monolithic, combining storage and compute. It is also process-oriented (rather than [thread-based](https://engineeringatscale.substack.com/p/will-postgresql-switch-to-a-thread)). This means bottlenecks

- Compute vs Storage Separation: [Serverless](https://jack-vanlightly.com/analyses/2023/11/15/neon-serverless-postgresql-asds-chapter-3), Branching, Fast Cloning/Backups, Decomposing Systems
- MVCC - vacuums, Monolithic, Index behaviour
- Specialisms: Analytics, time series, AI (vector)
- ORMs
- Analytics companies buying relational DBs
- Upgrades

I recommend [Hussein Nasser](https://www.youtube.com/@hnasr)'s YouTube channel, which has a short video explaining the Postgres internals.
{{< youtube id="Q56kljmIN14" start=0 loading="lazy" autoplay=false >}}

### Decision Points ⚖️
This section covers the factors I would consider when choosing a new Postgres provider.  

#### Query Patterns ❓
- Compatability - [wire protocol](https://www.yugabyte.com/postgresql/compare-postgresql-compatibility/)
- OLAP / HTAP
- NoSQL / SQL
- Read / write heavy (sharding / replicas), MVCC model, differences between MySQL and Postgres
- Spiky = Serverless, Steady = Provisioned

#### Compatibility 💘
- Service limitations

Figma - sharding

#### Risk Appetite 🎲
- Management - self-hosting
- Upgrade timelines - https://www.instantdb.com/essays/pg_upgrade, Lyft
- Security (encryption)
- Full/root data access
- (e.g. Cloud-agnostic, new company)

#### Budget 💰
...

#### Distributed Workloads 🌍
- Read replicas / global endpoints

#### Third-party Technology 🛠
- Extensions / integrations

#### Multi-Tenant Workloads 🏘
- What is your model? (Siloed, pooled)?

#### Downtime 🔥
- (e.g. during scaling events / upgrades)

#### Benchmarks 🌍
...

### Starting Point 📍
Having covered the decision points, it is clear that there is a lot to think about upfront. In the absence of other information and to avoid being overwhelmed, I would adopt these principles to start.

1. **Stay as close to the roots 🪾**: core Postgres as possible, for as long as possible.
1. **Benchmark 📐**:
1. **Know your options 🧠**: Sideways moves, upgrades, tenancy models, keep on top of trends.
1. **Avoid sprawl 🐙**: Early on, default to your existing Postgres instance before reaching for new platforms or databases.

There is no way to know the future, but with these principles in mind you will do better than most at adopting the right flavour of Postgres for your use case.

### Summary 🧵
In this post, we 

I may blog on some of the [idiosyncrasies](https://www.avestura.dev/blog/explaining-the-postgres-meme).

[Postgres FM](https://postgres.fm/)

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
