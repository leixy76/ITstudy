## 20250305GPT-45-Goes-Big-Claude-37-Reasons-Alexa+-Goes-Agentic

[GPT-4.5 Goes Big, Claude 3.7 Reasons, Alexa+ Goes Agentic, and more...](https://www.deeplearning.ai/the-batch/issue-291/)

Dear friends,

Continuing our discussion on the Voice Stack，I'd like to explore an area that today's voice-based systems mostly struggle with：Voice Activity Detection（VAD）and the turn-taking paradigm of communication.

继续我们关于语音栈的讨论，我想探讨一个目前的语音系统普遍面临挑战的领域：语音活动检测（VAD）以及语音交流中的轮替机制。

When communicating with a text-based chatbot，the turns are clear：You write something，then the bot does，then you do，and so on. The success of text-based chatbots with clear turn-taking has influenced the design of voice-based bots，most of which also use the turn-taking paradigm.

在使用文字聊天机器人时，对话的轮替非常清晰：你输入文字，然后机器人回复，接着你再次输入，以此类推。文字聊天机器人凭借清晰的轮替机制获得了成功，这也影响了语音机器人的设计，大多数语音机器人也采用了这种轮替模式。

A key part of building such a system is a VAD component to detect when the user is talking. This allows our software to take the parts of the audio stream in which the user is saying something and pass that to the model for the user's turn. It also supports interruption in a limited way，whereby if a user insistently interrupts the AI system while it is talking，eventually the VAD system will realize the user is talking，shut off the AI's output，and let the user take a turn. This works reasonably well in quiet environments.

构建此类系统的关键在于 VAD 组件，它负责检测用户何时开始说话。这样，我们的软件就能从音频流中提取出用户正在说话的部分，并将其传递给模型，完成用户的这一轮发言。VAD 也在一定程度上支持打断功能：如果用户在 AI 系统正在说话时执意打断，VAD 系统最终会识别出用户正在说话，从而关闭 AI 的输出，让用户进行发言。在安静的环境中，这种机制效果良好。

However，VAD systems today struggle with noisy environments，particularly when the background noise is from other human speech. For example，if you are in a noisy cafe speaking with a voice chatbot，VAD — which is usually trained to detect human speech — tends to be inaccurate at figuring out when you，or someone else，is talking.（In comparison，it works much better if you are in a noisy vehicle，since the background noise is more clearly not human speech.）It might think you are interrupting when it was merely someone in the background speaking，or fail to recognize that you've stopped talking. This is why today's speech applications often struggle in noisy environments.

然而，目前的 VAD 系统在嘈杂环境中表现不佳，尤其是在背景噪声包含其他人说话的声音时。例如，如果你在嘈杂的咖啡馆里与语音聊天机器人交谈，VAD（通常经过训练来识别人类语音）往往难以准确判断是你还是其他人在说话。(相比之下，如果你身处嘈杂的车辆中，情况会好得多，因为背景噪声通常不是人类语音。）系统可能会误认为你正在打断 AI 的发言，而实际上只是背景中有人在说话，或者无法识别你已经停止说话。这就是为什么现在的语音应用在嘈杂环境中经常表现不佳的原因。

Intriguingly，last year，Kyutai Labs published Moshi，a model（GitHub）that had many technical innovations. An important one was enabling persistent bi-direction audio streams from the user to Moshi and from Moshi to the user.

有趣的是，去年，Kyutai Labs 发布了 Moshi 模型（GitHub），它包含许多技术创新。其中一项重要的创新是，它实现了用户与 Moshi 之间的持久双向音频流。

If you and I were speaking in person or on the phone，we would constantly be streaming audio to each other（through the air or the phone system），and we'd use social cues to know when to listen and how to politely interrupt if one of us felt the need. Thus，the streams would not need to explicitly model turn-taking. Moshi works like this. It's listening all the time，and it's up to the model to decide when to stay silent and when to talk. This means an explicit VAD step is no longer necessary.（Moshi also included other innovations，such as an「inner monologue」that simultaneously generates text alongside the audio to improve the quality of responses as well as audio encoding.)

如果你和我面对面或者通过电话交谈，我们会持续地将音频传输给对方（通过空气或者电话系统）。我们会利用一些社交信号来判断何时应该倾听，以及在必要时如何礼貌地打断对方。因此，这种音频流不需要明确地模拟轮替机制。Moshi 的工作方式正是如此。它始终在倾听，并由模型自行决定何时保持沉默、何时开始说话。这意味着不再需要单独的 VAD 步骤。(Moshi 还包含其他创新，例如「内心独白」，它在生成音频的同时生成文本，从而提高回复质量，并进行音频编码。)

Just as the architecture of text-only transformers has gone through many evolutions（such as encoder-decoder models，decoder-only models，and reasoning models that generate a lot of「reasoning tokens」before the final output），voice models are going through a lot of architecture explorations. Given the importance of foundation models with voice-in and voice-out capabilities，many large companies right now are investing in developing better voice models. I'm confident we'll see many more good voice models released this year.

正如纯文本 Transformer 的架构经历了多次演变（例如，编码器-解码器模型、仅解码器模型，以及在最终输出之前生成大量「推理 Token」的推理模型），语音模型也在经历着大量的架构探索。鉴于具有语音输入和语音输出能力的基础模型至关重要，许多大型公司目前都在投资开发更优秀的语音模型。我相信今年我们会看到更多出色的语音模型发布。

It feels like the space of potential innovation for voice remains large. Hard technical problems，like the one of latency that I described last week and VAD errors，remain to be solved. As solutions get better，voice-to-voice will continue to be a promising category to build applications in.

总的来说，语音领域的创新空间仍然非常广阔。诸如我上周提到的延迟问题，以及 VAD 错误等技术难题，仍然有待解决。随着解决方案日臻完善，语音交互将继续成为一个充满应用前景的领域。

Keep building!

Andrew

### News

#### Text Generation by Diffusion

通过扩散模型生成文本

Typical large language models are autoregressive, predicting the next token, one at a time, from left to right. A new model hones all text tokens at once.

典型的大语言模型（LLM/Large Language Model）采用自回归方式，从左到右逐个预测下一个 Token。而一种新模型能够一次性处理所有的文本 Token。

What’s new: Inception Labs, a Silicon Valley startup, emerged from stealth mode with Mercury Coder, a diffusion model that generates code, in small and mini versions. Registered users can try it out here, and an API (sign up for early access here) and on-premises deployments are in the works. The company has not yet announced availability and pricing.

最新动态：硅谷初创公司 Inception Labs 推出 Mercury Coder，这是一种扩散模型，能够生成代码，并提供小型和迷你版本。注册用户可以在 [这里](链接）试用。该公司还在开发应用程序编程接口（API）(在此注册以获取提前使用权限）和本地部署方案，但尚未公布具体的可用性和定价信息。

[Inception Labs](https://www.inceptionlabs.ai/news?utm_campaign=The%20Batch&utm_medium=email&_hsenc=p2ANqtz-8cZzb9vbeszlMkfPdxoAqMWI20574PiENIIvB9YTe3R9SvDqfZDexOZKYlCItbhdU4OJQGeFYbD2WMoNfmQlNFUmk9Qg0nDNLSNC1EGyHrgXamZ-w&_hsmi=2&utm_content=2&utm_source=hs_email)

[Mercury Coder](https://chat.inceptionlabs.ai/auth)

How it works: Like image diffusion models, Mercury Coder improves its output over a number of steps by removing noise.

工作原理：与图像扩散模型类似，Mercury Coder 通过消除噪声，并经过多次迭代来改进其输出结果。

1 Inception Labs shared little information about the model, leaving details including parameter count, input size and output size, training data, and training methods undisclosed.

Inception Labs 公布的关于其模型的信息非常有限，包括模型参数量、输入 / 输出尺寸、训练数据以及训练方法等关键细节均未披露。

2 An October 2023 paper co-authored by an Inception Labs co-founder describes training a text diffusion model using score entropy. The model learned to estimate the transition ratio between two tokens; that is, the probability that token y is correct over the probability that the current token x is correct.

2023 年 10 月，一篇由 Inception Labs 联合创始人参与撰写的论文介绍了使用分数熵训练文本扩散模型的方法。该模型学习预测两个 Token 之间的转移比率，即 Token y 为正确 Token 的概率与当前 Token x 为正确 Token 的概率之比。

3 In their most successful experiments, the authors added noise to tokens by progressively masking an ever-greater percentage of tokens at random over several steps.

在作者们最成功的实验中，他们通过逐步增加随机屏蔽的 Token 比例，在多个步骤中向 Token 中引入噪声。

4 At inference, the model started with masked tokens and unmasked them over a number of steps. The estimated transition ratio determined how to change each token at each step.

在推理阶段，模型从被屏蔽的 Token 开始，并通过多个步骤逐步解除这些 Token 的屏蔽。预测的转移比率决定了每个步骤中如何修改每个 Token。

Results: Mercury Coder’s major advantage is speed, but it also performs well compared to several competitors.

结果：Mercury Coder 最突出的优势在于速度，同时相较于其他同类产品，性能也毫不逊色。

1 The Small and Mini versions are 3.5 to 18 times faster than comparable small coding models. Running on an Nvidia H100 graphics processing unit, Mercury Coder Small generates 737 tokens per second and Mercury Coder Mini generates 1,109 tokens per second. In comparison, Qwen 2.5 Coder 7B generates 207 tokens per second and GPT 4o-Mini generates 59 tokens per second.

在速度方面，Small 和 Mini 版本比其他小型编码模型快 3.5 到 18 倍。在 Nvidia H100 GPU 上，Mercury Coder Small 的 Token 生成速度达到每秒 737 个，而 Mercury Coder Mini 则高达每秒 1,109 个。作为对比，Qwen 2.5 Coder 7B 的速度为每秒 207 个 Token，GPT 4o-Mini 的速度为每秒 59 个 Token。

2 On coding tasks across six benchmarks, Mercury Coder Small outperforms Gemini 2.0 Flash-Lite, Claude 3.5 Haiku, GPT-4o Mini, and Qwen 2.5 Coder 7B on at least four. Mercury Coder Mini beats those models on at least two. Both versions of Mercury Coder lost to DeepSeek Coder V2 Lite on all six benchmarks.

在涵盖六项基准测试的编码任务中，Mercury Coder Small 在至少四项测试中表现优于 Gemini 2.0 Flash-Lite、Claude 3.5 Haiku、GPT-4o Mini 和 Qwen 2.5 Coder 7B。Mercury Coder Mini 至少在两项测试中超越了这些模型。但 Mercury Coder 的所有版本均在所有六项基准测试中不敌 DeepSeek Coder V2 Lite。

Behind the news: Several teams have built diffusion models that generate text, but previous efforts have not been competitive with autoregressive large language models (LLMs). Recently, LLaDA showed comparable performance to Meta’s Llama 2 7B but fell short of Llama 3 8B and other similarly sized modern LLMs.

最新进展：一些团队已经构建了能够生成文本的扩散模型（diffusion model），但早期的模型在与自回归大语言模型（LLM/Large Language Model）相比，性能并不突出。最近，LLaDA 的性能与 Meta 公司的 Llama 2 7B 相当，但仍落后于 Llama 3 8B 以及其他类似规模的现代大语言模型。

Why it matters: Text diffusion models are already faster than autoregressive models. They offer significant promise to accelerate text generation even further.

意义所在：文本扩散模型的速度已经超过了自回归模型，并有望进一步加速文本生成。

We’re thinking: Diffusion image generators have delivered good output with as little as four or even one step, generating output tokens significantly faster than autoregressive models. If text diffusion models can benefit from improvements in image generation, they could lead to rapid generation of lengthy texts and, in turn, faster agents and reasoning.

我们的观点：扩散图像生成器仅需少量步骤（甚至单步）就能产生高质量的图像。生成 Token 的速度远超自回归模型。如果文本扩散模型能够借鉴图像生成领域的进步，将有望快速生成长文本，进而加速 AI 智能体（AI Agent）的运行和推理过程。

#### OpenAI’s GPT-4.5 Goes Big

OpenAI 发布更大规模的 GPT-4.5 模型

OpenAI launched GPT-4.5, which may be its last non-reasoning model.

OpenAI 发布了 GPT-4.5，这可能是其最后一款非推理模型。

What’s new: GPT-4.5 is available as a research preview. Unlike OpenAI’s recent models o1 and o3, GPT-4.5 is not fine-tuned to reason by generating a chain of thought, although the company hinted that it may serve as a basis of a reasoning model in the future. Instead, it’s a huge model that was trained using a huge amount of computation. As OpenAI’s biggest model to date, GPT-4.5 is very expensive to run, and the company is evaluating whether to offer it via API in the long term.

更新内容：GPT-4.5 目前以研究预览版的形式提供。与 OpenAI 近期发布的 o1 和 o3 模型不同，GPT-4.5 并没有通过生成思维链（chain of thought）的方式进行微调以提升推理能力。不过，OpenAI 暗示该模型未来可能作为推理模型的基础。GPT-4.5 是 OpenAI 迄今为止规模最大的模型，因此运行成本非常高昂。OpenAI 正在评估长期通过 API 接口提供该模型的可能性。

1 Input/output: text and images in, text out. Voice and video interactions may be available in future updates.

输入 / 输出：输入：文本和图像；输出：文本。语音和视频互动功能可能在未来的更新中提供。

2 Availability/price: Via ChatGPT (currently ChatGPT Pro; soon ChatGPT Plus, Team, Enterprise, and Edu) and various APIs (Chat Completions, Assistants, and Batch). $75/$150 per million input/output tokens.

可用性 / 价格：通过 ChatGPT（目前为 ChatGPT Pro，即将推出 ChatGPT Plus、Team、Enterprise 和 Edu 版本）以及各种 API（Chat Completions、Assistants 和 Batch）提供。价格为每百万输入 / 输出 Token 75 美元 / 150 美元。

3 Features: Web search, function calling, structured output, streaming, system messages, canvas collaborative user interface.

功能：网页搜索、功能调用（function calling）、结构化输出、流式传输、系统消息、画布协作界面。

4 Undisclosed: Parameter count, input and output size, architecture, training data, training methods.

未公开：参数数量、输入和输出大小、架构、训练数据、训练方法。

How it works: OpenAI revealed few details about how GPT-4.5 was built. The model is bigger than GPT-4o, and it was pretrained and fine-tuned on more data using more computation — possibly 10x more, given OpenAI’s comment that “with every new order of magnitude of compute comes novel capabilities.”

工作原理：OpenAI 并没有公开太多关于 GPT-4.5 构建方式的细节。我们只知道，这个模型比 GPT-4o 更大，并且使用了更多的数据和计算资源进行预训练和微调 —— 计算量可能提升了 10 倍。正如 OpenAI 所说，「每一次计算能力的数量级提升，都会带来全新的能力。」

1 The model was trained on a combination of publicly available data and data from partnerships and in-house datasets, including data generated by smaller models. Its knowledge cutoff is October 2023.

该模型使用了包括公开数据、合作方数据以及内部数据集的混合数据集进行训练，其中也包括由较小模型所生成的数据。它的知识更新截止于 2023 年 10 月。

2 The data was filtered for quality, to eliminate personally identifying information, and to eliminate information that might contribute to proliferation of chemical, biological, radiological, and nuclear threats.

数据经过严格的质量过滤，以移除个人身份信息，并消除可能导致化学、生物、放射性和核威胁扩散的信息。

3 OpenAI developed unspecified techniques to scale up unsupervised pretraining, supervised fine-tuning, and alignment.

OpenAI 开发了一些未公开的技术，用于改进无监督预训练、监督微调和对齐。

Performance: “This isn’t a reasoning model and won’t crush benchmarks,” OpenAI CEO Sam Altman warned in a tweet. The company claims that GPT-4.5 offers improved general knowledge, adheres to prompts with more nuance, delivers greater creativity, and has higher emotional intelligence.

性能：「这并非一个推理模型，因此不会在基准测试中取得压倒性优势，」OpenAI 的 CEO Sam Altman 在一条推文中如此表示。该公司声称 GPT-4.5 提供了更丰富的通用知识，能更精确地理解提示，带来更高的创造力，并展现出更高的情商。

1 GPT-4.5 shows less propensity to hallucinate, or confabulate information, than other OpenAI models. On PersonQA (questions that involve publicly available facts about people), GPT-4.5 achieved 78 percent accuracy compared to GPT-4o (28 percent accuracy) and o1 (55 percent accuracy). Moreover, GPT-4.5 achieved a hallucination rate (lower is better) of 0.19 compared to GPT-4o (0.52) and o1 (0.20).

GPT-4.5 相比其他 OpenAI 模型，在生成内容时更不容易出现幻觉，也就是编造信息。在 PersonQA（关于人物公开信息的问答）测试中，GPT-4.5 的准确率达到了 78%，高于 GPT-4o（28%）和 o1（55%）。而且，GPT-4.5 的幻觉率（越低越好）为 0.19，同样低于 GPT-4o（0.52）和 o1（0.20）。

2 Its performance on coding benchmarks is mixed. On SWE-Bench Verified, GPT-4.5 achieved a 38 percent pass rate, higher than GPT-4o (30.7 percent) but well below deep research (61 percent), an agentic workflow that conducts multi-step research on the internet. On SWE-Lancer Diamond, which evaluates full-stack software engineering tasks, GPT-4.5 solved 32.6 percent of tasks, outperforming GPT-4o (23.3 percent) and o3-mini (10.8 percent) but again lagging deep research (around 48 percent).

GPT-4.5 在代码测试基准上的表现则喜忧参半。在 SWE-Bench Verified 测试中，GPT-4.5 的通过率为 38%，高于 GPT-4o（30.7%），但远低于 deep research（61%），这是一种在互联网上进行多步骤研究的 AI 智能体工作流。在 SWE-Lancer Diamond 测试中（该测试评估全栈软件工程任务），GPT-4.5 解决了 32.6% 的任务，优于 GPT-4o（23.3%）和 o3-mini（10.8%），但仍然落后于 deep research（约 48%）。

Behind the news: GPT-4.5’s release comes as OpenAI nears an announced transition away from developing separate general-knowledge and reasoning models. The launch also comes as OpenAI faces an ongoing shortage of processing power. CEO Sam Altman said that the company is “out of GPUs” and struggling to meet demand — a constraint that may impact whether OpenAI continues to offer GPT-4.5 via API.

新闻背后：GPT-4.5 的发布正值 OpenAI 接近宣布转变，不再分别开发通用知识模型和推理模型。此次发布也正值 OpenAI 面临持续的算力短缺。CEO Sam Altman 表示，该公司表示面临「GPU 不足」的问题，并且难以满足需求 —— 这一限制可能会影响 OpenAI 是否继续通过 API 提供 GPT-4.5。

Why it matters: GPT-4.5 highlights a growing divide in AI research over whether to pursue performance gains by scaling up processing during pretraining or inference. Despite the success of approaches that consume extra processing power at inference, such as agentic techniques and reasoning models such as its own o family, OpenAI clearly still sees value in pretraining larger and larger models.

重要性：GPT-4.5 突显了 AI 研究中日益增长的分歧。研究人员正在争论，究竟应该通过在预训练或推理期间扩大处理规模来追求性能提升，还是另辟蹊径。尽管在推理时消耗额外算力的方法取得了成功，例如 AI 智能体技术和推理模型（如其自身的 o 系列模型，具体名称未知），但 OpenAI 显然仍然认为预训练更大规模的模型具有价值。

We’re thinking: There’s still more juice to be squeezed out of bigger models! We’re excited to see what the combination of additional compute applied to both pretraining and inference can achieve.

我们的想法：更大的模型仍然有潜力可挖！我们很高兴看到应用于预训练和推理的额外计算能力相结合能够实现什么。

#### Budget for Reasoning to the Token

Token 级推理预算

Anthropic’s Claude 3.7 Sonnet implements a hybrid reasoning approach that lets users decide how much thinking they want the model to do before it renders a response.

Anthropic 的 Claude 3.7 Sonnet 采用了一种混合推理方法，让用户可以控制模型在生成回复前进行「思考」的程度。

What’s new: Claude 3.7 Sonnet was trained for strong performance in coding and front-end web development, with less emphasis on math and computer-science competition problems. It implements tool use and computer use (but not web search) and lets users toggle between immediate responses and extended thinking mode, which can improve outputs by allocating a specific number of tokens to reasoning at inference. Like DeepSeek-R1 and Google Gemini Flash Thinking — and unlike OpenAI o1 — Claude 3.7 Sonnet fully displays reasoning tokens. Anthropic considers this functionality experimental, so it may change.

最新消息：Claude 3.7 Sonnet 经过训练，在编码和前端 Web 开发方面表现出色。与此相对，它对数学和计算机科学竞赛问题的侧重较少。它实现了工具使用和计算机使用（但没有 Web 搜索），并允许用户在立即响应和增强思考模式之间切换。后者可以通过在推理时为推理分配特定数量的 Token 来改进输出。与 DeepSeek-R1 和 Google Gemini Flash Thinking 类似，但与 OpenAI o1 不同，Claude 3.7 Sonnet 能够完全显示推理 Token。Anthropic 认为此功能是实验性的，因此可能会发生变化。

1 Input/output: text and images in (up to 200,000 tokens), text out (up to 128,000 tokens).

输入 / 输出：文本和图像（高达 200,000 个 Token），文本输出（高达 128,000 个 Token）。

2 Availability/price: Via Anthropic tiers Free (extended thinking not available), Pro, Team, and Enterprise; Anthropic API; Amazon Bedrock; Google Cloud Vertex AI. $3/$15/$15 per million input/output/thinking tokens.

可用性 / 价格：通过 Anthropic 的 Free（不支持扩展思考），Pro，Team 和 Enterprise 版本；Anthropic API；Amazon Bedrock；Google Cloud Vertex AI。每百万输入 / 输出 / 思考（Thinking）Token 的价格分别为 3 美元 / 15 美元 / 15 美元。

3 Undisclosed: parameter count, architecture, training data, training method.

未公开：参数数量、架构、训练数据、训练方法。

4 Anthropic also introduced Claude Code, a command-line tool for AI-assisted coding, which is available as a limited research preview. Claude Code can edit files, write and run tests, commit and push code to GitHub, and use command-line tools.

Anthropic 还推出了 Claude Code，这是一个用于 AI 辅助编码的命令行工具，目前提供有限的研究预览版本。Claude Code 可以编辑文件、编写和运行测试、提交代码并将代码推送到 GitHub，以及使用命令行工具。

How it works: Anthropic pretrained Claude 3.7 Sonnet on a mix of public and proprietary data (which explicitly did not include Claude users’ inputs and outputs). The team fine-tuned Claude 3.7 Sonnet using constitutional AI, which encourages a model to follow a set of human-crafted rules.

工作原理：Anthropic 使用包含公共数据和私有数据的混合数据集预训练了 Claude 3.7 Sonnet（明确排除了 Claude 用户的输入和输出）。随后，研究团队采用基于章程的 AI（constitutional AI）对 Claude 3.7 Sonnet 进行了微调，该方法旨在引导模型遵守一套由人工制定的规则。

1 When the model’s extended thinking mode is enabled, API users can control the thinking budget by specifying a number of tokens up to 128,000. (The specified budget is a rough target, so the number of tokens consumed may differ.)

启用模型的扩展思考模式后，API 用户可以通过指定 Token 数量（最多 128,000 个）来控制思考预算。(这个指定的预算只是一个大致的目标，实际消耗的 Token 数量可能会有所出入。)

2 Anthropic says that extended thinking mode often is more effective given a general instruction to “think deeply” rather than step-by-step instructions.

Anthropic 认为，相比于提供逐步指令，直接给出「深入思考」的通用指令，通常能让扩展思考模式更有效地工作。

3 Visible thinking tokens are considered a research preview while Anthropic examines how they affect user interactions with the model. The company highlights three issues: Visible thinking tokens don’t reflect the model’s internal instructions that establish its character and therefore seem to be devoid of personality, they may not reflect the model’s actual reasoning process, and they can reveal flaws that malicious actors may exploit.

可见的思考 Token 目前被视为研究预览版本，Anthropic 正在研究它们对用户与模型交互的影响。Anthropic 强调了三个问题：首先，可见的思考 Token 无法反映模型内部用于塑造其特性的指令，因此显得缺乏个性；其次，它们可能无法真实反映模型的推理过程；最后，它们可能会暴露一些缺陷，被恶意行为者利用。

4 Extended thinking mode processes tokens serially, but Anthropic is experimenting with parallel thinking that follows multiple independent thought processes and chooses the best one according to a majority vote.

扩展思考模式以串行方式处理 Token。Anthropic 也在尝试并行思考模式，该模式会并行运行多个独立的思考过程，并根据多数投票选择最优方案。

Performance: Claude 3.7 Sonnet shows exceptional performance in general knowledge, software engineering, and agentic tasks.

性能：Claude 3.7 Sonnet 在通用知识、软件工程和 AI 智能体任务中表现出卓越的性能。

1 On the GPQA Diamond (graduate-level science questions), Claude 3.7 Sonnet achieved 84.8 percent in parallel extended thinking mode with a 64,000-token budget. By comparison, X’s Grok 3 beta achieved 84.6 percent (majority voting with 64 tries), and OpenAI’s o3-mini achieved 79.7 percent with high effort.

在 GPQA Diamond（研究生级别的科学问题）上，Claude 3.7 Sonnet 在并行扩展思维模式下，利用 64,000 个 Token 预算，取得了 84.8% 的优异成绩。相比之下，公司 X 的 Grok 3 beta 达到了 84.6%（通过 64 次尝试的多数投票实现），而 OpenAI 的 o3-mini 在投入大量计算资源后达到了 79.7%。[20]

2 On SWE-Bench Verified, which evaluates the ability to solve real-world software engineering problems, Claude 3.7 Sonnet achieved 70.3 percent without extended thinking, averaged over 16 trials. OpenAI’s o3-mini achieved 49.3 percent with high effort, and DeepSeek R1 achieved 49.2 percent with extended thinking, 32,000 tokens.

在 SWE-Bench Verified 上，这是一个评估解决实际软件工程问题能力的基准测试，Claude 3.7 Sonnet 在未采用扩展思维的情况下，经过 16 次试验平均达到了 70.3%。OpenAI 的 o3-mini 在投入大量计算资源后达到了 49.3%，DeepSeek R1 则在使用扩展思维和 32,000 个 Token 的情况下达到了 49.2%。

3 TAU-bench evaluates agentic reasoning. On the Retail subset, which assesses performance in product recommendations and customer service, Claude 3.7 Sonnet achieved 81.2 percent without extended thinking, outperforming OpenAI’s o1 (73.5 percent). In the Airline subset, which measures multi-step reasoning in tasks like flight bookings and customer support, Claude 3.7 Sonnet achieved 58.4 percent, likewise ahead of o1 (54.2 percent).

TAU-bench 评估 AI 智能体的推理能力。在 Retail 子集（评估产品推荐和客户服务能力）上，Claude 3.7 Sonnet 在未采用扩展思维的情况下达到了 81.2%，超过了 OpenAI 的 o1（73.5%）。在 Airline 子集（衡量在航班预订和客户支持等任务中的多步骤推理）上，Claude 3.7 Sonnet 达到了 58.4%，同样领先于 o1（54.2%）。

4 On AIME 2024, competitive high-school math problems, Claude 3.7 Sonnet achieved 80.0 percent in parallel extended thinking mode with a 64,000-token budget. In this test, it underperformed o3-mini with high effort (87.3 percent) and o1 (83.3 percent).

在 AIME 2024（一项具有挑战性的高中数学竞赛）中，Claude 3.7 Sonnet 在并行扩展思维模式下，利用 64,000 个 Token 预算，获得了 80.0% 的成绩。在这个测试中，它的表现不如投入大量计算资源后的 o3-mini（87.3%）和 o1（83.3%）。

Behind the news: Anthropic’s approach refines earlier efforts to enable users to control the incremental expense of computing extra tokens at inference. For instance, OpenAI o1 offers three levels of reasoning or “effort” — each of which allocates more tokens to reasoning — while X’s Grok 3 offers two.

新闻背后：Anthropic 的方法对之前的研究进行了改进，让用户可以在推理时控制计算额外 Token 所需的费用。例如，OpenAI 的 o1 提供了三个级别的推理「强度」—— 每个级别分配用于推理的 Token 数量不同 —— 而 X 公司的 Grok 3 则提供了两个级别。

Why it matters: Test-time compute, or additional processing at inference, is powerful but expensive, and not all tasks benefit from it. So it’s helpful to let users choose how much to apply. Claude 3.7 Sonnet improves its predecessor’s general performance and provides an ample budget for additional reasoning.

重要原因：在测试阶段进行计算，或者说在推理时进行额外的处理，能力很强但成本也很高，而且并非所有任务都需要这种额外的计算。因此，让用户能够自主选择使用多少计算资源就显得很有意义。Claude 3.7 Sonnet 在前代产品的基础上提升了整体性能，并为额外的推理任务提供了充足的资源预算。

We’re thinking: The cost of inference is rising as agentic workflows and other compute-intensive tasks become more widely used. Yet the cost of AI on a per-token basis is falling rapidly. Intelligence is becoming steadily cheaper and more plentiful.

我们的想法：随着 AI 智能体工作流和其他计算密集型任务的普及，推理成本正在上升。与此同时，AI 按 Token 收费的价格却在快速下降。智能正在变得越来越廉价，也更加普及。

#### Amazon’s Next-Gen Voice Assistant

亚马逊的下一代语音助手

Amazon announced Alexa+, a major upgrade to its long-running voice assistant.

Amazon 发布了 Alexa+，这是对其长期运行的语音助手的一次重大升级。

What’s new: Alexa+, which accepts spoken commands and responds conversationally, is designed to work with a variety of vendors as an autonomous agent to make purchases, book reservations, play media, and so on. It will roll out in the U.S. over coming weeks, initially on some Echo Show devices and eventually nearly every current Echo speaker.

新内容：Alexa+ 能够接受语音指令，并以对话的方式做出回应。它被设计成一个自主 AI 智能体，可以与各种供应商协作，完成诸如购物、预订和播放媒体等任务。它将在未来几周内在美国逐步推出，首先在部分 Echo Show 设备上提供，最终将覆盖几乎所有现有的 Echo 扬声器。

How it works: Alexa+ updates the system to take advantage of generative AI including Anthropic Claude, Amazon Nova, and other large language models. Inputs are filtered through a routing system that determines the best model to respond to any given request. It’s trained to understand colloquial, conversational language. Its personality is designed to be “smart, considerate, empathetic, and inclusive” as well as humorous.

工作原理：Alexa+ 对系统进行了升级，从而能够利用生成式 AI（Generative AI）技术，包括 Anthropic Claude、Amazon Nova 以及其他大语言模型（LLM/Large Language Model）。用户的输入会经过一个路由系统，该系统会判断哪个模型最适合响应当前请求。Alexa+ 经过专门训练，能够理解日常口语和会话式的表达。在人格设定上，它被设计为「聪明、体贴、富有同情心和包容性」，并且不失幽默感。

1 Alexa+  interacts with online vendors to manage smart-home devices (Philips Hue, Ring, Roborock), reserve restaurant seats (OpenTable, Vagaro), play music (Amazon Music, Spotify, Apple Music, iHeartRadio) and videos (Amazon Video, Hulu, Netflix, Disney+), book local service technicians (Thumbtack), and purchase items (Amazon Fresh, Whole Foods, Grubhub, Uber Eats, Ticketmaster). Amazon+ will cost $19.99 per month, free with an Amazon Prime membership ($139 per year). (Disclosure: Andrew Ng is a member of Amazon’s board of directors.)

Alexa+ 连接到在线供应商，以管理智能家居设备（例如 Philips Hue、Ring、Roborock），预订餐厅座位（例如 OpenTable、Vagaro），播放音乐（例如 Amazon Music、Spotify、Apple Music、iHeartRadio）和视频（例如 Amazon Video、Hulu、Netflix、Disney+），预订本地服务技术人员（Thumbtack），以及购买商品（例如 Amazon Fresh、Whole Foods、Grubhub、Uber Eats、Ticketmaster）。Amazon Prime 会员可以免费使用 Amazon+，否则每月收费 19.99 美元（Amazon Prime 会员年费为 139 美元）。（利益披露：Andrew Ng 是 Amazon 董事会成员。）

2 The system recognizes individual users and keeps track of personalized information such as dates; recipes, and preferences in sports, food, music, and movies. In addition, it can respond to queries based on purchase records, video and music playbacks, shipping addresses, documents, emails, photos, messages, and so on.

该系统识别个人用户，并跟踪个性化信息，例如日期、食谱，以及在体育、食物、音乐和电影方面的偏好。此外，它可以根据用户的购买记录、视频和音乐播放历史、送货地址、文档、电子邮件、照片和消息等信息，回复用户的查询。

3 It can behave proactively, for instance, advising users to start their commute early if traffic is heavy.

它可以主动提供建议，例如，如果交通拥堵，会建议用户提前开始通勤。

4 The system calls what Amazon calls experts — groups of systems, APIs, and instructions — that orchestrate API calls to accomplish online tasks. For instance, it can navigate and use the web to perform tasks such as finding and booking, say, a local repair service to fix a broken household appliance.

该系统使用 Amazon 所谓的「专家」—— 一组系统、API 和指令的集合 —— 来编排 API 调用，从而完成在线任务。例如，它可以浏览和使用网络来执行查找和预订等任务，比如寻找本地维修服务来修理损坏的家用电器。

5 Alexa+ can deliver timely news and information based on partnerships with news sources including Associated Press, Business Insider, Politico, Reuters, USA Today, and The Washington Post.

Alexa+ 与多家新闻机构合作，包括 Associated Press、Business Insider、Politico、Reuters、USA Today 和 The Washington Post，从而可以提供及时的新闻和信息。

Behind the news: Amazon launched Alexa in 2014, and the voice assistant now resides in over 600 million devices worldwide. However, users relied on it more to set timers, report sports scores, and play music than to purchase products, and Alexa revenue lagged. Following cutbacks in 2021, Amazon made multibillion-dollar investments in Anthropic and set about updating the technology for the generative AI era.

事件背景：Amazon 在 2014 年推出了 Alexa，目前 Alexa 已在全球超过 6 亿台设备上运行。然而，用户更倾向于使用它来设置定时器、查询体育比分和播放音乐，导致 Alexa 的营收表现不佳。在 2021 年进行调整后，Amazon 对 Anthropic 进行了数十亿美元的投资，并着手更新这项技术，以适应生成式 AI（Generative AI）时代的需求。

Why it matters: Alexa, along with Apple’s Siri and Google Assistant, pioneered the market for voice assistants. However, as large language models (LLMs) blossomed, all three systems fell behind the times. (Google allows Android users to substitute one of its Gemini LLMs for Google Assistant, but the system still calls Google Assistant for some tasks.) Alexa+ is the first major voice-assistant update that aims to take advantage of LLMs as well as emerging agentic technology and improved voice interactions, and the rollout is taking these capabilities to a large, existing user base.

重要性分析：Alexa 与 Apple 的 Siri 和 Google Assistant 一道，开创了语音助手市场。然而，随着大语言模型（LLM/Large Language Model）的蓬勃发展，这三者在技术发展上都显得有些滞后。（Google 允许 Android 用户使用 Gemini 大语言模型来替代 Google Assistant，但在某些任务中，系统仍然会调用 Google Assistant。）Alexa+ 是首个重要的语音助手更新，旨在利用大语言模型、新兴的 AI 智能体（AI Agent）技术以及改进的语音交互能力。此次更新将为庞大的现有用户群带来这些新功能。

We’re thinking: Rapid improvements in the voice stack are opening doors not only for voice assistants but for a galaxy of applications that rely on spoken input and output. Product designers will need to learn how to design smooth user voice experiences. Watching how Alexa+ manages them will provide useful guidelines.

展望：语音技术体系的快速发展不仅为语音助手打开了大门，也为各种依赖语音交互的应用带来了新的可能性。产品设计师需要学习如何设计流畅的用户语音体验。观察 Alexa+ 如何处理这些问题，将为产品设计提供有益的参考。