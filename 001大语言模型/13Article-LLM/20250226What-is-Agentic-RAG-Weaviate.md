## 20250226What-is-Agentic-RAG-Weaviate

[What is Agentic RAG | Weaviate](https://weaviate.io/blog/what-is-agentic-rag)

[Blog | Weaviate](https://weaviate.io/blog)

While Retrieval-Augmented Generation (RAG) dominated 2023, agentic workflows are driving massive progress in 2024. The usage of AI agents opens up new possibilities for building more powerful, robust, and versatile Large Language Model(LLM)-powered applications. One possibility is enhancing RAG pipelines with AI agents in agentic RAG pipelines.

虽然检索增强生成（RAG）在 2023 年占据主导地位，但 AI 智能体工作流在 2024 年取得了显著进展。AI 智能体的使用为构建更强大、更稳健和更通用的由大语言模型（LLM）驱动的应用程序开辟了新的可能性。其中一种可能性是，利用 AI 智能体增强 RAG 管道，构建基于 AI 智能体的 RAG 管道。

This article introduces you to the concept of agentic RAG, its implementation, and its benefits and limitations.

本文将向您介绍基于 AI 智能体的 RAG 的概念、其实现方式以及其优点和局限性。

### 01. Fundamentals of Agentic RAG​

智能体 RAG 基础

Agentic RAG describes an AI agent-based implementation of RAG. Before we go any further, let’s quickly recap the fundamental concepts of RAG and AI agents.

智能体 RAG 描述的是一种基于 AI 智能体的 RAG 实现。在深入探讨之前，我们先快速回顾一下 RAG 和 AI 智能体的基本概念。

#### What is Retrieval-Augmented Generation (RAG)​

什么是检索增强生成（RAG)

Retrieval-Augmented Generation (RAG) is a technique for building LLM-powered applications. It leverages an external knowledge source to provide the LLM with relevant context and reduce hallucinations.

检索增强生成（RAG）是一种用于构建由 LLM 驱动的应用的技术。它利用外部知识源为 LLM 提供相关上下文，从而减少幻觉。

A naive RAG pipeline consists of a retrieval component (typically composed of an embedding model and a vector database) and a generative component (an LLM). At inference time, the user query is used to run a similarity search over the indexed documents to retrieve the most similar documents to the query and provide the LLM with additional context.

一个简单的 RAG 管道包含两个主要组件：检索组件（通常由嵌入模型和向量数据库构成）和生成组件（一个 LLM）。在进行推理时，系统会使用用户查询对索引文档执行相似性搜索，以检索与查询最相关的文档，并为 LLM 提供额外的上下文。

Typical RAG applications have two considerable limitations:

典型的 RAG 应用有两个相当大的局限性：

1 The naive RAG pipeline only considers one external knowledge source. However, some solutions might require two external knowledge sources, and some solutions might require external tools and APIs, such as web searches.

简单的 RAG 流程只考虑一个外部知识来源。然而，某些解决方案可能需要两个外部知识来源，还有一些可能需要外部工具和 API，例如网络搜索。

2 They are a one-shot solution, which means that context is retrieved once. There is no reasoning or validation over the quality of the retrieved context.

它们是单次检索方案，这意味着上下文信息只会被检索一次，并且不会对检索到的上下文质量进行推理或验证。

#### What are Agents in AI Systems​

什么是 AI 系统中的 AI 智能体

With the popularity of LLMs, new paradigms of AI agents and multi-agent systems have emerged. AI agents are LLMs with a role and task that have access to memory and external tools. The reasoning capabilities of LLMs help the agent plan the required steps and take action to complete the task at hand.
Thus, the core components of an AI agent are:

随着大语言模型（LLMs）的普及，AI 智能体和多智能体系统的新范式已经出现。AI 智能体是具有角色和任务，并且可以访问记忆和外部工具的 LLM。LLM 的推理能力可以帮助 AI 智能体规划完成任务所需的步骤，并采取行动。

因此，AI 智能体的核心组件是：

1 LLM (with a role and a task)

大语言模型（LLM）(拥有角色和任务)

2 Memory (short-term and long-term)

记忆（短期和长期记忆)

