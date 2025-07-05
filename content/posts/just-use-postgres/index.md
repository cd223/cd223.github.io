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

A common adage for any developer choosing a database technology is _"just use Postgres"_. Whilst this advice is well-intended, it needs revisiting in 2025. With all the recent innovations and acquisitions, Postgres providers are behaving like JavaScript frameworks of the 2010s (with a new one to consider every 6 months).

This means that once someone has settled on using Postgres instead of other databases, there is an _entirely new decision tree_ they need to follow before they can launch their system. 🌳

{{< callout type="note" title="" >}}
**TL;DR**: The answer to _"Which one do I choose?"_ is always _"It depends"_, but this post signposts exactly what those deciding factors are. ⚖️ 
{{< /callout >}}

{{< imgresize src="elephant-sanctuary.jpg" width="700" height="500" alt="Thailand elephant sanctuary" >}}
_Postgres uses an elephant as its mascot. This means I have a good excuse to reminisce on my March 2025 trip to Thailand_ 🇹🇭

### Postgres Renaissance 🎨
The saying [_"just use Postgres"_](https://mccue.dev/pages/8-16-24-just-use-postgres) is deliberately simplistic. It is intended to reduce analysis paralysis at a critical point in a system's lifetime. Postgres is the "boring" choice because it has been battle-tested in production for decades by thousands of companies. Being [open-source](https://github.com/postgres/postgres) and [extensible](https://medium.com/agedb/introduction-to-postgresql-extensions-770e37f3fae1), it has a [thriving community](https://www.postgresql.org/community/). There is very little to gain by choosing a less-proven technology. Or one with restrictive licensing. Or adopting several solutions with their own cost models. It closes the fewest number of doors when a project's uncertainty is at its highest. 

Recent Postgres versions and extensions (e.g [`pgvector`](https://github.com/pgvector/pgvector)) have introduced and significantly improved support for vector/JSON data, which makes it even harder to justify starting with a specialised store. Extensions like [`pg_duckdb`](https://github.com/duckdb/pg_duckdb) support column-oriented, analytical workloads inside a row-oriented, transactional system. [Many](https://www.tigerdata.com/blog/how-to-collapse-your-stack-using-postgresql-for-everything) [articles](https://dev.to/shayy/postgres-is-too-good-and-why-thats-actually-a-problem-4imc) exist on the versatility of Postgres. Some even go as far as stating you can host a full REST API with [PostgREST](https://docs.postgrest.org/en/v13/) (though I haven't come across Production examples of this).

In the recent times, database technologies derived from Postgres have exploded in number and seen rapid success. In the last few months alone:
- 🤑 [Databricks acquired Neon](https://www.databricks.com/company/newsroom/press-releases/databricks-agrees-acquire-neon-help-developers-deliver-ai-systems), a serverless Postgres provider.
- 🤑 [Snowflake acquired Crunchy Data](https://www.crunchydata.com/blog/crunchy-data-joins-snowflake), a hosted Postgres provider.
- 🎉 [AWS Aurora DSQL](https://aws.amazon.com/blogs/aws/amazon-aurora-dsql-is-now-generally-available/) was released.
- 🎉 PlanetScale expanded on its MySQL foundation, to offer a [Postgres alternative](https://planetscale.com/blog/planetscale-for-postgres).

Below is a _non-exhaustive_ list of recent technologies derived from Postgres, and their offerings.

{{< callout type="note" title="Notable systems (Click to expand/collapse)" collapse="true" >}}

| Technology                                                                                                  | Description                                                                                                                                                         |
|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **[Neon](https://neon.com/)**                                                                               | Serverless, fully-managed instances with autoscaling and branching.                                                                                                 |
| **[Nile](https://www.thenile.dev/)**                                                                        | Serverless, fully-managed instances for multi-tenant applications (e.g. B2B SaaS).                                                                                  |
| **[Supabase](https://supabase.com/database)**                                                               | Open-source Firebase alternative - either managed or self-hosted.                                                                                                   |
| **[TigerData (TimescaleDB)](https://www.tigerdata.com/)**                                                   | Optimized for time-series and real-time analytics - either managed or self-hosted.                                                                                  |
| **[CockroachDB](https://www.cockroachlabs.com/)**                                                           | Distributed SQL with Postgres compatibility - either managed or self-hosted.                                                                                        |
| **[PlanetScale Postgres](https://planetscale.com/blog/planetscale-for-postgres)**                           | Managed instances, emphasizing performance and scalability based on [NVMe SSDs](https://planetscale.com/blog/announcing-metal).                                     |
| **[Prisma](https://www.prisma.io/postgres)**                                                                | Serverless, fully-managed instances with a TypeScript [Object Relational Mapper (ORM)](https://www.prisma.io/docs).                                                 |
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
Choosing Postgres over other relational databases doesn't always go to plan. Uber famously [switched](https://www.uber.com/en-GB/blog/postgres-to-mysql-migration/) to MySQL after facing slowness during writes, favouring the way MySQL handles index updates. Other systems have [faced issues](https://www.cs.cmu.edu/~pavlo/blog/2023/04/the-part-of-postgresql-we-hate-the-most.html) such as table bloat and transaction ID wraparound due to the MVCC model Postgres adopts, in favour of locks.
This is a good opportunity to preach the lessons from [_Designing Data Intensive Applications_](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/). Without understanding the underlying storage and retrieval technology these databases rely on, you are likely to face surprises in Production.

### Recent Trends 🔨
In this section we go over the main innovations that have emerged in recent years, which have caused the explosion in providers, each with their own unique offerings. As Postgres is open-source, it is possible to cherry-pick features and compromise on some fundamental aspects in order to unlock new behaviours.

#### Compute <> Storage Divide ➗
Postgres pre-dates the age of cloud and distributed systems. As such, it is monolithic (combining storage and compute on the same server) and process-oriented (rather than [thread-oriented](https://engineeringatscale.substack.com/p/will-postgresql-switch-to-a-thread)). To thrive in a cloud-native world, providers have decoupled storage and compute layers, which allows each layer to scale independently. This change enables [serverless](https://jack-vanlightly.com/analyses/2023/11/15/neon-serverless-postgresql-asds-chapter-3) systems like Neon and AWS Aurora Serverless. Use of durable block storage like S3 means lightweight VMs can run the Query Engine and hold minimal state, allowing horizontal scalability. Different systems embrace this to different extents. For example, Aurora Serverless v2 incurs a 15 second cold-start when [scaling up from zero](https://aws.amazon.com/blogs/database/introducing-scaling-to-0-capacity-with-amazon-aurora-serverless-v2/).

Besides scalability, the other by-products of standalone storage are [database branching](https://neon.com/docs/introduction/branching) and [fast backups](https://aws.amazon.com/blogs/aws/amazon-aurora-fast-database-cloning/) due to copy-on-write semantics. These are game-changing features that a traditional Postgres system cannot provide. 

#### Relaxing Isolation for Speed 🏎️
Postgres is flexible in supporting 4 levels of [transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) at session or transaction level. It turns out that if we constrain the level of isolation to nothing stronger than `Repeatable Read` (using something like Snapshot Isolation) rather than `Serializable`, we require far less consensus before transactions can commit or return data.     

In most applications, the key-set of data being read is far greater than the key-set of data being written, and reads outnumber writes by an order of magnitude. This realisation along with constraining isolation level to `Repeatable Read` is core to the [way AWS DSQL scales](https://brooker.co.za/blog/2024/12/17/occ-and-isolation.html). By constraining in one dimension, new technologies are unlocking scale that a traditional setup could not match.

#### New Data Primitives 📊️
Being a general purpose and extensible database, some providers have imposed an opinionated abstraction on top of core Postgres. For example, TigerData introduces `hypertables` to model time-series data, which would otherwise require boilerplate database partitioning and scheduled pruning jobs through `pg_partman` and `pg_cron`.  

AI companies make use of vector stores (through `pgvector` and HNSW indexes) to build RAG (Retrieval Augmented Generation) pipelines. The recent Databricks and Snowflake acquisitions show that engineers increasingly value an "all-in-one" platform rather than a standalone OLAP solution.

{{< callout type="note" title="" >}}
If you are new to Postgres, I recommend [Hussein Nasser](https://www.youtube.com/@hnasr)'s YouTube channel, which has a short video explaining the Postgres internals.
{{< /callout >}}
{{< youtube id="Q56kljmIN14" start=0 loading="lazy" autoplay=false >}}

### Decision Points ⚖️
This section covers the questions I would consider when choosing a new Postgres provider.  

#### Query Patterns ❓
- OLAP / HTAP
- NoSQL / SQL
- Read / write heavy (sharding / replicas), MVCC model, differences between MySQL and Postgres
- Spiky = Serverless, Steady = Provisioned

#### Compatibility 💘
- Service limitations - Figma - sharding
- Compatability - [wire protocol](https://www.yugabyte.com/postgresql/compare-postgresql-compatibility/)

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
Having raised the important questions, it is clear that there is a lot to think about upfront. In the absence of any other information (and to avoid being overwhelmed!), I would adopt these principles.

1. **Stay close to the roots 🪾**: core Postgres as possible, for as long as possible.
1. **Benchmark 📐**:
1. **Know your options 🧠**: Sideways moves, upgrades, tenancy models, keep on top of trends.
1. **Avoid sprawl 🐙**: Early on, default to your existing Postgres instance before reaching for new platforms or databases.

There is no way to know the future, but with these principles in mind you will do better than most at adopting the right flavour of Postgres for your use case.

### Summary 🧵
In this post, we revisited the advice to _"just use Postgres"_ refreshed for 2025, in the broader context of acquisitions and recent product launches. It is an exciting time to be a developer working with Postgres, as the technology continues to evolve almost 40 years after its [inception at Berkeley](https://www.postgresql.org/docs/7.0/intro60.htm). 

By answering the questions above, you can have some idea of whether a provider offers the solution you need.

In future posts, I may dive into some of the [idiosyncrasies](https://www.avestura.dev/blog/explaining-the-postgres-meme) of Postgres or dive into systems like AWS' DSQL.  There are some great creators in the space which make it far easier to keep up to date in the meantime:
- [Postgres FM](https://postgres.fm/) 🎧
- [Scaling Postgres](https://www.scalingpostgres.com/) 🎧

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
