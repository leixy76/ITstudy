## 20250312DeepSeek-R1-Uncensored-QwQ-32B-Puts-Reasoning-in-Smaller-Model

[DeepSeek-R1 Uncensored, QwQ-32B Puts Reasoning in Smaller Model, and more...](https://www.deeplearning.ai/the-batch/issue-292/)

Dear friends,

Some people today are discouraging others from learning programming on the grounds AI will automate it. This advice will be seen as some of the worst career advice ever given. I disagree with the Turing Award and Nobel prize winner who wrote,「It is far more likely that the programming occupation will become extinct [...] than that it will become all-powerful. More and more，computers will program themselves.」​ Statements discouraging people from learning to code are harmful!

现在有些人以「AI 会自动化编程工作」为由，劝退大家学习编程。我认为这是非常糟糕的职业建议。图灵奖和诺贝尔奖得主 [姓名] 曾写道：「编程这个职业更有可能消失 [...]，而不是变得无所不能。未来，计算机将会越来越多地自己编写程序。」我并不同意这种观点。阻止人们学习编程的言论，危害很大！

In the 1960s，when programming moved from punchcards（where a programmer had to laboriously make holes in physical cards to write code character by character）to keyboards with terminals，programming became easier. And that made it a better time than before to begin programming. Yet it was in this era that Nobel laureate Herb Simon wrote the words quoted in the first paragraph. Today's arguments not to learn to code continue to echo his comment.

在 20 世纪 60 年代，编程方式从穿孔卡片（punchcards）(程序员必须在卡片上打孔来编写代码）转移到带有终端的键盘，编程变得更加容易。这使得当时的编程环境比以往任何时候都更友好。然而，正是在这个时代，诺贝尔奖得主 Herb Simon 写下了本文第一段引用的那句话。时至今日，那些不鼓励学习编程的论调，依然与他的观点遥相呼应。

As coding becomes easier，more people should code，not fewer!

随着编码变得越来越容易，应该有更多人参与进来，而不是越来越少！

Over the past few decades，as programming has moved from assembly language to higher-level languages like C，from desktop to cloud，from raw text editors to IDEs to AI assisted coding where sometimes one barely even looks at the generated code（which some coders recently started to call vibe coding），it is getting easier with each step.（By the way，to learn more about AI assisted coding，check out our video-only short course,「Build Apps with Windsurf's AI Coding Agents.」)

在过去的几十年里，编程经历了巨大的变革：从汇编语言到 C 语言等高级语言，从桌面应用到云端应用，从原始文本编辑器到集成开发环境（IDE），再到现在的 AI 辅助编码。在 AI 的帮助下，有时人们甚至几乎不用去看生成的代码（最近一些程序员开始称之为「氛围编码」，指一种更凭感觉的编码方式），每一步都变得更加轻松。（如果您想了解更多关于 AI 辅助编码的信息，请观看我们的视频短课程：「利用 Windsurf 的 AI 编码智能体构建应用」。）

I wrote previously that I see tech-savvy people coordinating AI tools to move toward being 10x professionals — individuals who have 10 times the impact of the average person in their field. I am increasingly convinced that the best way for many people to accomplish this is not to be just consumers of AI applications，but to learn enough coding to use AI-assisted coding tools effectively.

我之前写过，我看到精通技术的人正在利用 AI 工具，努力成为 10 倍效能的专业人士 —— 即在各自领域拥有十倍于常人影响力的人。我越来越相信，对很多人来说，实现这一目标最好的方法，不仅仅是使用 AI 应用，而是要学习足够的编程知识，从而高效地使用 AI 辅助编程工具。

One question I'm asked most often is what someone should do who is worried about job displacement by AI. My answer is：Learn about AI and take control of it，because one of the most important skills in the future will be the ability to tell a computer exactly what you want，so it can do that for you. Coding（or getting AI to code for you）is the best way to do that.

我经常被问到的一个问题是，人们应该如何应对 AI 可能带来的工作岗位流失。我的回答是：去了解 AI，掌握它。因为未来最重要的技能之一，就是能够准确地告诉计算机你想要什么，然后让它帮你实现。而学习编程（或者利用 AI 来帮你编程），是掌握这项技能的最佳途径。

When I was working on the course Generative AI for Everyone and needed to generate AI artwork for the background images，I worked with a collaborator who had studied art history and knew the language of art. He prompted Midjourney with terminology based on the historical style，palette，artist inspiration and so on — using the language of art — to get the result he wanted. I didn't know this language，and my paltry attempts at prompting could not deliver as effective a result.

当我在开发《人人可用的生成式 AI（Generative AI)》课程，需要生成 AI 艺术作品作为背景图像时，我和一位研究艺术史、精通艺术语言的合作者一起工作。他运用艺术领域的专业术语，例如历史风格、配色方案、艺术家灵感等等来提示 Midjourney，从而获得理想的画面。我不具备相关的专业知识，效果远不如他。

Similarly，scientists，analysts，marketers，recruiters，and people of a wide range of professions who understand the language of software through their knowledge of coding can tell an LLM or an AI-enabled IDE what they want much more precisely，and get much better results. As these tools continue to make coding easier，this is the best time yet to learn to code，to learn the language of software，and learn to make computers do exactly what you want them to do.

同样，科学家、分析师、营销人员、招聘人员，以及各行各业掌握编程知识、理解软件语言的人们，可以更精确地告诉大语言模型（LLM）或 AI 赋能的集成开发环境（IDE）他们想要什么，从而获得更好的结果。随着这些工具不断降低编码的门槛，现在正是学习编程、掌握软件语言、并让计算机完全听你指挥的最佳时机。

Keep building!

Andrew

### News

#### Compact Reasoning

紧凑推理

Most models that have learned to reason via reinforcement learning were huge models. A much smaller model now competes with them.

以往，通过强化学习掌握推理能力的模型通常体量巨大。如今，一个规模较小的模型也加入了竞争。

What's new: Alibaba introduced QwQ-32B，a large language model that rivals the reasoning prowess of DeepSeek-R1 despite its relatively modest size.

最新进展：阿里巴巴推出了 QwQ-32B，这是一个大语言模型，虽然模型规模相对较小，但其推理能力足以和 DeepSeek-R1 匹敌。

1 Input/output: Text in（up to 131,072 tokens），text out

输入 / 输出：文本输入（最多 131,072 个 Token（Token)），文本输出