3 Planning (e.g., reflection, self-critics, query routing, etc.)

规划（例如，反思、自我批评、查询路由等)

4 Tools (e.g., calculator, web search, etc.)

工具（例如，计算器、网络搜索等等)

One popular framework is the ReAct framework. A ReAct agent can handle sequential multi-part queries while maintaining state (in memory) by combining routing, query planning, and tool use into a single entity.

一种流行的框架是 ReAct 框架。ReAct 智能体就像一个整合了多种功能的智能助手，它将路由、查询规划和工具使用组合成一个统一的整体，从而能够处理连续的、包含多个步骤的查询，同时保持状态（存储于内存中）。

2023012ReAct: Synergizing Reasoning and Acting in Language Models

[[2210.03629] ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)

ReAct = Reason + Act (with LLMs)

The process involves the following steps:

这个过程主要包括以下几个步骤：

1 Thought: Upon receiving the user query, the agent reasons about the next action to take

思考：在接收到用户查询后，AI 智能体（AI Agent）会思考下一步该怎么做

2 Action: the agent decides on an action and executes it (e.g., tool use)

行动：AI 智能体决定执行某个行动并执行它（例如，使用工具）

3 Observation: the agent observes the feedback from the action

观察：AI 智能体接收其行动产生的反馈。

4 This process iterates until the agent completes the task and responds to the user.

这个过程循环往复，直到 AI 智能体完成任务并响应用户。

### 02. What is Agentic RAG?

什么是 Agentic RAG？

Agentic RAG describes an AI agent-based implementation of RAG. Specifically, it incorporates AI agents into the RAG pipeline to orchestrate its components and perform additional actions beyond simple information retrieval and generation to overcome the limitations of the non-agentic pipeline.

Agentic RAG 是一种利用 AI 智能体的 RAG（检索增强生成）实现方案。更具体地说，它将 AI 智能体整合到 RAG 流程中，由 AI 智能体来协调 RAG 的各个组成部分，并执行超出简单信息检索和内容生成的额外操作，从而克服传统 RAG 流程的局限性。

Agentic RAG describes an AI agent-based implementation of RAG.

Agentic RAG 描述的是一种基于 AI 智能体的 RAG（Retrieval Augmented Generation）实现。

How does Agentic RAG work?

Agentic RAG 是如何工作的呢？

Although agents can be incorporated in different stages of the RAG pipeline, agentic RAG most commonly refers to the use of agents in the retrieval component.

尽管 AI 智能体可以被应用到 RAG 流程的各个环节，但 Agentic RAG 通常指的是在检索环节中使用 AI 智能体。

Specifically, the retrieval component becomes agentic through the use of retrieval agents with access to different retriever tools, such as:

具体来说，检索组件通过使用检索 AI 智能体而具备了主动性，这些 AI 智能体可以访问各种检索工具，例如：

1 Vector search engine (also called a query engine) that performs vector search over a vector index (like in typical RAG pipelines)

向量搜索引擎（也称为查询引擎)：它通过向量索引执行向量搜索（就像在典型的 RAG 流程中一样）。

2 Web search

网络搜索

3 Calculator

计算器

4 Any API to access software programmatically, such as email or chat programs

and many more.

任何可以通过 API 以编程方式访问的软件，例如电子邮件或聊天程序等等。

The RAG agent can then reason and act over the following example retrieval scenarios:

RAG AI 智能体可以针对以下示例检索场景进行推理和执行操作：

Decide whether to retrieve information or not

决定是否检索信息

Decide which tool to use to retrieve relevant information

决定使用哪个工具来检索相关信息

Formulate the query itself

构建查询本身

Evaluate the retrieved context and decide whether it needs to re-retrieve.

评估检索到的上下文，并决定是否需要重新检索。

#### Agentic RAG Architecture

In contrast to the sequential naive RAG architecture, the core of the agentic RAG architecture is the agent. Agentic RAG architectures can have various levels of complexity. In the simplest form, a single-agent RAG architecture is a simple router. However, you can also add multiple agents into a multi-agent RAG architecture. This section discusses the two fundamental RAG architectures.

