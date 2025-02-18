## 20250216Introducing-Citations-on-the-Anthropic-API-Anthropic

[Introducing Citations on the Anthropic API \ Anthropic](https://www.anthropic.com/news/introducing-citations-api)

Anthropic API 引入引用标注 \ Anthropic

Jan 23, 2025

Today, we're launching Citations, a new API feature that lets Claude ground its answers in source documents. Claude can now provide detailed references to the exact sentences and passages it uses to generate responses, leading to more verifiable, trustworthy outputs.

今天，我们推出了 Citations，这是一个新的 API 功能，它能让 Claude 的回答都基于原始文档。现在，Claude 可以针对它用来生成回复的具体句子和段落提供详细的参考引用，这使得输出结果更易于验证，也更加可信。

Citations is generally available on the Anthropic API and Google Cloud's Vertex AI.

引用功能通常可以在 Anthropic API 和 Google Cloud 的 Vertex AI 上使用。

### 01. Trust by verification

通过验证来增强可信度

All Claude models are trained to be trustworthy and steerable by design. Citations builds upon this foundation, addressing a specific need in AI applications: verifying the sources behind AI-generated responses.

所有 Claude 模型在设计之初就被训练成具有高可靠性和可控性。引用（Citations）功能在此基础上更进一步，解决了 AI 应用中的一个特殊需求：验证 AI 生成内容的信息来源。

Previously, developers relied on complex prompts that instruct Claude to include source information, often resulting in inconsistent performance and significant time investment in prompt engineering and testing. With Citations, users can now add source documents to the context window, and when querying the model, Claude automatically cites claims in its output that are inferred from those sources.

过去，开发者们需要依赖复杂的提示（prompts）来指示 Claude 引用来源信息，但这样做常常导致性能不稳定，并且需要在提示工程（prompt engineering）和测试上花费大量时间。现在，有了 Citations 功能，用户可以将源文档添加到上下文窗口（context window）中。在查询模型时，Claude 会自动在其输出中标明引用的来源，这些引用都来自用户提供的文档。

Our internal evaluations show that Claude's built-in citation capabilities outperform most custom implementations, increasing recall accuracy by up to 15%.1

我们内部的评估显示，Claude 自带的引用功能比大多数用户自行开发的方案表现更出色，能够将召回准确率提升高达 15%。1

### 02. Use cases

用例

With Citations, developers can create AI solutions that offer enhanced accountability across use cases like:

通过引用（Citations），开发者可以创建 AI 解决方案，在如下应用场景中提供更强的责任追踪能力：

1 Document summarization: Generate concise summaries of long documents, like case files, with each key point linked back to its original source.

文档摘要：生成长文档（例如案件材料）的精炼摘要，并将每个要点链接回原始出处。

2 Complex Q&A: Provide detailed answers to user queries across a large corpus of documents, like financial statements, with each response element traced back to specific sections of relevant texts.

复杂问答：能够回答用户提出的复杂问题，答案的来源是大量的文档资料，例如财务报表。更重要的是，答案的每一个细节都能追溯到相关文本的具体章节。

3 Customer support: Create support systems that can answer complex queries by referencing multiple product manuals, FAQs, and support tickets, always citing the exact source of information.

客户支持：构建支持系统，该系统能够通过参考多份产品手册、常见问题（FAQ）和支持工单，回答复杂的客户咨询，并始终注明信息的准确来源。

### 03. How it works

工作原理

When Citations is enabled, the API processes user-provided source documents (PDF documents and plain text files) by chunking them into sentences. These chunked sentences, along with user-provided context, are then passed to the model with the user's query. Alternatively, users can provide their own chunks for the source documents.

当启用 Citations 功能后，API 会对用户提供的原始文档（PDF 文档和纯文本文件）进行处理，具体方法是将文档拆分成多个句子。这些拆分后的句子，以及用户提供的相关背景信息，会连同用户的查询一同发送给模型。此外，用户也可以选择自行划分原始文档的内容块。

Claude analyzes the query and generates a response that includes precise citations based on the provided chunks and context for any claims derived from the source material. Cited text will reference source documents to minimize hallucinations.

Claude 分析查询，并生成包含精确引用的回复。这些引用基于所提供的文本块（chunk）和上下文，针对所有源自原始材料的主张。引用的文本将参考源文档，从而最大限度地减少「幻觉」(hallucination）现象。

This approach offers superior flexibility and ease of use, as it doesn't require file storage and seamlessly integrates with the Messages API.

这种方案具有更出色的灵活性和易用性，因为它无需文件存储，并且能够与消息 API（Messages API）无缝集成。

### 04. Pricing

定价

Citations uses our standard token-based pricing model. While it may use additional input tokens to process documents, users will not pay for output tokens that return the quoted text itself.

引文功能采用我们标准的基于 Token（Token）的定价模型。虽然它可能会使用额外的输入 Token 来处理文档，但用户不需要为返回的引文内容支付额外的输出 Token 费用。

### 05. Customer spotlight: Thomson Reuters

客户聚焦：Thomson Reuters

Thomson Reuters uses Claude to power their AI platform, CoCounsel, helping legal and tax professionals synthesize expert knowledge and deliver comprehensive advice to clients.

Thomson Reuters 利用 Claude 来驱动其 AI 平台 CoCounsel，助力法律和税务专业人士整合专业知识，为客户提供更全面的咨询服务。

"For CoCounsel to be trustworthy and immediately useful for practicing attorneys, it needs to cite its work. We first built this ourselves, but it was really hard to build and maintain. That's why we were excited to test out Anthropic's Citations functionality. It makes citing and linking to primary sources much easier to build, maintain, and deploy to our users. This capability not only helps minimize hallucination risk but also strengthens trust in AI-generated content. The Citations feature will enable us to build an even more accurate and thorough AI assistant for lawyers," said Jake Heller, Head of Product, CoCounsel, Thomson Reuters.

「为了让 CoCounsel 对执业律师来说值得信赖且能快速上手，它需要提供参考文献。我们最初尝试自主开发这一功能，但发现构建和维护都异常困难。因此，我们很高兴能测试 Anthropic 公司的 Citations 功能。该功能使得引用和链接到原始资料变得更容易构建、维护并部署给我们的用户。这项能力不仅有助于最大限度地降低（大语言模型）的幻觉风险（hallucination risk），还能增强人们对 AI 生成内容的信任。Citations 功能将助力我们为律师们打造一个更加精准和完善的 AI 助手，」Thomson Reuters 旗下 CoCounsel 的产品负责人 Jake Heller 说道。

### Customer Spotlight: Endex

客户聚焦：Endex

Endex uses Claude to power an Autonomous Agent for financial firms.

Endex 使用 Claude 为金融公司提供 AI 智能体（Autonomous Agent）的支持。

"With Anthropic's Citations, we reduced source hallucinations and formatting issues from 10% to 0% and saw a 20% increase in references per response. This removed the need for elaborate prompt engineering around references and improved our accuracy when conducting complex, multi-stage financial research," said Tarun Amasa, CEO, Endex.

「借助 Anthropic 的 Citations 功能，我们将来源方面的幻觉（hallucinations）和格式问题从 10% 降低到 0%，并且每次回复的参考文献数量增加了 20%。这消除了围绕参考文献进行复杂提示工程（prompt engineering）的需求，提示工程是指为了获得期望的输出结果而进行的精细化提示语设计。同时，也提高了我们在进行复杂、多阶段金融研究时的准确性，」Endex 首席执行官 Tarun Amasa 说道。

### Get started

Citations is now available for the new Claude 3.5 Sonnet and Claude 3.5 Haiku. To start using Citations, explore our documentation.

引文功能现已支持最新的 Claude 3.5 Sonnet 和 Claude 3.5 Haiku 模型。想开始使用引文功能？请查阅我们的相关文档。

[Citations - Anthropic](https://docs.anthropic.com/en/docs/build-with-claude/citations)

```py
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=1024,
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "type": "document",
                    "source": {
                        "type": "text",
                        "media_type": "text/plain",
                        "data": "The grass is green. The sky is blue."
                    },
                    "title": "My Document",
                    "context": "This is a trustworthy document.",
                    "citations": {"enabled": True}
                },
                {
                    "type": "text",
                    "text": "What color is the grass and sky?"
                }
            ]
        }
    ]
)
print(response)
```

#### Footnotes

[1] Our evaluations compared the Citations feature against prompt-based approaches described in our prompt library and cookbooks.

[2](https://twitter.com/intent/tweet?text=https://www.anthropic.com/news/introducing-citations-api)

[3](https://www.linkedin.com/shareArticle?mini=true&url=https://www.anthropic.com/news/introducing-citations-api)