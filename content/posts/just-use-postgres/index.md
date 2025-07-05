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

A common adage for any developer choosing a database technology is _"just use Postgres"_. Whilst this advice is well-intended, it needs revisiting in 2025 in light of recent innovations. In this post, we dissect what it means today, at a time when Postgres providers are behaving like JavaScript frameworks of the 2010s, with a new one to consider every 6 months.

{{< callout type="note" title="" >}}
This means that once someone has settled on Postgres as they have been told, there is an _entirely new decision tree_ they need to follow before they can launch their system. 🌳
{{< /callout >}}

{{< imgresize src="elephant-sanctuary.jpg" width="700" height="500" alt="Types of Multi Agent architectures" >}}
_A good excuse to reminisce on my March trip to Krabi, Thailand_ 🇹🇭

### Postgres Renaissance 🎨
The saying [_"just use Postgres"_](https://mccue.dev/pages/8-16-24-just-use-postgres) is deliberately simplistic, intended to reduce analysis paralysis at a critical point in a system's lifetime. Postgres is the "boring" choice because it has been battle-tested in production for decades by thousands of companies. Being open-source and extensible, it has a [thriving community](). There is very little to gain by choosing a less-proven technology, or one with restrictive licensing or a separate cost model. It closes the fewest number of doors when a project's uncertainty is at its highest. 

Recent Postgres versions and extensions (e.g [`pgvector`]()) have introduced native support for JSON/vector data, which makes it even harder to justify starting with a specialised store when you can have a stack that supports both. Extensions like [`pg_duckdb`]() support column-oriented analytical workloads in a technology that was intended for transactional, row storage. [Many](https://www.tigerdata.com/blog/how-to-collapse-your-stack-using-postgresql-for-everything) [articles](https://dev.to/shayy/postgres-is-too-good-and-why-thats-actually-a-problem-4imc) exist on the versatility of Postgres. Some even go as far as stating you can host a full REST API with [PostgREST]() (though I haven't come across Production examples).

In the recent times, database technologies derived from Postgres have exploded in number and seen rapid success. In the last few months alone:
- [Databricks acquired Neon](), a serverless Postgres provider.
- [Snowflake acquired Crunchy Data](), a hosted Postgres provider.
- [AWS Aurora DSQL]() was released.
- PlanetScale expanded on its MySQL foundation, to offer a [Postgres alternative]().

Below is a _non-exhaustive_ list of technologies derived from Postgres.

{{< callout type="note" title="Notable Systems (Click to expand/collapse)" collapse="true" >}}

| Technology               | Description |
|--------------------------|-------------|
| **[Neon]()**             | The         |
| **[Nile]()**             | The         |
| **[Supabase]()**             | The         |
| **[TimescaleDB]()**          | The         |
| **[TigerData]()**            | The         |
| **[CockroachDB]()**          | The         |
| **[PlanetScale Postgres]()** | The         |
| **[Prisma]()**               | The         |
| **[YugabyteDB]()**           | The         |
| **[Crunchy Data]()**         | The         |
| **[Heroku]()**               | The         |
| **[AWS Aurora]()**           | The         |
| **[Google Cloud SQL]()**     | The         |
| **[Azure Database]()**       | The         |

{{< /callout >}}

{{< imgresize src="postgres-everything.png" width="475" height="350" alt="Types of Multi Agent architectures" >}}
_Image credit: [TigerData](https://www.tigerdata.com/blog/how-to-collapse-your-stack-using-postgresql-for-everything)_

### Cautionary Tales ⚠️
This decision to adopt Postgres over other relational database systems doesn't always go to plan. Uber famously [switched](https://www.uber.com/en-GB/blog/postgres-to-mysql-migration/) to MySQL after facing slowness during writes. Other systems have [faced issues](https://www.cs.cmu.edu/~pavlo/blog/2023/04/the-part-of-postgresql-we-hate-the-most.html) such as table bloat due to the MVCC (and vacuum) model Postgres adopts in favour of locks.
This is a good opportunity to preach the lessons from [_Designing Data Intensive Applications_](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/). Without understanding the underlying storage and retrieval technology these databases rely on, you are likely to face surprises in Production.

### Recent Trends 🔨
Bare-metal Postgres is monolithic, combining storage and compute. It is also process-oriented (rather than [thread-based]()). This means bottlenecks

- Compute vs Storage Separation: [Serverless](https://jack-vanlightly.com/analyses/2023/11/15/neon-serverless-postgresql-asds-chapter-3), Branching, Fast Cloning/Backups, Decomposing Systems
- MVCC - vacuums, Monolithic, Index behaviour
- Specialisms: Analytics, time series, AI (vector)
- ORMs

I recommend [Hussein Nasser](https://www.youtube.com/@hnasr)'s YouTube channel, which has a short video explaining the Postgres internals.
{{< youtube id="Q56kljmIN14" start=0 loading="lazy" autoplay=false >}}

### Decision Points ⚖️

#### Query Patterns ❓
- Compatability - [wire protocol](https://www.yugabyte.com/postgresql/compare-postgresql-compatibility/)
- Service limitations
- OLAP / HTAP
- NoSQL / SQL
- Read / write heavy (sharding / replicas), MVCC model, differences between MySQL and Postgres
- Spiky = Serverless, Steady = Provisioned

#### Risk Appetite 🎲
- Management - self-hosting
- Security (encryption)
- Full/root data access
- (e.g. Cloud-agnostic, new company)

#### Distributed Workloads 🌍
- Read replicas / global endpoints

#### Third-party Technology 🛠
- Extensions / integrations

#### Multi-Tenant Workloads 🏘
- What is your model? (Siloed, pooled)?

#### Downtime 🔥
- (e.g. during scaling events / upgrades)

#### Budget 💰
...

#### Benchmarks 🌍
...

### Starting Point 📍
- Self-hosted vs hosted
- Benchmark
- Upgrade Plan

### Summary 🧵
In this post, we 

I may blog on some of the [idiosyncrasies](https://www.avestura.dev/blog/explaining-the-postgres-meme).

[Postgres FM](https://postgres.fm/)

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
