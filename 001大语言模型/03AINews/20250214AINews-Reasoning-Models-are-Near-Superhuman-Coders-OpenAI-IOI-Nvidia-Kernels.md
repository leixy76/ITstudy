## 20250214AINews-Reasoning-Models-are-Near-Superhuman-Coders-OpenAI-IOI-Nvidia-Kernels

[[AINews] Reasoning Models are Near-Superhuman Coders (OpenAI IOI, Nvidia Kernels) • Buttondown](https://buttondown.com/ainews/archive/ainews-reasoning-models-are-near-superhuman/)

This is AI News! an MVP of a service that goes thru all AI discords/Twitters/reddits and summarizes what people are talking about, so that you can keep up without the fatigue. Signing up here opts you in to the real thing when we launch it

这是 AI 新闻！一个最小可行产品（MVP）的服务，它会浏览所有关于 AI 的 Discord/Twitter/Reddit 频道，并总结人们正在讨论的内容，让你在不感到疲劳的情况下也能掌握最新动态。现在注册，当我们的正式产品上线时，您将成为首批用户。

"Wait" is all you need.

AI News for 2/5/2025-2/6/2025. We checked 7 subreddits, 433 Twitters and 29 Discords (210 channels, and 4396 messages) for you. Estimated reading time saved (at 200wpm): 490 minutes. You can now tag @smol_ai for AINews discussions!

「稍安勿躁」，精彩马上呈现。

以下是 2025 年 2 月 5 日到 6 日的 AI 新闻摘要。我们为你搜罗了 7 个 Reddit 子版块（subreddit，一种在线社区）、433 个 Twitter 账号和 29 个 Discord 服务器（包含 210 个频道，共计 4396 条消息）。据估算，这能为你节省大约 490 分钟的阅读时间（按每分钟阅读 200 字计算）。现在，你可以通过 @smol_ai 标签来参与 AINews 相关讨论了！

We're regrettably late to covering this paper, but late is better than never. s1: Simple test-time scaling documents a new reasoning model with 2 novel contributions:

未找到意译内容

finetuned from Qwen 2.5 32B on just 1000 questions paired with reasoning traces distilled from Gemini 2.0 Flash Thinking, filtered for difficulty, diversity, and quality (26 mins of training on 16 H100s)
controllable test-time compute by either forcefully terminating the model's thinking process or lengthening it by appending "Wait" multiple times to the model's generation when it tries to end.
Lead author Niklas Muennighoff, who notably worked on Bloom, StarCoder, MTEB, and contributed to BIG-bench, notes that this second trick reproduces the famous o1 scaling chart:

未找到意译内容

[AINews] Reasoning Models are Near-Superhuman Coders (OpenAI IOI, Nvidia Kernels)

RL is all you need.

[AINews] 推理模型正逼近超人类程序员的水平（OpenAI IOI，Nvidia Kernels)

强化学习（RL）足以解决所有问题。

AI News for 2/12/2025-2/13/2025. We checked 7 subreddits, 433 Twitters and 29 Discords (211 channels, and 5290 messages) for you. Estimated reading time saved (at 200wpm): 554 minutes. You can now tag @smol_ai for AINews discussions!

AI 新闻，2025 年 2 月 12 日 - 2025 年 2 月 13 日。我们为您检索了 7 个 subreddit、433 个 Twitter 以及 29 个 Discord（包含 211 个频道和 5290 条消息）。据估算，这能为您节省 554 分钟的阅读时间（按每分钟阅读 200 字计算）。欢迎使用 @smol_ai 标签来参与 AINews 的相关讨论！

This is a rollup of two distinct news items with nevertheless the same theme:

o3 achieves a gold medal at the 2024 IOI and obtains a Codeforces rating on par with elite human competitors - in particular, the Codeforces score is at the 99.8-tile - only 199 humans are better than o3. Notably, team member Alex Wei noted that all the "inductive bias" methods also failed compared to the RL bitter lesson. image.png

未找到意译内容

In Automating GPU Kernel Generation with DeepSeek-R1 and Inference Time Scaling, Nvidia found that DeepSeek r1 could write custom kernels that "turned out to be better than the optimized kernels developed by skilled engineers in some cases" image.png

在 Nvidia 的一篇关于使用 DeepSeek-R1 自动化 GPU 内核生成和推理时间缩放的论文中，他们发现 DeepSeek r1 能够编写自定义内核，并且「在某些情况下，其性能甚至优于由经验丰富的工程师开发的优化内核」image.png（此为论文中的截图）。

In the Nvidia case, the solution was also extremely simple, causing much consternation. image.png

The Table of Contents and Channel Summaries have been moved to the web version of this email: [AINews] Reasoning Models are Near-Superhuman Coders (OpenAI IOI, Nvidia Kernels)!

在英伟达的案例中，解决方案也极其简单，令人大跌眼镜。image.png

目录和频道摘要已移动到该邮件的网络版本中：[AINews] 推理模型接近超人程序员（OpenAI IOI，Nvidia Kernels)!

AI Twitter Recap

AI Tools and Resources

未找到意译内容

OpenAI Updates on o1, o3-mini, and DeepResearch: OpenAI announced that o1 and o3-mini now support both file & image uploads in ChatGPT. Additionally, DeepResearch is now available to all Pro users on mobile and desktop apps, expanding accessibility.

OpenAI 发布 o1、o3-mini 和 DeepResearch 的更新：OpenAI 宣布 o1 和 o3-mini 现在在 ChatGPT 中支持文件和图片上传功能。此外，DeepResearch 现已向所有 Pro 用户开放，可在移动和桌面应用中使用，提升了易用性。

Distributing Open Source Models Locally with Ollama: @ollama discusses distributing and running open source models for developers locally, highlighting it's complementary to hosted OpenAI models.

使用 Ollama 在本地部署开源模型：@ollama 探讨了如何为开发者在本地分发和运行开源模型，并强调这与 OpenAI 提供的云端托管模型形成互补关系。

'Deep Dive into LLMs' by @karpathy: @TheTuringPost shares a free 3+ hour video by @karpathy exploring how AI models like ChatGPT are built, including topics like pretraining, post-training, reasoning, and effective model use.

「深入研究大语言模型」——@karpathy：@TheTuringPost 分享了 @karpathy 制作的免费视频，时长超过 3 小时。视频探讨了 ChatGPT 等 AI 模型是如何构建的，内容涵盖预训练（pretraining）、指令微调（post-training）、推理（reasoning）以及如何有效地使用这些模型。

ElevenLabs' Journey in AI Voice Synthesis: @TheTuringPost details how @elevenlabsio evolved from a weekend project to a $3.3 billion company, offering AI-driven TTS, voice cloning, and dubbing tools without open-sourcing.

ElevenLabs 的 AI 语音合成之旅：@TheTuringPost 详细介绍了 @elevenlabsio 是如何从一个周末小项目成长为一家价值 33 亿美元的公司的。该公司提供由 AI 驱动的 TTS（Text-to-Speech，文本转语音）、语音克隆和配音工具，但并没有选择开源。

DeepResearch from OpenAI as a Mind-blowing Research Assistant: @TheTuringPost reviews DeepResearch from OpenAI, a virtual research assistant powered by a powerful o3 model with RL engineered for deep chain-of-thought reasoning, highlighting its features and benefits.

[OpenAI 的 DeepResearch：令人惊艳的科研助手：@TheTuringPost 对 OpenAI 的 DeepResearch 进行了评测。DeepResearch 是一款虚拟科研助手，它由强大的 o3 模型驱动，并采用了强化学习（RL）技术，能够进行深度链式思考推理。评测着重介绍了 DeepResearch 的各项特性和优势。]

Release of OpenThinker Models: @ollama announces OpenThinker models, fine-tuned from Qwen2.5, that surpass DeepSeek-R1 distillation models on some benchmarks.

AI Research Advances

OpenThinker 模型发布：@ollama 发布了 OpenThinker 模型，这些模型基于 Qwen2.5 进行微调，并在某些基准测试中表现优于 DeepSeek-R1 蒸馏模型。

AI 研究新进展

DeepSeek R1 Generates Optimized Kernels: @abacaj reports that they put R1 in a loop for 15 minutes, resulting in code "better than the optimized kernels developed by skilled engineers" in some cases.

DeepSeek R1 生成优化后的内核：@abacaj 报告称，他们让 R1 循环运行 15 分钟，在某些情况下生成的代码「优于经验丰富的工程师开发的优化内核（kernel）」。

Importance of Open-source AI for Scientific Discovery: @stanfordnlp emphasizes that failure to invest in open-source AI could hinder scientific discovery in western universities that cannot afford closed models.

开源 AI 对于科学发现的重要性：正如 @stanfordnlp 所强调的，如果不在开源 AI 上进行投入，可能会阻碍西方大学的科学发现，原因在于这些大学可能难以承担使用闭源模型的成本。

Sakana AI Labs' 'TAID' Paper Receives Spotlight at ICLR2025: @SakanaAILabs announces their new knowledge distillation method 'TAID' has been awarded a Spotlight (Top 5%) at ICLR2025.

Sakana AI Labs 的 'TAID' 论文在 ICLR2025 大会上备受瞩目：@SakanaAILabs 宣布他们新的知识蒸馏方法 'TAID'（全称待补充）已在 ICLR2025 上获得 Spotlight 展示（Top 5%）。

Apple's Research on Scaling Laws: @awnihannun highlights two recent papers from Apple on scaling laws for MoEs and knowledge distillation, contributed by @samira_abnar, @danbusbridge, and others.

未找到意译内容

AI Infrastructure and Efficiency

Advocating Data Centers over Mobile for AI Compute: @JonathanRoss321 argues that running AI on mobile devices is less energy-efficient compared to data centers, using analogies to illustrate the efficiency differences.

[AI 基础设施和效率相比于移动设备，更推荐使用数据中心进行 AI 计算：@JonathanRoss321 认为，相比于数据中心，在移动设备上运行 AI 的能效比更低，并通过类比来解释这种效率上的差异。]

AI Security and Safety

Vulnerabilities in AI Web Agents Exposed: @micahgoldblum demonstrates how adversaries can fool AI web agents like Anthropic's Computer Use into sending phishing emails or revealing credit card info, highlighting the brittleness of underlying LLMs.

AI 安全与保障

AI Web 智能体中暴露的漏洞：研究员 @micahgoldblum 演示了攻击者如何欺骗 AI Web 智能体，例如 Anthropic 公司的「Computer Use」功能（让 AI 使用计算机），使其发送网络钓鱼邮件或泄露信用卡信息，突显了其底层大语言模型的安全性不足。

Meta's Automated Compliance Hardening (ACH) Tool: @AIatMeta introduces their ACH tool that hardens platforms against regressions with LLM-based test generation, enhancing compliance and security.

Meta 的自动化合规性强化（Automated Compliance Hardening，ACH）工具：@AIatMeta 推出了他们的 ACH 工具。该工具利用基于大语言模型（LLM）的测试生成技术来强化平台，防止出现功能退化（regression），从而增强平台的合规性和安全性。

AI Governance and Policy

Insights from the France Action Summit: @sarahookr shares observations from the France Action Summit, noting that such summits are valuable as catalysts for important AI discussions and emphasizing the importance of understanding national efforts and scientific progress.

人工智能治理与政策法国行动峰会的启示：@sarahookr 分享了她在法国行动峰会上的观察，她认为此类峰会能够推动重要的人工智能（AI）讨论，具有重要价值。同时，她还强调了深入了解各国在人工智能领域的投入和科研进展的重要性。

Shifting from 'AI Safety' to 'Responsible AI': @AndrewYNg advocates for changing the conversation away from 'AI safety' towards 'responsible AI', arguing that it will speed up AI's benefits and better address actual problems without hindering development.

从「AI 安全（AI Safety）」转向「负责任的 AI（Responsible AI）」：@AndrewYNg 倡导将讨论的焦点从「AI 安全」转移到「负责任的 AI」，他认为这能够更快地发挥 AI 的优势，更好地应对实际问题，同时也不会妨碍 AI 技术的发展。

Memes/Humor

'Rizz GPT' and Social Challenges Post-Lockdown: @andersonbcdefg humorously comments on how zoomers are building versions of 'Rizz GPT' because their brains are damaged from lockdown and they don't know how to have normal conversations.

Memes / 幽默

「Rizz GPT」和疫情封锁后的社交难题：@andersonbcdefg 幽默地评论说，Z 世代正在开发各种「Rizz GPT」版本，因为疫情封锁可能对他们（的大脑）造成了影响，导致他们不太擅长正常的社交对话。「Rizz」可以理解为一种魅力或吸引力，"Rizz GPT」大概就是指能够生成有魅力回复的 AI。

