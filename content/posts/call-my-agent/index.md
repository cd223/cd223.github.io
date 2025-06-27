---
title: "Call My Agent 🤖"
date: 2025-06-27
tags: ["artificial intelligence", "book"]
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

This is the first "book club" post on this blog. This week, we take a brief step into the world of GenAI Agents, having read "_[Principles of Building AI Agents](https://mastra.ai/book)_" by [Sam Bhagwat](https://www.linkedin.com/in/sambhagwat/). 📚 

The need for a second edition just months after release highlights how fast this space is moving.

> _The title is a terrible pun on a French [TV show](https://en.wikipedia.org/wiki/Call_My_Agent!)..._ 📺

### My Two Cents 🪙
Like most waves of change and hype in the tech industry, the GenAI topic (coined as "[Software 3.0](https://www.nextbigfuture.com/2025/06/software-3-0-by-karpathy.html)") causes [divisiveness](https://www.elastic.co/blog/generative-ai-hype-myths-it-leaders) and [scepticism](https://www.mcsweeneys.net/articles/a-company-reminder-for-everyone-to-talk-nicely-about-the-giant-plagiarism-machine). A lot of this reaction is justified. 
AI is not a new field - it has been around for decades. However, the release of ChatGPT in November 2022 created a fresh wave of noise around Generative AI. 

Not long ago, we had a hype cycle around Blockchain and Cryptocurrency, which did not cause the revolution it promised. Blockchain often felt like a solution in search of a problem. GenAI has a plethora of tangible [use cases](https://aws.amazon.com/ai/generative-ai/use-cases/), but needs to answer difficult questions in many areas before it can allay concerns. 
Namely surrounding the ethical, legal, socioeconomic, environmental and security impact of adopting this technology at scale. This is why the marketing can sometimes feel premature.

We could place a lot of these hype cycles along different points of the [Gartner Hype Cycle](https://en.wikipedia.org/wiki/Gartner_hype_cycle). 
Blockchain and Cryptocurrency has found its niche after the hype has [calmed down](https://www.cio.com/article/3838169/rip-finally-to-the-blockchain-hype.html). GenAI could [follow a similar path](https://techxplore.com/news/2025-06-ai-hype-blockchain-frenzy-dies.html) once the dust settles. 

To avoid bloat, this post purely focuses on the _engineering discipline_ that the book introduces, rather than the impact of this technology or my personal use of it for [productivity](https://newsletter.pragmaticengineer.com/p/two-years-of-using-ai). I will save those for a future post.
Criticism, if justified, needs to come from a place of education.

{{< imgresize src="gartner-hype-cycle.jpg" width="900" height="500" alt="Gartner Hype Cycle" >}}
_*Image credit: [Gartner](https://www.gartner.com/en/insights/gartner-hype-cycle)*_

### The Book 📖️
I first learned about this book from a [Tweet](https://x.com/GergelyOrosz/status/1926342778012786853) ("X"?) by [Gergely Orosz](https://www.pragmaticengineer.com/). Out of curiosity, I downloaded the e-book and Sam kindly reached out to send across a physical copy. 

It is a short read (2-3 hours) for technical readers that introduces _a lot_ of breadcrumbs for people to go away and read more on. This means that by the end, you are not an expert, but carry a lot of the terms you need to do research and have conversations about the topic. It uses a top-down approach, building on top of LLMs, not explaining their foundations. 
I am _not_ being sponsored to write this - I just think it is great organic marketing and enjoy shorter reads.

[Mastra](https://mastra.ai/) is a company building a framework for building AI Agents and orchestrating them with workflows. Sam is a co-founder of the [Gatsby](https://www.gatsbyjs.com/docs) web framework, and is taking an interesting bet on the TypeScript community as the place to start, with some early adoption [examples](https://www.stackone.com/blog/a-new-direction-for-tool-orchestration).

The book is available in [virtual (free)](https://mastra.ai/book) or [physical (paid)](https://www.amazon.co.uk/Principles-Building-Agents-Sam-Bhagwat/dp/B0DYH5GHDD/ref=sr_1_1) mediums.

In the next few sections, I'll go over some takeaways and my open questions.

{{< imgresize src="principles-ai-agents.jpg" width="800" height="550" alt="Principles of Building AI Agents" >}}
_*With thanks to [Sam Bhagwat](https://www.linkedin.com/in/sambhagwat/)*_

### Jargon Busting 🧑‍🏫
The book introduces a lot of terminology. A true test of my understanding is whether I can now explain these concepts, which is what this section tries to achieve. Feel free to skip this section if you already have a good understanding.

> _**Disclaimer ⚠️**: I did have some background knowledge before reading this book, but not much. Academic readers might cringe at my attempt._

| Term                   | Definition                                                                                                                                                                                                                                                                                                    | Example                                                                                           |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **LLM**                | Large Language Model. Probabilistic model trained on natural language which, when given a training corpus and input, will predict the most likely output using mathematical operations (e.g., matrix multiplication). These can be _hosted_ or _open source_.                                                 | GPT-o1, Gemini, Llama                                                                             |
| **Prompt**             | Input to an LLM (commonly textual). These can be _system_ or _user_ level, which alters the scope (e.g. chat-level or individual query respectively). Prompt engineering is the practice of tailoring prompts to improve outputs.                                                                             | `"ChatGPT is cool!"`                                                                              |
| **Token**              | Single raw chunk of text, taken from a larger document or textual input.                                                                                                                                                                                                                                      | `["Chat", "G", "PT", " is", " cool", "!"]`                                                        |
| **Embedding / Vector** | Transformed `N`-dimensional data structure representing the _semantic meaning_ of a token or document. `N` is typically ~1536. This structure is used for _similarity searches_ in `N`-dimensional space, which gives a numerical reading on how relevant the stored content is to the input prompt.          | `[0.12, ..., 0.95]`                                                                               |
| **Context Window**     | The number of text chunks (tokens in the input and output) which the LLM can handle at any one time when processing a query.                                                                                                                                                                                  | GPT-4 = ~128k tokens.                                                                             |
| **Agent**              | A long-lived process that uses LLMs to perform tasks. They may be allocated memory, invoke tools, access resources, and maintain context over time.                                                                                                                                                           | AI assistant that books meetings.                                                                 |
| **MCP**                | Model Context Protocol. Defined by [Anthropic](https://www.anthropic.com/news/model-context-protocol) which stipulates how an agent should retrieve information from a third-party source. An MCP Server (hosted locally or remotely) declares its _prompts_, _tools_ and _resources_ for MCP clients to use. | Agent that is given instructions for connecting to a database to find weather information.        |
| **Tool (MCP)**         | Method for the agent to perform a task e.g. a web resource lookup, or calling another Agent.                                                                                                                                                                                                                  | `fetch_weather(city)`                                                                             |
| **Resource (MCP)**     | Data source used by the agent when performing tasks e.g. a database.                                                                                                                                                                                                                                          | `city_db`                                                                                         |
| **Prompt (MCP)**       | Templated instructions for the agent to perform a task e.g. details needed to call a tool or read from a resource.                                                                                                                                                                                            | `"Search {query} in {resource}"`                                                                  |
| **A2A**                | Agent To Agent Protocol. Defined by [Google](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/) which stipulates how an Agent should communicate with another Agent, given they are likely built independently.                                                                   | `Agent1` asking `Agent2` to extract data.                                                         |
| **RAG**                | Retrieval Augmented Generation. A method for enhancing the information available to an LLM by performing on-demand searches against a vector database to enrich a prompt.                                                                                                                                     | Retrieval of FAQs before answering queries.                                                       |
| **Vector Database**    | A data store specialised in storage and retrieval of `N`-dimensional vectors.                                                                                                                                                                                                                                 | [pgvector](https://github.com/pgvector/pgvector/), [Pinecone](https://www.pinecone.io/)           |
| **Agentic Workflow**   | An emerging practice which defines the tasks agents perform as steps in a deterministic orchestration workflow - as a set of steps or graph.                                                                                                                                                                  | `Fetch doc → summarise → email`                                                                   |
| **Guardrail**          | Measures which act as additional context in the prompts given to LLMs to minimise the risk of them producing insecure or malicious output. More of a _guidance_ mechanism than a watertight measure.                                                                                                          | Requesting that PII is not returned.                                                              |
| **Eval**               | Methods for evaluating the effectiveness and accuracy of an Agent.                                                                                                                                                                                                                                            | [OpenAI Evals](https://cookbook.openai.com/examples/evaluation/getting_started_with_openai_evals) |

If you are a visual learner, then I am a fan of the [ByteByteGo](https://www.youtube.com/@ByteByteGo) YouTube channel, which has a short video explaining some of these concepts.
{{< youtube id="eHEHE2fpnWQ" start=0 loading="lazy" autoplay=false >}}

### Key Snippets ✂️
Despite being a short read, the book is full of advice from practical experience. This section summarises the main lessons.

#### Non-Determinism 🎲
Embrace not knowing the answer. The book makes it very clear from the start that adopting this technology means being comfortable with non-determinism. A lot of Software Engineering is made easier by ensuring our programs exhibit repeatable, deterministic behaviour, so this introduces new challenges. In this field, the fundamental building blocks are _probabilistic_. The same input may generate infinite variations of output. Going back to the "[Software 3.0](https://www.nextbigfuture.com/2025/06/software-3-0-by-karpathy.html)" concept, even "2.0" (ML and Neural Nets) can be made deterministic (by fixing weights and parameters), so this marks a complete departure.

#### Size vs Cost vs Performance 💰
Start simple, then optimise. A trade-off is required between cost, performance and accuracy. Cheaper models will produce fast, less accurate responses, which might be enough for some use cases. The book advises starting with a costlier model whilst volumes are low, then optimising. One should start by exhausting the LLM's context window, before building workflows or RAG pipelines.

There are clever UX techniques one might employ to make it look like the agent is doing useful work, showing its workings and reasoning. A few solutions mentioned stream their responses via web-sockets, making use of tools like [ElectricSQL](https://electric-sql.com/). 

As for the choice between _hosted_ versus _open source_ models (e.g., [Claude](https://www.anthropic.com/claude) vs [DeepSeek](https://deep-seek.chat/)), it is a natural reaction to want to see the inner workings of these models. In reality, I am reminded of the choice when people adopt cloud computing. A _hosted_ model provides much less of the hassle in getting up and running with this technology, which doesn't differentiate a business. On the surface there is not as much vendor lock-in (_yet_) compared to public cloud, but that may change. Each model has their own strengths, meaning that once a production system is tuned, it is hard to justify the effort to migrate. Some systems adopt a hybrid of models and [route prompts](https://arxiv.org/html/2502.00409v1) based on rules (which is the equivalent of going "multi-cloud" in my analogy).  

#### Prompt Techniques 🔁 
Structure matters. In most models there is a meaningful difference in output between "_Zero-Shot_" and "[_Chain Of Thought_](https://www.promptingguide.ai/techniques/cot)" prompting. Some models are specifically designed for [everything-upfront](https://www.latent.space/p/o1-skill-issue) interactions, rather than a chat. Much like a human would work better solving a problem if it had some examples, hints, and a schema (e.g., XML, JSON) to work with, so do LLMs.   

The book also recommends the "_seed crystal_" approach, which involves asking an LLM how it should be prompted to do a task. Think of it like "meta-prompting".

#### Infrastructure 🛠️ 
Agents are stateful and resource intensive. This constrains the infrastructure that companies can use to host them. Most serverless infrastructure will buckle under their resource usage, or time-out within 15 minutes. With the move to represent agents as workflows (e.g. [Mastra](https://mastra.ai/), [LangGraph](https://www.langchain.com/langgraph)), I do wonder if there is space to move orchestration into the infrastructure, much like we have seen with solutions like AWS [Step Functions](https://aws.amazon.com/step-functions/), which replaces orchestration in code. If a breakthrough were to happen in this space, it would change the cost-profiles of this technology, linking it more dynamically to usage which is much more attractive for firms with limited budgets (e.g. start-ups).

#### Observability and Testing 🔎
Selection and usage of tools - 

### My Takeaways ✍️
Having read the book and surrounding articles for this blog, I have some takeaways which I would adopt if I was to build a "production" agentic system. I am not an expert, so I would love to hear differing views or stories from real systems. 

1. **Value-First 📐**
    - Measuring what matters (https://techinformed.com/is-klarnas-scale-back-on-ai-a-turning-point-for-cx/)
    - https://www.infoq.com/news/2025/06/openai-o3-pro/

1. **Human-First 🧍‍♂️** 
    - Abstraction comes at a cost
    - https://surma.dev/things/langgraph
    - Assistance, not autonomy - https://incident.io/building-with-ai
    - Circuit breaker
    - o11y
    - Language / regional differences

1. **Security-First 🔐**
    - Security (Legal trifecta) https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/
    - Authentication
    - Bot detection
    - Consensus on protocols, registries (not like CVEs / IANA / IETF)
    - https://www-finos-org.cdn.ampproject.org/c/s/www.finos.org/blog/finos-ai-governance-framework-v1.0-turning-drafts-into-deployable-guardrails
    - Confidence scores
    - Selection of tools

1. **Determinism-First 🧠**
    - ...

https://stratechery.com/2025/checking-in-on-ai-and-the-big-five

{{< imgresize src="standards.png" width="900" height="500" alt="XKCD Comic on Competing Standards" >}}
_*Image credit: [XKCD](https://xkcd.com/927/)*_

### Summary 🧵
In this post, we reviewed the terminology and topics discussed in "_[Principles of Building AI Agents](https://mastra.ai/book)_" by [Sam Bhagwat](https://www.linkedin.com/in/sambhagwat/). If this blog sounded interesting, I'd recommend downloading or buying the book directly, and following their work.

It is my first meaningful deep-dive into the engineering practices behind this technology. This space is clearly changing rapidly. If we look back on this post in 1-2 years, I would be interested to see what changes. Perhaps the majority of future use cases [won't even need an LLM](https://arxiv.org/pdf/2506.02153)!

As for next steps, there are some free courses on the topic by the likes of [Mastra](https://mastra.ai/course) and [Hugging Face](https://huggingface.co/learn/agents-course/unit0/introduction), which I may dive into. If you have got to the end of this post and have further recommendations, please do get in touch.

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
