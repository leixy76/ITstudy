## 20250322Getting-Started-Model-Context-Protocol

[Getting Started: Model Context Protocol | by Chris McKenzie | Medium](https://medium.com/@kenzic/getting-started-model-context-protocol-e0a80dddff80)

Dec 19, 2024

Discover how MCP simplifies AI integrations，unlocks real-time data access，and empowers developers to build smarter，scalable solutions

探索 MCP 如何简化 AI 集成，解锁实时数据访问，并助力开发者构建更智能、可扩展的解决方案。

AI systems today are stuck behind a wall of data silos and fragmented integrations，making it hard to connect them to the tools and systems where information actually lives. I can't count the number of times I've had to copy content from one data source，and paste it into Claude or ChatGPT. And if you want to avoid this，every new data source requires a custom integration. At best this is a slight pain，and at worst，it is slowing progress and creating scalability headaches.

如今，人工智能系统受限于数据孤岛和碎片化集成，难以连接到存储实际信息的工具和系统。我已经记不清多少次需要从一个数据源复制内容，再粘贴到 Claude 或 ChatGPT 中。如果你想避免这种重复劳动，每接入一个新的数据源都需要进行定制化集成。理想情况下，这仅仅带来轻微的不便；而更糟糕的情况是，它会拖慢开发进度，并引发扩展性问题。

Model Context Protocol（MCP）solves this by introducing a universal standard for connecting AI to data and tools. Instead of patchwork solutions，it provides a streamlined，open protocol that simplifies integrations，breaks down silos，and unlocks the full potential of AI to deliver relevant，high-quality results.

模型上下文协议（Model Context Protocol，MCP）通过引入一种通用标准，将人工智能（AI）连接到数据和工具，从而解决了这个问题。它没有采用临时的补丁方案，而是提供了一个简化的、开放的协议，旨在简化集成过程，打破数据壁垒（消除不同系统和数据源之间的隔离状态），并充分释放 AI 的潜力，以提供相关且高质量的结果。

> "even the most sophisticated models are constrained by their isolation from data — trapped behind information silos and legacy systems." ~ Anthropic

即使是最先进的模型，也因为与数据的隔离而受到限制 —— 它们被困于信息孤岛和遗留系统之中。—— Anthropic

### 01. What is MCP and Why Does It Matter?

什么是 MCP，为什么它很重要？

AI is stuck in a frustrating loop：(rewrite）powerful tools，limited by fragmented data connections. Every new data source demands a custom integration，creating silos and scalability headaches for developers. The result? AI systems can't fully tap into the context they need to deliver truly relevant and useful outputs.

AI 正面临一个令人沮丧的困境：即使拥有强大的工具，却受限于零散的数据连接。每当需要接入新的数据源，开发者们就不得不进行定制化的整合工作，从而导致数据孤岛的出现，并带来扩展性问题。这样的结果是，AI 系统无法充分利用所需的上下文信息，进而难以提供真正相关且有用的输出。

That's where the Model Context Protocol（MCP）comes in. MCP is an open standard by Anthropic，designed to provide a universal way to connect data sources with AI-powered tools. Whether it's your content repositories，business tools，or developer environments，MCP simplifies the process of building secure，two-way connections so AI can finally work the way it's supposed to.

这正是模型上下文协议（Model Context Protocol，MCP）出现的原因。MCP 是由 Anthropic 提出的开放标准，旨在提供一种通用方法，将各种数据源与人工智能（AI）驱动的工具相连接。无论数据源是您的内容仓库、业务工具，还是开发者环境，MCP 都能简化构建安全双向连接的过程，从而使 AI 能够真正发挥其应有的作用。

With MCP，developers no longer have to reinvent the wheel for every data source. Instead，they can focus on creating smarter，more connected AI systems that scale without the constant drag of maintaining fragmented integrations.

借助 MCP，开发人员无需针对每个数据源重复构建基础设施。相反，他们能够专注于构建更智能、关联性更强的 AI 系统，这些系统可以轻松扩展，而摆脱了持续维护碎片化集成带来的负担。

### 02. How MCP Works

MCP 的工作原理

MCP works by bridging two key components：MCP servers that expose data sources and MCP clients（AI apps）that connect to those servers. This architecture is simple but incredibly flexible，allowing AI systems to easily access the data and tools they need in real time，while providing a permissions framework to control access.

MCP 的核心在于连接两个关键部分：一类是 MCP 服务器，它们负责开放各种数据源；另一类是 MCP 客户端（AI 应用），它们连接到这些服务器。这种架构设计简洁却极具灵活性，让 AI 系统能够轻松、实时地获取所需的数据和工具，同时还提供了一套权限管理机制来控制数据访问。

To make adoption easy，MCP includes three main pieces:

为了方便用户使用，MCP 包含三个主要组成部分：

1 Hosts are LLM applications（like Claude Desktop or IDEs）that initiate connections

主机：指那些能够发起连接的大语言模型（LLM）应用程序，例如 Claude Desktop 或集成开发环境（IDE）。

2 Clients maintain 1:1 connections with servers，inside the host application

在宿主程序内部，客户端与服务器保持一对一的连接

3 Servers provide context，tools，and prompts to clients

服务器为客户端提供上下文、工具和提示

You can review the specifications here

### 03. How to use it

如何使用它

You can start leveraging the protocol today in minutes. While there are many permutations of servers and clients，for this demo I'm going to use the Claude desktop client and Knowledge Graph Memory Server.

您可以在几分钟内开始使用该协议。虽然服务器和客户端的组合方式有很多种，但在此演示中，我将使用 Claude 桌面客户端和知识图谱内存服务器（Knowledge Graph Memory Server）。

To Start，Download Desktop app if you don't already have it.

首先，如果您还没有桌面应用程序，请下载它。

Now let's add the Knowledge Graph Memory Server to Claude for storing and retrieving information. However，I encourage you to navigate to repo readme to see list of available servers. They've been updating this frequently，so I'd keeping an eye on it.

现在让我们将知识图谱内存服务器添加到 Claude，用于存储和检索信息。但是，我鼓励您浏览到仓库的说明文档（repo readme）以查看可用服务器的列表。他们一直在频繁更新可用服务器列表，因此我建议您密切关注。

[servers/src/memory at main · modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/memory)

Start by going to settings，and click「Edit Config.」If claude_desktop_config.json doesn't automatically open，then open it in your editor of choice.

首先进入设置，然后点击「编辑配置」(Edit Config.）。如果 `claude_desktop_config.json` 文件没有自动打开，请在您常用的编辑器中打开它。

Add the following config to the file:

将以下配置添加到文件中：

```
{
    "mcpServers": {
        "memory": {
            "command": "npx",
            "args": [
                "-y",
                "@modelcontextprotocol/server-memory"
            ]
        }
    }
}
```

Save and close. That's it!

保存并关闭。就这样！

Now you can begin to add nodes and edges to your knowledge graph. For this demo，I'll use the famous paper,"Attention Is All You Need".

现在，你可以开始向你的知识图谱中添加节点和边了。这次演示，我将以著名的论文「Attention Is All You Need」为例。

I start by dropping in the following prompt:

我首先输入下面的提示语：

```
Read the following research paper，and add key concepts and their relationships to the knowledge base:
[PASTE CONTENTS OF RESEARCH PAPER HERE]
```

```
Read the following research paper，and add key concepts and their relationships to the knowledge base:
http://arxiv.org/abs/1706.03762
```

Claude will now ask for permission to write to your knowledge graph (or memory). Click “Allow for this Chat”. Working with the memory server, Claude will create nodes and edges in the graph with key concepts and their relationships.

Once this is done, you can start a new chat thread (or even close Claude, as the data is stored locally and not tied to a session).

完成上述步骤后，您可以开始新的对话（甚至可以关闭 Claude，因为数据存储在本地，与当前会话无关）。

Enter a prompt similar to:

接下来，输入如下提示语：

```
Based on your knowledge in the knowledge base on the subject of attention in transformers，create a mermaid graph that shows the key concepts and relationships
```

根据您在关于 Transformer 的注意力机制主题的知识库中的知识，创建一个 mermaid 图表，展示核心概念和相互关系。

The end result should look something like:

最终结果应该类似这样：

> Note：your results may vary depending on the version of Claude as well as how it interpreted your prompt and parsed the article. I encourage you to play around with testing this on different models and prompts.

注意：您的结果可能会因为 Claude 的版本，以及它如何理解您的提示和解析文章而有所不同。建议您在不同的模型和提示上试试看。

From here you can continue to build relationships between concepts，add more detailed information，or use the knowledge to help perform other tasks. This is just one of the many servers you have access to，and I encourage you to install others，including the sqlite server.

从这里你可以继续构建概念之间的关系，添加更详细的信息，或者利用这些知识来辅助完成其他任务。这只是你能够访问的众多服务器之一，我建议你安装其他的服务器，例如 sqlite 服务器。

### Next Steps

下一步

While not in the scope of this article，you can develop your own custom integrations using the open protocol，and Anthropic's Python and TypeScript SDKs.

虽然这超出了本文的讨论范围，但你可以使用开放协议以及 Anthropic 的 Python 和 TypeScript SDK 开发自己的定制集成。

### Final Thoughts

总结与思考

The Model Context Protocol represents a promising shift in how AI systems interact with data，breaking down silos and simplifying integrations. By adopting MCP，developers can focus on building smarter，scalable AI solutions without the burden of fragmented systems. Whether you're leveraging pre-built servers or exploring custom integrations，MCP provides the foundation for unlocking AI's full potential — one seamless connection at a time.

模型上下文协议（MCP）代表了 AI 系统与数据交互方式的一个很有前景的变革，它打破了数据孤岛，简化了集成过程。通过采用 MCP，开发人员可以专注于构建更智能、可扩展的 AI 解决方案，而无需被零散的系统所困扰。无论您是使用预先构建的服务器，还是探索自定义集成方案，MCP 都为充分释放 AI 的潜力奠定了基础 —— 通过每一次无缝连接，逐步实现。