'Big Day for Communicable Diseases': @stevenheidel posts a cryptic message stating it's a "big day for communicable diseases", adding a touch of humor.

AI Reddit Recap

' 传染性疾病的大日子 '：@stevenheidel 发布了一条神秘消息，称这是「传染病防治的重要日子」，带点玩笑的意味。

AI Reddit 回顾

/r/LocalLlama Recap

Theme 1. Google's FNet: Potential for Improved LLM Efficiency via Fourier Transforms

/r/LocalLlama 社区精选主题 1. 谷歌的 FNet：利用傅里叶变换提升大语言模型效率的潜力

This paper might be a breakthrough Google doesn't know they have (Score: 362, Comments: 24): The FNet paper from 2022 explores using Fourier Transforms to mix tokens, suggesting potential major efficiency gains in model training. The author speculates that replicating this approach or integrating it into larger models could lead to a 90% speedup and memory reduction, presenting a significant opportunity for advancements in AI model efficiency.

这篇论文可能是一项 Google 尚未察觉的突破性成果（得分：362，评论：24)：2022 年的 FNet 论文探索了使用傅里叶变换来混合 Token（Token），表明在模型训练中可能实现显著的效率提升。作者推测，复制这种方法或将其集成到更大的模型中，可能会带来 90% 的速度提升和内存减少，为提升 AI 模型效率提供了一个重要的机会。

Efficiency and Convergence Challenges: Users reported that while FNet worked, it was less effective than traditional attention mechanisms, particularly in small models, and faced significant convergence issues. This raises doubts about its scalability and efficacy in larger models.

效率和收敛性挑战：用户报告说，虽然 FNet 能够运行，但它不如传统的注意力机制（Attention Mechanism）有效，尤其是在小型模型中，并且面临着显著的收敛问题。这引发了人们对它在大型模型中的可扩展性和有效性的担忧。

Alternative Approaches and Comparisons: Discussions mentioned alternative models like Holographic Reduced Representations (Hrrformer), which claims superior performance with less training, and M2-BERT, which shows greater accuracy on benchmarks. These alternatives highlight the complexity of evaluating trade-offs between training speed, accuracy, and generalization.

替代方法与比较： 文中讨论了一些替代模型，例如声称能够以更少训练获得更优性能的全息降维表示（Hrrformer），以及在基准测试中表现出更高准确性的 M2-BERT。这些替代方案凸显了评估训练速度、准确性和泛化能力之间权衡的复杂性。

Integration and Implementation: The FNet code is available on GitHub, but its integration with existing models like transformers is non-trivial due to its implementation in JAX. Users discussed potential hybrid approaches, such as creating variants like fnet-llama or fnet-phi, to explore differences in performance and hallucination tendencies.

集成与实现：FNet 的代码已在 GitHub 上开源，但由于其使用了 JAX 框架实现，因此与现有的 Transformer 等模型集成并非易事。一些开发者讨论了潜在的混合方案，例如创建 fnet-llama 或 fnet-phi 等变体，以探索它们在性能和产生幻觉方面的差异。

Theme 2. DIY High-Performance Servers for 70B LLMs: Strategies and Cost

Who builds PCs that can handle 70B local LLMs? (Score: 108, Comments: 160): Building a home server capable of running 70B parameter local LLMs is discussed, with a focus on using affordable, older server hardware to maximize cores, RAM, and GPU RAM. The author inquires if there are professionals or companies that specialize in assembling such servers, as they cannot afford the typical $10,000 to $50,000 cost for high-end GPU-equipped home servers.

主题 2. 用于 70B 大语言模型的 DIY 高性能服务器：策略与成本有哪些人自己动手组装可以运行 70B 大语言模型的 PC？（得分：108，评论：160)： 本文讨论了如何构建一台能够运行 700 亿参数的大语言模型（LLM）的家庭服务器，重点在于使用经济实惠的旧服务器硬件，尽可能增加内核数量、内存（RAM）和 GPU 显存（GPU RAM）。作者想知道是否有专业人士或公司专门提供组装此类服务器的服务，因为他们无法承担配备高端 GPU 的家庭服务器通常 1 万到 5 万美元的成本。

Building a home server for 70B parameter LLMs can be achieved for under $3,000 using components like an Epyc 7532, 256GB RAM, and MI60 GPUs, as suggested by Psychological_Ear393. Some users like texasdude11 have shared setups using dual NVIDIA 3090s or P40 GPUs for efficient performance, providing detailed guides and YouTube videos for assembly and operation.

正如 Psychological_Ear393 建议的那样，使用 Epyc 7532 处理器、256GB 内存和 MI60 GPU 等组件，花费不到 3,000 美元就能构建一台运行 700 亿参数大语言模型（LLM/Large Language Model）的家用服务器。一些用户，例如 texasdude11，分享了他们使用双 NVIDIA 3090 或 P40 GPU 获得高效性能的配置方案，并提供了详细的组装和使用指南以及 YouTube 视频。

The NVIDIA A6000 GPU is highlighted for its speed and capability in running 70B models; however, it is costly at around $5,000. Alternatives include setups with multiple RTX 3090 or 3060 GPUs, with users like Dundell and FearFactory2904 suggesting cost-effective builds using second-hand components.

NVIDIA A6000 GPU 因其快速运行 70B 模型的能力而引人关注，但价格昂贵，大约为 5,000 美元。另一种选择是使用多个 RTX 3090 或 3060 GPU 搭建系统。Dundell 和 FearFactory2904 等用户建议使用二手零件，以更经济的方式构建。

Users discuss the viability of using Macs, particularly M1 Ultra with 128GB RAM, for running 70B models efficiently, especially for chat applications, as noted by synn89. Future potential options include waiting for Nvidia Digits or AMD Strix Halo, which may offer better performance for home inference tasks.

用户正在讨论使用 Mac 电脑，特别是配备 128GB 内存的 M1 Ultra 芯片的 Mac，来高效运行 70B（700 亿参数）大语言模型的可行性，尤其是在聊天应用中。正如用户 synn89 指出的那样，这引发了广泛关注。此外，未来的潜在选择还包括等待 Nvidia Digits 或 AMD Strix Halo，它们或许能为本地推理提供更优异的性能。

Theme 3. Gemini2.0's Dominance in OCR Benchmarking and Context Handling

Gemini beats everyone is OCR benchmarking tasks in videos. Full Paper : https://arxiv.org/abs/2502.06445 (Score: 114, Comments: 26): Gemini-1.5 Pro excels in OCR benchmarking tasks for videos, achieving a Character Error Rate (CER) of 0.2387, Word Error Rate (WER) of 0.2385, and an Average Accuracy of 76.13%. Despite GPT-4o having a slightly higher overall accuracy at 76.22% and the lowest WER, Gemini-1.5 Pro is highlighted for its superior performance compared to models like RapidOCR and EasyOCR. Full Paper

主题 3. Gemini2.0 在光学字符识别（OCR）基准测试和上下文处理中的优势

Gemini 在视频的光学字符识别（OCR）基准测试任务中表现卓越，超越了所有其他模型。完整论文：https://arxiv.org/abs/2502.06445（分数：114，评论：26)：在视频 OCR 基准测试中，Gemini-1.5 Pro 表现出色，其字符错误率（CER）为 0.2387，词错误率（WER）为 0.2385，平均准确率达到 76.13%。尽管 GPT-4o 的总体准确率稍高，为 76.22%，并且具有最低的 WER，Gemini-1.5 Pro 仍然因其超越 RapidOCR 和 EasyOCR 等模型的卓越性能而备受关注。完整论文

RapidOCR is noted as a fork of PaddleOCR, with minimal expected deviation in scores from its origin. There is interest in exploring direct PDF processing capabilities using Gemini-1.5 Pro, with a link provided for implementation on Google Cloud Vertex AI here.

RapidOCR 被认为是 PaddleOCR 的一个分支，预期其得分与原始版本几乎没有差别。我们有兴趣探索使用 Gemini-1.5 Pro 直接处理 PDF 文件的能力，这里提供了一个在 Google Cloud Vertex AI 上实现的链接。

Users express a need for OCR benchmarking to include handwriting recognition, with Azure FormRecognizer praised for handling cursive text. A user reported that Gemini 2.0 Pro performed exceptionally well on Russian handwritten notes compared to other language models.

用户提出，光学字符识别（OCR）的基准测试应该纳入手写识别能力。其中，Azure FormRecognizer 因为能够出色地识别草书字体而广受好评。有用户反馈，相较于其他大语言模型，Gemini 2.0 Pro 在处理俄语手写笔记时表现尤为突出。

There is a call for broader comparisons across multiple languages and models, including Gemini 2, Tesseract, Google Vision API, and Azure Read API. Despite some frustrations with Gemini's handling of simple tasks, users acknowledge its advancements in visual labeling, and Moondream is highlighted as a promising emerging model, with plans to add it to the OCR benchmark repository.

现在需要对多种语言和多种模型进行更广泛的比较，包括 Gemini 2、Tesseract、Google Vision API 和 Azure Read API。尽管 Gemini 在处理简单任务时会让用户感到有些沮丧，但大家也认可其在视觉标签方面的进步。Moondream 模型作为一个很有潜力的新兴模型，受到了特别关注，并且计划将其添加到光学字符识别（OCR，Optical Character Recognition）的评测基准库中。

NoLiMa: Long-Context Evaluation Beyond Literal Matching - Finally a good benchmark that shows just how bad LLM performance is at long context. Massive drop at just 32k context for all models. (Score: 402, Comments: 75): The NoLiMa benchmark highlights significant performance degradation in LLMs at long context lengths, with a marked drop at just 32k tokens across models like GPT-4, Llama, Gemini 1.5 Pro, and Claude 3.5 Sonnet. The graph and table show that scores fall below 50% of the base score at these extended lengths, indicating substantial challenges in maintaining performance with increased context.

NoLiMa：超越字面匹配的长文本评估 - 终于出现了一个优秀的基准，揭示了大语言模型（LLM/Large Language Model）在处理长文本时表现不佳的现状。所有模型在 32k Token 的上下文长度下，性能均出现显著下降（得分：402，评论：75）。NoLiMa 基准测试表明，大语言模型在处理长文本时性能会明显降低，例如 GPT-4、Llama、Gemini 1.5 Pro 和 Claude 3.5 Sonnet 等模型，在 32k Token 长度时就已出现性能断崖式下跌。图表显示，在更长的文本长度下，这些模型的得分甚至低于其初始分数的 50%，表明大语言模型在扩展上下文长度时，维持性能面临着巨大的挑战。

Degradation and Benchmark Comparisons: The NoLiMa benchmark shows substantial performance degradation in LLMs like llama3.1-70B, which scores 43.2% at 32k context length compared to 94.8% on RULER. This benchmark is considered more challenging than previous ones like LongBench, which focuses on multiple-choice questions and doesn't fully capture performance degradation across context lengths.

退化和基准比较：NoLiMa 基准测试显示，像 llama3.1-70B 这样的大语言模型（LLM）性能显著退化，在 32k 上下文长度下，NoLiMa 基准测试的得分是 43.2%，而 RULER 基准测试的得分是 94.8%。这个基准被认为比以前的基准，如 LongBench 更具挑战性，后者侧重于多项选择题，并且无法全面评估不同上下文长度下的性能退化。

Model Performance and Architecture Concerns: There's significant discussion on how reasoning models like o1/o3 handle long contexts, with some models performing poorly on hard subsets of questions. The limitations of current architectures, such as the quadratic complexity of attention mechanisms, are highlighted as a barrier to maintaining performance over long contexts, suggesting a need for new architectures like RWKV and linear attention.

模型性能与架构考量：关于 o1/o3 这类推理模型如何处理长文本信息，业界存在大量讨论，部分模型在面对难题时表现不佳。当前模型架构存在局限性，例如注意力机制（attention mechanisms）的二次复杂度，成为维持长文本性能的瓶颈。因此，我们需要 RWKV、线性注意力（linear attention）等新架构来突破限制。

Future Model Testing and Expectations: Participants express interest in testing newer models like Gemini 2.0-flash/pro and Qwen 2.5 1M, hoping for improved performance in long-context scenarios. There's skepticism about claims of models handling 128k tokens effectively, with some users emphasizing that practical applications typically perform best with contexts under 8k tokens.

未来模型测试与期望：参与者们表示，他们有兴趣测试更新的模型，例如 Gemini 2.0-flash/pro 和 Qwen 2.5 1M，并期望这些模型在长上下文场景下能有更好的性能表现。对于某些模型声称可以有效处理 128k 个 Token（tokens）的说法，人们持怀疑态度，一些用户强调，在实际应用中，通常上下文长度低于 8k 个 Token 时，模型的表现才是最好的。

