---
title: "Taming Llamas and Whales 🦙🐳"
date: 2025-07-13
tags: ["artificial intelligence", "book"]
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

...

### The course
- LLM transformer architecture - end-of-sequence token, a custom stop sequence, or a max-token limit.
- Attention mechanisms - positional importance, Beam search - multiple candidate sequences rather than
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

### The setup
Ollama:  it downloads a model file that contains all the weights, architecture config, and tokenizer. This is often:

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