2 Architecture: Transformer，32.5 billion total parameter

架构：Transformer，总参数量 325 亿

3 Performance: Outperforms OpenAI o1-mini and DeepSeek-R1 on some bencharks

性能：在某些基准测试中，性能优于 OpenAI o1-mini 和 DeepSeek-R1

4 Features: Chain-of-thought reasoning，function calling，multilingual in 29 languages

功能：思维链推理（Chain-of-thought reasoning，一种模仿人类思考方式的推理方法），函数调用（function calling，允许模型调用外部工具或 API），29 种语言的多语言支持

5 Undisclosed: Output size，training data

未公开：输出规模，训练数据

6 Availability/price: Free via Qwen Chat. Weights are free to download for noncommercial and commercial uses under an Apache 2.0 license.

可用性 / 价格：通过 Qwen Chat 免费使用。权重在 Apache 2.0 许可下免费下载，可用于商业和非商业用途。

How it works: QwQ-32B is a version of Qwen2.5-32B that was fine-tuned to generate chains of thought using reinforcement learning（RL). Fine-tuning proceeded in two stages.

工作原理：QwQ-32B 是 Qwen2.5-32B 的一个版本，它经过微调，使用强化学习（Reinforcement Learning，RL）来生成思维链。微调过程分为两个阶段。

1 The first stage of RL fine-tuning focused on math and coding tasks. The model earned rewards for correct final outcomes（no partial credit for intermediate steps). An accuracy verifier checked its math solutions，while a code-execution server verified generated code for predefined test cases.

强化学习（RL）微调的第一阶段侧重于数学和编码任务。模型只有在得到正确的最终结果时才会获得奖励（中间步骤没有奖励）。一个准确性验证程序会检查其数学解答是否正确，而代码执行服务器则会验证其生成的代码是否能通过预定义的测试用例。

2 The second stage encouraged the model to follow instructions，use tools，and align its values with human preferences while maintaining math and coding performance，again rewarding final outcomes. In this stage，the model earned rewards from an unspecified reward model and some rule-based verifiers.

第二阶段旨在引导模型更好地遵循指令、运用工具，并使其价值取向与人类的偏好相契合，同时保证其在数学和编程方面的能力。同样，最终的结果也会被奖励。在这个阶段，模型会从一个具体的奖励模型（具体细节未公开）以及一些基于规则的验证系统那里获得奖励。

Performance: On several benchmarks for math，coding，and general problem solving，QwQ-32B outperforms OpenAI o1-mini（parameter count undisclosed）and achieves performance roughly comparable to DeepSeek-R1（671 billion parameters，37 billion active at any moment).

性能：在数学、编程和通用问题解决等多个基准测试中，QwQ-32B 的表现优于 OpenAI 的 o1-mini（参数数量未知），并且性能与 DeepSeek-R1（总参数 6710 亿，每次激活 370 亿）大致相当。

1 On AIME24（high-school competition math problems），QwQ-32B achieved 79.5 percent accuracy，well ahead of o1-mini（63.6 percent）but slightly behind DeepSeek-R1（79.8 percent).

在 AIME24（高中数学竞赛题）上，QwQ-32B 模型取得了 79.5% 的准确率，远超 o1-mini 模型（63.6%），但略低于 DeepSeek-R1 模型（79.8%）。