Theme 4. Innovative Architectural Insights from DeepSeek: Expert Mixtures and Token Predictions

Let's build DeepSeek from Scratch | Taught by MIT PhD graduate (Score: 245, Comments: 28): An MIT PhD graduate is launching a comprehensive educational series on building DeepSeek's architecture from scratch, focusing on foundational elements such as Mixture of Experts (MoE), Multi-head Latent Attention (MLA), Rotary Positional Encodings (RoPE), Multi-token Prediction (MTP), Supervised Fine-Tuning (SFT), and Group Relative Policy Optimisation (GRPO). The series, consisting of 35-40 in-depth videos totaling over 40 hours, aims to equip participants with the skills to independently construct DeepSeek's components, positioning them among the top 0.1% of ML/LLM engineers.

主题 4. 来自 DeepSeek 的创新架构见解：混合专家模型与 Token 预测让我们从零开始构建 DeepSeek | 由麻省理工学院博士毕业生授课（得分：245，评论：28)：一位麻省理工学院博士毕业生正在启动一个综合教育系列，该系列旨在从零开始构建 DeepSeek 的架构，重点关注以下基础要素：混合专家模型（Mixture of Experts，MoE）、多头潜在注意力机制（Multi-head Latent Attention，MLA）、旋转位置编码（Rotary Positional Encodings，RoPE）、多 Token 预测（Multi-token Prediction，MTP）、监督微调（Supervised Fine-Tuning，SFT）和组相对策略优化（Group Relative Policy Optimisation，GRPO）。该系列包含 35-40 个深度视频，总时长超过 40 小时，旨在使参与者掌握独立构建 DeepSeek 各个组件的技能，从而成为顶尖的 ML / 大语言模型工程师。

Skepticism about Credentials: Some users express skepticism about the emphasis on prestigious credentials like MIT, suggesting that the content's quality should stand on its own without relying on the author's background. There's a call for content to be judged independently of the creator's academic or professional affiliations.

对资历的怀疑： 一些用户对内容创作者强调其麻省理工学院（MIT）等名校背景的做法表示怀疑，认为内容质量本身应该足够优秀，不应依赖于作者的资历。大家希望根据内容本身来判断其价值，而不是看创作者的学术或专业背景。

Missing Technical Details: A significant point of discussion is the omission of Nvidia's Parallel Thread Execution (PTX) as a cost-effective alternative to CUDA in the series, highlighting a perceived gap in addressing DeepSeek's efficiency and cost-effectiveness. This suggests that understanding the technical underpinnings, not just the capabilities, is crucial for appreciating DeepSeek's architecture.

遗漏的技术细节：一个重要的讨论点是，该系列文章忽略了英伟达（Nvidia）的并行线程执行（Parallel Thread Execution，PTX），认为它本可以作为 CUDA 的一种更经济高效的替代方案。这一点暴露了文章在分析 DeepSeek 的效率和成本效益时存在的明显不足。这表明，要真正理解 DeepSeek 的架构，不仅要了解它的能力，更要深入理解其背后的技术原理。

Uncertainty about Computing Power: There is contention regarding the actual computing power used in DeepSeek's development, with some users criticizing speculative figures circulating online. The discussion underscores the importance of accurate data, particularly regarding resources like datasets and computing power, in understanding and replicating AI systems.

计算能力之谜：关于 DeepSeek 在研发过程中究竟使用了多少计算资源，各方说法不一，一些用户对在网络上流传的各种猜测性数据提出了质疑。这场讨论凸显了获取准确数据的重要性，尤其是在数据集和计算能力这类关键资源上，这对于理解和复现 AI 系统至关重要。

Other AI Subreddit Recap

/r/Singularity, /r/Oobabooga, /r/MachineLearning, /r/OpenAI, /r/ClaudeAI, /r/StableDiffusion, /r/ChatGPT

其他 AI 相关 Reddit 子版块精选以下是一些与 AI 相关的热门 Reddit 子版块，涵盖了奇点、本地大语言模型部署、机器学习研究、OpenAI、ClaudeAI、Stable Diffusion 等主题：

/r/Singularity，/r/Oobabooga，/r/MachineLearning，/r/OpenAI，/r/ClaudeAI，/r/StableDiffusion，/r/ChatGPT

Theme 1. OpenAI merges o3 into unified GPT-5

OpenAI cancels its o3 AI model in favor of a ‘unified' next-gen release (Score: 307, Comments: 66): OpenAI has decided to cancel its o3 AI model project, opting instead to focus on developing a unified next-generation release with GPT-5. The strategic shift suggests a consolidation of resources and efforts towards a single, more advanced AI model.

主题 1. OpenAI 将 o3 合并到统一的 GPT-5 中

OpenAI 取消 o3 AI 模型，转而支持「统一的」下一代版本（得分：307，评论：66)：OpenAI 决定取消 o3 AI 模型项目，转而专注于开发统一的、基于 GPT-5 的下一代版本。这一战略转变表明，OpenAI 正在将资源和精力集中投入到开发单一的、更先进的 AI 模型中。

There is a significant debate around whether OpenAI's move to integrate the o3 model into GPT-5 represents progress or a lack of innovation. Some users argue that this integration is a strategic simplification aimed at usability, while others see it as a sign of stagnation in model development, with DeepSeek R1 being cited as a competitive free alternative.

关于 OpenAI 将 o3 模型整合到 GPT-5 中，这究竟是进步还是缺乏创新，目前存在着激烈的争论。一部分用户认为，这种整合是一种战略上的简化，目的是为了提升用户体验，使其更加便捷。而另一部分人则认为，这表明 OpenAI 在模型开发上已经停滞不前，并指出 DeepSeek R1 是一个具有竞争力的免费替代方案。

Many commenters express concern over the loss of user control with the automatic model selection approach, fearing it may lead to suboptimal results. Users like whutmeow and jjjiiijjjiiijjj prefer manual model selection, worried that algorithmic decisions may prioritize company costs over user needs.

许多评论员都对自动模型选择带来的用户控制权降低表示担忧，他们害怕这会导致不够理想的结果。像 whutmeow 和 jjjiiijjjiiijjj 这样的用户更喜欢手动选择模型，他们担心算法的决策可能会优先考虑公司的成本，而忽略用户的需求。

The discussion also highlights confusion over the terminology used, with several users correcting the notion that o3 is canceled, clarifying instead that it is being integrated into GPT-5. This has led to concerns about misleading headlines and the potential implications for OpenAI's strategic direction and leadership.

讨论中，大家对于使用的术语也存在一些困惑，有用户指出，所谓 o3 被「取消」的说法并不准确，更准确的说法是它将被整合到 GPT-5 中。这引发了人们对具有误导性的新闻标题的担忧，以及对 OpenAI 的战略方向和领导层可能产生的影响。

Altman said the silent part out loud (Score: 126, Comments: 59): Sam Altman announced that Orion, initially intended to be GPT-5, will instead launch as GPT-4.5, marking it as the final non-CoT model. Reports from Bloomberg, The Information, and The Wall Street Journal indicate that GPT-5 has faced significant challenges, showing less improvement over GPT-4 than its predecessor did. Additionally, the o3 model will not be released separately but will integrate into a unified system named GPT-5, likely due to the high operational costs revealed by the ARC benchmark, which could financially strain OpenAI if widely and frivolously used by users.

Altman 直言不讳（得分：126，评论：59)：Sam Altman 宣布，原计划命名为 GPT-5 的 Orion 将以 GPT-4.5 的名义发布，并将其标记为最终的非 CoT 模型（non-CoT model）。来自 Bloomberg、《The Information》和《华尔街日报》的报告表明，GPT-5 面临着重大挑战，其相对于 GPT-4 的改进幅度不如 GPT-4 相对于其前代模型的改进幅度大。此外，o3 模型不会单独发布，而是会整合到名为 GPT-5 的统一系统中，这很可能是因为 ARC 基准测试显示其运营成本极高，如果用户大量且不加节制地使用，可能会给 OpenAI 带来巨大的财务负担。

Hardware and Costs: The inefficiency of running models on inappropriate hardware, such as Blackwell chips, and the misinterpretation of cost data due to repeated queries, were discussed as factors impacting the launch and operation of GPT-4.5 and GPT-5. Deep Research queries are priced at $0.50 per query, with plans offering 10 for plus members and 2 for free users.

硬件和成本：在不适合的硬件上运行模型，例如 Blackwell 芯片，效率会比较低。此外，由于重复查询造成的成本数据偏差，也被认为是影响 GPT-4.5 和 GPT-5 发布和运营的重要因素。深度研究查询（Deep Research queries）的定价为每次查询 0.50 美元，Plus 会员可以获得 10 次查询机会，免费用户则有 2 次。

Model Evolution and Challenges: There is a consensus that non-CoT models may have reached a scalability limit, prompting a shift towards models with reasoning capabilities. This transition is seen as a necessary evolution, with some suggesting that GPT-5 represents a new direction rather than an iterative improvement over GPT-4.

模型进化与挑战：业界普遍认为，不具备链式推理能力的模型（non-CoT）可能已经达到了扩展瓶颈，因此，发展重点转向了具备推理能力的模型。这种转变被认为是模型发展的必然趋势，甚至有人认为，GPT-5 的出现标志着一个全新的方向，而不仅仅是 GPT-4 的简单升级。

Reasoning and Model Selection: Discussions highlighted the potential advantages of reasoning models, with some users noting that reasoning models like o3 may overthink, while others suggest using a hybrid approach to select the most suitable model for specific tasks. The concept of models with adjustable thinking times being costly was also debated, as well as the potential for OpenAI to implement usage caps to manage expenses.

推理与模型选择：讨论聚焦于推理模型的潜在优势。一些用户指出，像 o3 这样的推理模型可能存在过度推理的问题，而另一些用户则建议采用混合策略，针对特定任务选择最合适的模型。此外，关于具备可调节推理时长的模型成本高昂的问题，也引发了讨论，以及 OpenAI 是否可能通过设置使用上限来控制成本。

I'm in my 50's and I just had ChatGPT write me a javascript/html calculator for my website. I'm shook. (Score: 236, Comments: 62): The author, in their 50s, used ChatGPT to create a JavaScript/HTML calculator for their website and was impressed by its ability to interpret vague instructions and refine the code, akin to a conversation with a web developer. Despite their previous limited use of AI, they were astonished by its capabilities, reflecting on their long history of observing technological advancements since 1977.

我五十多岁了，刚用 ChatGPT 为我的网站生成了一个 JavaScript/HTML（JavaScript/HTML）计算器。我感到非常震撼！（在某平台上的得分：236，评论数：62)：这位五十多岁的作者使用 ChatGPT 为其网站创建了一个 JavaScript/HTML 计算器，ChatGPT 能够理解含糊不清的指令并改进代码，这让作者印象深刻，感觉就像是在与一位专业的网页开发人员交流。尽管作者之前很少使用 AI，但 ChatGPT 的强大能力仍然让他们感到惊讶，回想起自 1977 年以来所见证的各种技术进步。

Users shared experiences of ChatGPT aiding in diverse coding tasks, from creating SQL queries to building wikis and servers, emphasizing its utility in guiding through unfamiliar technologies. FrozenFallout and redi6 highlighted its role in simplifying complex processes and error handling, even for those with limited technical knowledge.

用户分享了 ChatGPT 在各种编程任务中提供助力的经验，包括创建 SQL 查询、构建维基和服务器等。他们强调 ChatGPT 能够引导用户学习不熟悉的技术，简化复杂流程，并辅助处理错误，即使是对于技术知识有限的用户也十分有效。FrozenFallout 和 redi6 特别提到了 ChatGPT 在简化复杂流程和错误处理方面的价值。

Front_Carrot_1486 and BroccoliSubstantial2 expressed a shared sense of wonder at AI's rapid advancements, comparing it to past technological shifts, and noting the generational perspective on witnessing tech evolving from sci-fi to reality. They appreciated AI's ability to provide solutions and alternatives, despite occasional errors.

Front_Carrot_1486 和 BroccoliSubstantial2 都对人工智能（AI）的飞速发展感到惊叹，他们将其与以往的技术变革相提并论，并表示亲眼见证科技从科幻变成现实，这本身就带有一种时代感。尽管人工智能偶尔也会出错，但他们对它能够提供解决方案和替代方案这一点表示赞赏。

Recommendations for further exploration included trying Cursor with a membership for a more impressive experience, as suggested by TheoreticalClick, and exploring app development with AI guidance, as mentioned by South-Ad-9635.

