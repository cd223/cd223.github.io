---
title: "Taming Llamas, Parrots & Whales 🦙🦜🐳"
date: 2025-07-14
tags: ["artificial intelligence", "programming"]
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

I often find concepts easier to reason about with practical examples. Having written a [blog post](https://chrisdavies.dev/posts/call-my-agent/) about AI agents without getting hands-on, it still felt a bit abstract. This post dives deeper, fresh from completing the [Hugging Face](https://huggingface.co/learn/agents-course/unit0/introduction) and [Mastra](https://mastra.ai/course) courses, with all the _"WTF?"_ moments thrown in.  

> _A stark reminder of why they call them **Large** Language Models, and how many footguns exist if you're not careful._

{{< callout type="note" title="Quiz ❓" collapse="false" >}}
Only one of these is a Pokémon. Can you spot it?

_Ollama, LlamaIndex, LangChain, LangGraph, Klinklang, Mastra, Koog_.
{{< /callout >}}
{{< callout type="note" title="Answer 👀" collapse="true" >}}
Klinklang
{{< /callout >}}

### The course
- LLM transformer architecture - end-of-sequence token, a custom stop sequence, or a max-token limit.
- Attention mechanisms—positional importance, Beam search - multiple candidate sequences rather than
- [Chat templates](https://huggingface.co/docs/transformers/main/en/chat_templating) - system, user, assistant - tokens with entire conversation. e.g. ChatML
```python
messages = [
    {"role": "system", "content": "You are a math tutor."},
    {"role": "user", "content": "What is calculus?"},
    {"role": "assistant", "content": "Calculus is a branch of mathematics..."},
    {"role": "user", "content": "Can you give me an example?"},
]
```
- Base models vs instruct models
- Thought, Act, Observe cycle / ReAct (CoT) - (enclosed between <think> and </think> special tokens). 
- "Stop and parse" - JSON or code
- [smolagents](https://huggingface.co/blog/smolagents)
- https://huggingface.co/spaces/agents-course/First_agent_template/tree/main
- CodeAgent vs ToolCallingAgent - https://github.com/huggingface/smolagents/blob/main/src/smolagents/agents.py#L756-L761
- https://www.anthropic.com/engineering/building-effective-agents
- https://simonwillison.net/2025/Jul/6/supabase-mcp-lethal-trifecta/

Ollama: It downloads a model file that contains all the weights, architecture config, and tokenizer. This is often:

| Framework                           | Purpose                                                                                                                                                                                                                   |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Ollama**                          | A lightweight runtime for running large language models (like LLaMA, Mistral, etc.) locally with minimal setup. Designed for ease-of-use and local development, especially on Mac/Windows/Linux.                          |
| **smolagents**                      | A minimalist framework for building autonomous agents using small, composable tools. Emphasizes simplicity and avoids complex orchestration, often relying on plain Python scripts and clear control logic.               |
| **LangChain**                       | A popular Python framework to build apps with LLMs using chains, agents, memory, and tools. Widely adopted but criticized for complexity.                                                                                 |
| **LangGraph**                       | A graph-based extension of LangChain, designed to build stateful, multi-step AI workflows. Models tasks as nodes in a directed graph, supporting complex control flow and memory across steps.                            |
| **LlamaIndex (formerly GPT Index)** | A data framework that connects LLMs to external data sources like PDFs, SQL, or APIs by creating structured indices. Optimized for retrieval-augmented generation (RAG).                             |
| **Mastra**                          | A TypeScript/JavaScript framework for building reliable AI workflows, including agents, tools, memory, and planning. Emphasizes modularity and clean APIs for building LLM-powered apps in the Node/TypeScript ecosystem. |
| **LangChain4J**                     | A Java port of LangChain, enabling LLM apps in JVM-based languages. Brings chains, agents, memory, and tool integrations to the Java ecosystem.                                                                           |
| **Koog**                            | A Kotlin-native framework for building AI agents and assistants. Focuses on strong type safety, composability, and seamless integration with the Kotlin/Java ecosystem.                                                   |

<img src="https://cdn-uploads.huggingface.co/production/uploads/noauth/23sIUZINj5eBos3HZyQ54.webp"  alt="Hugging Face Cert"/>

```shell
qwen2 ollama show qwen2:7b
  Model
    architecture        qwen2
    parameters          7.6B
    context length      32768
    embedding length    3584
    quantization        Q4_0

  Capabilities
    completion
    tools

  Parameters
    stop    "<|im_start|>"
    stop    "<|im_end|>"

  System
    You are a helpful assistant.

  License
    Apache License
    Version 2.0, January 2004
    ...
```

{{< imgresize src="proj-setup.png" width="2880" height="1800" alt="End result" >}}

{{< imgresize src="end-result.png" width="2880" height="1588" alt="End result" >}}

### Get in touch 📧
As I say in my [About](../../about/) page, I would love to hear from you. If you got to the end of this post and have anything to share, please get in touch on [LinkedIn](https://www.linkedin.com/in/c-j-davies/) or [Twitter](https://x.com/c_davies21).