Agentic RAG（Agentic RAG）架构与顺序的朴素 RAG 架构相比，Agentic RAG 架构的核心是 AI 智能体（AI Agent）。Agentic RAG 架构可以具有不同的复杂程度。在最简单的形式中，单智能体 RAG 架构就是一个简单的路由器。但是，您也可以将多个 AI 智能体添加到多智能体 RAG 架构中。本节将讨论两种基本的 Agentic RAG 架构，重点介绍它们的特点和应用。

Single-Agent RAG (Router)

单智能体 RAG（路由器)

In its simplest form, agentic RAG is a router. This means you have at least two external knowledge sources, and the agent decides which one to retrieve additional context from. However, the external knowledge sources don't have to be limited to (vector) databases. You can retrieve further information from tools as well. For example, you can conduct a web search, or you could use an API to retrieve additional information from Slack channels or your email accounts.

在最简单的形式中，类智能体 RAG 就像一个路由器。这意味着你至少拥有两个外部知识来源，而 AI 智能体（AI Agent）决定从哪个知识源检索额外的上下文。当然，外部知识来源不必仅限于向量数据库。你还可以从各种工具中获取更多信息。例如，你可以直接进行网络搜索，或者使用 API 从 Slack 频道或你的电子邮件帐户中获取更多信息。

Multi-agent RAG Systems

多智能体 RAG 系统

As you can guess, the single-agent system also has its limitations because it's limited to only one agent with reasoning, retrieval, and answer generation in one. Therefore, it is beneficial to chain multiple agents into a multi-agent RAG application.

可以想到，单智能体系统也存在局限性，因为它将推理、检索和答案生成都限制在一个智能体中完成。因此，将多个智能体链接到 RAG（Retrieval-Augmented Generation）应用中会更有优势。

For example, you can have one master agent who coordinates information retrieval among multiple specialized retrieval agents. For instance, one agent could retrieve information from proprietary internal data sources. Another agent could specialize in retrieving information from your personal accounts, such as email or chat. Another agent could also specialize in retrieving public information from web searches.

例如，可以设置一个主 AI 智能体，由它来协调多个专业检索 AI 智能体之间的信息检索。例如，一个 AI 智能体可以从专有的内部数据源检索信息；另一个 AI 智能体可以专门从你的个人账户，如电子邮件、聊天等检索信息；还有一个 AI 智能体可以专门从网络搜索中检索公共信息。

Beyond Retrieval Agents

超越检索智能体（Retrieval Agents)

The above example shows the usage of different retrieval agents. However, you could also use agents for purposes other than retrieval. The possibilities of agents in the RAG system are manifold.

以上面的例子为例，它展示了如何使用不同的检索智能体。除此之外，你还可以将智能体用于检索之外的其他目的。智能体在 RAG 系统中的应用潜力是巨大的。

### 03. Agentic RAG vs. (Vanilla) RAG​

Agentic RAG vs. 原始 RAG（Vanilla RAG)

While the fundamental concept of RAG (sending a query, retrieving information, and generating a response) remains the same, tool use generalizes it, making it more flexible and powerful.

虽然 RAG 的基本概念（发送查询、检索信息和生成响应）保持不变，但工具的使用使其更加通用，从而使其更加灵活和强大。

Think of it this way: Common (vanilla) RAG is like being at the library (before smartphones existed) to answer a specific question. Agentic RAG, on the other hand, is like having a smartphone in your hand with a web browser, a calculator, your emails, etc.

可以这样理解：传统的 RAG 就像在没有智能手机的时代，你在图书馆里查找资料来回答一个特定的问题。而 Agentic RAG，就像你手握一台智能手机，可以使用网络浏览器、计算器、电子邮件等各种应用。

|                                            | Vanilla RAG | Agentic RAG |
| :----------------------------------------- | :---------- | :---------- |
| Access to external tools                   | No          | Yes         |
| Query pre-processing                       | No          | Yes         |
| Multi-step retrieval                       | No          | Yes         |
| Validation of retrieved information      | No          | Yes         |

### 04. Implementing Agentic RAG​

实施 Agentic RAG