2 On LiveCodeBench（code generation，repair，and testing），QwQ-32B achieved 63.4 percent，outperforming o1-mini（53.8 percent）but trailing DeepSeek-R1（65.9 percent).

在 LiveCodeBench（代码生成、代码修复和测试）方面，QwQ-32B 的表现为 63.4%，超过了 o1-mini（53.8%），但不如 DeepSeek-R1（65.9%）。

3 On LiveBench（problem-solving in math，coding，reasoning，and data analysis），QwQ-32B reached 73.1 percent，ahead of o1-mini（59.1 percent）and DeepSeek-R1（71.6 percent).

在 LiveBench（数学、编程、推理和数据分析问题解决）方面，QwQ-32B 的表现为 73.1%，优于 o1-mini（59.1%）和 DeepSeek-R1（71.6%）。

4 On IFEval（following instructions），QwQ-32B achieved 83.9 percent，outperforming DeepSeek-R1（83.8 percent）but behind o1-mini（84.8 percent).

在 IFEval（按照说明）评测中，QwQ-32B 得分 83.9%，优于 DeepSeek-R1（83.8%），但低于 o1-mini（84.8%）。

5 On BFCL（function calling），QwQ-32B achieved 66.4 percent，better than DeepSeek-R1（60.3 percent），and o1-mini（62.8 percent).

在 BFCL（函数调用，Function Calling）评测中，QwQ-32B 得分 66.4%，优于 DeepSeek-R1（60.3%）和 o1-mini（62.8%）。

Behind the news: DeepSeek's initial model，DeepSeek-R1-Zero，similarly applied RL to a pretrained model. That effort produced strong reasoning but poor readability（for example，math solutions with correct steps but jumbled explanations). To address this shortcoming，the team fine-tuned DeepSeek-R1 on long chain-of-thought examples before applying RL. In contrast，QwQ-32B skipped preliminary fine-tuning and applied RL in two stages，first optimizing for correct responses and then for readability.

新闻幕后：DeepSeek 的早期模型 DeepSeek-R1-Zero，也采用了类似的方法，即对预训练模型应用强化学习（RL）。这种方法虽然带来了强大的推理能力，但模型生成的内容可读性不佳（例如，数学题的解题步骤正确，但解释却杂乱无章）。为了解决这个问题，DeepSeek 团队在应用强化学习之前，先利用大量的长链推理示例对 DeepSeek-R1 进行了微调。相比之下，QwQ-32B 则跳过了预先的微调步骤，而是分两个阶段应用强化学习：首先优化模型的回答准确性，然后再提升其可读性。

Why it matters: RL can dramatically boost LLMs' reasoning abilities，but the order in which different behaviors are rewarded matters. Using RL in stages enabled the team to build a 32 billion parameter model — small enough to run locally on a consumer GPU — that rivals a much bigger mixture-of-experts model，bringing powerful reasoning models within reach for more developers. The Qwen team plans to scale its RL approach to larger models，which could improve the next-gen reasoning abilities further while adding greater knowledge.

重要性：强化学习（RL）能够显著增强大语言模型（LLM）的推理能力。但对不同行为进行奖励的先后顺序至关重要。通过分阶段地应用强化学习（RL），该团队成功构建了一个 320 亿参数的模型（足够在消费级 GPU 上本地运行），其性能可以媲美更大的混合专家模型。这使得开发者们能够更容易地获取强大的推理模型。Qwen 团队计划将此强化学习（RL）方法扩展到更大规模的模型，有望在提升下一代推理能力的同时，进一步扩充模型的知识储备。

We're thinking: How far we've come since「Let's think step by step」!

我们不禁感慨：自从「让我们逐步思考」项目启动以来，我们已经取得了多么大的进步！

#### Microsoft Tackles Voice-In，Text-Out

微软攻克语音输入到文本输出的难题

Microsoft debuted its first official large language model that responds to spoken input.

微软发布了其首个能够响应语音输入的官方大语言模型。

What's new: Microsoft released Phi-4-multimodal，an open weights model that processes text，images，and speech simultaneously.

要点：微软发布了 Phi-4-multimodal，这是一种开放权重模型，能够同时处理文本、图像和语音。

[Empowering innovation: The next generation of the Phi family | Microsoft Azure Blog](https://azure.microsoft.com/en-us/blog/empowering-innovation-the-next-generation-of-the-phi-family/?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz--3y3RXjUXVVnR-2W24Pwv0YfKeZMzD3pMv8YYZ-9CvFwDTMLGRGK4pRgeKyhGyMyH-4ZnT)

[microsoft/Phi-4-multimodal-instruct · Hugging Face](https://huggingface.co/microsoft/Phi-4-multimodal-instruct)

1 Input/output: Text，speech，images in（up to 128,000 tokens); text out（0.34 seconds to first token，26 tokens per second)

