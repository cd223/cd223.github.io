---
title: "Call My Agent 🤖"
date: 2025-06-24
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

> _The title is a terrible pun on a French [TV show](https://en.wikipedia.org/wiki/Call_My_Agent!)..._ 📺

### My Two Cents 🪙
Like most waves of change and hype in the tech industry, the GenAI topic (coined as "[Software 3.0](https://www.nextbigfuture.com/2025/06/software-3-0-by-karpathy.html)") causes [divisiveness](https://www.elastic.co/blog/generative-ai-hype-myths-it-leaders) and [scepticism](https://www.mcsweeneys.net/articles/a-company-reminder-for-everyone-to-talk-nicely-about-the-giant-plagiarism-machine). A lot of this reaction is justified. 
Not long ago, we had a hype cycle around Blockchain and Cryptocurrency, which did not cause the revolution it promised. Blockchain often felt like a solution in search of a problem. GenAI has a plethora of tangible [use cases](https://aws.amazon.com/ai/generative-ai/use-cases/), but needs to answer difficult questions in many areas before it can allay concerns. 
Namely, the ethical, socioeconomic, environmental and security impact of adopting this technology at scale.

We could place a lot of these hype cycles along different points of the [Gartner Hype Cycle](https://en.wikipedia.org/wiki/Gartner_hype_cycle). 
Blockchain and Cryptocurrency has found its niche after the hype has [calmed down](https://www.cio.com/article/3838169/rip-finally-to-the-blockchain-hype.html). GenAI could [follow a similar path](https://techxplore.com/news/2025-06-ai-hype-blockchain-frenzy-dies.html) once the dust settles. 

To avoid bloat, this post purely focuses on the _engineering discipline_ that the book introduces, rather than the impact of this technology or my personal use of it for [productivity](https://newsletter.pragmaticengineer.com/p/two-years-of-using-ai). I will save those for a future post.
Criticism, if justified, needs to come from a place of education.

{{< imgresize src="gartner-hype-cycle.jpg" width="900" height="500" alt="Gartner Hype Cycle" >}}
_*Image credit: [Gartner](https://www.gartner.com/en/insights/gartner-hype-cycle)*_

### The Book 📖️
I first learned about this book from a [Tweet](https://x.com/GergelyOrosz/status/1926342778012786853) ("X"?) by [Gergely Orosz](https://www.pragmaticengineer.com/). Out of curiosity, I downloaded the e-book and Sam kindly reached out to send across a physical copy. 

It is a short read (1-2 hours) for technical readers that introduces _a lot_ of breadcrumbs for people to go away and read more on. This means that by the end, you are not an expert, but carry a lot of the terms you need to do research and have conversations about the topic. It uses a top-down approach, building on top of LLMs, not explaining their foundations. 
I am _not_ being sponsored to write this - I just think it is great organic marketing and enjoy shorter reads.

[Mastra](https://mastra.ai/) is a company building a framework for building AI Agents and orchestrating them with workflows. Sam is a co-founder of the [Gatsby](https://www.gatsbyjs.com/docs) web framework, and is taking an interesting bet on the TypeScript community as the place to start, with some early adoption [examples](https://www.stackone.com/blog/a-new-direction-for-tool-orchestration).

The book is available in [virtual](https://mastra.ai/book) or [physical](https://www.amazon.co.uk/Principles-Building-Agents-Sam-Bhagwat/dp/B0DYH5GHDD/ref=sr_1_1) form.

In the next few sections, I'll go over some takeaways and my open questions.

{{< imgresize src="principles-ai-agents.jpg" width="800" height="550" alt="Principles of Building AI Agents" >}}
_*With thanks to [Sam Bhagwat](https://www.linkedin.com/in/sambhagwat/)*_

### Jargon Busting 🧑‍🏫
The book introduces a lot of terminology. A true test of my understanding is whether I can now explain these concepts having read the book, which is what this section tries to achieve. 

> _**Disclaimer ⚠️**: I did have some background knowledge before reading this book, but not much. Academic readers might cringe at my attempt._

| Term                | Definition                                                                                                                                                                                                                                                                                             | Example               |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| **LLM**             | A probabilistic model trained on natural language which given a training corpus and some input, will predict the most likely output using matrix multiplication.                                                                                                                                       | GPT-o1, Gemini, Llama |
| **Prompt**          | Input to an LLM (commonly textual). These can be _system_ or _user_ level, which alters the scope (e.g. chat-level or individual query respectively).                                                                                                                                                  | ...                   |
| **Token**           | A raw chunk of text, taken from a larger document or textual input.                                                                                                                                                                                                                                    | ...                   |
| **Vector**          | A transformed `N`-dimensional data structure representing a token. `N` is typically ~1536.                                                                                                                                                                                                             | ...                   |
| **Context Window**  | The number of text chunks (tokens in the input and output) which the LLM can handle at any one time when processing a query.                                                                                                                                                                           | ...                   |
| **Agent**           | A                                                                                                                                                                                                                                                                                                      | ...                   |
| **Memory**          | ...                                                                                                                                                                                                                                                                                                    | ...                   |
| **Tool**            | A method for the agent to access data e.g. a database, web resource or even another Agent.                                                                                                                                                                                                             | ...                   |
| **MCP**             | A protocol (like HTTP) defined by [Anthropic](https://www.anthropic.com/news/model-context-protocol) which stipulates how an agent should retrieve information from a third-party source. An MCP Server (hosted locally or remotely) declares its prompts, tools and resources for MCP clients to use. | ...                   |
| **A2A**             | A protocol defined by [Google](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/) which stipulates how an Agent should communicate with another Agent.                                                                                                                     | ...                   |
| **RAG**             | A method for enhancing the information available to an LLM.                                                                                                                                                                                                                                            | ...                   |
| **Vector Database** | A data store specialised in storage and retrieval of `N`-dimensional vectors.                                                                                                                                                                                                                          | pg_vector, Pinecone   |
| **Guardrail**       | ...                                                                                                                                                                                                                                                                                                    | ...                   |
| **Eval**            | Methods for evaluating the effectiveness and accuracy of an Agent.                                                                                                                                                                                                                                     | ...                   |

If you are a visual learner, then I am a big fan of the [ByteByteGo](https://www.youtube.com/@ByteByteGo) YouTube channel, which has a short video summarizing the concept of an agent.
{{< youtube id="eHEHE2fpnWQ" start=0 loading="lazy" autoplay=false >}}

### Takeaways 📝
- Non-determinism

### Open Questions ❓
- Measuring what matters (https://techinformed.com/is-klarnas-scale-back-on-ai-a-turning-point-for-cx/)
- https://www.infoq.com/news/2025/06/openai-o3-pro/
- Abstraction comes at a cost
- Assistance, not autonomy
- Consensus on protocols, registries (not like CVEs / IANA / IETF)
- Transparency: Confidence scores
- Selection of tools
- o11y
- Language / regional differences
- Security (Legal trifecta) https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/
- Do you need an LLM (https://arxiv.org/pdf/2506.02153)
- https://stratechery.com/2025/checking-in-on-ai-and-the-big-five
- https://surma.dev/things/langgraph

### Summary 🧵
As you might expect, free courses are available on the topic by the likes of [Mastra](https://mastra.ai/course) and [Hugging Face](https://huggingface.co/learn/agents-course/unit0/introduction).
- Future posts may dive into the topics mentioned in the intro, or practical examples of hosted systems.

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