As outlined earlier, agents are comprised of multiple components. To build an agentic RAG pipeline, there are two options: a language model with function calling or an agent framework. Both implementations get to the same result, it will just depend on the control and flexibility you want.

如前所述，AI 智能体由多个组件构成。要构建 Agentic RAG 管道，有两种选择：使用具备函数调用功能的语言模型，或者选择 AI 智能体框架。两种实现方式都能达到相似的效果，选择哪一种取决于你对控制和灵活性的需求。

#### Language Models with Function Calling​

具有函数调用的语言模型语言

Language models are the main component of agentic RAG systems. The other component is tools, which enable the language model access to external services. Language models with function calling offer a way to build an agentic system by allowing the model to interact with predefined tools. Language model providers have added this feature to their clients.

模型是 Agentic RAG 系统的核心。另一个关键组成部分是工具，它赋予了语言模型访问外部服务的能力。具有函数调用功能的语言模型，允许模型与预定义的工具进行交互，从而提供了一种构建 Agentic 系统的方法。各大语言模型提供商已经在其 API 中添加了函数调用功能。

In June 2023, OpenAI released function calling for gpt-3.5-turbo and gpt-4. It enabled these models to reliably connect GPT’s capabilities with external tools and APIs. Developers quickly started building applications that plugged gpt-4 into code executors, databases, calculators, and more.

2023 年 6 月，OpenAI 为 gpt-3.5-turbo 和 gpt-4 发布了函数调用功能。这使得这些模型能够可靠地将 GPT 的能力与外部工具和 API 连接起来。开发人员迅速开始构建各种应用，将 gpt-4 连接到代码执行器、数据库和计算器等等。

Cohere further launched their connectors API to add tools to the Command-R suite of models. Additionally, Anthropic and Google launched function calling for Claude and Gemini. By powering these models with external services, it can access and cite web resources, execute code and more.

Cohere 还推出了 Connector API，以便向 Command-R 模型套件添加工具。此外，Anthropic 和 Google 也分别为 Claude 和 Gemini 推出了函数调用功能。通过外部服务为这些模型提供支持，它们可以访问并引用 Web 资源、执行代码等操作。

Function calling isn’t only for proprietary models. Ollama introduced tool support for popular open-source models like Llama3.2, nemotron-mini, and others.
To build a tool, you first need to define the function. In this snippet, we’re writing a function that is using Weaviate’s hybrid search to retrieve objects from the database:

函数调用功能并非仅限于闭源模型。Ollama 为流行的开源模型（如 Llama3.2、nemotron-mini 等）引入了工具支持。

要创建一个工具，首先需要定义其功能。以下代码展示了如何编写一个函数，利用 Weaviate 的混合搜索从数据库中检索对象：

```py
def get_search_results(query: str) -> str:
    """Sends a query to Weaviate's Hybrid Search. Parses the response into a {k}:{v} string."""
    
    response = blogs.query.hybrid(query, limit=5)
    
    stringified_response = ""
    for idx, o in enumerate(response.objects):
        stringified_response += f"Search Result: {idx+1}:\n"
        for prop in o.properties:
            stringified_response += f"{prop}:{o.properties[prop]}"
        stringified_response += "\n"
    
    return stringified_response
```

We will then pass the function to the language model via a tools_schema. The schema is then used in the prompt to the language model:

```py
tools_schema=[{
    'type': 'function',
    'function': {
        'name': 'get_search_results',
        'description': 'Get search results for a provided query.',
        'parameters': {
          'type': 'object',
          'properties': {
            'query': {
              'type': 'string',
              'description': 'The search query.',
            },
          },
          'required': ['query'],
        },
    },
}]
```

Since you’re connecting to the language model API directly, you’ll need to write a loop that routes between the language model and tools:


```py
def ollama_generation_with_tools(user_message: str,
                                 tools_schema: List, tool_mapping: Dict,
                                 model_name: str = "llama3.1") -> str:
    messages=[{
        "role": "user",
        "content": user_message
    }]
    response = ollama.chat(
        model=model_name,
        messages=messages,
        tools=tools_schema
    )
    if not response["message"].get("tool_calls"):
        return response["message"]["content"]
    else:
        for tool in response["message"]["tool_calls"]:
            function_to_call = tool_mapping[tool["function"]["name"]]
            print(f"Calling function {function_to_call}...")
            function_response = function_to_call(tool["function"]["arguments"]["query"])
            messages.append({
                "role": "tool",
                "content": function_response,
            })
    
    final_response = ollama.chat(model=model_name, messages=messages)
    return final_response["message"]["content"]
```