一些建议供您进一步探索，例如 TheoreticalClick 建议您购买 Cursor 会员，以获得更好的使用体验；South-Ad-9635 则建议您可以尝试在 AI 的辅助下进行应用开发。

Theme 2. Anthropic and OpenAI enhance reasoning models

OpenAI increased its most advanced reasoning model's rate limits by 7x. Now your turn, Anthropic. (Score: 486, Comments: 72): OpenAI has significantly increased the rate limits of its advanced reasoning model, o3-mini-high, by 7x for Plus users, allowing up to 50 per day. Additionally, OpenAI o1 and o3-mini now support both file and image uploads in ChatGPT.

主题 2. Anthropic 和 OpenAI 提升推理模型能力

OpenAI 将其最先进的推理模型的使用频率提升了 7 倍。现在轮到 Anthropic 了。(得分：486，评论：72)：OpenAI 大幅提升了其高级推理模型 o3-mini-high 的使用频率，OpenAI Plus 用户现在每天最多可以使用 50 次。此外，OpenAI o1 和 o3-mini 现在在 ChatGPT 中支持文件和图像上传功能。

Users express strong dissatisfaction with Anthropic's perceived lack of urgency to respond to competitive pressures, with some canceling subscriptions due to the lack of compelling updates or features. Concerns include the company's focus on safety and content moderation over innovation, potentially losing their competitive edge.

用户强烈表达了对 Anthropic 公司在应对市场竞争方面反应迟缓的不满，部分用户由于缺少有吸引力的更新或功能，已经取消了订阅。他们担心 Anthropic 过度关注安全性和内容审核，而忽略了创新，这可能会导致其丧失竞争优势。

The increased rate limits for OpenAI's o3-mini-high model have been positively received, especially by Plus users, who appreciate the enhanced access. However, some believe that OpenAI prioritizes API business customers over web/app users, leading to lower limits for the latter.

OpenAI 的 o3-mini-high 模型提升了访问频率限制，受到了用户的积极欢迎，特别是 Plus 会员（Plus users），他们对访问权限的提升表示赞赏。然而，有些人认为 OpenAI 更加重视通过 API 接口使用 OpenAI 服务的商业客户（API business customers），导致网页和应用程序用户（web/app users）的访问频率限制较低。

There is a sentiment of disappointment towards Anthropic, with users feeling that their focus on safety and corporate customers is overshadowing innovation and responsiveness to market competition. Some users express frustration with Claude's limitations and the lack of viable alternatives with similar capabilities.

目前，不少用户对 Anthropic 感到失望，他们认为 Anthropic 过分强调安全性和服务企业客户，导致其在创新方面表现不足，对市场竞争的反应也较为迟缓。一些用户对 Claude 的种种限制感到不满，同时也苦于市场上缺乏具有类似功能的替代产品。

The Information: Claude hybrid reasoning model may be released in next few weeks (Score: 160, Comments: 44): Anthropic is reportedly set to release a Claude hybrid reasoning model in the coming weeks, offering a sliding scale feature that reverts to a non-reasoning mode when set to 0. The model is said to outperform o3-mini on some programming benchmarks and excels in typical programming tasks, while OpenAI's models are superior for academic and competitive coding.

信息：Claude 混合推理模型或于未来几周内发布（得分：160，评论：44)：据报道，Anthropic 计划在未来几周内发布 Claude 混合推理模型。该模型提供一种滑动比例调节功能，当该功能设置为 0 时，模型将切换回非推理模式。据说该模型在某些编程基准测试中表现优于 o3-mini，并且擅长处理常见的编程任务，而 OpenAI 的模型在学术研究和竞赛性质的编程方面更具优势。

Anthropic's Focus on Safety is criticized by some users, with comparisons made to OpenAI's reduced censorship and the Gemini 2.0 models, which are praised for being less restricted. Some users find the censorship efforts to be non-issues, while others see them as unnecessary corporate appeasement.

Anthropic 公司对安全性的重视受到了一些用户的批评。他们将 Anthropic 与 OpenAI 审查制度的放松，以及 Gemini 2.0 模型进行了比较，后者因为限制较少而备受赞誉。有些用户觉得这些审查措施根本不成问题，而另一些用户则认为这是企业不必要的妥协行为。

There is skepticism about the Claude hybrid reasoning model's effectiveness for writing tasks, with concerns that it might suffer similar issues to o3-mini. Users express a need for larger and more effective context windows, noting that Claude's supposed 200k token context starts to degrade significantly after 32k tokens.

人们对 Claude 混合推理模型在写作任务中的效果持保留态度，担心它可能面临与 o3-mini 相似的难题。用户们希望获得更大、更有效的上下文窗口（context window），并且指出，Claude 宣称的 20 万 Token（Token）上下文，在超过 3.2 万 Token 之后，性能就开始明显衰退。

Users discuss the importance of context windows and output complexity, with some finding o3-mini-high's output overly complex and others emphasizing the need for a context window that maintains its integrity beyond 64k tokens.

用户讨论了上下文长度和输出复杂性的重要性。有些人认为 o3-mini-high 模型的输出过于繁琐，而另一些人则强调需要更大的上下文长度，即使超过 64k Token 也能保持信息的完整性。

Deep reasoning coming soon (Score: 121, Comments: 42): The post titled "Deep reasoning coming soon" with the body content "Hhh" lacks substantive content and context to provide a detailed summary.

[深度推理指日可待（得分：121，评论：42)：这篇题为「深度推理指日可待」的帖子，内容只有简单的「Hhh」几个字母，缺乏实际信息和必要的背景介绍，因此无法进行详细解读。]

Code Output Concerns: Estebansaa expressed skepticism about the value of deep reasoning if it can't surpass the current output of 300-400 lines of code and match o3's capability of over 1000 lines per request. Durable-racoon questioned the need for such large outputs, suggesting that even 300 lines can be overwhelming for review.

关于代码输出的讨论：Estebansaa 表达了对深度推理实用性的怀疑，如果它无法超越目前 300-400 行的代码生成能力，并达到 o3 系统每次请求生成超过 1000 行代码的水平。Durable-racoon 质疑了对如此庞大代码量的必要性，认为即使 300 行代码也可能使代码审查不堪重负。

API Access Issues: Hir0shima and others discussed the challenges of API access, highlighting the high costs and frequent errors. Zestyclose_Coat442 noted the unexpected expenses even when errors occur, while Mutare123 mentioned the likelihood of hitting response limits.

API 访问问题：Hir0shima 等人讨论了应用程序编程接口（API）访问所面临的挑战，主要集中在高昂的成本和频繁出现的错误上。Zestyclose_Coat442 指出，即使在使用 API 时出现错误，也会产生意想不到的费用。Mutare123 则提到，API 很容易达到响应上限。

Release Impatience: Joelrog pointed out that recent announcements about deep reasoning are still within a short timeframe, arguing against impatience and emphasizing that companies generally adhere to their release plans.

避免对发布操之过急：Joelrog 指出，最近关于深度推理的公告仍然是在很短的时间范围内，因此不应过早期待发布。他还强调，公司通常会遵循其发布计划。

AI Discord Recap

A summary of Summaries of Summaries by Gemini 2.0 Flash Exp

AI Discord 概要

Gemini 2.0 Flash Exp 实验版总结的精简总结

Theme 1. Reasoning LLM Models - Trends in New releases

Nous Research Debuts DeepHermes-3 for Superior Reasoning: Nous Research launched the DeepHermes-3 Preview, showcasing advancements in unifying reasoning and intuitive language model capabilities, requiring a specific system prompt with tags to enable long chain of thought reasoning, enhancing systematic problem-solving. Benchmarks report significant enhancements in mathematical reasoning.

主题 1. 推理大语言模型模型 - 新版本趋势

Nous Research 发布 DeepHermes-3，实现卓越推理：Nous Research 推出了 DeepHermes-3 Preview，这款模型在统一推理和直观语言模型能力方面取得了显著进展。为了激活其强大的长程思维链推理能力，DeepHermes-3 需要特定的系统提示，并带有相应的标签。这种设计旨在提升模型系统性问题解决能力。基准测试结果表明，DeepHermes-3 在数学推理方面的表现有了显著提升。

Anthropic Plans Reasoning-Integrated Claude Version: Anthropic is set to release a new Claude model combining traditional LLM and reasoning AI capabilities, controlled by a token-based sliding scale, for tasks like coding, with rumors that it may be better than OpenAI's o3-mini-high in several benchmarks. The unveiling of these models and their new abilities signals the beginning of a new era of hybrid thinking in AI systems.

Anthropic 计划推出推理集成 Claude 版本：Anthropic 计划发布一款新的 Claude 模型，该模型结合了传统的大语言模型（LLM）和推理 AI 能力，通过 Token 数量进行动态调节，用于编码等任务。有传言称，在多个基准测试中，它的表现可能优于 OpenAI 的 o3-mini-high。这些模型及其新功能的发布，标志着人工智能系统混合式思考的新开端。

Scale With Intellect as Elon Promises Grok-3: Elon Musk announced Grok 3, nearing launch, boasting superior reasoning capabilities over existing models, hinting at new levels of 'scary smart' AI with a launch expected in about two weeks, amidst a $97.4 billion bid for OpenAI's nonprofit assets. This announcement is expected to change the game.

埃隆·马斯克承诺 Grok-3 将具备更强智能：埃隆·马斯克宣布 Grok-3 即将发布，它拥有比现有模型更强大的推理能力，预示着 AI 将达到一个「令人惊叹的智能」的新水平，预计将在大约两周内发布。与此同时，他还提出了以 974 亿美元收购 OpenAI 的非营利性资产。预计这一消息将会颠覆行业格局。

Theme 2. Tiny-yet-Mighty LLMs and Tooling Improvements

DeepSeek-R1 Generates GPU Kernel Like A Boss: NVIDIA's blog post features LLM-generated GPU kernels, showcasing DeepSeek-R1 speeding up FlexAttention and achieving 100% numerical correctness on 🌽KernelBench Level 1, while also achieving 96% accurate results on Level-2 issues of the KernelBench benchmark. This automates computationally expensive tasks by allocating additional resources, but concerns arose over the benchmark itself.

主题 2. 小身材，大能量：大语言模型与工具的进步

DeepSeek-R1：生成 GPU 内核的专家：NVIDIA 的博客重点介绍了由大语言模型生成的 GPU 内核。DeepSeek-R1 加速了 FlexAttention，并在 🌽KernelBench Level 1 测试中实现了 100% 的数值正确性，同时在 KernelBench 基准测试的 Level-2 问题上实现了 96% 的准确率。通过分配额外的资源，DeepSeek-R1 实现了计算密集型任务的自动化。然而，人们开始关注该基准测试本身的可靠性 [20]。

Hugging Face Smolagents Arrive and Streamline Your Workflow: Hugging Face launched smolagents, a lightweight agent framework alternative to deep research, with a processing time of about 13 seconds for 6 steps. Users can modify the original code to extend execution when run on a local server, providing adaptability.

Hugging Face Smolagents 发布，助力工作流程提速：Hugging Face 推出了 smolagents，一个轻量级的 AI 智能体（AI Agent）框架，旨在替代深度研究，在 6 个步骤的处理中，仅需约 13 秒。用户可以修改原始代码，使其在本地服务器上运行时能够扩展执行，从而具备更好的适应性。

Codeium's MCP Boosts Coding Power: Windsurf Wave 3 (Codeium) introduces features like the Model Context Protocol (MCP), which integrates multiple AI models for enhanced efficiency and output, allowing users to configure tool calls to user-defined MCP servers and achieve higher quality code. The community is excited for this hybrid AI framework!

Codeium 的 MCP 加速编码：Windsurf Wave 3（Codeium）引入了例如模型上下文协议（Model Context Protocol，MCP）这样的功能，它集成了多个 AI 模型，从而提升效率和输出质量。用户可以将工具调用配置到自定义的 MCP 服务器上，以获得更高质量的代码。社区对这种混合 AI 框架非常期待！

Theme 3. Perplexity Finance Dashboard and Analysis of AI Models

Perplexity Launches Your All-In-One Finance Dashboard: Perplexity released a new Finance Dashboard providing market summaries, daily highlights, and earnings snapshots. Users are requesting a dedicated button for dashboards on web and mobile apps.

主题 3. Perplexity 金融仪表盘和 AI 模型分析

Perplexity 发布多合一金融仪表盘：Perplexity 发布了一个新的金融仪表盘，提供市场总结、每日亮点和盈利概览。用户建议在网页和移动应用上增加一个仪表盘专用按钮。

Model Performance Gets Thorough Scrutiny at PPLX AI: The models that Perplexity AI uses are in question. Debates emerged regarding AI models, specifically the efficiency and accuracy of R1 compared to alternatives like DeepSeek and Gemini.

