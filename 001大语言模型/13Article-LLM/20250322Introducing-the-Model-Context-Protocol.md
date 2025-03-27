## 20250322Introducing-the-Model-Context-Protocol

[Introducing the Model Context Protocol \ Anthropic](https://www.anthropic.com/news/model-context-protocol)

Announcements # Introducing the Model Context Protocol

Nov 25，2024

Today，we're open-sourcing the Model Context Protocol（MCP），a new standard for connecting AI assistants to the systems where data lives，including content repositories，business tools，and development environments. Its aim is to help frontier models produce better，more relevant responses.

今天，我们开源了模型上下文协议（Model Context Protocol，MCP），这是一个新的标准，旨在将 AI 助手连接到数据所在的系统中，包括内容仓库、业务工具和开发环境。它的目的是帮助前沿模型，产出更好、更相关的响应。

As AI assistants gain mainstream adoption，the industry has invested heavily in model capabilities，achieving rapid advances in reasoning and quality. Yet even the most sophisticated models are constrained by their isolation from data—trapped behind information silos and legacy systems. Every new data source requires its own custom implementation，making truly connected systems difficult to scale.

随着 AI 助手日益普及，行业在模型能力上投入了大量资源，并在推理和质量上取得了飞速的进步。然而，即使是最先进的模型也受到数据孤立的限制 —— 它们被困于信息孤岛和老旧系统之中。每接入一个新的数据源，都需要进行定制开发，这使得真正互联互通的系统难以扩展。

MCP addresses this challenge. It provides a universal，open standard for connecting AI systems with data sources，replacing fragmented integrations with a single protocol. The result is a simpler，more reliable way to give AI systems access to the data they need.

MCP 正是为了解决这一难题而生。它提供了一个通用的、开放的标准，用于连接 AI 系统和各种数据源，从而用一套统一的协议取代过去零散的集成方式。最终，AI 系统可以更简单、更可靠地获取所需的数据。

### 01. Model Context Protocol

The Model Context Protocol is an open standard that enables developers to build secure，two-way connections between their data sources and AI-powered tools. The architecture is straightforward：developers can either expose their data through MCP servers or build AI applications（MCP clients）that connect to these servers.

模型上下文协议模型上下文协议（Model Context Protocol）是一个开放标准，旨在帮助开发者在数据源和人工智能驱动的工具之间建立安全的双向连接。其架构非常简单：开发者既可以通过 MCP 服务器开放自己的数据，也可以构建 AI 应用程序（MCP 客户端）并连接到这些服务器。

Today，we're introducing three major components of the Model Context Protocol for developers:

今天，我们为开发者介绍模型上下文协议的三个主要组成部分：

1 The Model Context Protocol specification and SDKs

模型上下文协议规范和软件开发工具包（SDK)