Your query will then look like this:

```py
ollama_generation_with_tools("How is HNSW different from DiskANN?",
                            tools_schema=tools_schema, tool_mapping=tool_mapping)
```

#### Agent Frameworks​

AI 智能体框架

Agent Frameworks such as DSPy, LangChain, CrewAI, LlamaIndex, and Letta have emerged to facilitate building applications with language models. These frameworks simplify building agentic RAG systems by plugging pre-built templates together.

为了更方便地使用语言模型构建应用，涌现出了 DSPy、LangChain、CrewAI、LlamaIndex 和 Letta 等 AI 智能体框架。这些框架通过组合预构建的模板，简化了 Agentic RAG 系统的构建过程。

1 DSPy supports ReAct agents and Avatar optimization. Avatar optimization describes the use of automated prompt engineering for the descriptions of each tool.

DSPy 支持 ReAct 智能体和 Avatar 优化。Avatar 优化指的是使用自动提示工程来优化对每个工具的描述。

2 LangChain provides many services for working with tools. LangChain’s LCEL and LangGraph frameworks further offer built-in tools.

LangChain 提供了许多用于处理工具的服务。LangChain 的 LCEL 和 LangGraph 框架还提供了内置工具。

3 LlamaIndex further introduces the QueryEngineTool, a collection of templates for retrieval tools.

LlamaIndex 进一步引入了 QueryEngineTool，这是一组用于检索工具的模板集合。

4 CrewAI is one of the leading frameworks for developing multi-agent systems. One of the key concepts utilized for tool use is sharing tools amongst agents.

CrewAI 是开发多智能体系统的领先框架之一。其工具使用的关键概念之一是在多个智能体之间共享工具。

5 Swarm is a framework built by OpenAI for multi-agent orchestration. Swarm similarly focuses on how tools are shared amongst agents.

Swarm 是一个由 OpenAI 构建的用于多智能体编排的框架。Swarm 同样关注如何在多个智能体之间共享工具。

6 Letta interfaces reflecting and refining an internal world model as functions. This entails potentially using search results to update the agent’s memory of the chatbot user, in addition to responding to the question.

Letta 通过接口将反映和改进内部世界模型的功能视作函数。这意味着，除了回答问题之外，它还可能使用搜索结果来更新智能体对聊天机器人用户的记忆。

### 05. Why are Enterprises Adopting Agentic RAG​

企业为什么纷纷选择 Agentic RAG？​

Enterprises are moving on from vanilla RAG to building agentic RAG applications. Replit released an agent that helps developers build and debug software. Additionally, Microsoft announced copilots that work alongside users to provide suggestions in completing tasks. These are only a few examples of agents in production and the possibilities are endless.

企业正在从传统的 RAG（Retrieval-Augmented Generation，检索增强生成）转向构建 Agentic RAG 应用。例如，Replit 发布了一款 AI 智能体（AI Agent），可以帮助开发者构建和调试软件。此外，Microsoft 也推出了与用户协同工作的 Copilot，在任务完成过程中提供智能建议。这些只是 Agent（AI Agent）在实际应用中的几个例子，未来拥有无限可能。

#### Benefits of Agentic RAG​

Agentic RAG 的优势​

The shift from vanilla RAG to agentic RAG allows these systems to produce more accurate responses, perform tasks autonomously, and better collaborate with humans.
The benefit of agentic RAG lies primarily in the improved quality of retrieved additional information. By adding agents with access to tool use, the retrieval agent can route queries to specialized knowledge sources. Furthermore, the reasoning capabilities of the agent enable a layer of validation of the retrieved context before it is used for further processing. As a result, agentic RAG pipelines can lead to more robust and accurate responses.