输入 / 输出：文本、语音、图像输入（最多 128,000 个 Token)；输出文本（首个 Token 耗时 0.34 秒，每秒 26 个 Token)

2 Performance: State of the art in speech transcription. Comparable to similar models in other tasks

性能：语音转录能力达到最先进水平。在其他任务中，性能与其他类似模型不相上下。

3 Knowledge cutoff: June 2024

知识截止日期：2024 年 6 月

4 Architecture: transformer，5.6 billion parameters

架构：Transformer （一种神经网络架构），拥有 56 亿个参数

5 Features: Text-image-speech processing，multilingual，tool use.

功能：处理文本、图像和语音，支持多语种，以及使用工具。

6 Undisclosed: Training datasets，output size

未公开：训练数据集，输出规模。

7 The company also released Phi-4-mini，an open weights 3.8 billion-parameter version of its biggest large language model（LLM), Phi-4. Phi-4-mini outperforms larger models including Llama 3.1 8B and Ministral-2410 8B on some benchmarks.

该公司还发布了 Phi-4-mini，这是一个拥有 38 亿参数的开放权重版本，也是其最大的大语言模型（LLM）Phi-4 的精简版。在一些评测基准上，Phi-4-mini 的表现甚至超过了 Llama 3.1 8B 和 Ministral-2410 8B 这样更大的大语言模型（LLM）。

8 Availability/price: Weights are free to download for noncommercial and commercial use under a MIT license.

可用性 / 价格：模型权重根据 MIT 许可证免费提供下载，可用于非商业和商业用途。

How it works: Phi-4-multimodal has six components：Phi-4-mini，vision and speech encoders as well as corresponding projectors（which modify the vision or speech embeddings so the base model can understand them），and two LoRA adapters. The LoRA adapters modify the base weights depending on the input：One adapter modifies them for speech-text problems，and one for vision-text and vision-speech problems.

工作原理：Phi-4-multimodal 包含六个主要组成部分：Phi-4-mini 模型、视觉和语音编码器，以及对应的投影器（Projector），用于调整视觉或语音嵌入（Embedding），使基础模型能够理解它们。此外，还有两个 LoRA 适配器。这些 LoRA 适配器会根据输入内容调整基础权重：一个适配器专门处理语音 - 文本问题，另一个则处理视觉 - 文本和视觉 - 语音问题。