[Model Context Protocol](https://github.com/modelcontextprotocol)

2 Local MCP server support in the Claude Desktop apps

Claude 桌面应用支持本地 MCP 服务器

[Download - Claude](https://claude.ai/download)

3 An open-source repository of MCP servers

MCP 服务器的开源代码仓库

Claude 3.5 Sonnet is adept at quickly building MCP server implementations，making it easy for organizations and individuals to rapidly connect their most important datasets with a range of AI-powered tools. To help developers start exploring，we're sharing pre-built MCP servers for popular enterprise systems like Google Drive，Slack，GitHub，Git，Postgres，and Puppeteer.

Claude 3.5 Sonnet 擅长快速构建 MCP 服务器的实现，这使得各个组织和个人能够迅速将他们最重要的数据集与各种 AI 驱动的工具连接起来。为了帮助开发者快速上手，我们分享了预先构建好的 MCP 服务器，它们可以用于连接如 Google Drive、Slack、GitHub、Git、Postgres 和 Puppeteer 等流行的企业系统。

Early adopters like Block and Apollo have integrated MCP into their systems，while development tools companies including Zed，Replit，Codeium，and Sourcegraph are working with MCP to enhance their platforms—enabling AI agents to better retrieve relevant information to further understand the context around a coding task and produce more nuanced and functional code with fewer attempts.

早期采用者，例如 Block 和 Apollo，已经将 MCP 集成到他们的系统之中。同时，Zed、Replit、Codeium 和 Sourcegraph 等开发工具公司也正与 MCP 合作，致力于增强各自的平台。这将使 AI 智能体（AI Agent）能够更有效地检索相关信息，从而更深入地理解编码任务的背景信息，并能以更少的迭代次数生成更精确、功能更强大的代码。

"At Block，open source is more than a development model—it's the foundation of our work and a commitment to creating technology that drives meaningful change and serves as a public good for all,」said Dhanji R. Prasanna，Chief Technology Officer at Block.「Open technologies like the Model Context Protocol are the bridges that connect AI to real-world applications，ensuring innovation is accessible，transparent，and rooted in collaboration. We are excited to partner on a protocol and use it to build agentic systems，which remove the burden of the mechanical so people can focus on the creative."

「在 Block，开源不仅仅是一种开发模式，更是我们一切工作的基石。我们致力于创造能够驱动积极变革、服务大众的技术，并将其视为一项公共事业，」Block 首席技术官 Dhanji R. Prasanna 说道。「像模型上下文协议（Model Context Protocol）这样的开放技术，是连接人工智能（AI）与现实世界应用的桥梁，确保创新具有可访问性、透明性，并建立在协作的基础之上。我们很高兴能参与该协议的合作开发，并用它来构建 AI 智能体（AI Agent），从而让人们摆脱重复性工作的束缚，专注于更具创造力的任务。」

Instead of maintaining separate connectors for each data source，developers can now build against a standard protocol. As the ecosystem matures，AI systems will maintain context as they move between different tools and datasets，replacing today's fragmented integrations with a more sustainable architecture.

开发者们无需再为每个数据源维护单独的连接器，现在他们可以基于一个标准协议进行开发。随着生态系统的逐渐成熟，AI 系统在不同的工具和数据集之间迁移时，能够保持上下文信息。这将以一种更可持续的架构，取代目前这种各自为政、碎片化的集成方式。

### Getting started

快速上手

Developers can start building and testing MCP connectors today. All Claude.ai plans support connecting MCP servers to the Claude Desktop app.

开发者现在就可以开始构建和测试 MCP（Managed Compute Provider）连接器了。所有 Claude.ai 的套餐都支持将 MCP 服务器连接到 Claude 桌面应用。

Claude for Work customers can begin testing MCP servers locally，connecting Claude to internal systems and datasets. We'll soon provide developer toolkits for deploying remote production MCP servers that can serve your entire Claude for Work organization.

Claude for Work 的客户可以开始在本地测试 MCP 服务器（MCP servers），将 Claude 连接到内部系统和数据集。我们很快将提供开发者工具包，用于部署远程生产 MCP 服务器（MCP servers），这些服务器可以为您的整个 Claude for Work 组织提供支持。

To start building:

要开始构建：

1 Install pre-built MCP servers through the Claude Desktop app

通过 Claude 桌面应用安装预先构建好的 MCP 服务器

2 Follow our quickstart guide to build your first MCP server

按照我们的快速入门指南，构建您的第一个 MCP 服务器。

3 Contribute to our open-source repositories of connectors and implementations

参与到我们的开源项目中，贡献连接器和各种实现。

### An open community

一个开放的社区

We're committed to building MCP as a collaborative，open-source project and ecosystem，and we're eager to hear your feedback. Whether you're an AI tool developer，an enterprise looking to leverage existing data，or an early adopter exploring the frontier，we invite you to build the future of context-aware AI together.

我们致力于将 MCP 构建为一个协作的开源项目和生态系统，并期待您的反馈。无论您是 AI 工具开发者，希望利用现有数据的企业，还是探索前沿技术的尝鲜者，我们都邀请您一起，共同塑造具有上下文感知能力的 AI 的未来。