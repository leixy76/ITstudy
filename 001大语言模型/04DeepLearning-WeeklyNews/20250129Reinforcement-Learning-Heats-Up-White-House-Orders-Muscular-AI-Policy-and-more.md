## Reinforcement-Learning-Heats-Up-White-House-Orders-Muscular-AI-Policy-and-more

[Reinforcement Learning Heats Up, White House Orders Muscular AI Policy, and more...](https://www.deeplearning.ai/the-batch/issue-286/)

Jan 29, 2025

Dear friends,

亲爱的朋友们，

The buzz over DeepSeek this week crystallized, for many people, a few important trends that have been happening in plain sight: (i) China is catching up to the U.S. in generative AI, with implications for the AI supply chain. (ii) Open weight models are commoditizing the foundation-model layer, which creates opportunities for application builders. (iii) Scaling up isn’t the only path to AI progress. Despite the massive focus on and hype around processing power, algorithmic innovations are rapidly pushing down training costs.

本周关于 DeepSeek 的热烈讨论，让很多人明确了几个早已显现的重要趋势：第一，中国在生成式 AI（Generative AI）领域正迎头赶上美国，这将对 AI 供应链产生影响。第二，开放权重模型正在将基础模型层转变为一种通用商品，这为应用开发者创造了更多机会。第三，持续扩大规模并非实现 AI 进步的唯一途径。尽管算力一直备受关注和热捧，但算法创新正在快速降低训练成本。

Here’s what I think DeepSeek has caused many people to realize:

DeepSeek 的出现让许多人意识到：

China is catching up to the U.S. in generative AI. When ChatGPT was launched in November 2022, the U.S. was significantly ahead of China in generative AI. Impressions change slowly, and so even recently I heard friends in both the U.S. and China say they thought China was behind. But in reality, this gap has rapidly eroded over the past two years. With models from China such as Qwen (which my teams have used for months), Kimi, InternVL, and DeepSeek, China had clearly been closing the gap, and in areas such as video generation there were already moments where China seemed to be in the lead.

中国正在生成式 AI 领域赶上美国。当 ChatGPT 于 2022 年 11 月推出时，美国在生成式 AI 领域明显领先于中国。人们的印象转变需要时间，所以即使最近，我还听到一些美国和中国的朋友认为中国在该领域仍然落后。但实际上，过去两年里这种差距迅速缩小。得益于来自中国的模型，例如 Qwen（我的团队已经使用了几个月）、Kimi、InternVL 和 DeepSeek，中国显然一直在缩小差距，在视频生成等领域，中国甚至在某些时候已经展现出领先的势头。

I’m thrilled that DeepSeek-R1 was released as an open weight model, with a technical report that shares many details. In contrast, a number of U.S. companies have pushed for regulation to stifle open source by hyping up hypothetical AI dangers such as human extinction. It is now clear that open source/open weight models are a key part of the AI supply chain: Many companies will use them. If the U.S. continues to stymie open source, China will come to dominate this part of the supply chain and many businesses will end up using models that reflect China’s values much more than America’s.

我很高兴 DeepSeek-R1 以开放权重模型发布，并且有一份技术报告分享了很多细节。相比之下，一些美国公司一直在推动监管，通过夸大诸如人类灭绝等假想中的 AI 风险，试图扼杀开源。现在很明显，开源 / 开放权重模型是 AI 供应链中的一个关键环节：许多公司将会使用它们。如果美国继续阻碍开源，中国将主导该供应链的这一环节，并且许多企业最终会使用更符合中国价值观，而非美国价值观的模型。

Open weight models are commoditizing the foundation-model layer. As I wrote previously, LLM token prices have been falling rapidly, and open weights have contributed to this trend and given developers more choice. OpenAI’s o1 costs $60 per million output tokens; DeepSeek R1 costs $2.19. This nearly 30x difference brought the trend of falling prices to the attention of many people.

开放权重模型正在推动基础模型层走向商品化。正如我之前所写的那样，大语言模型（LLM/Large Language Model）的 Token 价格一直在快速下降，开放权重促成了这一趋势，并为开发者提供了更多选择。例如，OpenAI 的 o1 模型，其成本为每百万个输出 Token 60 美元；而 DeepSeek 的 R1 模型，成本仅为 2.19 美元。正是这近 30 倍的巨大差异，让人们开始关注价格下跌的趋势。

Blue whale logo biting and breaking a computer chip, with debris flying.

蓝鲸 logo 咬碎一块电脑芯片，碎片飞溅。

The business of training foundation models and selling API access is tough. Many companies in this area are still looking for a path to recouping the massive cost of model training. The article “AI’s $600B Question” lays out the challenge well (but, to be clear, I think the foundation model companies are doing great work, and I hope they succeed). In contrast, building applications on top of foundation models presents many great business opportunities. Now that others have spent billions training such models, you can access these models for mere dollars to build customer service chatbots, email summarizers, AI doctors, legal document assistants, and much more.

训练基础模型和销售 API 接口的业务并不好做。很多公司依然在探索如何收回训练模型所消耗的巨额成本。「AI's $600B Question」一文很好地阐述了这一难题（需要声明的是，我认为这些基础模型公司做出了卓越的贡献，并且衷心祝愿他们取得成功）。相比之下，基于基础模型构建应用则蕴藏着巨大的商机。如今，其他公司已经投入数十亿美元训练出这些模型，开发者只需花费少量资金就能调用它们，从而构建各种应用，例如客户服务聊天机器人、邮件总结工具、AI 医生、法律文档助手等等。

Scaling up isn’t the only path to AI progress. There’s been a lot of hype around scaling up models as a way to drive progress. To be fair, I was an early proponent of scaling up models. A number of companies raised billions of dollars by generating buzz around the narrative that, with more capital, they could (i) scale up and (ii) predictably drive improvements. Consequently, there has been a huge focus on scaling up, as opposed to a more nuanced view that gives due attention to the many different ways we can make progress. Driven in part by the U.S. AI chip embargo, the DeepSeek team had to innovate on many optimizations to run on less-capable H800 GPUs rather than H100s, leading ultimately to a model trained (omitting research costs) for under $6M of compute.

规模化并非是人工智能（AI）进步的唯一途径。将模型规模化作为推动进步的手段，存在过多的炒作。平心而论，我早期也曾是模型规模化的倡导者。一些公司正是通过制造这种声势，宣称拥有更多资金就能（i）扩大模型规模，(ii）从而可预测地提升模型性能，以此募集到数十亿美元。因此，业界过度关注了规模的扩大，而忽略了其他同样能推动进步的多种途径。由于美国对 AI 芯片的禁运，DeepSeek 团队不得不进行诸多优化创新，以便在性能相对较弱的 H800 GPU 上（而非 H100）运行模型，最终将一个模型的训练成本控制在 600 万美元以内（未计入研发成本）。

It remains to be seen if this will actually reduce demand for compute. Sometimes making each unit of a good cheaper can result in more dollars in total going to buy that good. I think the demand for intelligence and compute has practically no ceiling over the long term, so I remain bullish that humanity will use more intelligence even as it gets cheaper.

这是否真的能减少对算力的需求，还有待观察。有时，降低某个东西的单价反而可能导致人们在该事物上花费更多的钱。我认为，从长远来看，对智能和算力的需求几乎没有上限，所以我仍然很乐观，即使智能变得越来越便宜，人类也会更多地使用它。

I saw many different interpretations of DeepSeek’s progress on social media, as if it was a Rorschach test that allowed many people to project their own meaning onto it. I think DeepSeek-R1 has geopolitical implications that are yet to be worked out. And it’s also great for AI application builders. My team has already been brainstorming ideas that are newly possible only because we have easy access to an open advanced reasoning model. This continues to be a great time to build!

我在社交媒体上看到了对 DeepSeek 进展的各种解读，就像一面镜子，不同的人都能从中看到自己想看到的东西。我认为 DeepSeek-R1 具有地缘政治意义，这些影响还有待进一步显现。同时，它对人工智能应用开发者也大有裨益。我的团队已经在积极讨论，涌现出许多新的想法，这些想法的实现，都得益于我们能够轻松使用这种开放的高级推理模型。现在，仍然是创造的绝佳时代！

Keep learning,

Andrew

### News

新闻

Diagram of a reinforcement learning system for training LLMs, showing data and weight flow processes.

用于训练大语言模型的强化学习系统的图表，展示了数据和权重流动过程。

#### Reinforcement Learning Heats Up

强化学习成为热点

Reinforcement learning is emerging as an avenue for building large language models with advanced reasoning capabilities.

强化学习正在成为构建具有高级推理能力的大语言模型的途径。

What’s new: Two recent high-performance models, DeepSeek-R1 (and its variants including DeepSeek-R1-Zero) and Kimi k1.5, learned to improve their generated lines of reasoning via reinforcement learning. o1 pioneered this approach last year.

最新进展：最近，DeepSeek-R1（以及它的变体，包括 DeepSeek-R1-Zero）和 Kimi k1.5 这两个高性能模型，通过强化学习，学会了改进它们生成的推理过程。o1 公司去年率先使用了这种方法。

Reinforcement learning (RL) basics: RL rewards or punishes a model for performing particular actions or achieving certain objectives. Unlike supervised and unsupervised learning, which compare the model's output to a known ground truth, RL doesn’t explicitly tell a model what it should output. Instead, the model starts out behaving randomly and discovers desired behaviors by earning rewards for its actions. This makes RL especially popular for training machine learning models that play games or control robots.

强化学习（RL）基础：强化学习通过奖励或惩罚的方式，来引导模型执行特定的动作或达成某些目标。与监督学习和无监督学习不同，后两者会将模型的输出与已知的标准答案进行比较，而强化学习则不会明确告知模型应该输出什么。相反，模型最初会随机行动，然后通过其行为所获得的奖励来逐步发现期望的行为模式。因此，强化学习在训练那些能够玩游戏或控制机器人的机器学习模型中尤其受欢迎。

How it works: To improve the chain of thought (CoT) generated by a large language model (LLM), reinforcement learning encourages the model to generate correct solutions to math, coding, science, and other problems that have known solutions. Unlike typical LLM training, in which the model simply generates the next token of its output and receives feedback token by token, this method rewards the model for generating a sequence of reasoning steps that lead to an accurate conclusion, even if doing so requires generating many intermediate tokens between the prompt and the response — to plan an outline, check the conclusion, or reflect on the approach — without explicit training on the reasoning steps to take.

工作原理：为了改进由大语言模型（LLM）生成的思维链（CoT，Chain of Thought），强化学习鼓励模型为数学、编程、科学和其他具有已知解决方案的问题生成正确的解决方案。与典型的大语言模型训练不同，在典型的大语言模型训练中，模型会生成输出的下一个 Token（Token），并逐个 Token（Token）接收反馈，而这种方法会奖励模型，如果它能生成一系列推理步骤并最终得出准确的结论，即使这样做需要在提示和响应之间生成许多中间 Token（Token）才能计划大纲、检查结论或反思方法，且无需针对推理步骤进行明确的训练。

1 The DeepSeek team found that fine-tuning via reinforcement learning alone (after pretraining) was sufficient for DeepSeek-R1-Zero to learn problem-solving strategies like double checking its answer. However, the model also showed quirky behaviors such as mixing different languages in its output. The team overcame these issues in DeepSeek-R1 by supervised fine-tuning on a small number of long CoT examples prior to reinforcement learning.

DeepSeek 团队发现，仅通过强化学习进行微调（在预训练之后）就足以让 DeepSeek-R1-Zero 学习到解决问题的策略，例如双重检查答案。不过，该模型也出现了一些奇怪的现象，比如在输出中混合使用不同的语言。为了解决这些问题，DeepSeek-R1 团队在进行强化学习之前，先用少量长链式思维（Chain of Thought，CoT）示例进行了监督式微调。

2 Similarly, the Kimi k1.5 team found that fine-tuning the model on long CoTs prior to reinforcement learning enabled it to devise its own problem-solving strategies. The resulting long responses proved to be more accurate but also more expensive to generate, so the team added a second round of reinforcement learning that encouraged the model to produce shorter responses. On the AIME 2024 benchmark of advanced math problems, this process reduced the average number of tokens in the response by around 20 percent, and on MATH-500, it cut the average number of output tokens by roughly 10 percent.

类似地，Kimi k1.5 团队发现，在强化学习之前，先用长链式思维（CoT）对模型进行微调，可以使模型能够设计自己的问题解决策略。实验表明，由此产生的长回复虽然更准确，但生成成本也更高。因此，该团队增加了第二轮强化学习，以鼓励模型生成更短的回复。在 AIME 2024 高级数学问题基准测试中，这一过程使回复的平均 Token 数量减少了约 20%，而在 MATH-500 测试中，输出 Token 的平均数量减少了约 10%。

3 OpenAI has disclosed limited information about how it trained o1, but team members have said they used reinforcement learning to improve the model’s chain of thought.

OpenAI 披露的关于如何训练 o1 模型的信息有限，但团队成员表示，他们使用了强化学习来改进模型的思维链。

Behind the news: While RL has been a staple technique for training models to play games and control robots, its role in developing LLMs has been confined to alignment with human preferences. Reinforcement learning to match judgements of humans (reinforcement learning from human feedback, or RLHF) or AI (Constitutional AI, which uses reinforcement learning from AI feedback or RLAIF) were the primary methods for encouraging LLMs to align with human preferences prior to the development of direct preference optimization.

新闻背景：虽然强化学习（RL）一直是训练模型玩游戏和控制机器人的主要技术手段，但它在大语言模型（Large Language Model，LLM）开发中的作用主要集中在与人类偏好对齐上。在直接偏好优化（Direct Preference Optimization）技术出现之前，主要通过强化学习来匹配人类的判断（从人类反馈中进行强化学习，Reinforcement Learning from Human Feedback，RLHF）或是 AI 的判断（宪法 AI，它使用从 AI 反馈中进行强化学习，Reinforcement Learning from AI Feedback，RLAIF），以此来鼓励大语言模型与人类的偏好保持一致。

Why it matters: Reinforcement learning has surprising utility in training large language models to reason. As researchers press models into service in more complex tasks — math, coding, animated graphics, and beyond — reinforcement learning is emerging as an important path to progress.

为什么重要： 强化学习在训练大语言模型进行推理方面展现出令人惊喜的作用。随着研究人员将大语言模型应用于更复杂的任务，例如数学、编程、动画图像等，强化学习正在成为取得进展的重要方法。

We’re thinking: Less than three years ago, reinforcement learning looked too finicky to be worth the trouble. Now it’s a key direction in language modeling. Machine learning continues to be full of surprising twists!

回顾过去：不到三年前，强化学习看起来还过于复杂，让人觉得不值得尝试。而现在，它已经成为语言建模（Language Modeling）的一个关键方向。机器学习领域总是充满着令人意想不到的惊喜！

#### Computer Use Gains Momentum

计算机应用方兴未艾

OpenAI introduced an AI agent that performs simple web tasks on a user’s behalf.

OpenAI 推出了一款 AI 智能体，它可以代替用户完成一些简单的网络操作。

What’s new: Operator automates online actions like buying goods, booking tickets and completing forms by navigating websites in a browser-like environment within ChatGPT. It’s available on desktops as a research preview for subscribers to ChatGPT Pro ($200 per month). OpenAI promises broader availability to come as well as API access to the underlying model and improved ability to coordinate multi-step tasks like scheduling meetings across calendars from different vendors.

最新动态：Operator（Operator）通过在 ChatGPT 中模拟浏览器环境来访问网站，从而自动执行在线操作，比如购买商品、预订机票和填写表格。目前，它以研究预览版的形式在桌面端向 ChatGPT Pro 订阅用户开放（每月 200 美元）。OpenAI 承诺未来将进一步扩大使用范围，并提供底层模型的应用程序编程接口（API）访问权限，以及提升协调多步骤任务的能力，例如在不同服务商的日历上安排会议。

How it works: Operator uses a new model called Computer-Using Agent (CUA) that accepts text input and responds with web actions.

它是如何工作的：Operator 使用了一种名为计算机使用智能体（Computer-Using Agent，CUA）(CUA）的新模型，该模型接受文本输入并通过 Web 操作做出响应。

1 Users type commands into ChatGPT. CUA translates these inputs into structured instructions executes them by interacting directly with web elements like buttons, menus, and text fields. OpenAI didn’t disclose CUA’s architecture or training methods but said it was trained on simulated and real-world browser scenarios via reinforcement learning.

用户将命令输入到 ChatGPT 中。CUA 将这些输入转换为结构化指令，并通过与网页上的各种元素，比如按钮、菜单和文本框等直接互动来执行这些指令。OpenAI 并未公开 CUA 的具体架构和训练方法，但提到 CUA 是通过强化学习，在模拟和真实环境的浏览器使用场景中训练而成。

2 CUA earns high marks on some measures in tests performed by OpenAI. On WebVoyager, which evaluates web tasks, CUA succeeded 87 percent of the time. On OSWorld, a benchmark that evaluates the ability of multimodal agents to perform complex tasks that involve real-world web and desktop apps, CUA achieved a success rate of 38.1 percent. In separate tests performed by Kura and Anthropic, on WebVoyager, Kura achieved 87 percent while DeepMind’s Mariner achieved 83.5 percent, and on OSWorld, Claude Sonnet 3.5 with Computer Use achieved 22 percent.

在 OpenAI 执行的测试中，CUA 在某些指标上获得了高分。在评估 Web 任务的 WebVoyager 上，CUA 的成功率为 87%。在 OSWorld 上，这是一个基准测试，用于评估多模态智能体在执行复杂任务时的能力，这些任务涉及真实的 Web 应用和桌面应用。CUA 在该测试中的成功率为 38.1%。在 Kura 和 Anthropic 执行的单独测试中，在 WebVoyager 上，Kura 的成功率为 87%，而 DeepMind 的 Mariner 的成功率为 83.5%；在 OSWorld 上，集成了计算机使用功能的 Claude Sonnet 3.5 的成功率为 22%。

3 Operator is restricted from interacting with unverified websites and sharing sensitive data without the user’s consent. It offers content filters, and a separate model monitors Operator in real time and pauses the agent in case of suspicious behavior.

Operator 被限制与未经授权的网站进行互动，并且在未经用户许可的情况下，无法分享敏感信息。它提供内容过滤器，并且一个单独的模型实时监控 Operator，并在出现可疑行为时暂停智能体。

Behind the news: Operator rides a wave of agents designed to automate everyday tasks. Last week, OpenAI introduced ChatGPT Tasks, which lets users schedule reminders and alerts but doesn’t support web interaction. (Early users complained that Tasks was buggy and required overly precise instructions.) Anthropic’s Computer Use focuses on basic desktop automation, while DeepMind’s Project Mariner is a web-browsing assistant built on Gemini 2.0. Perplexity Assistant automates mobile apps such as booking Uber rides on Android phones.

背景信息：Operator 的出现，是自动化日常任务这一智能体浪潮中的一部分。上周，OpenAI 推出了 ChatGPT Tasks，它允许用户安排提醒和警报，但不支持 Web 交互（Early users complained that Tasks was buggy and required overly precise instructions.）。Anthropic 的 Computer Use 主要关注基础的桌面自动化，而 DeepMind 的 Project Mariner 则是一个基于 Gemini 2.0 构建的网页浏览助手。Perplexity Assistant 可以自动化移动应用，例如在 Android 手机上预订 Uber 行程。

Why it matters: In early reports, users said Operator sometimes was less efficient than a human performing the same tasks. Nevertheless, agentic AI is entering the consumer market, and Operator is poised to give many people their first taste. It’s geared to provide AI assistance for an endless variety of personal and business uses, and — like ChatGPT was for other developers of LLMs — and it’s bound to serve as a template for next-generation products.

为什么重要：在早期的报告中，用户指出 Operator 在执行某些任务时，效率有时不如人工。尽管如此，AI 智能体（AI Agent）正在快速进入消费市场，而 Operator 有望让众多用户首次体验到 AI 智能体的能力。它的设计目标是为各种个人和商业场景提供 AI 辅助。正如 ChatGPT 对其他大语言模型（LLM/Large Language Model）开发者具有重要意义一样，Operator 也很可能成为下一代 AI 产品的设计蓝本。

We’re thinking: Computer use is maturing, and the momentum behind it is palpable. AI developers should have in their toolbox.

我们认为：计算机应用日趋成熟，其发展势头有目共睹。AI 开发者应将相关技术纳入工具箱中。

#### White House Orders Muscular AI Policy

白宫颁布强力 AI 政策

Under a new president, the United States reversed its approach to AI regulation, seeking global dominance by reducing restrictions.

在美国新任总统的领导下，一改以往的 AI 监管策略，转而通过减少限制，积极寻求全球领先地位。

What’s new: President Trump, who took office last week, signed an executive order that set a 180-day deadline to draft an AI Action Plan. The order aims to boost national security, economic competitiveness, and U.S. leadership in artificial intelligence.

最新消息：上周刚刚就职的特朗普总统签署了一项行政命令，设定了 180 天的期限，用于制定一份人工智能（Artificial Intelligence）行动方案。这项命令旨在加强国家安全、提高经济竞争力，并巩固美国在人工智能领域的领导地位。

How it works: The executive order assigns responsibility for crafting the AI Action Plan to three key figures in the administration: Michael Kratsios, assistant to the president for science and technology (and former managing director of Scale AI); venture capitalist David Sacks, the new special advisor for AI and cryptocurrency; and national security advisor Michael Waltz.

它是如何运作的：这项行政命令指定了三位政府要员负责制定 AI 行动计划：总统科学和技术助理 Michael Kratsios（曾任 Scale AI 总经理)；风险投资家 David Sacks，新任 AI 和加密货币特别顾问；以及国家安全顾问 Michael Waltz。

1 The AI Action Plan must “sustain and enhance America’s global AI dominance in order to promote human flourishing, economic competitiveness, and national security.”

AI 行动计划必须「维持和加强美国在全球人工智能领域的领先地位，以促进人类繁荣、经济竞争力和国家安全」。

2 The order directs agency heads to suspend or eliminate policies created under President Biden’s 2023 executive order, which President Trump revoked, that may conflict with advancing U.S. AI dominance and national security.

该命令指示各机构负责人暂停或取消在前总统拜登 2023 年行政命令下制定的政策（特朗普总统已撤销该命令），这些政策可能与提升美国人工智能领先地位和国家安全相冲突。

3 U.S. companies are to develop AI systems “free from ideological bias or engineered social agendas,” reflecting the administration’s belief that AI systems encode liberal political biases.

美国公司应开发「免受意识形态偏见或人为设定的社会目标影响」的人工智能系统，这反映了本届政府的观点，即人工智能系统带有自由主义的政治偏见。

4 The order directs the federal Office of Management and Budget to award government contracts to AI companies that align with the administration’s emphasis on advancing U.S. competitiveness and national security.

该命令指示联邦管理和预算办公室（OMB）将政府合同授予符合本届政府关于提升美国竞争力和国家安全的重点的人工智能公司。

5 Most provisions leave significant discretion to the team that will draft the action plan, making their interpretation and implementation open-ended.

大多数条款为将起草行动计划的团队留下了很大的自由裁量权，使其解释和实施具有开放性，具体体现在 [此处需要补充说明开放性体现在哪些方面]。

AI infrastructure build-out: Along with the executive order, President Trump announced Stargate, a joint venture that involves OpenAI, Oracle, and SoftBank. The three companies outlined a plan to invest $100 billion in computing infrastructure for AI, such as next-generation data centers, and $500 billion over four years. In addition, the administration declared a national energy emergency with respect to U.S. supplies of energy and issued an order to ramp up domestic energy production. These measures aim to support energy-intensive AI initiatives like Stargate by removing regulatory barriers to building oil, gas, and renewable energy projects on federal lands.

人工智能基础设施建设：伴随该行政命令，特朗普总统宣布了 Stargate，这是一个涉及 OpenAI、Oracle 和软银的合资企业。这三家公司概述了一项计划，即投资 1000 亿美元用于人工智能计算基础设施，例如下一代数据中心，并在四年内投资 5000 亿美元。此外，本届政府宣布美国能源供应进入国家能源紧急状态，并发布命令以提高国内能源产量。这些措施旨在通过消除在联邦土地上建设石油、天然气和可再生能源项目的监管障碍，来支持 Stargate 这样能源密集型的人工智能项目。

Why it matters: The Trump administration says that Biden’s 2023 regulations were “onerous and unnecessary,” stifled innovation, and jeopardized U.S. leadership in AI. The new order reduces bureaucratic oversight of AI development, creating a more permissive regulatory environment (except when it comes to ideological bias).

重要性：特朗普政府认为，拜登在 2023 年颁布的法规「过于繁琐，实属多余」，不仅阻碍了创新，还威胁到美国在人工智能（AI）领域的领先地位。这项新命令旨在减少对人工智能开发的行政干预，营造一个更为宽松的监管环境（但在意识形态偏见方面有所收紧）。

We’re thinking: The Biden administration’s 2023 executive order aimed to guard against hypothetical, rather than actual, AI risks. It introduced thresholds of processing used to train models as a measure of their risk — a poorly thought-out proxy. To be fair, the AI Safety Institute under the U.S. National Institute of Standards and Technology didn’t hamper AI progress as much as some had feared, but overall the order was not helpful to AI innovation or safety. We’re pleased that the new administration is focusing on AI progress rather than hypothetical risks.

我们认为：拜登政府 2023 年的行政命令旨在防范的是假想的 AI 风险，而非实际存在的风险。该命令引入了训练模型时使用的处理阈值，并将其作为衡量风险的标准，但这是一个欠考虑的指标。平心而论，美国国家标准与技术研究院（U.S. National Institute of Standards and Technology）下属的 AI 安全研究所，其对 AI 发展的影响并没有像某些人预期的那么大。但总体而言，该行政命令对 AI 创新和安全并没有起到积极作用。我们欣慰地看到，新政府正将重心放在推动 AI 进步上，而不是防范那些假想的风险。

#### Fine-Tuning Fine Points

微调的关键点

Bar chart comparing active vs. random sampling effects on length, diversity, and toxicity after fine-tuning.

条形图比较了微调后，主动采样与随机采样对生成文本的长度、多样性和毒性的影响。

The practice of fine-tuning models on synthetic data is becoming well established. But synthetic training data, even if it represents the training task well, may include characteristics like toxicity that impart unwelcome properties in the trained model’s output, and it may inconsistently represent desired traits such as the target output length. Researchers developed a method that reduces aspects of generated data and retains desired ones.

使用合成数据微调模型正变得越来越普遍。然而，即使合成训练数据与训练任务非常匹配，也可能包含一些不良特征，例如毒性，从而导致训练后模型的输出中出现不受欢迎的属性。此外，合成数据在期望特征（例如目标输出长度）的呈现上可能存在不一致。因此，研究人员开发了一种方法，旨在减少生成数据中的不良因素，同时保留所需的特性。

What’s new: Luísa Shimabucoro and colleagues at Cohere introduced active inheritance, a fine-tuning method that automatically selects synthetic training examples that have desirable characteristics.

最新进展：Luísa Shimabucoro 和 Cohere 公司的同事们提出了一种名为主动继承（active inheritance）的微调方法。该方法能够自动筛选出具备特定优势的合成训练样本。

Key insight: A naive way to generate synthetic fine-tuning data is to feed prompts to a model, collect its output, and use that as the fine-tuning set. But synthetic data is cheap, so we can afford to be more choosy. By generating several responses to each prompt, we can select the one that best suits our purposes.

核心思想：一种简单的生成合成微调数据的方法是，向模型输入提示（prompts），收集模型的输出，并将其用作微调数据集。由于合成数据成本较低，我们可以更有选择性。具体来说，针对每个提示生成多个回复，然后选择最符合我们需求的回复。

How it works: The authors used Llama 2 7B and Mixtral 8x7B as both teachers and students in all combinations. They prompted the models with 52,000 prompts from the Alpaca dataset and used automated methods to evaluate their outputs in terms of characteristics including social bias, toxicity, word count, lexical diversity, and calibration (how well a model’s estimated probabilities match its accuracy).

工作原理：作者使用了 Llama 2 7B 和 Mixtral 8x7B，并将它们在所有可能的组合中分别作为老师和学生。他们使用来自 Alpaca 数据集的 52,000 个提示来引导这些模型，并使用自动化的方法评估模型的输出，评估的指标包括社会偏见、毒性、字数、词汇多样性和校准（Calibration，即模型预测的概率与其真实准确度是否一致）。

1 The authors generated 10 responses to each prompt.

作者针对每个提示（prompt）生成了 10 个回复。

2 For each response, they measured social bias according to StereoSet, CrowS-Pairs, and Bias Benchmark for Question-Answering. They measured toxicity according to Perspective API and their own code. They measured calibration according to HELM. They used TextDescriptives to calculate metrics related to text.

对于每个回复，他们使用 StereoSet、CrowS-Pairs 和 Bias Benchmark for Question-Answering 等基准测试来测量社会偏见。他们使用 Perspective API 以及他们自己编写的代码来测量毒性。他们使用 HELM 来测量模型的校准程度（calibration），即模型的预测准确性。他们还使用 TextDescriptives 来计算与文本相关的各种指标。

3 They fine-tuned separate models on (i) the initial responses, (ii) one response to each prompt selected at random, and (iii) the response to each prompt that best maximized each desired characteristic.

他们分别在以下数据集上对模型进行了微调：(i）初始回复，(ii）针对每个提示随机选择的一个回复，以及（iii）针对每个提示，选择最能体现所需特征的那个回复。

Results: Fine-tuning on the best response for each characteristic improved performance with respect to that characteristic beyond using the initial outputs or selecting outputs randomly.

结果表明，使用针对每个特征的最佳回复进行微调，在提升该特征的表现方面，比使用初始输出或随机选择的输出效果更好。

1 The authors’ method helped Mixtral 8x7B to generate less-toxic responses. For example, before fine-tuning, the model’s expected maximum toxicity measured 65.2 (lower is better). After fine-tuning on the lowest-toxicity responses generated by Llama 2 7B, Mixtral 8x7B’s expected maximum toxicity fell to 43.2. Conversely, after fine-tuning on random responses generated by Llama 2 7B, its expected maximum toxicity rose to 70.3.

作者的方法帮助 Mixtral 8x7B 生成毒性更低的回应。例如，在微调之前，该模型预测的最大毒性为 65.2（数值越低代表毒性越小）。使用 Llama 2 7B 生成的毒性最低的回应进行微调后，Mixtral 8x7B 的预期最大毒性降至 43.2。相反，在使用 Llama 2 7B 生成的随机回应进行微调后，其预期最大毒性升至 70.3。

2 It also helped Llama 2 7B to cut its toxicity. Before fine-tuning, the model’s expected maximum toxicity was 71.7. After fine-tuning on its own least-toxic responses, expected maximum toxicity dropped to 50.7. Fine-tuning on random responses made its expected maximum toxicity fall less sharply to 68.1.

该方法还有助于 Llama 2 7B 降低其毒性。在微调之前，该模型的预期最大毒性为 71.7。使用 Llama 2 7B 自身生成的毒性最低的回应进行微调后，预期最大毒性降至 50.7。使用随机回应进行微调，其预期最大毒性降低的幅度稍小，为 68.1。

3 Examining the impact of the authors’ method on more typical measures of performance, fine-tuning on the least-toxic responses and fine-tuning on random responses had about the same effect across seven benchmarks. Fine-tuning Llama 2 7B on its own least-toxic responses increased performance on average from 59.97 percent accuracy to 60.22 percent accuracy, while fine-tuning on random responses increased performance on average from 59.97 percent accuracy to 61.05 percent accuracy.

为了评估作者的方法对模型性能的影响，研究人员还在七个基准测试中，考察了对毒性最低的回应进行微调和对随机回应进行微调的效果。结果显示，这两种微调方式对模型性能的影响大致相同。使用 Llama 2 7B 自身生成的毒性最低的回应进行微调，使其性能平均从 59.97% 的准确率提高到 60.22% 的准确率；而使用随机回应进行微调，使其性能平均从 59.97% 的准确率提高到 61.05% 的准确率。

4 However, the process degraded performance in some cases. Fine-tuning Mixtral-8x7B on the least-toxic Llama 2 7B responses decreased its average performance across seven benchmarks for question answering and common-sense reasoning from 70.24 percent accuracy to 67.48 percent accuracy. Fine-tuning it on random Llama 2 7B responses cut its average performance from 70.24 percent accuracy to 65.64 percent accuracy.

然而，在某些情况下，该过程也会降低模型性能。在毒性最低的 Llama 2 7B 回应上对 Mixtral-8x7B 进行微调，使其在七个问题回答、常识推理等基准测试中的平均性能从 70.24% 的准确率降至 67.48% 的准确率。使用随机的 Llama 2 7B 回应进行微调，使其平均性能从 70.24% 的准确率降至 65.64% 的准确率。

Why it matters: Training on synthetic data is becoming increasingly common. While it shows great promise, best practices for data generation are still being formulated. The authors’ method helps by automatically steering models toward generating more desirable responses, reducing negative traits and reinforcing positive traits.

重要性：使用合成数据进行训练正变得越来越普遍。尽管这种方法前景广阔，但数据生成的最佳实践仍在不断完善中。作者提出的方法能够自动引导模型生成更符合预期的回应，从而减少负面特征并加强正面特征。

We’re thinking: Knowledge distillation lately has led to more capable and compact models. This approach adds levers of fine control to that technique.

我们的想法是：近来，知识蒸馏（Knowledge distillation）已经催生出性能更强、体积更小的模型。而本文提出的方法，则为这项技术增加了更精细的控制能力。