1 The speech encoder is a Conformer (which combines convolutional layers with a transformer）and the speech projector is a vanilla neural network. They trained Phi-4-multimodal to convert 2 million hours of speech to text，modifying only the speech encoder and projector. They further trained the system to convert speech to text，translate speech to other languages，summarize speech，and answer questions about speech，modifying only the speech encoder and the speech-text LoRA adapter.

语音编码器采用 Conformer 架构（一种结合了卷积层和 Transformer 的结构），而语音投影器则是一个简单的神经网络。研究人员训练了 Phi-4-multimodal 模型，使其能够将 200 万小时的语音转化成文本，在这个过程中，他们只调整了语音编码器和投影器。此外，他们还训练该系统执行更多任务，例如语音转文本、语音翻译、语音摘要以及语音问答。在这些任务中，他们仅修改了语音编码器和语音-文本 LoRA 适配器。

2 The vision encoder is based on a pretrained SigLIP-400M vision transformer，and the vision projector is a vanilla neural network. They trained the model to process text and images in four stages：(i）They trained Phi-4-multimodal to caption images，modifying only the vision projector.（ii）They trained the system on 500 billion tokens to caption images，transcribe text in images，and perform other tasks，modifying only the vision encoder and projector.（iii）They trained the system to answer questions about images，charts，tables，and diagrams and to transcribe text in images，modifying the vision encoder，project，and vision-text LoRA adapter.（iv）Finally，they trained the system to compare images and summarize videos，modifying only the vision projector and vision-text LoRA adapter.

视觉编码器基于预训练的 SigLIP-400M 视觉 Transformer，视觉投影器是一个标准神经网络。他们训练模型分四个阶段处理文本和图像：（i）他们训练 Phi-4-multimodal 模型生成图像描述，仅修改视觉投影器。（ii）他们在 5000 亿个 Token 上训练系统，使其能够生成图像描述、转录图像中的文本并执行其他任务，仅修改视觉编码器和投影器。（iii）他们训练系统回答关于图像、图表、表格和示意图的问题，并转录图像中的文本，修改视觉编码器、视觉投影器和视觉 - 文本 LoRA 适配器。（iv）最后，他们训练系统比较图像并生成视频摘要，仅修改视觉投影器和视觉 - 文本 LoRA 适配器。

3 To adapt Phi-4-multimodal for images and speech，they trained the system to generate the text responses to a subset of the text-vision data that had been converted to speech-image using a proprietary text-to-speech engine，modifying only the text-vision LoRA adapter，vision encoder，and vision projector.

为了让 Phi-4-multimodal 能够处理图像和语音，研究者们训练系统，使其可以对文本 - 视觉数据的子集生成文本回复。这个子集的数据通过一种专有的文本转语音引擎，被转换成了语音 - 图像的格式。在训练过程中，仅修改了文本 - 视觉 LoRA 适配器、视觉编码器和视觉投影器。

4 Example inference：Given a question as speech and an image，the audio encoder and projector convert the speech to tokens，and the image encoder and projector convert the image into tokens. Given the tokens，Phi-4-multimodal，which uses the weights of Phi-4-mini modified by the vision-text/vision-speech LoRA adapter，generates a text response.

示例推理：对于一个语音问题和一张图像，音频编码器和投影器将语音转换成 Token，图像编码器和投影器将图像转换成 Token。然后，Phi-4-multimodal（它使用了经过视觉 - 文本 / 视觉 - 语音 LoRA（Low-Rank Adaptation）适配器调整后的 Phi-4-mini 的模型权重） ，会根据这些 Token 生成一段文本回复。

Results: The authors compared Phi-4-multimodal to other multimodal models on text-vision，vision-speech，text-speech tasks.

结果：作者在文本 - 视觉、视觉 - 语音和文本 - 语音等任务上，将 Phi-4-multimodal 与其他多模态模型进行了比较。

2 Across 11 text-vision benchmarks，Phi-4-multimodal came in fourth out of 11 models. It outperformed Qwen2.5-VL-3B，Claude 3.5 Sonnet，and GPT 4o-mini. It trailed Qwen2.5-VL-7B，GPT-4o，and Gemini-2 Flash.

在 11 个文本 - 视觉基准测试中，Phi-4-multimodal 在 11 个模型中位列第四，性能优于 Qwen2.5-VL-3B、Claude 3.5 Sonnet 和 GPT 4o-mini，但逊色于 Qwen2.5-VL-7B、GPT-4o 和 Gemini-2 Flash。

3 Across four vision-speech benchmarks，Phi-4-multimodal outperformed by at least 6 percentage points Gemini-2.0-Flash，Gemini-2.0-Flash-Lite-preview，and InternOmni.

在四个视觉 - 语音基准测试中，Phi-4-multimodal 的表现至少比 Gemini-2.0-Flash、Gemini-2.0-Flash-Lite-preview 以及 InternOmni 高 6 个百分点以上。

4 Phi-4-multimodal outperformed all competitors in Microsoft's report（including Qwen2-audio，Gemini 2.0 Flash，and GPT-4o）at transcribing speech from text in three datasets. It also achieved competitive performance in speech translation，outperforming its competitors on two of four datasets.

根据 Microsoft 的报告，Phi-4-multimodal 在语音转录任务中表现出色，在三个数据集上均超越了所有竞争对手，这些对手包括 Qwen2-audio、Gemini 2.0 Flash 和 GPT-4o。在语音翻译方面，它也展现了强大的竞争力，在四个数据集中，有两个数据集上的表现优于其他模型。

Behind the news: This work adds to the growing body of models with voice-in/text-out capability，including the open weights DiVA model developed by a team led by Diyi Yang at Stanford University.

背景信息：这项研究进一步丰富了语音输入、文本输出模型的案例。此类模型还包括由斯坦福大学 Diyi Yang 领导的团队开发的开源 DiVA 模型。

Why it matters: The architectural options continue to expand for building neural networks that process text，images，audio，and various combinations. While some teams maintain separate models for separate data modalities，like Qwen2.5 (for text）and Qwen2.5-VL）(for vision-language tasks），others are experimenting with mixture-of-expert models like DeepSeek-V3. Phi-4-multimodal shows that Mixture-of-LoRAs is an effective approach for processing multimodal data — and gives developers a couple of new open models to play with.

重要性：构建用于处理文本、图像、音频以及它们之间各种组合的神经网络，其架构选择正在不断扩展。一些团队为不同的数据类型维护着单独的模型，例如 Qwen2.5（用于文本）和 Qwen2.5-VL（用于视觉语言任务）。另一些团队则在尝试混合专家模型（Mixture-of-Expert Models），例如 DeepSeek-V3。Phi-4-multimodal 表明，Mixture-of-LoRAs 是一种处理多模态数据的有效方法，它为开发者们提供了几个新的开源模型进行实验。

We're thinking: Output guardrails have been built to ensure appropriateness of text output，but this is difficult to apply to a voice-in/voice-out architecture.（Some teams have worked on guardrails that screen audio output directly，but the technology is still early.）For voice-based applications，a voice-in/text-out model can generate a candidate output without a separate，explicit speech-to-text step，and it accommodates text-based guardrails before it decides whether or not to read the output to the user.

我们正在考虑：为了确保文本输出的适当性，已经建立了输出安全机制，但这很难应用于语音输入 / 语音输出（voice-in/voice-out）架构。(一些团队已经致力于直接筛选音频输出的安全机制，但这项技术仍处于早期阶段。）对于基于语音的应用程序，语音输入 / 文本输出（voice-in/text-out）模型可以在没有单独的、显式的语音转文本步骤的情况下生成候选输出，并且在决定是否向用户播放输出内容之前，它可以应用基于文本的安全机制。

#### Judge Upholds Copyright in AI Training Case

法官维护 AI 训练案例中的版权

A United States court delivered a major ruling that begins to answer the question whether，and under what conditions，training an AI system on copyrighted material is considered fair use that doesn't require permission.

美国一家法院做出了一项重要裁决，该裁决初步解答了一个重要问题：在何种情况下，使用受版权保护的材料训练 AI 系统，可以被认定为「合理使用」，从而无需获得版权许可。

What's new: A U.S. Circuit judge ruled on a claim by the legal publisher Thomson Reuters that Ross Intelligence，an AI-powered legal research service，could not claim that training its AI system on materials owned by Thomson Reuters was a so-called「fair use.」Training the system did not qualify as fair use，he decided，because its output competed with Thomson Reuters' publications.

最新进展：美国巡回法院的一位法官做出裁决，驳回了法律出版商 Thomson Reuters 的一项诉求。该诉求针对的是 Ross Intelligence（一家由 AI 驱动的法律研究服务公司），Ross Intelligence 声称，使用 Thomson Reuters 拥有的材料来训练其 AI 系统属于「合理使用」。法官认为，训练 AI 系统不属于合理使用范畴，因为训练结果与 Thomson Reuters 的出版物构成了竞争关系。

How it works: Thomson Reuters had sued Ross Intelligence after the defendant trained an AI model using 2,243 works produced by Thomson Reuters without the latter's permission. This ruling reversed an earlier decision in 2023，when the same judge had allowed Ross Intelligence's fair-use defense to proceed to trial. In the new ruling，he found that Ross Intelligence's use failed to meet the definition of fair use in key respects.（A jury trial is scheduled to determine whether Thomson Reuters' copyright was in effect at the time of the infringement and other aspects of the case.)

事件经过：Thomson Reuters 起诉 Ross Intelligence，原因是后者未经许可，使用了 Thomson Reuters 创作的 2243 部作品来训练一个 AI 模型。此裁决推翻了 2023 年的一项早期裁决，当时，同一位法官曾允许 Ross Intelligence 以合理使用为理由进行辩护，进入审判阶段。但在新的裁决中，法官认为 Ross Intelligence 的行为在关键方面不符合「合理使用」的定义。(计划进行陪审团审判，以确定在侵权发生时，Thomson Reuters 的版权是否仍然有效，以及确定案件的其他相关问题。)

1 Ross Intelligence's AI-powered service competed directly with Thomson Reuters，potentially undermining its market by offering a derivative product without licensing its works. Use in a competing commercial product undermines a key factor in fair use.

Ross Intelligence 的人工智能驱动服务直接与 Thomson Reuters 展开竞争，并且可能通过提供未经授权的衍生产品来损害 Thomson Reuters 的市场地位。将该服务应用于具有竞争力的商业产品中，会减损「合理使用（fair use）」原则中的一个关键因素。

2 The judge found that Ross Intelligence's use was commercial and not transformative，meaning it did not significantly alter or add new meaning to Thomson Reuters' works — another key factor in fair use. Instead，it simply repackaged the works.

法官裁定，Ross Intelligence 的行为属于商业用途，且不具有变革性，也就是说，它并没有对 Thomson Reuters 的作品进行显著的修改或赋予其新的含义。这是判断是否属于合理使用的另一个关键因素。相反，它仅仅是对这些作品进行了重新包装。

3 The ruling acknowledged that Thomson Reuters' works were not highly creative but noted that they possessed sufficient originality for copyright protection due to the editorial creativity and judgment involved in producing it.

裁决结果表明，虽然汤森路透（Thomson Reuters）的作品不属于极富创造性的类型，但其在编辑过程中的创造性选择和判断，赋予了作品足够的原创性，使其受到版权保护。

4 Although Ross Intelligence used only small portions of Thomson Reuters' works，this did not weigh strongly in favor of fair use because those portions represented the most important summaries produced by Ross Intelligence.

尽管 Ross Intelligence 仅使用了 Thomson Reuters 作品中的一小部分，但这并没有显著地支持「合理使用」原则，因为这些被使用的部分恰恰是 Ross Intelligence 生成的最关键的摘要信息。

Behind the news: The ruling comes amid a wave of lawsuits over AI training and copyright in several countries. Many of these cases are in progress，but courts have weighed in on some.

新闻背景：在多个国家，关于人工智能（AI）训练和版权的诉讼如同浪潮般涌现，而这项裁决正是在这样的背景下发布的。虽然大多数案件仍在审理中，但法院已经对部分案件做出了裁决。

1 The New York Times is suing OpenAI and Microsoft，arguing that their models generate output that competes with its journalism.

《纽约时报》正在起诉 OpenAI 和 Microsoft，理由是它们的大模型产出的内容直接与《纽约时报》的新闻报道构成竞争关系。

2 Condé Nast，McClatchy，and other major publishers recently filed a lawsuit against Cohere，accusing it of using copyrighted news articles to train its AI models.

Condé Nast、McClatchy 和其他主要出版商最近起诉了 Cohere，指控它未经授权使用受版权保护的新闻文章来训练 AI 模型。

3 Sony，UMG，and Warner Music filed lawsuits against AI music companies including Suno and Udio for allegedly using copyrighted recordings without permission.

Sony、UMG 和 Warner Music 对 Suno 和 Udio 等多家 AI 音乐公司提起了诉讼，指控它们未经授权使用了受版权保护的音乐录音。

4 A judge dismissed key arguments brought by software developers who claimed that GitHub Copilot was trained on software they created in violation of open source licenses. The judge ruled in favor of Microsoft and OpenAI.

针对 GitHub Copilot 涉嫌违反开源许可协议，使用开发者所创建的软件进行训练一事，相关软件开发人员的关键诉求被法官驳回。法官最终裁定 Microsoft 和 OpenAI 胜诉。

5 In Germany，the publisher of the LAION dataset won a case in which a court ruled that training AI models on publicly available images did not violate copyrights.

在德国，LAION 数据集的发布方打赢了一场官司。法院判定，用公开的图片来训练 AI 模型，并不构成侵权。

Why it matters: The question of whether training（or copying data to train）AI systems is a fair use of copyrighted works hangs over the AI industry，from academic research to commercial projects. In the wake of this ruling，courts may be more likely to reject a fair-use defense when AI companies train models on copyrighted material to create output that overlaps with or replaces traditional media，as The New York Times alleges in its lawsuit against OpenAI. However，the ruling leaves room for fair use with respect to models whose output doesn't compete directly with copyrighted works.

为什么这很重要：训练（或复制数据以训练）AI 系统，是否构成对受版权保护作品的合理使用，这个问题对整个 AI 行业至关重要，无论是学术研究还是商业项目都深受影响。这一裁决暗示，未来如果 AI 公司使用受版权保护的材料训练模型，并且生成的作品与传统媒体的内容存在重叠或替代关系，那么法院可能更不愿意支持「合理使用」的抗辩理由。《纽约时报》在起诉 OpenAI 的案件中就提出了类似的指控。然而，对于那些生成内容不与受版权保护作品直接竞争的模型，该裁决仍然保留了「合理使用」的可能性。

We're thinking: Current copyright laws weren't designed with AI in mind，and rulings like this one fill in the gaps case by case. Clarifying copyright for the era of generative AI could help our field move forward faster.

我们的观点是：现行的版权法在制定之初并未将人工智能（AI）纳入考量，因此，类似的判决正是在通过个案来弥补法律的不足。如果能明确生成式 AI 时代的版权归属问题，将有助于推动我们整个领域更快地发展。

#### DeepSeek-R1 Uncensored

DeepSeek-R1 无审查版

Large language models built by developers in China may，in some applications，be less useful outside that country because they avoid topics its government deems politically sensitive. A developer fine-tuned DeepSeek-R1 to widen its scope without degrading its overall performance.

由中国开发者构建的大语言模型（Large Language Model，LLM），在某些应用场景下，于中国境外的使用价值可能会降低，因为它们会尽量避免触及其政府认定的政治敏感话题。一位开发者对 DeepSeek-R1 进行了微调，目的是在不牺牲其整体性能的前提下，使其能够处理更广泛的主题。

What's new: Perplexity released R1 1776，a version of DeepSeek-R1 that responds more freely than the original. The model weights are available to download under a commercially permissive MIT license.

最新消息：Perplexity 发布了 R1 1776，它是 DeepSeek-R1 的一个版本，其响应比原始版本更加开放。该模型的权重在 MIT 许可下发布，允许商业用途，可供下载。

How it works: The team modified DeepSeek-R1's knowledge of certain topics by fine-tuning it on curated question-answer pairs.

它是如何工作的：研究团队通过微调 DeepSeek-R1，修改了它对特定主题的认知。具体来说，他们使用了精心挑选的问答数据对 DeepSeek-R1 进行了训练。

1 Human experts identified around 300 topics that are censored in China.

人类专家识别出约 300 个在中国受到审查的主题。

2 The authors developed a multilingual classifier that spots text related to these topics.

作者们开发了一种多语种分类器，用于识别与特定主题相关的文本。

3 They identified 40,000 prompts that the classifier classified as sensitive with high confidence. They discarded those that contained personally identifiable information.

他们利用该分类器识别出 40,000 个被高度确信为敏感的提示（prompts）。随后，他们剔除了其中包含个人身份信息的提示（prompts）。

4 For each prompt，they produced factual，chain-of-thought responses that mirrored DeepSeek-R1's typical reasoning processes.

对于每一个提示（prompt，英文为 prompt），他们都生成了基于事实、具有链式思考（chain-of-thought，英文为 chain-of-thought）过程的回应，这些回应与 DeepSeek-R1 典型的推理过程十分相似。

5 They fine-tuned DeepSeek-R1 on the resulting prompt-response pairs.

他们利用这些提示（prompt）和回应配对的数据，对 DeepSeek-R1 进行了微调。

Results: The fine-tuned model responded to politically charged prompts factually without degrading its ability to generate high-quality output.

Results：微调后的模型能够对涉及政治话题的提问给出如实回答，同时保持其生成高质量内容的能力。

1 The authors fed their model 1,000 diverse prompts that covered frequently censored topics. An unspecified combination of human and AI judges rated the models' responses according to the degree to which they are（i）evasive and（ii）censored outright.

作者使用了 1,000 个涵盖常见审查主题的各种各样的提示来测试他们的模型。人类和 AI 评委以某种方式（具体比例未说明）对模型回答进行评分，评分标准是回答中（i）回避问题的程度和（ii）直接进行审查的程度。

2 100 percent of the fine-tuned model's responses were rated uncensored，whereas the original version censored around 85 percent of sensitive queries. By comparison，DeepSeek-V3 censored roughly 73 percent，Claude-3.5-Sonnet around 5 percent，o3-mini about 1 percent，and GPT-4o 0 percent.

经过微调的模型，其回复的 100% 被评定为未经过内容审查，而原始版本则会对大约 85% 的敏感查询进行审查。相比之下，DeepSeek-V3 大约审查了 73% 的内容，Claude-3.5-Sonnet 大约 5%，o3-mini 大约 1%，而 GPT-4o 则完全没有审查。

3 Evaluated on four language and math benchmarks（MMLU，DROP，MATH-500，and AIME 2024）and unspecified internal benchmarks，the fine-tuned and original models performed nearly identically. Their scores differed by a few tenths of a percent except on AIME 2024（competitive high-school math problems），where the fine-tuned model achieved 79.8 percent compared to the original's 80.96 percent.

在四个语言和数学基准测试（MMLU、DROP、MATH-500 和 AIME 2024）以及未公开的内部基准测试上进行评估，微调后的模型和原始模型的表现几乎相同。它们的得分差异仅为零点几个百分点，但在 AIME 2024（竞争性高中数学问题）上除外，微调后的模型和原始模型分别达到了 79.8% 和 80.96%。

Behind the news: Among the first countries to regulate AI，China requires AI developers to build models that uphold「Core Socialist Values」and produce true and reliable output. When these objectives conflict，the political goal tends to dominate. While large language models built by developers in China typically avoid contentious topics，the newer DeepSeek models enforce this more strictly than older models like Qwen and Yi，using methods akin to Western measures for aligning output，like Reinforcement Learning from Human Feedback and keyword filters.

新闻解读：中国是最早一批监管人工智能（AI）的国家之一，它要求 AI 开发者所构建的模型必须符合「社会主义核心价值观」，并确保生成的内容真实可信。如果这些目标之间出现冲突，通常政治目标会优先。虽然中国开发者构建的大语言模型（LLM/Large Language Model）倾向于避开敏感话题，但更新的 DeepSeek 模型在这方面比 Qwen 和 Yi 等早期模型执行得更为严格。它们采用的手段与西方用于优化模型输出的方法类似，例如基于人类反馈的强化学习（Reinforcement Learning from Human Feedback）以及关键词过滤。

Why it matters: AI models tend to reflect their developers' values and legal constraints. Perplexity's targeted fine-tuning approach addresses this barrier to international adoption of open-source models.

重要性：人工智能（AI）模型往往会体现开发者的价值观和法律限制。Perplexity 公司有针对性的微调策略，旨在解决开源模型在国际上被广泛采用时所面临的这一障碍。

We're thinking: As models with open weights are adopted by the global community，they become a source of soft power for their developers，since they tend to reflect their developers' values. This work reflects a positive effort to customize a model to reflect the user's values instead — though how many developers will seek out a fine-tuned version rather than the original remains to be seen.

我们认为：随着开放权重（open weights）模型被全球广泛应用，它们也成为了开发者的一种软实力来源，因为这些模型往往会体现开发者的价值观。而这项研究则展示了一种积极的尝试，即对模型进行定制，使其能够反映 * 用户 * 的价值观 —— 至于有多少开发者会选择这种定制后的微调版本，而不是原始版本，还有待进一步观察。