PPLX AI 正在仔细评估模型性能：Perplexity AI 使用的 AI 模型正受到密切关注。人们针对 AI 模型展开了讨论，尤其是 R1 相对于 DeepSeek 和 Gemini 等其他模型的效率和准确性。

DeepSeek R1 Trounces OpenAI in Reasoning Prowess: A user reported Deepseek R1 displayed impressive reasoning when handling complex SIMD functions, outperforming o3-mini on OpenRouter. Users on HuggingFace celebrated V3's coding ability, and some on Unsloth AI saw it successfully handle tasks with synthetic data and GRPO/R1 distillation.

DeepSeek R1 在推理能力上表现出色：有用户报告称，DeepSeek R1 在处理复杂的 SIMD（单指令多数据流）函数时，展现出令人印象深刻的推理能力，性能优于 OpenRouter 上的 o3-mini 模型。HuggingFace 社区的用户也对 V3 版本的编码能力赞赏有加。此外，Unsloth AI 平台上的部分用户观察到，DeepSeek R1 能够成功处理包含合成数据以及采用 GRPO/R1 蒸馏的任务。

Theme 4. Challenges and Creative Solutions

DOOM Game Squeezed into a QR Code: A member successfully crammed a playable DOOM-inspired game, dubbed The Backdooms, into a single QR code, taking up less than 2.4kb, and released the project as open source under the MIT license for others to experiment with. The project used compression like .kkrieger, and has a blog post documenting the approach.

主题 4. 挑战与创造性解决方案将 DOOM 游戏塞进二维码：一位开发者成功地将一款受 DOOM 启发的、名为 The Backdooms 的可玩游戏压缩进了一个二维码中。这个游戏仅占用不到 2.4kb 的空间，并且该开发者还在 MIT 许可下以开源方式发布了该项目，供其他开发者学习和实验。该项目使用了类似 .kkrieger（一种极致压缩技术）的压缩方法，并撰写博文详细介绍了其实现方法。

Mobile Devices Limit RAM, Prompting Resourceful Alternatives: Mobile users note 12GB phones only allowing 2GB of accessible memory, hindering model performance, and one suggested an alternative 16GB ARM SBC for portable computing at ~\$100. If you don't have a fancy phone, upgrade it.

移动设备的内存限制催生了巧妙的替代方案：移动用户发现，即使手机配备了 12GB 内存，实际可供使用的只有 2GB，这在一定程度上妨碍了模型（models）的性能。因此，有人建议使用价格约为 100 美元的 16GB ARM 单板计算机（Single Board Computer，SBC）作为便携式计算的替代方案。如果您使用的不是高端手机，可以考虑升级设备。