相比于传统的 RAG，Agentic RAG 能够更准确地生成回复，更自主地执行任务，并更好地与人类进行协作。Agentic RAG 的主要优势在于它能有效提升检索到的信息的质量。通过引入具备工具使用权限的 AI 智能体，检索 AI 智能体可以将查询导向特定的知识库。更重要的是，AI 智能体的推理能力还可以在信息被用于后续处理前，对其进行验证，确保上下文的准确性。因此，Agentic RAG 流程可以生成更可靠、更精准的回复。

#### Limitations of Agentic RAG​

Agentic RAG 的局限性​

However, there are always two sides to every coin. Using an AI agent a for subtask means incorporating an LLM to do a task. This comes with the limitations of using LLMs in any application, such as added latency and unreliability. Depending on the reasoning capabilities of the LLM, an agent may fail to complete a task sufficiently (or even at all). It is important to incorporate proper failure modes to help an AI agent get unstuck when they are unable to complete a task.

当然，任何事物都具有两面性。使用 AI 智能体来执行子任务，意味着需要集成大语言模型（LLM）来完成特定工作。这也意味着会受到大语言模型（LLM）本身的限制，例如更高的响应延迟和潜在的不可靠性。这里的延迟不仅包括推理时间，还包括大语言模型（LLM）从外部工具获取信息的时间。此外，由于受到大语言模型（LLM）推理能力的限制，AI 智能体可能无法充分完成任务，甚至完全失败。因此，在设计系统时，必须考虑到各种可能的失败情况，并加入相应的应对机制，以便 AI 智能体在遇到问题时能够及时「自救」。

### Summary​

总结​

This blog discussed the concept of agentic RAG, which involves incorporating agents into the RAG pipeline. Although agents can be used for many different purposes in a RAG pipeline, agentic RAG most often involves using retrieval agents with access to tools to generalize retrieval.

本文探讨了 Agentic RAG 的概念，即如何将 AI 智能体融入到 RAG 流程中。尽管 AI 智能体可以在 RAG 流程中发挥多种作用，但 Agentic RAG 最常见的应用是利用具备工具访问权限的检索 AI 智能体来增强检索的泛化能力。

This article discussed agentic RAG architectures using single-agent and multi-agent systems and their differences from vanilla RAG pipelines.

本文还介绍了基于单 AI 智能体和多 AI 智能体系统的 Agentic RAG 架构，并阐述了它们与传统 RAG 流程的不同之处。

With the rise and popularity of AI agent systems, many different frameworks are evolving for implementing agentic RAG, such as LlamaIndex, LangGraph, or CrewAI.
Finally, this article discussed the benefits and limitations of agentic RAG pipelines.

随着 AI 智能体系统的日益普及，涌现出许多用于实现 Agentic RAG 的框架，例如 LlamaIndex、LangGraph 和 CrewAI。这些框架各有特点，例如 LlamaIndex 侧重于数据索引，LangGraph 侧重于多智能体的协同。

最后，本文还分析了 Agentic RAG 流程的优点和局限性。

### Further Resources​

更多资源​

Notebook using Swarm

[recipes/integrations/llm-frameworks/function-calling/openai/openai-swarm.ipynb at main · weaviate/recipes](https://github.com/weaviate/recipes/blob/main/integrations/llm-frameworks/function-calling/openai/openai-swarm.ipynb)

Notebook using Letta and Weaviate

[recipes/integrations/llm-frameworks/letta at main · weaviate/recipes](https://github.com/weaviate/recipes/tree/main/integrations/llm-frameworks/letta)

Notebooks on using function calling in Ollama

[recipes/integrations/llm-frameworks/function-calling/ollama at main · weaviate/recipes](https://github.com/weaviate/recipes/tree/main/integrations/llm-frameworks/function-calling/ollama)

Notebook on Vanilla RAG versus Agentic RAG

[recipes/integrations/llm-frameworks/agentic-rag-benchmark/vanilla-rag-vs-agentic-rag.ipynb at main · weaviate/recipes](https://github.com/weaviate/recipes/blob/main/integrations/llm-frameworks/agentic-rag-benchmark/vanilla-rag-vs-agentic-rag.ipynb)