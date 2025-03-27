## 20250323MCP-101-An-Introduction-to-Model-Context-Protocol

[MCP 101: An Introduction to Model Context Protocol | DigitalOcean](https://www.digitalocean.com/community/tutorials/model-context-protocol#one-protocol-to-rule-them-all)

Published on March 18, 2025

Model Context Protocol (MCP) has emerged as a hot topic in AI circles. Scrolling through social media, we’ve been seeing MCP posts by explainers, debaters, and memers alike. A quick search on Google or YouTube reveals pages upon pages of new content covering MCP. Clearly, the people are excited. But about what exactly? Well, it’s quite simple: if models are only as good as the context provided to them, a mechanism that standardizes how this context augmentation occurs is a critical frontier of improving agentic capabilities.

模型上下文协议（MCP）已经成为 AI 领域备受关注的热点。在社交媒体上，经常能看到科普人士、辩论者以及表情包爱好者发布与 MCP 相关的帖子。快速在 Google 或 YouTube 上搜索，也会发现大量关于 MCP 的新内容。显然，大家对 MCP 充满兴趣。那么，MCP 究竟是什么呢？其实很简单：如果模型的性能受限于其所获得的上下文信息，那么，标准化上下文增强机制就成为了提升 AI 智能体能力的关键。

For those who have not had the time to dive into this concept, fear not. The goal of this article is to give you an intuitive understanding around the ins and outs of MCP.

如果您还没有时间深入了解这个概念，请不用担心。本文旨在帮助您直观地理解 MCP 的方方面面。

Prerequisites

先决条件

While this explanation of Model Context Protocol (MCP) aims to be accessible, understanding its role in the evolving landscape of AI applications will be greatly enhanced by a foundational understanding of the capabilities of Large Language Models (LLMs) – particularly how they process information and utilize tools.

虽然本文力求以通俗易懂的方式解释模型上下文协议（Model Context Protocol，MCP），但为了更好地理解 MCP 在快速发展的人工智能应用中的作用，建议读者对大语言模型（Large Language Models，LLMs）的基本原理有所了解，特别是它们如何处理信息和使用工具。

### 01. Introduction

介绍

Introduced November 2024 by Anthropic as an open-source protocol, MCP allows for the integration between LLM applications and external data sources and tools.

MCP 协议由 Anthropic 公司于 2024 年 11 月推出，并以开源协议的形式发布。它允许大语言模型（LLM/Large Language Model）应用与外部数据源和工具进行集成。

Some exciting applications built with MCP have emerged. For example, Blender-MCP allows Claude to directly interact with and control Blender, resulting in prompt assisted 3D modeling, scene creation, and manipulation.

一些基于 MCP 的令人兴奋的应用涌现出来。例如，Blender-MCP 允许 Claude 直接与 Blender 交互并控制 Blender，从而实现在提示词的辅助下进行 3D 建模、场景创建和操作。

[ahujasid/blender-mcp](https://github.com/ahujasid/blender-mcp)

One Protocol to Rule Them All
Protocols are a set of rules for formatting and processing data. As its name suggests, MCP (Model Context Protocol) is indeed a protocol – specifically a set of rules that standardizes how LLMs connect with external sources of information.

一种统领所有协议的协议协议是一套用于格式化和处理数据的规则。正如其名称所示，MCP（Model Context Protocol）确实是一种协议，它定义了一套规则，用于标准化大语言模型（Large Language Model，LLM）如何与外部信息源进行连接。

Before MCP, there was LSP
The Language Server Protocol (LSP) emerged as a standard for how integrated development environments (IDEs) communicate with language-specific tools. Essentially, LSP allows any IDE that supports it to seamlessly integrate with various programming languages.

在 MCP 之前，就已经有了 LSP
语言服务器协议（LSP）的出现，是为了规范集成开发环境（IDE）如何与特定编程语言的工具进行通信的标准。本质上，LSP 使得任何支持它的 IDE 都能无缝集成各种编程语言。

With LSP, a single Go language server, for instance, can be built following the LSP standard, and any LSP-compatible IDE (ex: VS Code, JetBrains products, or Neovim) can automatically leverage it to offer features like autocompletion, error detection, and code navigation for Go.

借助语言服务器协议（Language Server Protocol，LSP），开发者可以按照 LSP 标准构建专门的 Go 语言服务器。这样，任何兼容 LSP 的集成开发环境（IDE），例如 VS Code、JetBrains 产品或 Neovim，都能直接利用该服务器为 Go 语言提供自动补全、错误检测和代码导航等功能。

Inspired by LSP, MCP overcomes the MxN integration problem we see with language model integrations, where each new language model (M) requires custom connectors and prompts to interface with each enterprise tool (N). By adopting MCP, both models and tools conform to a common interface, reducing the integration complexity from M×N to M+N.

借鉴 LSP 的思想，MCP 旨在解决语言模型集成中常见的 MxN 集成难题。这里的 MxN 问题指的是，每当有新的语言模型（M）需要集成时，都需要为其定制专门的连接器和提示语，才能与各种企业工具（N）配合使用。而通过采用 MCP，模型和工具都遵循统一的接口标准，从而将集成复杂度从 M×N 降低到 M+N，大大简化了集成过程。

Standardization
The beauty of standardization is that we don’t need to maintain a different connector for each data source. For AI applications that intend to preserve contextual information while navigating across various sources of information in their tool and data stack, standardization allows us to transition towards building systems that are more robust and scalable.

标准化标准化的优势在于，我们不再需要为每个数据源维护不同的连接器。对于那些希望在工具和数据栈中，跨多个信息源传递上下文信息的 AI 应用来说，标准化使得构建更强大、更易于扩展的系统成为可能。

### 02. The Components of MCP

MCP 的组成部分

There are three key components to MCP:mcp components

MCP 有三个关键组成部分：

MCP Host: User-facing AI interface (Claude app, IDE plugin, etc.) that connects to multiple MCP servers.

MCP Host：面向用户的人工智能界面（Claude app、IDE 插件等），可以连接到多个 MCP 服务器。

MCP Client: Intermediary that manages secure connections between host and servers, with one client per server for isolation. The Client is in the host application.

MCP 客户端：作为中间桥梁，负责管理主机与服务端之间的安全连接。为了确保各个服务端之间的隔离性，每个服务端都会对应一个 MCP 客户端。该客户端存在于主机应用程序内部。

MCP Server: External program providing specific capabilities (tools, data access, domain prompts) that connects to various data sources like Google Drive, Slack, GitHub, databases, and web browsers.

MCP 服务器：这是一种外部程序，它提供特定的功能（工具、数据访问和特定领域的提示），并能连接到各种数据源，例如 Google Drive、Slack、GitHub、数据库和 Web 浏览器。

MCP wins over other protocols because baked into its build is the intuition Anthropic has developed around building agents as articulated in their “Building Effective Agents” blog post.

MCP 优于其他协议，原因在于它融合了 Anthropic 在构建 AI 智能体方面的经验。这些经验总结于 Anthropic 发布的博文「构建有效智能体」中。

Significant growth has been observed on the server side, with over a thousand community-built, open-source servers as well as official integrations from companies. There’s also been substantial open-source adoption, with contributors enhancing the core protocol and infrastructure.

在服务器端，我们观察到了显著的增长：不仅涌现出超过一千个由社区构建的开源服务器，而且还有来自各公司的官方集成。同时，开源的应用也得到了长足发展，许多贡献者都在致力于改进核心协议和基础设施。

### 03. Server-side Primitives

服务端基础组件

| Feature | Tools | Resources | Prompts |
|---|---|---|---|
| **Function** | Enables servers to expose executable functionality to clients | Allows servers to expose data and content that can be read by clients and used as context for LLM interactions | Predefined templates and workflows that servers can define for standardized LLM interactions |
| **Control Type** | Model-controlled | Application-controlled | User-controlled |
| **Control Meaning** | Tools are exposed from servers to clients; they represent dynamic operations that can be invoked by the LLM and modify state or interact with external systems. | Client application decides how and when resources should be used | Prompts are exposed from servers to clients with the intention of the user |

| 特性 | 工具 | 资源 | 提示 |
|---|---|---|---|
| **函数** | 使服务器能够向客户端提供可执行的函数 | 允许服务器公开可以被客户端读取的数据和内容，这些数据和内容可以作为大语言模型（LLM）交互的上下文 | 服务器可以为标准化的大语言模型（LLM）交互预先定义模板和工作流程 |
| **控制类型** | 模型控制 | 应用控制 | 用户控制 |
| **控制方式** | 工具从服务器暴露给客户端，代表着可以被大语言模型（LLM）调用的动态操作，用于修改状态或与外部系统进行交互。| 客户端应用决定如何以及何时使用这些资源。| 提示从服务器暴露给客户端，最终由用户来使用。|

### 04. Client-side Primitives

客户端基本要素

Roots

A Root defines a specific location within the host’s file system or environment that the server is authorized to interact with. Roots define the boundaries where servers can operate and allow clients to inform servers about relevant resources and their locations.

根（Root）定义了服务器被授权访问的主机文件系统或环境中的特定位置。根（Root）划定了服务器可以操作的范围，并允许客户端告知服务器相关资源及其所在位置。

Sampling

采样（Sampling)

Sampling is an underutilized yet powerful feature offered by MCP that reverses the traditional client-server relationship for LLM interactions. Instead of clients making requests to servers, sampling allows MCP servers to request LLM completions from the client. This gives clients full control over model selection, hosting, privacy, and cost management. Servers can request specific inference parameters like model preferences, system prompts, temperature settings, and token limits, while clients maintain the authority to decline potentially malicious requests or limit resource usage. This approach is valuable in scenarios where clients interact with unfamiliar servers that still require access to intelligent capabilities.

采样（Sampling）是 MCP 提供的一项强大功能，但尚未得到充分利用。它颠覆了传统的大语言模型（LLM/Large Language Model）交互模式，不再是客户端向服务器发送请求，而是 MCP 服务器主动向客户端请求大语言模型补全。这样一来，客户端就能全面掌控模型选择、模型部署、数据隐私和成本开销。服务器可以指定推理参数，例如偏好的模型、系统提示、温度系数和 Token 数量上限。同时，客户端仍然有权拒绝潜在的恶意请求或限制资源使用。在某些场景下，客户端需要和陌生的服务器交互，但又必须使用 AI 能力， 这种采样（Sampling）方法就显得非常有价值。

### 05. Conclusion

结论

By establishing a common protocol for connecting language models with external tools and data sources, MCP eliminates the need for custom connectors and creates a more robust ecosystem.

通过建立一套通用协议，用于连接大语言模型与外部工具和数据源，MCP 避免了对定制连接器的需求，并创造了一个更具活力的生态系统。

The community approach creates what one might call “compounding innovation” or “3D chess”. Each contributor builds atop others’ work. The network effects are substantial and the pie grows larger for everyone.

社区模式孕育了一种可以称之为「累积式创新」或者「3D 象棋」的现象。每一位贡献者都在前人的基础上添砖加瓦。由此产生的网络效应非常显著，最终让所有参与者都能从中受益。

Anthropic’s bet was that empowering developers with an open MCP would allow it to grow faster, evolve more robustly, and ultimately deliver more value than any closed system they could build alone. Time will tell if they were right, but history suggests they were.

Anthropic 的策略是，通过一个开放的 MCP（Model Collaboration Platform）赋能开发者，从而实现比他们独自构建任何封闭系统更快的增长速度、更强大的发展韧性，并最终创造出更大的价值。时间会给出答案，但历史经验告诉我们，他们的选择是正确的。

### References and Excellent Resources

[Why MCP Won - Latent.Space](https://www.latent.space/p/why-mcp-won)

[The Model Context Protocol (MCP) by Anthropic: Origins, functionality, and impact | mcp – Weights & Biases](https://wandb.ai/onlineinference/mcp/reports/The-Model-Context-Protocol-MCP-by-Anthropic-Origins-functionality-and-impact--VmlldzoxMTY5NDI4MQ)

[Model Context Protocol (MCP), clearly explained (why it matters) - YouTube](https://www.youtube.com/watch?v=7j_NE6Pjv-E)

[Building Agents with Model Context Protocol - Full Workshop with Mahesh Murag of Anthropic - YouTube](https://www.youtube.com/watch?v=kQmXtrmQ5Zg)