Hugging Face Agents Course Leaves Users Disconnected: With users experiencing connection issues during the agents course, a member suggested changing the endpoint to a new link (https://jc26mwg228mkj8dw.us-east-1.aws.endpoints.huggingface.cloud) and also indicated a model name update to deepseek-ai/DeepSeek-R1-Distill-Qwen-32B was required, which is likely caused by overload. Try a different browser, and if all else fails... disconnect.

Hugging Face Agents 课程出现连接问题：由于用户在 Agents 课程（Agents Course）中遇到连接问题，一位成员建议将端点更改为新的链接（https://jc26mwg228mkj8dw.us-east-1.aws.endpoints.huggingface.cloud），并指出模型名称需要更新为 deepseek-ai/DeepSeek-R1-Distill-Qwen-32B，这很可能是由于服务器过载导致的。您可以尝试更换浏览器，如果问题仍然存在，请断开连接稍后再试。

Theme 5. Data, Copyrights, and Declarations

US Rejects AI Safety Pact, Claims Competitive Edge: The US and UK declined to sign a joint AI safety declaration, with US leaders emphasizing their commitment to maintaining AI leadership. Officials cautioned engaging with authoritarian countries in AI could compromise infrastructure security.

主题 5. 数据、版权和声明美国拒绝人工智能安全协议，声称拥有竞争优势：美国和英国拒绝签署联合人工智能安全声明。美国领导人强调，他们致力于保持在人工智能领域的领先地位。官员们同时警告说，与专制国家在人工智能领域的合作可能会威胁到基础设施安全。

Thomson Reuters Wins Landmark AI Copyright Case: Thomson Reuters has won a significant AI copyright case against Ross Intelligence, determining that the firm infringed its copyright by reproducing materials from Westlaw. US Circuit Court Judge Stephanos Bibas dismissed all of Ross's defenses, stating that none of them hold water.

Thomson Reuters 赢得具有里程碑意义的 AI 版权案件：Thomson Reuters 赢得了一起针对 Ross Intelligence 的具有里程碑意义的涉及 AI 的版权案件，裁定其复制 Westlaw 材料构成侵权。美国巡回法院法官 Stephanos Bibas 驳回了 Ross 的所有辩护，认为其理由均不成立。

LLM Agents MOOC Certificate Process Delayed: Numerous participants in LLM Agents course haven't received prior certificates, and must observe a manual send, while others needing help locating them are reminded that the declaration form is necessary for certificate processing. Where's my diploma?

大语言模型（LLM/Large Language Model）智能体（AI Agent）MOOC 证书流程延迟：许多大语言模型智能体课程的参与者尚未收到之前的证书，需要等待手动补发。同时，若有学员需要协助查找证书，请注意，必须提交声明表才能处理证书。我的证书在哪里？

PART 1: High level Discord summaries

Unsloth AI (Daniel Han) Discord

PART 1：Discord 重点摘要

Unsloth AI（Daniel Han）Discord

DeepSeek's Dynamic Quantization Reduces Memory: Users explained that dynamic quantization implemented in DeepSeek models helps reduce memory usage while maintaining performance, though it currently mostly applies to specific models and detailed the benefits.

DeepSeek 的动态量化减少内存：用户解释说，DeepSeek 模型中实现的动态量化（Dynamic Quantization）有助于减少内存使用，同时保持性能。尽管动态量化目前主要适用于 DeepSeek 的特定模型，用户也详细说明了其优势。

Dynamic Quantization is a work in progress to reduce VRAM and run the 1.58-bit Dynamic GGUF version by Unsloth.

GRPO Training Plateaus Prompt Regex Tweaks: Concerns were raised about obtaining expected rewards during GRPO training, with users observing a plateau in performance indicators and unexpected changes in completion lengths, with further details in Unsloth's GRPO blog post.

动态量化（Dynamic Quantization）是一项持续进行的技术，旨在减少 VRAM 占用，并支持 Unsloth 提供的 1.58-bit 动态 GGUF 版本。

GRPO 训练停滞以及提示词 Regex 的调整：在 GRPO 训练过程中，用户对于获得预期奖励表示担忧，他们发现性能指标停滞不前，补全长度也出现了意料之外的变化。更多细节请参考 Unsloth 的 GRPO 博客文章。

One user reported modifying regex for better training outcomes, but inconsistencies in metrics remain a problem, and the impact on Llama3.1 (8B) performance metrics is unclear.

一位用户报告称，通过修改正则表达式（regex）以期获得更好的训练效果，但指标数据的不一致性仍然存在，而且这些修改对 Llama3.1（8B）模型性能指标的具体影响尚不明确。

Rombo-LLM-V3.0-Qwen-32b Impresses: A new model, Rombo-LLM-V3.0-Qwen-32b, has been released, showcasing impressive performance across various tasks, with more details in a redditor's post.

Rombo-LLM-V3.0-Qwen-32b 表现出色： 新模型 Rombo-LLM-V3.0-Qwen-32b 已发布，在各项任务中展现出令人印象深刻的性能。更多详情请参考一位 Reddit 用户的帖子。

Details on how to support the model developer's work on Patreon to vote for future models and access private repositories for just $5 a month.

Lavender Method Supercharges VLMs: The Lavender method was introduced as a supervised fine-tuning technique that improves the performance of vision-language models (VLMs) using Stable Diffusion, with code and examples available at AstraZeneca's GitHub page.

只需每月 5 美元，即可通过 Patreon 支持模型开发者的工作，并参与未来模型的投票和访问私有仓库，了解更多详情。

薰衣草方法助力 VLMs： 薰衣草方法是一种监督式微调技术，旨在利用 Stable Diffusion 改进视觉 - 语言模型（VLMs，Vision-Language Models）的性能。代码和示例可在 AstraZeneca 的 GitHub 页面上找到。

This method achieved performance boosts, including a +30% increase on 20 tasks and a +68% improvement on OOD WorldMedQA, showcasing the potential of text-vision attention alignment.

该方法带来了显著的性能提升，例如在 20 项任务中取得了超过 30% 的提升，并且在 OOD WorldMedQA 数据集上更是提升了 68%，充分展现了文本 - 视觉注意力对齐（text-vision attention alignment）的巨大潜力。

HuggingFace Discord

DOOM Game Squeezed into a QR Code: A member successfully crammed a playable DOOM-inspired game, dubbed The Backdooms, into a single QR code, taking up less than 2.4kb, and released the project as open source under the MIT license here.

HuggingFace Discord

二维码里玩 DOOM：有位奇才把一款受 DOOM 启发的迷你游戏「The Backdooms」塞进了一个小小的二维码里！这个游戏只有不到 2.4kb，而且已经以 MIT 许可证开源。项目地址在这里。

The creator documented the approach in this blog post providing insights on the technical challenges and solutions involved.

Steev AI Assistant Simplifies Model Training: A team unveiled Steev, an AI assistant created to automate AI model training, reducing the need for constant supervision, further information available at Steev.io.

创建者在一篇博文中记录了此方法，深入介绍了其中涉及的技术挑战和解决方案。

Steev AI 助手：简化模型训练：一个团队推出了 Steev，这是一款旨在自动执行 AI 模型训练的 AI 智能体，从而减少了持续人工干预的需求。更多信息，请访问 Steev.io 了解详情。

The goal is to simplify the AI training process, eliminating tedious and repetitive tasks, and allowing researchers to concentrate on core aspects of model development and innovation.

目标是简化 AI 训练流程，去除繁琐和重复性的工作，使研究人员能够专注于模型开发和创新等核心环节。

Rombo-LLM V3.0 Excels in Coding: A fresh model, Rombo-LLM-V3.0-Qwen-32b, has been launched, excelling in coding and math tasks, as shown in this Reddit post.

The model's use of Q8_0 quantization significantly boosts its efficiency, allowing it to perform complex tasks without heavy computational requirements.

Rombo-LLM V3.0：编码能力再创新高： 全新模型 Rombo-LLM-V3.0-Qwen-32b 已正式发布，在代码编写和数学运算方面表现优异，如 Reddit 论坛所示。

该模型采用 Q8_0 量化技术，显著提升效率，使其能够以更低的计算成本执行复杂的任务。

Agents Course Verification Proves Problematic: Numerous participants in the Hugging Face AI Agents Course have reported ongoing problems verifying their accounts via Discord, resulting in recurring connection failures.

AI 智能体课程验证出现问题：Hugging Face AI 智能体课程的许多参与者报告称，他们一直无法通过 Discord 验证帐户，并因此反复出现连接失败的情况。

Recommended solutions included logging out, clearing cache, and trying different browsers, and a lucky few eventually managed to complete the verification process.

推荐的解决方案包括注销、清除缓存以及尝试不同的浏览器。只有少数幸运的人最终成功完成了验证。

New Endpoints Suggested for Agent Connection: With users experiencing connection issues during the agents course, a member suggested changing the endpoint to a new link (https://jc26mwg228mkj8dw.us-east-1.aws.endpoints.huggingface.cloud) and also indicated a model name update to deepseek-ai/DeepSeek-R1-Distill-Qwen-32B was required.

关于 Agent 连接的新端点建议：有用户反映在 agents 课程中遇到了连接问题，一位成员建议将端点更换为新的链接（https://jc26mwg228mkj8dw.us-east-1.aws.endpoints.huggingface.cloud）。同时，他还提到需要将模型名称更新为 deepseek-ai/DeepSeek-R1-Distill-Qwen-32B。

This fix could solve the recent string of issues faced by course participants trying to use LLMs in their agent workflows.

OpenAI Discord

这个修复或许能解决近来课程学员们在使用大语言模型构建 AI 智能体工作流时遇到的一连串问题。

OpenAI Discord

Pro users Get Deep Research Access: Deep research access is now available for all Pro users on multiple platforms including mobile and desktop apps (iOS, Android, macOS, and Windows).

专业版用户尊享深度研究权限：现在，所有专业版用户都可以在多个平台，包括移动端和桌面端应用（iOS、Android、macOS 和 Windows）上，使用深度研究权限。

This enhances research capabilities on various devices.

OpenAI o1 & o3 support File & Image Uploads: OpenAI o1 and o3-mini now support both file and image uploads in ChatGPT.

此举增强了在各种设备上的研究能力。

OpenAI o1 和 o3 支持文件及图像上传：OpenAI o1 和 o3-mini 现在支持在 ChatGPT 中上传文件和图像。

Additionally, o3-mini-high limits have been increased by 7x for Plus users, allowing up to 50 uploads per day.

OpenAI Unveils Model Spec Update: OpenAI shared a major update to the Model Spec, detailing expectations for model behavior.

此外，Plus 用户在使用 o3-mini-high 时的上传限制提升了 7 倍，现在每天最多可以上传 50 次。

OpenAI 发布模型规范（Model Spec）更新：OpenAI 发布了模型规范（Model Spec）的重大更新，详细阐述了对模型应有行为的期望。

The update emphasizes commitments to customizability, transparency, and fostering an atmosphere of intellectual freedom.

OpenAI's Ownership Faces Scrutiny: Discussions revolve around the possibility of OpenAI being bought by Elon Musk, with many expressing skepticism about this happening and hopes for open-sourcing the technology if it occurs.

更新强调了对可定制性、透明度和培养学术自由的氛围的承诺。

OpenAI 所有权问题引关注：讨论围绕着埃隆·马斯克可能收购 OpenAI 的可能性展开，许多人对此表示怀疑，并希望如果收购发生，相关技术能够开源。

Users speculate that major tech companies may prioritize profit over public benefit, leading to fears of excessive control over AI.

GPT-4o has free limits: Custom GPTs operate on the GPT-4o model, with limits that are changing daily based on various factors, with only some fixed values like AVM 15min/month.

用户担心大型科技公司可能会为了追求利润，过度控制 AI 技术，从而损害公众利益。

GPT-4o 具有免费使用限制：定制 GPT 是基于 GPT-4o 模型运行的，其限制会根据多种因素每日调整，只有 AVM（Audio Visual Model）等少数指标存在固定限制，如每月 15 分钟。

Users must observe the limits based on their region and usage timezone.

Cursor IDE Discord

用户必须遵守根据其所在地区和使用时区所设定的限制。

Cursor IDE Discord （Cursor 集成开发环境的 Discord 社区）

o3-mini Falls Behind Claude: Users have observed that OpenAI's o3-mini model underperforms in tool calling compared to Claude, often requiring multiple prompts to achieve desired outcomes, which led to frustration.

o3-mini 的表现不如 Claude：用户观察到，与 Claude 相比，OpenAI 的 o3-mini 模型在工具调用（tool calling）方面的表现不佳，通常需要多次提示才能达到预期的结果，这导致了用户的沮丧。

Many expressed that Claude's reasoning models excel at tool use, suggesting the integration of a Plan/Act mode similar to Cline to improve user experience.

Hybrid AI Model Excites Coders: The community shows excitement for Anthropic's upcoming hybrid AI model, which reportedly surpasses OpenAI's o3-mini in coding tasks when leveraging maximum reasoning capabilities.

很多人都认为，Claude 的推理模型在工具使用方面表现出色，建议加入类似 Cline 的 Plan/Act 模式，从而提升用户体验。

混合 AI 模型让程序员们眼前一亮： 社区对 Anthropic 即将发布的混合 AI 模型感到非常兴奋，据说，在充分发挥推理能力的情况下，该模型在编码任务中能够超越 OpenAI 的 o3-mini。

The anticipation stems from the new model's high performance on programming benchmarks, indicating it could significantly boost coding workflows relative to current alternatives.

人们对这款新模型的期待，源于它在编程基准测试中表现出的优异性能。这预示着，相比现有的其他方案，它有望大幅提升编码工作效率。

Tool Calling Draws Concern: Users voiced dissatisfaction with o3-mini's limited flexibility and efficiency in tool calling, questioning its practical utility in real-world coding scenarios.

工具调用引发关注： 用户对 o3-mini 在工具调用（Tool Calling）方面的有限灵活性和效率表示不满，并对其在实际编码场景中的实用性提出了疑问。

Discussions emphasized a demand for AI models to simplify complex coding tasks, prompting suggestions to establish best practices in prompting to elicit higher quality code.

讨论强调了对 AI 模型简化复杂编码任务的需求，从而建议建立提示词工程（prompting）方面的最佳实践，以生成更高质量的代码。

MCP Usage Becomes Topic of Discussion: The concept of MCP (Multi-Channel Processor) surfaced as a tool for improving coding tasks by integrating multiple AI models for enhanced efficiency and output.

MCP 的使用成为讨论话题：多通道处理器（MCP，Multi-Channel Processor）的概念开始受到关注，它被认为是一种能够提升编码效率的工具，通过整合多个 AI 模型来改进编码任务并提升最终产出。

Users have been sharing experiences and strategies for utilizing MCP servers to optimize coding workflows and overcome the limitations of individual models.

Windsurf Pricing Dissatisfies: Discussions touched on the inflexible pricing of Windsurf, specifically its restriction against users employing their own keys, which has led to user dissatisfaction.

用户一直在分享使用 MCP 服务器（MCP server）来优化编码工作流程和克服单个模型的局限性的经验和策略。

Windsurf 定价策略引发不满： 讨论涉及 Windsurf 不灵活的定价策略，特别是它不允许用户使用自己的 API 密钥，这导致了用户的不满。

Many users expressed a preference for Cursor's features and utility over competitors, highlighting its advantages in cost effectiveness and overall user experience.

许多用户表示，相较于其他产品，他们更喜欢 Cursor 的各项功能，并强调其在性价比和整体用户体验上的优势。

Nous Research AI Discord

DeepHermes-3 Unites Reasoning: Nous Research launched the DeepHermes-3 Preview, an LLM integrating reasoning with traditional language models, available on Hugging Face.

Nous Research AI Discord

DeepHermes-3：融合推理能力：Nous Research 推出了 DeepHermes-3 Preview，这是一款融合了推理能力与传统语言模型的大语言模型，现已在 Hugging Face 上发布。

The model requires a specific system prompt with tags to enable long chain of thought reasoning, enhancing systematic problem-solving, and has shown significant enhancements in mathematical reasoning.

该模型需要一个带有标签的特定系统提示，以实现长程的链式思考（Chain of Thought）推理，增强系统性的问题解决能力，并且在数学推理方面表现出显著的提升。

Nvidia's LLM Kernels Accelerate: Nvidia's blog post features LLM-generated GPU kernels speeding up FlexAttention while achieving 100% numerical correctness on 🌽KernelBench Level 1.

Nvidia 的大语言模型内核加速：Nvidia 的博客文章重点介绍了由大语言模型（LLM/Large Language Model）生成的 GPU 内核，它们加速了 FlexAttention，并在 🌽KernelBench Level 1 上实现了 100% 的数值正确性。

This signals notable progress in GPU performance optimization, and members suggested r1 kimik and synthlab papers for up-to-date information on LLM advancements.

这表明 GPU 性能优化方面有了长足的进步，有成员建议参考 r1 kimik 和 synthlab 的论文，以便了解大语言模型（LLM/Large Language Model）的最新进展。

Mobile Device RAMs Hamper: Members noted that 12GB phones are only allowing 2GB of accessible memory, which hindered their ability to run models.

A user suggested acquiring a 16GB ARM SBC for portable computing, which would allow for running small LLMs while traveling for ~100, providing an affordable option for those interested.

移动设备内存限制：有成员指出，即使是配备 12GB 内存的手机，实际仅允许使用 2GB 左右的内存，这严重限制了模型运行能力。

一位用户建议购买 16GB ARM 单板计算机（SBC/Single Board Computer）用于便携计算。这样一来，即使在旅途中也能运行小型大语言模型，而且花费不高，大约 100 美元左右，对于有需求的人来说，是个不错的选择。

US Rejects AI Safety Pact: The US and UK declined to sign a joint AI safety declaration, with US leaders emphasizing their commitment to maintaining AI leadership, according to ArsTechnica report.

美国未签署 AI 安全协议：根据 ArsTechnica 的报道，美国和英国没有签署一项联合的 AI 安全声明。美国领导人强调，他们将继续致力于保持在人工智能领域的领先地位。

Officials cautioned that engaging with authoritarian countries in AI could compromise national infrastructure security, citing examples like CCTV and 5G as subsidized exports for undue influence.

官员们警告说，在人工智能领域与专制国家进行合作，可能会危及国家基础设施安全。他们列举了闭路电视（CCTV，一种监控系统）和 5G 等案例，指出这些产品通过补贴出口，可能被用于施加不正当的影响。

OpenRouter (Alex Atallah) Discord

Groq DeepSeek R1 70B Sprints at 1000 TPS: OpenRouter users are celebrating the addition of Groq DeepSeek R1 70B, which hits a throughput of 1000 tokens per second, offering parameter customization and rate limit adjustments. The announcement was made on OpenRouter AI's X account.

OpenRouter（Alex Atallah）Discord

Groq DeepSeek R1 70B 达到 1000 TPS：OpenRouter 的用户们正在庆祝 Groq DeepSeek R1 70B 的加入，这款模型实现了每秒 1000 个 Token 的高吞吐量，并且支持参数自定义和速率限制调整。OpenRouter AI 在其 X（原 Twitter）平台上发布了这一消息。

This is part of a broader integration designed to enhance user interaction with the platform.

New Sorting Tweaks Boost UX: Users can now customize default sorting for model providers, focusing on throughput or balancing speed and cost in account settings. To access the fastest provider available, append :nitro to any model name, as highlighted in OpenRouter's tweet.

作为平台整体升级的一部分，本次更新旨在增强用户互动体验。

全新排序功能优化用户体验： 用户现在可以自定义模型服务商的默认排序方式。在账户设置中，用户可以选择优先考虑吞吐量，或者平衡速度与成本。如果您想使用最快的服务商，只需在模型名称后添加 :nitro，正如 OpenRouter 在推文中指出的那样。

This feature allows users to tailor their experience based on their priorities.

API Embraces Native Token Counting: OpenRouter plans to switch the usage field in the API from GPT token normalization to the native token count of models and they are asking for user feedback.

这个特性允许用户根据他们的优先级来定制使用体验。

API 采用原生 Token 计数：OpenRouter 计划切换 API 中的用量字段，从 GPT Token 归一化（GPT token normalization）调整为模型的原生 Token 计数，并正在寻求用户的反馈意见。

There are speculations about how this change might affect models like Vertex and other models with different token ratios.

Deepseek R1 Trounces OpenAI in Reasoning: A user reported Deepseek R1 displayed impressive reasoning when handling complex SIMD functions, outperforming o3-mini, saying it was 'stubborn'.

人们猜测，这种变化可能会对 Vertex 等模型以及其他具有不同 Token 数量比例的模型产生影响。

Deepseek R1 在推理能力上超越 OpenAI：有用户报告称，Deepseek R1 在处理复杂的 SIMD 函数时，展现出了令人印象深刻的推理能力，甚至超过了 o3-mini。该用户评价说，Deepseek R1 在处理这类问题时表现得非常「执着」。

The team is exploring this option and acknowledged user concerns about moderation issues.

Users Cry Foul on Google Rate Limits: Users are encountering frequent 429 errors from Google due to resource exhaustion, especially affecting the Sonnet model.

团队正在探索这个选项，并且承认用户对内容审核问题的担忧。

用户强烈抱怨 Google 频率限制：由于资源耗尽，用户在使用 Google 服务时频繁遇到 429 错误，特别是 Sonnet 模型受影响严重。

The OpenRouter team is actively addressing growing rate limit issues caused by Anthropic capacity limitations.

Perplexity AI Discord

OpenRouter 团队正在积极解决因 Anthropic 算力限制而日益加剧的速率限制（rate limit）问题。

Perplexity AI Discord

Perplexity Releases Finance Dashboard: Perplexity released a new Finance Dashboard providing market summaries, daily highlights, and earnings snapshots.

Users are requesting a dedicated button for dashboards on web and mobile apps.

Perplexity 发布金融仪表盘：Perplexity 发布了新的金融仪表盘，提供市场总结、每日亮点和收益概览。

用户希望在网页和移动 App 上增加一个仪表盘的专属按钮。

Doubts Arise Over AI Model Performance: Debates emerged regarding AI models, specifically the efficiency and accuracy of R1 compared to alternatives like DeepSeek and Gemini, as well as preferred usage and performance metrics.

人们对 AI 模型性能产生疑问：关于 AI 模型的讨论逐渐兴起，特别是关于 R1 与 DeepSeek、Gemini 等模型的效率和准确性对比，以及最佳使用方式和性能指标的讨论。

Members shared experiences, citing features and functionalities that could improve user experience.

Perplexity Support Service Criticized: A user reported issues with the slow response and lack of support from Perplexity's customer service related to being charged for a Pro account without access.

成员们分享了各自的使用体验，并提出了一些可以优化用户体验的功能和特性。

Perplexity 的支持服务受到用户批评：一位用户反馈称，Perplexity 的客服响应速度慢，而且未能解决其 Pro 账户被扣费但无法使用的问题。

This spurred discussion on the need for clear communication and effective support teams.

API Suffers Widespread 500 Errors: Multiple members reported experiencing a 500 error across all API calls, with failures in production.

由此引发了关于清晰沟通和高效支持团队重要性的讨论。

API 出现大规模 500 错误：多名成员报告称，所有 API 调用均出现 500 错误，同时生产环境也发生故障。

The errors persisted for some time before the API was reported to be back up.

Enthusiasm for Sonar on Cerebras: A member expressed strong interest in becoming a beta tester for the API version of Sonar on Cerebras.

错误持续了一段时间，之后据报告 API 恢复正常。

对 Cerebras 上 Sonar 的期待：一位成员表示，他非常有兴趣成为 Cerebras 上 Sonar 的 API 版本的 Beta 测试者。

The member stated they have been dreaming of this for months, indicating potential interest in this integration.

Codeium (Windsurf) Discord

这位成员提到，Ta 已经为此期待了好几个月，暗示了对这次整合的浓厚兴趣。

Codeium（Windsurf）Discord

Windsurf Wave 3 Goes Live!: Windsurf Wave 3 introduces features like the Model Context Protocol (MCP), customizable app icons, enhanced Tab to Jump navigation, and Turbo Mode, detailed in the Wave 3 blog post.

Windsurf Wave 3 正式发布！：Windsurf Wave 3 带来了一系列令人兴奋的新功能，包括模型上下文协议（Model Context Protocol，MCP），它能更好地理解用户的意图；你可以自定义应用程序的图标，让界面更具个性；「Tab to Jump」导航也得到了增强，操作更加便捷；还有 Turbo 模式，让你的体验更加流畅。Wave 3 博客文章详细介绍了这些新功能。

The update also includes major upgrades such as auto-executing commands and improved credit visibility, further detailed in the complete changelog.

MCP Server Options Elusive Post-Update?: After updating Windsurf, some users reported difficulty locating the MCP server options, which were resolved by reloading the window.

更新还包括重大升级，例如自动执行命令和改进的信用额度显示，更详细的信息请参见完整的更新日志。

更新后 MCP 服务器选项难觅？： 在更新 Windsurf 后，一些用户报告说难以找到 MCP 服务器选项，重新加载窗口后问题得到解决。

The issue highlighted the importance of refreshing the interface to ensure that the MCP settings appear as expected, enabling configuration of tool calls to user-defined MCP servers.

这个问题突显了刷新界面的重要性，这样可以确保 MCP（Management Control Plane）设置按预期显示，从而能够配置工具调用到用户定义的 MCP 服务器。

Cascade Plagued by Performance Woes: Users have been reporting that the Cascade model experiences sluggish performance and frequent crashing, often requiring restarts to restore functionality.

Cascade 饱受性能问题困扰： 用户报告称，Cascade 模型运行缓慢，且频繁崩溃，通常需要重启才能恢复正常。

Reported frustrations include slow response times and increased CPU usage during operation, underscoring stability problems.

Codeium 1.36.1 Seeks to Fix Bugs: The release of Codeium 1.36.1 aims to address existing problems, with users recommended to switch to the pre-release version in the meantime.

有用户反映，使用过程中存在响应时间过长和 CPU 占用率升高的问题，这些都表明其稳定性不佳。

Codeium 1.36.1 致力于修复 Bug：Codeium 1.36.1 版本的发布旨在解决当前存在的问题，建议用户尽快切换到预发布版本。

Past attempts at fixing issues with 2025 writing had been unsuccessful, highlighting the need for the update.

Windsurf Chat Plagued by Instability: Windsurf chat users are experiencing frequent freezing, loss of conversation history, and workflow disruptions.

此前，修复 2025 写作功能相关问题的尝试均告失败，这突显了本次更新的必要性。

Windsurf 聊天工具稳定性不佳：Windsurf 聊天用户经常遇到卡顿、对话历史记录丢失以及工作流程中断等问题。

Suggested solutions included reloading the application and reporting bugs to address these critical stability problems.

LM Studio Discord

为了解决这些关键的稳定性问题，建议的解决方案包括重新启动应用程序，以及报告程序错误。

LM Studio Discord

Qwen-2.5 VL Faces Performance Hiccups: Users report slow response times and memory issues with the Qwen-2.5 VL model, particularly after follow-up prompts, leading to significant delays.

Qwen-2.5 VL 性能表现不佳：用户报告 Qwen-2.5 VL 模型响应时间缓慢，并存在内存问题，尤其是在收到后续指令后，导致明显的延迟。

The model's memory usage spikes, possibly relying on SSD instead of VRAM, which is particularly noticeable on high-spec machines.

Decoding Speculation Requires Settings Tweaks: Difficulties uploading models related to Speculative Decoding led to troubleshooting, revealing users needed to adjust settings and ensure compatible models are selected.

模型的内存占用会突然增加，这可能是因为模型开始使用固态硬盘（SSD）存储，而不是速度更快的显存（VRAM）。这种情况在配置较高的机器上尤其明显。

解码推测需要优化设置：在上传与推测解码（Speculative Decoding）相关的模型时，用户遇到了一些问题。经过排查发现，用户需要调整设置，并选择兼容的模型才能解决这些问题。

The issue highlights the importance of matching model configurations with the selected speculative decoding functionality.

Tesla K80 PCIe sparks debate: The potential of using a $60 Tesla K80 PCIe with 24GB VRAM for LLM tasks was discussed, raising concerns about power and compatibility.

这个问题强调了模型配置与所选的推测解码功能相适配的重要性。

Tesla K80 PCIe 引发热议：有人讨论了使用一块拥有 24GB 显存（VRAM）、价格 60 美元的 Tesla K80 PCIe 来运行大语言模型（LLM/Large Language Model）的可能性，但也引发了人们对功耗和兼容性的担忧。

Users suggested that while affordable, the K80's older architecture and potential setup problems might make a GTX 1080 Ti a better alternative.

SanDisk Supercharges VRAM with HBF Memory: SanDisk introduced new high-bandwidth flash memory capable of enabling 4TB of VRAM on GPUs, aimed at AI inference applications requiring high bandwidth and low power.

有用户指出，虽然 K80 的价格比较亲民，但它的架构相对老旧，而且可能存在设置问题。相比之下，GTX 1080 Ti 或许是更好的选择。

SanDisk 利用 HBF 内存增强 VRAM：SanDisk 发布了一种新型高带宽闪存，该闪存能让 GPU 拥有高达 4TB 的 VRAM，主要面向需要高带宽和低功耗的 AI 推理（AI inference）应用。

This HBF memory positions itself as a potential alternative to traditional HBM in future AI hardware, according to Tom's Hardware.

GPU MODE Discord

据 Tom's Hardware 报道，这种 HBF 内存（High Bandwidth Fabric memory）有望成为未来 AI 硬件中传统 HBM 的替代方案。

GPU MODE Discord

Blackwell's Tensor Memory Gets Scrutinized: Discussions clarify that Blackwell GPUs' tensor memory is fully programmer managed, featuring dedicated allocation functions as detailed here, and it's also a replacement for registers in matrix multiplications.

Blackwell 的张量内存（Tensor Memory）受到关注：讨论澄清了 Blackwell GPU 的张量内存（Tensor Memory）完全由程序员管理，并具有专门的分配函数，具体细节请参考此处。此外，它还在矩阵乘法中替代了寄存器的作用。

Debates emerge regarding the efficiency of tensor memory in handling sparsity and microtensor scaling, which can lead to capacity wastage, complicating the fitting of accumulators on streaming multiprocessors if not fully utilized.

关于张量内存处理稀疏性（sparsity）和微张量缩放（microtensor scaling）的效率，目前存在一些争议。如果张量内存未被充分利用，可能会导致存储容量的浪费，进而增加流式多处理器（Streaming Multiprocessors）上累加器拟合的复杂性。

D-Matrix plugs innovative kernel engineering: D-Matrix is hiring for kernel efforts, inviting those with CUDA experience to connect and explore opportunities in their unique stack, recommending outreach to Gaurav Jain on LinkedIn for insights into their innovative hardware and architecture.

D-Matrix 注重创新内核工程：D-Matrix 正在招募内核工程师，欢迎拥有 CUDA 经验的人才加入，共同探索 D-Matrix 独特技术栈中的发展机会。如果您想深入了解 D-Matrix 的创新硬件和架构，建议您在 LinkedIn 上联系 Gaurav Jain。

D-Matrix's Corsair stack aims for speed and energy efficiency, potentially transforming large-scale inference economics, and claims a competitive edge against H100 GPUs, emphasizing sustainable solutions in AI.

D-Matrix 的 Corsair 架构旨在提升速度和能源效率，有望彻底改变大规模推理的成本效益，并声称其性能可以与 H100 GPU 相媲美，同时强调在人工智能（AI）领域提供可持续的解决方案。

SymPy Simplifies Backward Pass Derivation: Members show curiosity about using SymPy for deriving backward passes of algorithms, to manage complexity.

Discussion occurred around issues encountered with gradgradcheck(), relating to unexpected output behavior, with intent to clarify points and follow-up on GitHub if issues persist, hinting at the complexity in maintaining accurate intermediate outputs.

SymPy 简化反向传播推导：大家对使用 SymPy 来推导算法的反向传播过程，从而简化复杂性很感兴趣。

讨论集中在 gradgradcheck（）遇到的问题上，这些问题涉及意外的输出行为，目的是为了澄清一些关键点。如果问题仍然存在，将在 GitHub 上继续跟进，这也暗示了维护准确的中间结果的复杂性。

Reasoning-Gym Revamps Evaluation Metrics: The Reasoning-Gym community discusses performance drops on MATH-P-Hard, and releases a new pull request for Graph Coloring Problems, with standardization of the datasets with unified prompts to streamline evaluation processes, improving machine compatibility of outputs, detailed in the PR here.

[推理竞技场（Reasoning-Gym）改进了评估指标：推理竞技场社区讨论了 MATH-P-Hard 测试集上的性能下降问题，并发布了一个新的拉取请求（pull request），用于图着色问题（Graph Coloring Problems）。该请求对数据集进行了标准化，并使用统一的提示（prompts）来简化评估流程，提高输出结果的机器可读性。更多详细信息，请参考该 PR。]

Updates such as the Futoshiki puzzle dataset aim for cleaner solvers and improved logical frameworks, as seen in this PR, coupled with establishing a standard method for averaging scores across datasets for consistent reporting.

类似于 Futoshiki 谜题数据集的更新，其目标是提供更简洁的求解器和更完善的逻辑框架，正如本次 PR（Pull Request）中所展示的。同时，这类更新也致力于建立一套标准化的方法，用于计算跨数据集的平均分数，从而确保报告结果的一致性。

DeepSeek Automates Kernel Generation: NVIDIA presents the use of the DeepSeek-R1 model to automatically generate numerically correct kernels for GPU applications, optimizing them during inference.

DeepSeek 自动化内核生成：NVIDIA 展示了使用 DeepSeek-R1 模型来自动生成用于 GPU 应用的数值上正确的内核，并在推理过程中对它们进行优化。

The generated kernels achieved 100% accuracy on Level-1 problems and 96% on Level-2 issues of the KernelBench benchmark, but concerns were voiced about the saturation of the benchmark.

生成的代码在 KernelBench 测试的 Level-1 问题上达到了 100% 的准确率，在 Level-2 问题上达到了 96% 的准确率，但有人担心该测试的区分能力不足。

Interconnects (Nathan Lambert) Discord

GRPO Turbocharges Tulu Pipelines: Switching from PPO to GRPO in the Tulu pipeline resulted in a 4x performance gain, with the new Llama-3.1-Tulu-3.1-8B model showcasing advancements in both MATH and GSM8K benchmarks, as Costa Huang announced.

互连（Nathan Lambert）Discord

GRPO 加速 Tulu 流水线：正如 Costa Huang 宣布的那样，在 Tulu 流水线中，从 PPO 切换到 GRPO 后，性能提升了 4 倍。新的 Llama-3.1-Tulu-3.1-8B 模型在 MATH 和 GSM8K 基准测试中展示了进步。

This transition signifies a notable evolution from earlier models introduced last fall.

Anthropic's Claude Gets Reasoning Slider: Anthropic's upcoming Claude model will fuse a traditional LLM with reasoning AI, enabling developers to fine-tune reasoning levels via a sliding scale, potentially surpassing OpenAI's o3-mini-high in several benchmarks, per Stephanie Palazzolo's tweet.

这种转变预示着，它相较于去年秋季发布的早期模型，有了显著的进步。

Anthropic 的 Claude 模型新增推理调节功能：据 Stephanie Palazzolo 在社交媒体上透露，Anthropic 即将推出的 Claude 模型，会将传统的大语言模型（LLM）与推理 AI 相结合。新模型允许开发者通过一个滑动调节器，来精细控制模型的推理能力。在一些评测基准上，它的表现甚至可能超过 OpenAI 的 o3-mini-high 模型。

This represents a shift in model training and operational capabilities designed for coding tasks.

DeepHermes-3 Thinks Deeply, Costs More: Nous Research introduced DeepHermes-3, an LLM integrating reasoning with language processing, which can toggle long chains of thought to boost accuracy at the cost of greater computational demand, as noted in Nous Research's announcement.

这标志着在模型训练和操作能力上，针对编码任务进行了一次重要升级。

DeepHermes-3：更深入的推理，更高的成本：Nous Research 发布了 DeepHermes-3，这是一个融合了推理和语言处理能力的大语言模型（LLM/Large Language Model）。正如 Nous Research 在公告中指出的，该模型可以通过启用更长的推理链来提升准确性，但同时也需要消耗更多的计算资源。

The evaluation metrics and comparison with Tulu models sparked debate due to benchmark score discrepancies, specifically with the omission of comparisons to the official 8b distill release, which boasts higher scores (~36-37% GPQA versus r1-distill's ~49%).

评估指标以及与 Tulu 模型的比较之所以引发争议，主要是因为基准测试的分数存在差异。具体来说，报告中省略了与官方 8b distill 版本的对比，而该版本的基准分数更高（GPQA 约为 36 - 37 %，而 r1-distill 版本约为 49 %）。

EnigmaEval's Puzzles Stump AI: Dan Hendrycks unveiled EnigmaEval, a suite of intricate reasoning challenges where AI systems struggle, scoring below 10% on normal puzzles and 0% on MIT-level challenges, per Hendrycks' tweet.

EnigmaEval 谜题集让 AI 束手无策：Dan Hendrycks 公布了 EnigmaEval，这是一系列设计精巧、极具挑战性的推理谜题。在这些谜题面前，人工智能（AI）系统表现不佳。正如 Hendrycks 在推文中所说，AI 在普通难度谜题上的正确率低于 10%，而在麻省理工学院（MIT）难度的谜题中，正确率更是直接降至 0%。

This evaluation aims to push the boundaries of AI reasoning capabilities.

OpenAI Signals AGI Strategy Shift: Sam Altman hinted that OpenAI's current strategy of scaling up will no longer suffice for AGI, suggesting a transition as they plan to release GPT-4.5 and GPT-5; OpenAI will integrate its systems to provide a more seamless experience.

本次评估旨在拓展 AI 的推理能力边界。

OpenAI 暗示通用人工智能（AGI）战略转变：Sam Altman 暗示，OpenAI 当前的规模扩张战略可能不足以支撑其实现通用人工智能（AGI）的目标。这表明，随着 GPT-4.5 和 GPT-5 的发布计划提上日程，OpenAI 可能会进行战略转型；OpenAI 计划整合其现有系统，从而提供更加流畅和一体化的用户体验。

They will also address community frustrations with the model selection step.

Eleuther Discord

他们还将解决社区对模型选择环节的不满。

Eleuther Discord

Debate Emerges on PPO-Clip's Utility: Members rehashed applying PPO-Clip with different models to generate rollouts, echoing similar ideas from past conversations.

关于 PPO-Clip 实用性的讨论浮出水面： 成员们再次探讨了将 PPO-Clip（Proximal Policy Optimization Clip）应用于不同模型以生成 rollouts（轨迹数据）的方法，这与之前的讨论内容相似。

A member voiced skepticism regarding this approach's effectiveness based on previous attempts.

Forgetting Transformer Performance Tuned: A conversation arose around the Forgetting Transformer, particularly if changing from sigmoid to tanh activation could positively impact performance.

一位成员表示，根据以往的经验，他对这种方法的有效性持保留态度。

关于遗忘 Transformer 的性能调优：大家围绕遗忘 Transformer 展开了讨论，特别是将 sigmoid 激活函数（sigmoid activation）更改为 tanh 激活函数（tanh activation）是否能有效提升性能。

The conversation also entertained introducing negative attention weights, underscoring potential sophistication in attention mechanisms.

Citations of Delphi Made Easier: Members suggested it's beneficial to combine citations for Delphi from both the paper and the GitHub page for comprehensive attribution.

对话还探讨了引入负注意力权重，这突显了注意力机制（attention mechanisms）中可能存在的复杂性。

更方便地引用 Delphi：为了更全面地进行引用，有成员建议将 Delphi 的论文和 GitHub 页面上的引用信息合并。

It was also suggested that one use arXiv's autogenerated BibTeX entries for common papers for standardization purposes.

Hashing Out Long Context Model Challenges: Members highlighted concerns about the challenges associated with current benchmarks for long context models like HashHop and the iterative nature of solving 1-NN.

也有人建议，为了标准化起见，可以使用 arXiv 自动生成的 BibTeX 条目来引用常用论文。

深入探讨长文本模型面临的挑战： 成员们着重强调了当前长文本模型的评测基准所存在的挑战，例如 HashHop 以及解决 1-NN（1-Nearest Neighbor）问题的迭代特性。

Questions arose around the theoretical feasibility of claims made by these long context models.

Stability.ai (Stable Diffusion) Discord

关于这些长文本模型所宣称的性能，其理论上的可行性引起了一些疑问。

Stability.ai（Stable Diffusion）Discord 讨论区

Stable Diffusion users fail to save progress: A user reported losing generated images due to not having auto-save enabled in Stable Diffusion, then inquired about image recovery options.

Stable Diffusion 用户遇到无法保存进度的问题：有用户反映，因为没有开启 Stable Diffusion 的自动保存功能，导致生成的图片丢失，并询问是否有办法恢复这些图片。

The resolution to this problem involved debugging which web UI version they had in order to determine the appropriate save settings.

Linux throws ComfyUI users OOM Errors: A user switching from Windows to Pop Linux experienced Out Of Memory (OOM) errors in ComfyUI despite previous success.

解决此问题的关键在于调试 Web UI 的版本，以确定合适的保存设置。

Linux 系统下 ComfyUI 用户遇到 OOM 错误：一位用户从 Windows 切换到 Pop Linux 后，在使用 ComfyUI 时遇到了内存溢出（Out Of Memory，OOM）错误，这在他之前的 Windows 系统上从未发生过。

The community discussed confirming system updates and recommended drivers, highlighting the differences in dependencies between operating systems.

Character Consistency Challenges Plague AI Models: A user struggled with maintaining consistent character designs across models, sparking suggestions to use Loras and tools like FaceTools and Reactor.

社区讨论了系统更新的确认以及推荐驱动，并着重说明了不同操作系统之间存在的依赖关系差异。

AI 模型面临角色一致性难题：一位用户尝试在不同的模型中保持角色设计的一致性时遇到了困难，由此引发了关于使用 Loras、FaceTools 以及 Reactor 等工具的建议。

Recommendations emphasized selecting models designed for specific tasks.

Stability's Creative Upscaler Still MIA: Users questioned the release status of Stability's creative upscaler, with assertions it hadn't been released yet.

推荐重点在于选择专门为特定任务设计的模型。

Stability 的 Creative Upscaler 依然下落不明（Missing In Action，MIA)：用户询问 Stability 的 creative upscaler 的发布情况，并表示该工具尚未发布。

Discussions included the impact of model capabilities on requirements like memory and performance.

Account Sharing Questioned: A user's request to borrow a US Upwork account for upcoming projects triggered skepticism.

讨论内容涵盖了模型能力对诸如内存和性能等硬件需求的影响。

Upwork 账号共享惹争议：有用户提出借用美国地区的 Upwork 账号，以进行后续项目，这一请求引发了人们的担忧和质疑。

Members raised concerns about the feasibility and implications of 'borrowing' an account.

Latent Space Discord

成员们对「共享」账户的可行性和潜在影响提出了担忧。

Latent Space Discord

OpenAI Unifies Models with GPT-4.5/5: OpenAI is streamlining its product offerings by unifying O-series models and tools in upcoming releases of GPT-4.5 and GPT-5, per their roadmap update.

OpenAI 利用 GPT-4.5/5 统一模型：根据 OpenAI 最新的路线图更新，他们计划在即将发布的 GPT-4.5 和 GPT-5 中统一 O 系列模型和工具，以此来简化其产品线。

This aims to simplify the AI experience for developers and users by integrating all tools and features more cohesively.

Anthropic Follows Suit with Reasoning AI: Anthropic plans to soon launch a new Claude model that combines traditional LLM capabilities with reasoning AI, controllable via a token-based sliding scale, according to Stephanie Palazzolo's tweet.

这旨在通过更紧密地整合所有工具和功能，来简化开发者和用户的 AI 体验。

Anthropic 推出具备推理能力的 AI 模型：根据 Stephanie Palazzolo 的推文，Anthropic 计划很快推出一种新的 Claude 模型，该模型将传统的大语言模型（LLM/Large Language Model）能力与推理 AI 相结合，并允许通过基于 Token 的滑动条进行控制。

This echoes OpenAI's approach, signaling an industry trend towards integrating advanced reasoning directly into AI models.

DeepHermes 3 Reasoning LLM Preview Released: Nous Research has unveiled a preview of DeepHermes 3, an LLM integrating reasoning capabilities with traditional response functionalities to boost performance, detailed on HuggingFace.

这与 OpenAI 的策略不谋而合，预示着一种行业趋势：将高级推理能力直接融入 AI 模型中。

DeepHermes 3 推理大语言模型（LLM）预览版发布：Nous Research 在 HuggingFace 上发布了 DeepHermes 3 的预览版本。这款大语言模型（LLM）融合了推理能力与传统响应功能，旨在提升模型性能。

The new model seeks to deliver enhanced accuracy and functionality as a step forward in LLM development.

Meta Hardens Compliance with LLM-Powered Tool: Meta has introduced its Automated Compliance Hardening (ACH) tool, which utilizes LLM-based test generation to bolster software security by creating undetected faults for testing, explained in Meta's engineering blog.

新的模型旨在提供更高的准确性和功能性，作为大语言模型开发向前迈出的一步。

Meta 强化了由大语言模型驱动的工具的合规性：Meta 推出了其自动化合规性加强（Automated Compliance Hardening，ACH）工具，该工具利用基于大语言模型的测试生成来增强软件安全性，通过创建难以检测的错误来进行测试，这在 Meta 的工程博客中进行了解释。

This tool aims to enhance privacy compliance by automatically generating unit tests targeting specific fault conditions in code.

Yannick Kilcher Discord

这个工具旨在通过自动生成单元测试来增强隐私保护合规性，这些单元测试专门针对代码中特定的错误情况。

Yannick Kilcher Discord

Hugging Face Launches Smolagents: Hugging Face has launched smolagents, an agent framework alternative to deep research, with a processing time of approximately 13 seconds for 6 steps.

Hugging Face 发布 Smolagents：Hugging Face 发布了 smolagents，这是一个 AI 智能体（AI Agent）框架，旨在提供深度研究之外的另一种选择。在 6 个步骤的处理流程中，它大约需要 13 秒。

Users can modify the original code to extend execution when run on a local server, providing adaptability.

Musk Claims Grok 3 Outperforms Rivals: Elon Musk announced his new AI chatbot, Grok 3, is nearing release and outperforms existing models in reasoning capabilities, with a launch expected in about two weeks.

用户可以修改原始代码，从而在本地服务器上运行时扩展其功能，实现更好的适应性。

马斯克表示 Grok 3 性能超越竞品：埃隆·马斯克宣布，他的全新 AI 聊天机器人 Grok 3 接近完成，在推理能力上超过了目前已有的模型，预计将在两周左右发布。

This follows Musk's investor group's $97.4 billion bid to acquire OpenAI's nonprofit assets amid ongoing legal disputes with the company.

Thomson Reuters Wins Landmark AI Copyright Case:

此前，马斯克（Musk）的投资集团曾出价 974 亿美元，试图收购 OpenAI 的非营利性资产，但目前 OpenAI 正与该公司存在法律纠纷。

汤森路透（Thomson Reuters）赢得里程碑式的 AI 版权案件：