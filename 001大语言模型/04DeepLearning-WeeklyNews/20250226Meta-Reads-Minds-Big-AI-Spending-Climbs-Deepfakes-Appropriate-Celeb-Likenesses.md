## 20250226Meta-Reads-Minds-Big-AI-Spending-Climbs-Deepfakes-Appropriate-Celeb-Likenesses

[Meta Reads Minds, Big AI Spending Climbs, Deepfakes Appropriate Celeb Likenesses, and more...](https://www.deeplearning.ai/the-batch/issue-290/)


Published [Feb 26, 2025](https://www.deeplearning.ai/the-batch/tag/feb-26-2025/)Reading time 14 min read Share 

Dear friends,

The Voice Stack is improving rapidly. Systems that interact with users via speaking and listening will drive many new applications. Over the past year，I've been working closely with DeepLearning.AI，AI Fund，and several collaborators on voice-based applications，and I will share best practices I've learned in this and future letters.

语音技术体系正在快速发展。通过语音交互的系统将会催生许多新的应用。过去一年，我与 DeepLearning.AI、AI Fund 及一些合作者紧密合作，致力于基于语音的应用程序开发。我会在后续的文章中分享我所学到的经验。

Foundation models that are trained to directly input，and often also directly generate，audio have contributed to this growth，but they are only part of the story. OpenAI's RealTime API makes it easy for developers to write prompts to develop systems that deliver voice-in，voice-out experiences. This is great for building quick-and-dirty prototypes，and it also works well for low-stakes conversations where making an occasional mistake is okay. I encourage you to try it!

经过训练，能够直接输入，并且通常也能直接生成音频的基础模型（Foundation model）促进了这一增长，但这仅仅是其中的一部分。OpenAI 的 RealTime API 让开发者能够更轻松地编写提示词，从而构建可以提供语音输入、语音输出体验的系统。这非常适合构建快速原型，也适用于容错率较高、允许偶尔出错的轻松对话。我鼓励你亲自尝试一下！

[Realtime API - OpenAI API](https://platform.openai.com/docs/guides/realtime?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-_BuF-Wf7X_-nOlH7XesNh989iswtt1SPiiS17N_Kwf37hMN3VM9Ju-Ha9-PlOvw2-HoNBd)

However，compared to text-based generation，it is still hard to control the output of voice-in voice-out models. In contrast to directly generating audio，when we use an LLM to generate text，we have many tools for building guardrails，and we can double-check the output before showing it to users. We can also use sophisticated agentic reasoning workflows to compute high-quality outputs. Before a customer-service agent shows a user the message,「Sure，I'm happy to issue a refund,」we can make sure that（i）issuing the refund is consistent with our business policy and（ii）we will call the API to issue the refund（and not just promise a refund without issuing it).

然而，与基于文本的生成相比，控制语音输入语音输出模型的输出仍然具有挑战性。与直接生成音频不同，当我们使用大语言模型（LLM）生成文本时，我们拥有许多工具来建立安全机制，并且可以在向用户展示内容之前仔细检查输出结果。此外，我们还可以使用复杂的 AI 智能体（AI Agent）推理流程来生成高质量的内容。比如，在客服 AI 智能体（AI Agent）向用户发送「当然，我很乐意为您办理退款」消息之前，我们可以确保：(i）办理退款符合我们的业务规范；(ii）我们会调用 API 真正执行退款操作，而不是仅仅口头承诺。

In contrast，the tools to prevent a voice-in，voice-out model from making such mistakes are much less mature.

与此相反，用于防止语音交互模型犯此类错误的工具还尚不完善。

In my experience，the reasoning capability of voice models also seems inferior to text-based models，and they give less sophisticated answers.（Perhaps this is because voice responses have to be more brief，leaving less room for chain-of-thought reasoning to get to a more thoughtful answer.)

根据我的经验，语音模型的推理能力也似乎不如基于文本的模型，并且它们给出的答案不够完善。（也许这是因为语音回复必须更加简洁，从而减少了通过 Chain-of-thought（思维链）推理得出更富思考性的答案的可能性。）

When building applications where I need a high degree of control over the output，I use agentic workflows to reason at length about the user's input. In voice applications，this means I end up using a pipeline that includes speech-to-text（STT，also known as ASR，or automatic speech recognition）to transcribe the user's words，then processes the text using one or more LLM calls，and finally returns an audio response to the user via TTS（text-to-speech). This STT → LLM/Agentic workflow → TTS pipeline，where the reasoning is done in text，allows for more accurate responses.

在构建需要对输出进行精细控制的应用程序时，我通常会利用 AI 智能体工作流，对用户的输入进行深入分析。在语音应用中，我通常会采用这样一套流程：首先，使用语音转文本（STT，也称为 ASR，即自动语音识别）技术，将用户的语音转换成文本；然后，通过调用一个或多个大语言模型（LLM）来处理这些文本信息；最后，通过文本转语音（TTS）技术，将结果以语音的形式反馈给用户。在这个 STT → 大语言模型 /AI 智能体工作流 → TTS 管道中，推理过程以文本形式进行，从而可以获得更准确的反馈。

However，this process introduces latency，and users of voice applications are very sensitive to latency. When DeepLearning.AI worked with RealAvatar（an AI Fund portfolio company led by Jeff Daniel）to build an avatar of me，we found that getting TTS to generate a voice that sounded like me was not very hard，but getting it to respond to questions using words similar to those I would choose was. Even after a year of tuning our system — starting with iterating on multiple，long，mega-prompts and eventually developing complex agentic workflows — it remains a work in progress. You can play with it here.

然而，这个过程会带来延迟，而语音应用的用户对延迟非常敏感。当 DeepLearning.AI 与 RealAvatar（一家由 Jeff Daniel 领导、隶属于 AI Fund 旗下的公司）合作，为我打造一个数字形象时，我们发现，让 TTS（文本转语音）系统生成听起来像我的声音并不难，但要让它像我一样遣词造句来回答问题却非常困难。即使经过一年的系统优化 —— 从最初尝试各种冗长而复杂的「超级提示」(Mega-prompts，即包含大量信息的提示语），到最终开发出复杂的 AI 智能体（AI Agent）工作流程 —— 这项工作仍在进行中。您可以在这里体验一下。

[Avatar - DeepLearning.AI](https://www.deeplearning.ai/avatar/)

Initially，this agentic workflow incurred 5-9 seconds of latency，and having users wait that long for responses led to a bad experience. To address this，we came up with the following latency reduction technique. The system quickly generates a pre-response（short for preliminary response）that can be uttered quickly，which buys time for an agentic workflow to generate a more thoughtful，full response.（We're grateful to LiveKit's CEO Russ d'Sa and team for helping us get this working.）This is similar to how，if you were to ask me a complicated question，I might say「Hmm，let me think about that」or「Sure，I can help with that」— that's the pre-response — while thinking about what my full response might be.

最初，这种 AI 智能体（AI Agent）工作流程会造成 5-9 秒的延迟，过长的等待时间会严重影响用户体验。为了解决这个问题，我们提出了一种降低延迟的技术：系统会快速生成一个预响应（pre-response， preliminary response 的缩写），以便快速反馈给用户。这样做可以为 AI 智能体工作流程争取更多时间，从而生成更完善、更完整的响应。（我们感谢 LiveKit 的 CEO Russ d'Sa 及其团队为此提供的帮助。）就像当您问我一个复杂问题时，我可能会先说「嗯，让我想想」或者「好的，我来帮你」，这个「嗯」或者「好的」就是预响应，这样我就可以利用这段时间来思考如何给出完整的回答。

I think generating a pre-response followed by a full response，to quickly acknowledge the user's query and also reduce the perceived latency，will be an important technique，and I hope many teams will find this useful. Our goal was to approach human face-to-face conversational latency，which is around 0.3-1 seconds. RealAvatar and DeepLearning.AI，through our efforts on the pre-response and other optimizations，have reduced the system's latency to around 0.5-1 seconds.

我认为，先生成一个预响应，快速告知用户已收到提问，然后再生成完整回复，这样可以有效减少用户等待的感知时间，是一项非常重要的技术，希望对大家有所帮助。我们的目标是达到真人面对面交流的反应速度，大约在 0.3-1 秒之间。RealAvatar 和 DeepLearning.AI 团队通过预响应等一系列优化，已经将系统延迟降低到 0.5-1 秒左右。

Months ago，sitting in a coffee shop，I was able to buy a phone number on Twilio and hook it up to an STT → LLM → TTS pipeline in just hours. This enabled me to talk to my own LLM using custom prompts. Prototyping voice applications is much easier than most people realize!

几个月前，在咖啡馆里，我只花了几个小时，就在 Twilio 上买了一个电话号码，并将其连接到语音转文本（STT，Speech-to-Text）→ 大语言模型（LLM）→ 文本转语音（TTS，Text-to-Speech）的流程中。这让我能够通过定制的提示词与自己的 LLM 进行对话。语音应用的原型设计远比大多数人想象的要简单！

Building reliable，scaled production applications takes longer，of course，but if you have a voice application in mind，I hope you'll start building prototypes and see how far you can get! I'll keep building voice applications and sharing best practices and voice-related technology trends in future letters.

当然，构建可靠且可规模化部署的生产应用需要更长的时间，但如果你想做一个语音应用，我希望你开始构建原型，看看你能做到什么程度！我会继续开发语音应用，并在后续的文章中分享最佳实践和语音技术相关的趋势。

Keep building!

Andrew

继续加油！

Andrew

### News

#### Reading Minds，No Brain Implant Required

读心术，无需大脑植入

To date，efforts to decode what people are thinking from their brain waves often relied on electrodes implanted in the cortex. New work used devices outside the head to pick up brain signals that enabled an AI system，as a subject typed，to accurately guess what they were typing.

目前，解码人类思维的脑电波研究，通常需要植入大脑皮层的电极。而一项新的研究，利用放置在头部外部的设备捕捉脑电信号，让 AI 系统能够准确地猜测受试者正在输入的内容。

What's new: Researchers presented Brain2Qwerty，a non-invasive method to translate brain waves into text. In addition，their work shed light on how the brain processes language. The team included people at Meta，Paris Sciences et Lettres University，Hospital Foundation Adolphe de Rothschild，Basque Center on Cognition，Brain and Language，Basque Foundation for Science，Aix-Marseille University，and Paris Cité University.

最新进展：研究人员展示了 Brain2Qwerty，这是一种将脑电波转化为文本的非侵入性方法。此外，他们的研究也揭示了大脑处理语言的机制。该团队的成员来自 Meta、巴黎科学与文学院、阿道夫·罗斯柴尔德医院基金会、巴斯克认知、大脑和语言中心、巴斯克科学基金会、艾克斯 - 马赛大学和巴黎西岱大学等机构。

[Brain-to-Text Decoding: A Non-invasive Approach via Typing | Research - AI at Meta](https://ai.meta.com/research/publications/brain-to-text-decoding-a-non-invasive-approach-via-typing/?utm_campaign=The%20Batch&utm_medium=email&_hsenc=p2ANqtz-_yeFCpMAA6Jaz1qDjNRWVqO67v2Fw9USTQjBBmla9axbFPMyOeymLaS6VwpKYQjxZPPq4RhJhK4Z15yVch030hjm_wnxleejHjBLjuxzlNfkXXgxM&_hsmi=2&utm_content=2&utm_source=hs_email)

[From Thought to Action: How a Hierarchy of Neural Dynamics Supports Language Production | Research - AI at Meta](https://ai.meta.com/research/publications/from-thought-to-action-how-a-hierarchy-of-neural-dynamics-supports-language-production/?utm_campaign=The%20Batch&utm_medium=email&_hsenc=p2ANqtz-_zWfRD4SM_abrGq_-QsOeXBaI3vP9gfFPbbf-GN6dTupCY4YJGOq4l-73zNutchqutB6MIdkznqdSe3IZJxmQUZmfHx91lxnjka7cXXZm9MaCEbL4&_hsmi=2&utm_content=2&utm_source=hs_email)

Gathering brainwave data: The authors recorded the brain activity of 35 healthy participants who typed Spanish-language sentences. The participants were connected to either an electroencephalogram（EEG），which records the brain's electrical activity via electrodes on the scalp，or a magnetoencephalogram（MEG），which records magnetic activity through a device that surrounds the head but isn't attached. 15 participants used each device and five used both.

收集脑电波数据：作者记录了 35 名健康参与者在输入西班牙语语句时的脑部活动。参与者分别连接到脑电图（EEG）或脑磁图（MEG）。脑电图（EEG）通过头皮上的电极记录大脑的电活动；脑磁图（MEG）则通过一个环绕头部但不直接接触的设备来记录磁活动。其中，15 名参与者使用脑电图（EEG），15 名使用脑磁图（MEG），另有 5 名同时使用了两种设备。

1 Participants were asked to read and memorize short sentences of 5 to 8 words. They were shown one word at a time.

参与者被要求阅读并记住 5-8 个单词的短句。他们一次看到一个单词。

2 After a short waiting period，participants were asked to type the sentence. They could not see what they typed.

稍作等待后，参与者被要求输入句子。他们无法看到自己输入的内容。

3 The EEG dataset comprised around 4,000 sentences and 146,000 characters，while the MEG dataset comprised around 5,100 sentences and 193,000 characters.

EEG 数据集包含约 4,000 句话和 146,000 个字符，而 MEG 数据集包含约 5,100 句话和 193,000 个字符。

Thoughts into text: Brain2Qwerty used a system made up of a convolutional neural network，transformer，and a 9-gram character-level language model pretrained on Spanish Wikipedia. The system classified the text a user typed from their brain activity. The authors trained separate systems on MEG and EEG data.

将想法转化为文字：Brain2Qwerty 使用了一个系统，它由卷积神经网络、Transformer 和一个在西班牙语维基百科上预训练的 9-gram 字符级语言模型组成。这个系统能够根据用户的大脑活动，对他们想输入的文本进行分类。作者分别在 MEG 和 EEG 数据集上训练了各自的系统。

1 The convolutional neural network segmented brain activity into windows of 500 milliseconds each. The transformer took these windows as input and generated possible text characters and their probabilities. The two models learned to predict characters jointly.

卷积神经网络将大脑活动分割成若干个 500 毫秒的窗口。Transformer 模型将这些窗口作为输入，并生成可能的文本字符及其概率。这两个模型联合学习预测字符。

2 The pretrained language model，given the most recently predicted nine characters,  estimated the probability of the next character.

预训练语言模型会根据最近预测的九个字符，来估计下一个字符的概率。

3 At inference，the authors used a weighted average of probabilities from the transformer and language model. From that average，they computed the most likely sequence of characters as the final output.

在推理阶段，作者将 Transformer 和语言模型输出的概率进行加权平均。然后，他们从平均概率中计算出最有可能的字符序列，并将其作为最终的输出结果。

Results. The authors' MEG model achieved 32 percent character error rate（CER），much higher accuracy than the EEG competitors. Their EEG system outperformed EEGNet，a model designed to process EEG data that had been trained on the authors' EEG data. It achieved 67 percent CER，while EEGNet achieved 78 percent CER.

结果。作者的 MEG 模型实现了 32% 的字符错误率（CER），这意味着它比 EEG 竞争者具有更高的精度。他们的 EEG 系统性能优于 EEGNet，后者是一个专门设计用于处理 EEG 数据的模型，并且已经使用作者提供的 EEG 数据进行了训练。该系统实现了 67% 的字符错误率（CER），而 EEGNet 达到了 78% 的字符错误率（CER）。

Behind the news: For decades，researchers have used learning algorithms to interpret various aspects of brain activity with varying degrees of success. In recent years，they've used neural networks to generate text and speech from implanted electrodes，generate images of what people see while in an fMRI，and enable people to control robots using EEG signals.

研究背景：几十年来，研究人员一直在使用机器学习算法来解读大脑活动的各个方面，但成功程度不一。近年来，他们利用神经网络，从植入的电极中生成文本和语音，生成人们在 functional Magnetic Resonance Imaging（fMRI）中看到的内容的图像，并使人们能够利用 Electroencephalography（EEG）信号控制机器人。

Why it matters: In research into interpreting brain signals，subjects who are outfitted with surgical implants typically have supplied the highest-quality brain signals. fMRI scans，while similarly noninvasive，are less precise temporally，which makes them less useful for monitoring or predicting language production. Effective systems based on MEG，which can tap brain signals precisely without requiring participants to undergo surgery，open the door to collecting far more data，training far more robust models，and conducting a wider variety of experiments.

为什么重要：在脑信号解读的研究中，接受外科植入的主体通常能提供质量最高的脑信号。功能性磁共振成像（fMRI）扫描同样是非侵入性的，但其时间分辨率较低，因此不太适用于监测或预测语言的产生。而基于脑磁图（MEG）的有效系统，无需参与者接受手术即可精确地获取脑信号，这为收集更多数据、训练更强大的模型以及进行更广泛的实验打开了大门。

We're thinking: The privacy implications of such research may be troubling，but keep in mind that Brain2Qwerty's MEG system，which was the most effective approach tested，required patients to spend extended periods of time sitting still in a shielded room. We aren't going to read minds in the wild anytime soon.

我们需要考虑的是：这种研究的隐私影响可能令人不安，但请记住，Brain2Qwerty 的 MEG（脑磁图）系统是在测试中表现最好的方法，它需要患者长时间静坐在屏蔽室内。短期内，我们还无法在现实场景中读取思想。

#### Big AI Spending Continues to Rise

大型 AI 支出持续增长

Top AI companies announced plans to dramatically ramp up their spending on AI infrastructure.

顶级 AI 公司宣布计划大幅增加在 AI 基础设施上的投入。

What's new: Alphabet，Amazon，Meta，Microsoft，and others will boost their capital spending dramatically in 2025，pouring hundreds of billions of dollars into data centers where they process AI training，the companies said in their most recent quarterly reports. The surge suggests that more-efficient approaches to training models won't dampen the need for greater and greater processing power.

要点：Alphabet、Amazon、Meta、Microsoft 等公司在近期的季度报告中表示，它们将在 2025 年显著提升资本支出，计划投入数千亿美元建设数据中心，以支持 AI 模型的训练。这一趋势表明，即使模型训练方法日益高效，对更大规模计算能力的需求仍然十分旺盛。

How it works: Capital expenditures include long-term purchases like land，buildings，and computing hardware rather than recurring costs like salaries or electricity. The AI leaders signaled that most of this spending will support their AI efforts.

它是如何运作的：资本支出指的是土地、建筑物和计算硬件等长期资产的购置，而非工资或电力等日常运营成本。人工智能领域的领头羊们表示，这些资本投入主要将用于支持他们的人工智能研发工作。

1 Amazon has budgeted $105 billion to capital expenditures in 2025，35 percent more than last year. CFO Brian Olsavsky attributed the increase to the company's need to satisfy demand for AI services and tech infrastructure. CEO Andy Jassy emphasized that it reflects strong demand for AI and dismissed concerns that cheaper alternatives like DeepSeek would reduce overall spending.（Disclosure：Andrew Ng is a member of Amazon's board of directors.)

亚马逊已为 2025 年的资本支出预留了 1050 亿美元的预算，比去年增加了 35%。首席财务官 Brian Olsavsky 认为，增长的原因是公司需要满足市场对人工智能（AI）服务和技术基础设施的巨大需求。首席执行官 Andy Jassy 强调，这体现了市场对 AI 的强劲需求，并且他认为像 DeepSeek 这样更经济的替代方案不会减少总体支出。(声明：Andrew Ng 是亚马逊董事会成员。)

2 Alphabet allocated $75 billion to capital expenditures，up from $52.5 billion last year，to support growth in Google Services，Google Cloud，and Google DeepMind. The company indicated that most of this money would go to technical infrastructure including data centers and networking.

3 为了支持 Google Services、Google Cloud 和 Google DeepMind 的发展，Alphabet 公司投入了 750 亿美元作为资本支出，相比去年的 525 亿美元有所增加。公司方面表示，这笔资金的大部分将用于技术基础设施建设，例如数据中心和网络。

4 Meta's annual capital expenditures will amount to $65 billion，a huge jump from $39.2 billion last year. CEO Mark Zuckerberg argued that such spending on AI infrastructure and chips is needed to assure the company's lead in AI and integrate the technology into its social platforms.

Meta 的年度资本支出将达到 650 亿美元，比去年的 392 亿美元大幅增加。CEO Mark Zuckerberg 表示，这类在 AI 基础设施和芯片上的投入是必须的，以确保其在 AI 领域的领先地位，并将该技术整合到其社交平台中。

5 Microsoft said it would put around $80 billion — a figure that analysts expect to rise to $94 billion — into capital expenditures in 2025，another big jump following an 83 percent rise from 2023 to 2024. Most of this investment will support cloud infrastructure，servers，CPUs，and GPUs to meet demand for AI.

微软宣布，2025 年的资本支出将达到约 800 亿美元。分析师预测，这一数字还将进一步攀升至 940 亿美元。在此之前，微软在 2023 年到 2024 年间的资本支出已经大幅增长了 83%。这笔巨额投资主要用于支持云基础设施、服务器、CPU 和 GPU 等硬件设施的建设，以满足市场对人工智能（AI）的旺盛需求。

6 OpenAI，Oracle，SoftBank，and others announced Stargate，a project that intends immediately to put $100 billion — $500 billion over time — into data centers that would support development of artificial general intelligence. Elon Musk claimed in a tweet that the investors「don't actually have the money,」raising questions about the announcement's veracity.

OpenAI、Oracle、软银和其他公司宣布了一项名为「星际之门（Stargate）」的项目，计划立即投入 1000 亿美元，并将在未来投入总计 5000 亿美元，用于建设数据中心，以支持通用人工智能（AGI）的研发。埃隆·马斯克在推特上发文称，投资者「实际上并没有这笔钱」，这让人对该声明的真实性产生了怀疑。

Behind the news: DeepSeek initially surprised many members of the AI community by claiming to have trained a high-performance large language model at a fraction of the usual cost.

新闻背后：DeepSeek 最初宣称，他们以远低于通常水平的成本训练出了一个高性能的大语言模型（LLM），这让许多人工智能（AI）领域的从业者感到惊讶。

1 Specifically，DeepSeek-R1 reportedly cost less than $6 million and 2,048 GPUs to train.（For comparison，Anthropic's Claude 3.5 Sonnet cost「a few $10Ms to train,」 according to CEO Dario Amodei，and GPT-4 cost about $100 million to train, according to CEO Sam Altman.）Follow-up reports shed light on DeepSeek's actual infrastructure and noted that the $6 million figure represented only DeepSeek-R1's final training run，a small fraction of the total development cost.

具体来说，据报道，DeepSeek-R1 的训练成本不到 600 万美元以及 2,048 个 GPU（Graphics Processing Unit）。（为了进行比较，Anthropic 的 Claude 3.5 Sonnet 的训练成本，据其 CEO Dario Amodei 称，为「几千万美元」。而 GPT-4 的训练成本，据 OpenAI 的 CEO Sam Altman 称，约为 1 亿美元。）后续报告揭示了 DeepSeek 的实际基础设施，并指出 600 万美元的数字仅代表 DeepSeek-R1 的最终训练阶段，只占总开发成本的一小部分。

2 Furthermore，while initial reports said DeepSeek piggy-backed on a 10,000-GPU supercomputer owned by its parent company High-Flyer，a hedge fund，research firm SemiAnalysis questioned whether DeepSeek relied on High-Flyer's hardware. DeepSeek has spent around $1.6 billion on a cluster of 50,000 Nvidia GPUs, Tom's Hardware reported.

此外，虽然最初有报道称，DeepSeek 借助其母公司 High-Flyer（一家对冲基金）拥有的、包含 10,000 个 GPU 的超级计算机进行运算，但研究公司 SemiAnalysis 质疑 DeepSeek 是否真的使用了 High-Flyer 的硬件资源。据 Tom's Hardware 报道，DeepSeek 斥资约 16 亿美元，构建了一个包含 50,000 个 Nvidia GPU 的集群。

3 Initial excitement over the company's low training costs gave way to concerns about data sovereignty，security，and the cost of running DeepSeek-R1，which generates a larger number of reasoning tokens than similar models.

最初，大家对该公司训练成本低的优势感到兴奋，但随后也开始担心数据主权、安全以及运行 DeepSeek-R1 的成本。因为相比同类模型，DeepSeek-R1 在推理过程中会生成更多的 Token，这会导致更高的运行成本。

Why it matters: DeepSeek-R1's purported training cost fueled fears that demand for AI infrastructure would cool，but the top AI companies' plans show that it's not happening yet. A possible explanation lies in the Jevons Paradox，a 19th-century economic theory named after the English economist William Stanley Jevons. As a valuable product becomes more affordable，demand doesn't fall，it rises. According to this theory，even if training costs tumble，the world will demand ever greater processing power for inference.

为什么重要：DeepSeek-R1 宣称的训练成本引发了人们对 AI 基础设施需求可能降温的担忧，但头部 AI 公司的计划表明，这种情况目前还没有发生。对此，一个可能的解释是杰文斯悖论（Jevons Paradox），这是以 19 世纪英国经济学家威廉·斯坦利·杰文斯（William Stanley Jevons）命名的经济学理论。该理论指出，当一种有价值的产品变得更便宜时，需求不仅不会下降，反而会上升。因此，即使训练成本大幅降低，世界对用于推理的算力需求也会持续增长。

We're thinking: DeepSeek's low-cost technology momentarily rattled investors who had expected the next big gains would come from the U.S. rather than China. But DeepSeek's efficiency follows a broader pattern we've seen for years：The AI community steadily wrings better performance from less processing power.

我们的观点是：DeepSeek 的低成本技术让原本预期下一波重大收益来自美国的投资者们，一时有些措手不及。但 DeepSeek 的高效率，也印证了我们在人工智能（AI）领域观察多年的趋势：利用更少的处理能力，实现更卓越的性能。

#### Deepfake Developers Appropriate Celebrity Likenesses

Deepfake 开发者滥用名人肖像

A viral deepfake video showed media superstars who appeared to support a cause — but it was made without their participation or permission.

最近，一段病毒式传播的深度伪造视频引起了广泛关注，视频中一些媒体巨星「支持」了一项事业，但实际上，该视频的制作并未获得他们的任何授权或参与。

What's new: The video shows AI-generated likenesses of 20 Jewish celebrities ranging from Scarlett Johansson to Simon & Garfunkel. They appear wearing T-shirts that feature a middle finger inscribed with the Star of David above the word「KANYE.」The clip，which ends with the words「Enough is enough」followed by「Join the fight against antisemitism,」responds to rapper Kanye West，who sold T-shirts emblazoned with swastikas on Shopify before the ecommerce platform shut down his store.

最新进展：这段视频利用 AI 技术生成（AI-generated）了 20 位犹太名人的数字肖像，其中包括 Scarlett Johansson 和 Simon & Garfunkel 等。视频中，他们身穿印有特殊图案的 T 恤：一个指向前方的中指，上面刻着大卫之星，图案上方则标注着「KANYE」字样。视频结尾打出标语：「够了就是够了！」以及「加入到反对反犹太主义的斗争中来！」。制作该视频是为了回应说唱歌手 Kanye West 此前在 Shopify 平台上销售印有纳粹 swastika 标志 T 恤的事件 —— 此后，Shopify 关闭了他的店铺。

Who created it: Israeli developers Guy Bar and Ori Bejerano generated the video to spark a conversation about antisemitism，Bar told The Jerusalem Post. The team didn't reveal the AI models，editing tools，or techniques used to produce the video.

谁创造了它：以色列开发者 Guy Bar 和 Ori Bejerano 制作了这个视频，目的是为了引起大家对反犹太主义的关注和讨论，Bar 在接受《耶路撒冷邮报》采访时说。至于制作该视频所使用的 AI 模型、编辑工具和相关技术，该团队并没有对外透露。

Johansson reacts: Scarlett Johansson denounced the clip and urged the U.S. to regulate deepfakes. In 2024，she objected to one of the voices of OpenAI's voice assistant，which she claimed resembled her own voice，leading the company to remove that voice from its service. The prior year，her attorneys ordered a company to stop using an unauthorized AI-generated version of her image in an advertisement.

针对 Johansson 的回应：Scarlett Johansson 谴责了这段视频，并敦促美国监管深度伪造（deepfakes）。2024 年，她反对 OpenAI 语音助手的其中一个声音，认为该声音与她本人的声音非常相似，最终导致 OpenAI 将该声音从其服务中移除。在 2023 年，她的律师曾下令一家公司停止在广告中使用未经授权的 AI 生成的她的图像。

Likenesses up for grabs: Existing U.S. laws protect some uses of a celebrity's likeness in the form of a photo，drawing，or human lookalike，but they don't explicitly protect against reproduction by AI systems. This leaves celebrities and public figures with limited recourse against unauthorized deepfakes.

肖像权争夺：现行的美国法律在一定程度上保护了名人肖像的使用，例如照片、绘画或真人模仿，但并未明确禁止 AI 系统对其进行复制。这使得名人和公众人物在面对未经授权的深度伪造时，很难维护自己的权益。

1 U.S. lawmakers have introduced legislation that targets deepfake pornography，but it covers only sexually explicit deepfakes.

美国立法者已经推出了针对深度伪造色情内容的立法，但仅限于包含性内容的深度伪造。

2 The right of publicity，which falls under trademark law，offers some protection against the unauthorized use of a person's identity. However，it varies by state and provides broad exceptions for news，satire，and fine art.

形象权（right of publicity），属于商标法管辖，对未经授权使用个人身份的行为提供了一定的保护。但是，各州的规定有所不同，并且对新闻报道、讽刺作品和美术作品有较多豁免。

3 While some states outlaw misappropriation of names or likenesses，existing laws primarily target traditional forms of image misuse，such as false endorsements or unauthorized commercial exploitation. They do not explicitly cover AI-generated deepfakes used for noncommercial，political，or satirical purposes.

尽管一些州禁止擅自使用他人姓名或肖像，但现行法律主要针对的是传统的图像滥用形式，比如虚假代言或未经授权的商业利用。这些法律并没有明确涵盖用于非商业、政治或讽刺目的的，由 AI 生成的深度伪造（deepfakes）技术。

4 A 2023 agreement between Hollywood actors and movie studios protects actors against such uses of AI-generated images of their likenesses in films. However，it doesn't apply to deepfakes that are produced independently for distribution via social media networks.

好莱坞演员和电影制片公司在 2023 年达成了一项协议，旨在保护演员免受电影中使用 AI 生成的肖像侵权。然而，该协议不适用于那些独立制作并通过社交媒体传播的深度伪造（deepfakes）内容。

Why it matters: Non-consensual deepfake pornography is widely condemned，but AI enables many other non-consensual uses of someone's likeness，and their limits are not yet consistently coded into law. If the creators of the video that appropriated the images of celebrities had responded to Johansson's criticism with an AI-generated satire，would that be a legitimate exercise of free speech or another misuse of AI? Previously，an ambiguous legal framework may have been acceptable because such images，and thus lawsuits arising from them，were uncommon. Now，as synthetic likenesses of specific people become easier to generate，clear legal boundaries are needed to keep misuses in check.

重要性：未经授权的深度伪造色情内容备受谴责，但人工智能（AI）也使得未经允许使用他人肖像有了更多可能性，而这些应用的边界尚未被明确地纳入法律条文。假设，如果那些盗用名人形象制作视频的人，使用 AI 生成的讽刺作品来回应 Johansson 的批评，这会是合理的言论自由，还是另一种 AI 滥用？ 过去，由于此类图像及其引发的诉讼并不常见，模糊的法律框架或许还能接受。但现在，合成特定人物的肖像变得越来越容易，因此需要清晰的法律界限来约束滥用行为。

We're thinking: Creating unauthorized lookalikes of existing people is not a good way to advance any cause，however worthy. Developers should work with businesses policymakers to establish standards that differentiate legitimate uses from unfair or misleading exploitation.

我们认为：未经授权地创建现有人物的仿冒形象，无论出于多么崇高的目的，都不是推进任何事业的良好途径。开发者应该与商业领域的政策制定者携手合作，制定明确的标准，区分合理合法的应用与不正当或具有误导性的利用。

#### Reasoning in Vectors，Not Text

向量推理，而非文本

Although large language models can improve their performance by generating a chain of thought（CoT）— intermediate text tokens that break down the process of responding to a prompt into a series of steps — much of the CoT text is aimed at maintaining fluency（such as「a」,「of」,「we know that」）rather than reasoning（「a² + b² = c²」). Researchers addressed this inefficiency.

虽然大语言模型（LLM/Large Language Model）可以通过生成思维链（Chain of Thought，CoT）—— 一种将复杂问题拆解为一系列中间步骤的文本 Token —— 来提升性能，但这些 CoT 文本中，很多内容是为了保持语言的流畅性（例如「嗯」，「啊」，「我们知道」），而并非真正的推理过程（例如「勾股定理：a² + b² = c²」）。针对这种效率低下的问题，研究人员提出了解解决方案。

What's new: Shibo Hao，Sainbayar Sukhbaatar，and colleagues at Meta and University of California San Diego introduced Coconut (Chain of Continuous Thought），a method that trains large language models（LLMs）to process chains of thought as vectors rather than words.

研究发现：Shibo Hao、Sainbayar Sukhbaatar 以及 Meta 和加州大学圣地亚哥分校的同事们推出了 Coconut（Chain of Continuous Thought，持续思考链），这是一种训练大语言模型（Large Language Models，LLMs）的方法，它将思维链处理为向量而不是单词，从而使模型能够更好地理解和利用推理过程。

[[2412.06769] Training Large Language Models to Reason in a Continuous Latent Space](https://arxiv.org/abs/2412.06769?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-_BuF-Wf7X_-nOlH7XesNh989iswtt1SPiiS17N_Kwf37hMN3VM9Ju-Ha9-PlOvw2-HoNBd)

Key insight: A large language model（LLM）can be broken into an embedding layer，transformer，and classification layer. To generate the next text token from input text，the embedding layer embeds the text; given the text，the transformer outputs a hidden vector; and the classification layer maps the vector to text-token probabilities. Based on these probabilities，a decoding algorithm selects the next token to generate，which feeds back into the input text sequence to generate the next vector，and so on. When a model generates a CoT，committing to a specific word at each step limits the information available to the meanings of the words generated so far，while a vector could represent multiple possible words. Using vectors instead of text enables the CoT to encode richer information.

核心观点：一个大语言模型（LLM）可以拆解为三个主要部分：嵌入层、Transformer 和分类层。从输入文本生成下一个文本 Token 的过程是这样的：首先，嵌入层将文本转化为向量表示；然后，Transformer 根据这些向量输出一个隐藏向量；接着，分类层将这个隐藏向量映射为各个文本 Token 的概率。基于这些概率，解码算法会选择概率最高的 Token 作为下一个生成的 Token，并将这个 Token 反馈回输入文本序列，用于生成下一个向量，如此循环往复。当模型生成思维链（CoT）时，每一步都直接确定一个具体的词，这会限制模型能够获取的、关于已生成词汇含义的信息。而向量则可以同时代表多个可能的词。因此，使用向量代替文本，能让思维链（CoT）编码更丰富的信息。

How it works: The authors built three LLMs by fine-tuning a pre-trained GPT-2 on three datasets of prompts，CoTs，and final outputs: GSM8k (grade-school math word problems); ProntoQA (questions and answers about fictional concepts expressed in made-up words，including synthetic CoTs in natural language); and（3）ProsQA，a more challenging question-answering dataset introduced by the authors，inspired by ProntoQA but with longer reasoning steps.

它是如何工作的：作者通过在三个数据集上微调预训练的 GPT-2 模型，构建了三个大语言模型（LLM）。这三个数据集分别包含提示（prompts）、思维链（Chain-of-Thought，CoT）和最终输出：GSM8k（用于解决小学数学应用题的数据集)；ProntoQA（包含关于虚构概念的问题和答案，这些概念用自创的词汇表达，其中也包括用自然语言生成的合成思维链)；以及（3）ProsQA，一个由作者提出的更具挑战性的问答数据集，虽然其设计灵感来源于 ProntoQA，但它包含了更长的推理步骤。

1 Fine-tuning began with supervised training. The LLM learned to generate the text in the training set，including the CoT and final answers. As usual，the last-generated text token was fed back as input to produce the next token.

微调首先从监督训练开始。在此阶段，大语言模型学习生成训练集中的文本，包括思维链（CoT）和最终答案。与通常的做法一样，模型会将最后生成的文本 Token 反馈作为输入，用于生成下一个 Token。

2 Fine-tuning then progressed through k stages for each example. At each stage，the authors replaced a sentence in the CoT text with a thought vector（or two）to build a sequence of k replaced sentences. The start and end of the chain of thought vectors were marked by two special tokens. During vector steps，the LLM fed its output vectors back as input without decoding them into text. The LLM learned to generate only the remaining text tokens，not the thought vectors，which encouraged it to optimize its vector-based reasoning indirectly.

微调过程随后针对每个示例进行 k 个阶段。在每个阶段，作者会用一个思维向量（thought vector)（或两个）替换思维链（Chain-of-Thought，CoT）文本中的一个句子，从而构建出一个包含 k 个被替换句子的序列。思维向量链的起始和结束位置会用两个特殊的 Token 来标记。在向量步骤中，大语言模型（LLM）会将其输出的向量作为输入再次输入模型，而无需将这些向量解码成文本。大语言模型（LLM）学习只生成剩余的文本 Token，而不是思维向量，这鼓励它以一种间接的方式来优化其基于向量的推理能力。

3 During inference，the LLM generated a special token to mark the start of the chain of vectors. From this point，it fed back its output vectors，bypassing text decoding for six steps. Afterward，the LLM switched back to generating text for final output.

在推理过程中，大语言模型（LLM）会首先生成一个特殊的 Token，用于标记向量链的起始位置。接下来，它会跳过文本解码的环节，直接将输出的向量反馈回自身，并重复这个过程六次。完成向量链的处理后，大语言模型（LLM）才会切换回文本生成模式，输出最终结果。

Results: The authors compared their method to a pretrained GPT-2 that was fine-tuned on the same datasets to predict the next word，including reasoning.

结果：作者将他们的方法与一个预训练的 GPT-2 模型进行了比较，该 GPT-2 模型在相同的数据集上进行了微调，用于预测下一个单词，包括推理能力。

1 On ProntoQA，Coconut outperformed the fine-tuned GPT-2 while producing far fewer interim vectors（Coconut）or tokens（baseline LLMs). It achieved 99.8 percent accuracy after generating nine vectors（or tokens）on average，while GPT-2 achieved 98.8 percent accuracy using 92.5 text tokens.

在 ProntoQA 数据集上，Coconut 模型优于微调后的 GPT-2 模型，同时产生更少的中间向量（Coconut）或 Token（基线模型）。Coconut 模型平均生成 9 个向量后达到了 99.8% 的准确率，而 GPT-2 模型使用 92.5 个文本 Token 达到了 98.8% 的准确率。

2 Coconut excelled on ProsQA's more complex questions. It achieved 97.0 percent accuracy after generating 14.2 vectors（or tokens）on average，while GPT-2 achieved 77.5 percent accuracy after generating 49.4 text tokens on average.

在 ProsQA 更加复杂的问题上，Coconut 表现优异。平均生成 14.2 个向量（或 Token）后，Coconut 的准确率高达 97.0%，而 GPT-2 平均生成 49.4 个文本 Token 后，准确率仅为 77.5%。

Yes，but: On GSM8k，Coconut achieved 34.1 percent accuracy，while the baseline LLM achieved 42.9 percent. However，it generated significantly fewer vectors and tokens than the CoT generated tokens. Coconut generated 8.2 vectors on average compared to the baseline LLM's 25 text tokens.

在 GSM8k 数据集上，Coconut 取得了 34.1% 的准确率，而基准大语言模型（LLM）的准确率为 42.9%。然而，相比于通过思维链（Chain-of-Thought，CoT）生成的 Token，Coconut 所生成的向量和 Token 数量明显更少。具体来说，Coconut 平均生成 8.2 个向量，而基准大语言模型平均生成 25 个文本型 Token。

Why it matters: A traditional CoT commits to a single word at each step and thus encodes one reasoning path in a single CoT. Vectors are less interpretable to humans than language，but the model's output layer can still decode the thought vectors into probabilities over tokens. Further，inspecting the distribution of words stored along all continuous CoT vectors offers a way to understand multiple potential thought paths stored in one continuous CoT.

Why it matters：关键在于：传统的思维链（Chain-of-Thought，CoT）在每一步都专注于一个单独的词，因此单一的 CoT 编码了一条推理路径。相比语言，向量对人类而言更难理解，但模型的输出层依然可以将思维向量解码为 Token 的概率。此外，通过检查所有连续 CoT 向量中存储的词的分布，我们可以理解存储在同一个连续 CoT 中的多个潜在推理路径。

We're thinking: LLMs typically learn to reason over text，mainly because text data is widely available to train on. In contrast，neuroscience shows that the part of the human brain responsible for language largely goes quiet during reasoning tasks，which suggests that explicit language is not a key mechanism for reasoning. Coconut takes an intriguing step to enable LLMs to explore representations that don't encode the limitations of language.

我们的想法是：大语言模型（LLM）通常学习基于文本进行推理，这主要是因为有大量的文本数据可用于训练。相比之下，神经科学表明，人脑中负责语言的区域在进行推理时活动会显著降低，这表明明确的语言表达并非推理的关键。Coconut 采取了一个有趣的步骤，旨在使大语言模型能够探索不带有语言本身限制的表达形式。