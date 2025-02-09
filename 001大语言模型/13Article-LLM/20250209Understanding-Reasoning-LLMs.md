## 20250209Understanding-Reasoning-LLMs

[Understanding Reasoning LLMs - by Sebastian Raschka, PhD](https://magazine.sebastianraschka.com/p/understanding-reasoning-llms?continueFlag=c88ae10074507aefcbc4375ccc10431e)

[以 DeepSeek R1 为例学习“推理型大语言模型 [译] | 宝玉的分享](https://baoyu.io/translations/understanding-reasoning-llms)

Methods and Strategies for Building and Refining Reasoning Models

Sebastian Raschka, PhD

Feb 05, 2025

This article describes the four main approaches to building reasoning models, or how we can enhance LLMs with reasoning capabilities. I hope this provides valuable insights and helps you navigate the rapidly evolving literature and hype surrounding this topic.

本文介绍了构建推理模型的四种主要方法，也就是如何提升大语言模型（LLM/Large Language Model）的推理能力。希望本文能为您提供有价值的参考，助您在快速发展的相关文献和围绕此主题的各种热点中理清头绪。

In 2024, the LLM field saw increasing specialization. Beyond pre-training and fine-tuning, we witnessed the rise of specialized applications, from RAGs to code assistants. I expect this trend to accelerate in 2025, with an even greater emphasis on domain- and application-specific optimizations (i.e., "specializations").

2024 年，大语言模型（LLM/Large Language Model）领域呈现出日益专业化的趋势。除了预训练和微调之外，涌现出了各种专业应用，例如 RAG（检索增强生成）和代码助手。我预计 2025 年这一趋势将会加速，更加注重针对特定领域和应用的优化，也就是更加「专业化」。

Fig: Stages 1-3 are the common steps to developing LLMs. Stage 4 specializes LLMs for specific use cases.

开发大语言模型（LLM/Large Language Model）通常包括 1-3 阶段。而第 4 阶段则专注于根据特定应用场景对大语言模型进行定制。

The development of reasoning models is one of these specializations. This means we refine LLMs to excel at complex tasks that are best solved with intermediate steps, such as puzzles, advanced math, and coding challenges. However, this specialization does not replace other LLM applications. Because transforming an LLM into a reasoning model also introduces certain drawbacks, which I will discuss later.

推理模型便是这种定制化的一种体现。这意味着，我们需要对大语言模型进行优化，使其能够更好地处理那些需要分步骤解决的复杂任务，例如谜题、高等数学和编程挑战。但是，这种专业化并非要取代大语言模型的其他应用。因为将大语言模型改造为推理模型，也会带来一些局限性，我将在后文中进行讨论。

To give you a brief glimpse of what's covered below, in this article, I will:

为了让您对下文内容有个大致了解，在本文中，我将：

1 Explain the meaning of "reasoning model"

解释「推理模型」(reasoning model）的含义

2 Discuss the advantages and disadvantages of reasoning models

讨论推理模型（Reasoning Model）的优势与劣势

3 Outline the methodology behind DeepSeek R1

概述 DeepSeek R1 的设计方法

4 Describe the four main approaches to building and improving reasoning models

介绍构建与改进推理模型的四种主要思路

5 Share thoughts on the LLM landscape following the DeepSeek V3 and R1 releases

分享对 DeepSeek V3 与 R1 发布后，LLM 生态现状的看法

6 Provide tips for developing reasoning models on a tight budget

如何在预算有限的情况下开发推理模型？

I hope you find this article useful as AI continues its rapid development this year!

一些实用技巧希望这篇文章对您有所帮助，今年人工智能（AI）领域依旧会高速发展！

### 0.1 How do we define "reasoning model"?

我们该如何定义「推理模型」？

If you work in AI (or machine learning in general), you are probably familiar with vague and hotly debated definitions. The term "reasoning models" is no exception. Eventually, someone will define it formally in a paper, only for it to be redefined in the next, and so on.

如果你在人工智能（AI）领域工作（或者更广义的机器学习领域），你可能对那些模糊不清且备受争议的定义习以为常。「推理模型」这个术语也不例外。最终，总会有人在一篇论文中给出正式定义，但紧接着又会在另一篇论文中被重新定义，如此反复。

In this article, I define "reasoning" as the process of answering questions that require complex, multi-step generation with intermediate steps. For example, factual question-answering like "What is the capital of France?" does not involve reasoning. In contrast, a question like "If a train is moving at 60 mph and travels for 3 hours, how far does it go?" requires some simple reasoning. For instance, it requires recognizing the relationship between distance, speed, and time before arriving at the answer.

在本文中，我将「推理」定义为回答那些需要通过中间步骤进行复杂、多步骤生成的问题。举例来说，像「法国的首都是什么？」这样的事实性问题不涉及推理。与此相对，像「如果一列火车以每小时 60 英里的速度行驶 3 小时，那么它行驶了多远？」这样的问题就需要一些简单的推理。例如，需要理解距离、速度和时间之间的关系才能得出答案。

Fig: A regular LLM may only provide a short answer (as shown on the left), whereas reasoning models typically include intermediate steps that reveal part of the thought process. (Note that many LLMs who have not been specifically developed for reasoning tasks can also provide intermediate reasoning steps in their answers.)
Most modern LLMs are capable of basic reasoning and can answer questions like, "If a train is moving at 60 mph and travels for 3 hours, how far does it go?" So, today, when we refer to reasoning models, we typically mean LLMs that excel at more complex reasoning tasks, such as solving puzzles, riddles, and mathematical proofs.

普通的大语言模型（LLM）可能只会给出简短的答案，但推理模型通常会展示中间步骤，从而呈现部分的思考过程（值得注意的是，即使是那些并非专门为推理而设计的大语言模型（LLM），有时也能在回答中给出中间推理步骤）。现在的大多数大语言模型（LLM）都具备基本的推理能力，例如，它们可以回答「一列火车以 60 英里 / 小时的速度行驶 3 小时，那么它行驶了多少英里？」这样的问题。因此，我们现在所说的推理模型，通常是指那些擅长解决更复杂推理问题的大语言模型（LLM），比如解谜、猜谜语以及进行数学证明等。

Additionally, most LLMs branded as reasoning models today include a "thought" or "thinking" process as part of their response. Whether and how an LLM actually "thinks" is a separate discussion.

此外，现在市面上大多数标榜具有推理能力的大语言模型（LLM），都会在回复中包含一个「思考」或「思维」的过程。至于大语言模型（LLM）究竟有没有「思考」，以及如何「思考」，则是另外一个话题了。

Intermediate steps in reasoning models can appear in two ways. First, they may be explicitly included in the response, as shown in the previous figure. Second, some reasoning LLMs, such as OpenAI's o1, run multiple iterations with intermediate steps that are not shown to the user.

推理模型在进行推理时，中间步骤的展现方式主要有两种。第一种，中间步骤会明确地包含在模型的回复中，正如之前的图示所展示的。第二种，一些具备推理能力的大语言模型（LLM），例如 OpenAI 的 o1 模型，会在内部运行多次迭代以完成推理，但这些中间步骤并不会呈现给用户。

"Reasoning" is used at two different levels: 1) processing the input and generating via multiple intermediate steps and 2) providing some sort of reasoning as part of the response to the user.

「推理」这个概念可以体现在两个不同的层面：1 ）在处理输入信息和生成结果时，模型会经过多个中间步骤；2 ）模型能够提供某种形式的推理过程，作为对用户提问的回答。

### 02. When should we use reasoning models?

那么，我们应该在什么情况下使用推理模型呢？

Now that we have defined reasoning models, we can move on to the more interesting part: how to build and improve LLMs for reasoning tasks. However, before diving into the technical details, it is important to consider when reasoning models are actually needed.

在明确了推理模型的定义之后，接下来我们将探讨更有意思的内容：如何构建和优化大语言模型（LLM），使其更好地执行推理任务。不过，在深入研究技术细节之前，我们需要认真思考一个问题：究竟在什么情况下，我们才真正需要用到推理模型？

When do we need a reasoning model? Reasoning models are designed to be good at complex tasks such as solving puzzles, advanced math problems, and challenging coding tasks. However, they are not necessary for simpler tasks like summarization, translation, or knowledge-based question answering. In fact, using reasoning models for everything can be inefficient and expensive. For instance, reasoning models are typically more expensive to use, more verbose, and sometimes more prone to errors due to "overthinking." Also here the simple rule applies: Use the right tool (or type of LLM) for the task.

什么情况下我们需要推理模型？推理模型擅长处理复杂任务，例如解决高级数学难题、挑战性编码问题以及各种谜题。不过，对于像总结、翻译或知识问答这类简单的任务，推理模型并非必选项。实际上，对所有任务都使用推理模型可能会导致效率降低和成本增加。例如，使用推理模型的成本通常较高，输出内容也较为冗余，而且有时还会因为「过度思考」—— 即模型在简单问题上进行不必要的复杂分析 —— 而更容易出错。因此，一个简单的原则是：针对特定任务，选择合适的工具（或大语言模型（LLM/Large Language Model）类型）。

The key strengths and limitations of reasoning models are summarized in the figure below.

下图总结了推理模型的关键优势和局限。

The key strengths and weaknesses of reasoning models.

推理模型的关键优势与劣势

| Good at                               | Bad at                                         |
| :------------------------------------- | :--------------------------------------------- |
| + Deductive or inductive reasoning    | - Fast and cheap responses                     |
| (e.g., riddles, math proofs)          | (more inference time)                          |
| + Chain-of-thought reasoning           | - Knowledge-based tasks                       |
| (breaking down multi-step problems)    | (hallucination)                                |
| + Complex decision-making tasks       | - Simple tasks (“overthinking”)               |
| + Better generalization to novel problems |                                                 |

### 03. A brief look at the DeepSeek training pipeline

DeepSeek 的训练流程概览

Before discussing four main approaches to building and improving reasoning models in the next section, I want to briefly outline the DeepSeek R1 pipeline, as described in the DeepSeek R1 technical report. This report serves as both an interesting case study and a blueprint for developing reasoning LLMs.

在接下来的章节中，我们将讨论构建和改进推理模型的四种主要方法。在此之前，我想先简单介绍一下 DeepSeek R1 的训练流程，详细内容可以参考 DeepSeek R1 的技术报告。这份报告可以看作是一个有趣的案例，也为我们开发推理大语言模型（Large Language Model，LLM）提供了一个参考蓝图。

Note that DeepSeek did not release a single R1 reasoning model but instead introduced three distinct variants: DeepSeek-R1-Zero, DeepSeek-R1, and DeepSeek-R1-Distill.

请注意，DeepSeek 并没有发布单独的 R1 推理模型（Reasoning Model），而是推出了三个不同的版本：DeepSeek-R1-Zero、DeepSeek-R1 和 DeepSeek-R1-Distill。

Based on the descriptions in the technical report, I have summarized the development process of these models in the diagram below.

根据技术报告中的描述，我将这些模型的开发流程总结在了下图。

Fig: Development process of DeepSeeks three different reasoning models that are discussed in the DeepSeek R1 technical report.

图：DeepSeek R1 技术报告中讨论的 DeepSeek 三种推理模型的开发流程。

Next, let's briefly go over the process shown in the diagram above. More details will be covered in the next section, where we discuss the four main approaches to building and improving reasoning models.

接下来，我们简单了解一下上图所示的流程。更多细节将在下一节中介绍，届时我们将讨论构建和改进推理模型的四大主要方法。

(1) DeepSeek-R1-Zero: This model is based on the 671B pre-trained DeepSeek-V3 base model released in December 2024. The research team trained it using reinforcement learning (RL) with two types of rewards. This approach is referred to as "cold start" training because it did not include a supervised fine-tuning (SFT) step, which is typically part of reinforcement learning with human feedback (RLHF).

DeepSeek-R1-Zero：这个模型以 DeepSeek-V3 基础模型为基础，该模型是拥有 6710 亿参数的预训练模型，于 2024 年 12 月发布。研究团队使用强化学习（RL），并结合两种奖励机制对它进行了训练。这种方法被称为「冷启动」训练，因为它省略了监督微调（SFT）这一步骤。通常，监督微调是带有人工反馈的强化学习（RLHF）流程中的一部分。

(2) DeepSeek-R1: This is DeepSeek's flagship reasoning model, built upon DeepSeek-R1-Zero. The team further refined it with additional SFT stages and further RL training, improving upon the "cold-started" R1-Zero model.

DeepSeek-R1：这是 DeepSeek 的旗舰推理模型，以 DeepSeek-R1-Zero 为基础构建。该团队通过额外的 SFT（Supervised Fine-Tuning）阶段和进一步的强化学习（Reinforcement Learning）训练对其进行了优化，从而改进了未经预训练的 R1-Zero 模型。

(3) DeepSeek-R1-Distill*: Using the SFT data generated in the previous steps, the DeepSeek team fine-tuned Qwen and Llama models to enhance their reasoning abilities. While not distillation in the traditional sense, this process involved training smaller models (Llama 8B and 70B, and Qwen 1.5B–30B) on outputs from the larger DeepSeek-R1 671B model.

DeepSeek-R1-Distill*：为了提升 Qwen 和 Llama 模型的推理能力，DeepSeek 团队利用之前步骤生成的 SFT 数据对其进行了微调。虽然这并非传统意义上的知识蒸馏（knowledge distillation），但其过程与知识蒸馏类似，即使用更大的 DeepSeek-R1 671B 模型的输出结果来训练较小的模型，包括 Llama 8B 和 70B，以及 Qwen 1.5B–30B。

### 04. The 4 main ways to build and improve reasoning models

构建与改进推理模型的四种主要方式

In this section, I will outline the key techniques currently used to enhance the reasoning capabilities of LLMs and to build specialized reasoning models such as DeepSeek-R1, OpenAI's o1 & o3, and others.

本节将介绍目前提升大语言模型（LLM/Large Language Model）推理能力，以及构建专用推理模型的关键技术。这些专用模型包括 DeepSeek-R1、OpenAI 的 o1 和 o3 等模型。

Note: The exact workings of o1 and o3 remain unknown outside of OpenAI. However, they are rumored to leverage a combination of both inference and training techniques.

注意：除了 OpenAI 内部人员之外，o1 和 o3 的具体工作原理仍然不为人所知。不过，据说它们结合了推理和训练两种技术。

1) Inference-time scaling

推理时规模调整提高

One way to improve an LLM's reasoning capabilities (or any capability in general) is inference-time scaling. This term can have multiple meanings, but in this context, it refers to increasing computational resources during inference to improve output quality.

大语言模型（LLM）的推理能力（或任何其他能力）的一种方法是在推理时进行规模调整。这个术语有多种含义，但在此处，它指的是在推理过程中增加计算资源，以提升输出结果的质量。

A rough analogy is how humans tend to generate better responses when given more time to think through complex problems. Similarly, we can apply techniques that encourage the LLM to "think" more while generating an answer. (Although, whether LLMs actually "think" is a different discussion.)

一个粗略的类比是，人类在有更多时间思考复杂问题时，通常能给出更好的回答。类似地，我们可以使用一些技巧，来鼓励大语言模型（LLM/Large Language Model）在生成答案时进行更深入的「分析」（虽然，大语言模型是否真的具有「思考」能力是另一个话题）。

One straightforward approach to inference-time scaling is clever prompt engineering. A classic example is chain-of-thought (CoT) prompting, where phrases like "think step by step" are included in the input prompt. This encourages the model to generate intermediate reasoning steps rather than jumping directly to the final answer, which can often (but not always) lead to more accurate results on more complex problems. (Note that it doesn't make sense to employ this strategy for simpler knowledge-based questions, like "What is the capital of France", which is again a good rule of thumb to find out whether a reasoning model makes sense on your given input query.)

一种直接的推理期扩展方法是巧妙的提示工程。一个经典案例就是思维链（CoT）提示，即在输入提示中加入「一步一步思考」这样的引导语。这能鼓励模型生成中间推理步骤，而非直接跳到最终答案，从而在更复杂的问题上获得更准确的结果（尽管并非总是如此）。注意，对于「法国的首都是什么」这类简单的知识型问题，采用 CoT 提示没有实际意义。这条经验法则可以帮助我们判断，推理模型是否适用于给定的输入查询。

Fig: An example of classic CoT prompting from the 2022 Large Language Models are Zero-Shot Reasoners paper (https://arxiv.org/abs/2205.11916).

一个来自 2022 年的论文《大语言模型是零样本推理器》（Large Language Models are Zero-Shot Reasoners，https://arxiv.org/abs/2205.11916）的经典 CoT（Chain-of-Thought，思维链）提示示例。

[[2205.11916] Large Language Models are Zero-Shot Reasoners](https://arxiv.org/abs/2205.11916)

已下载论文：2025020Large Language Models are Zero-Shot Reasoners

The aforementioned CoT approach can be seen as inference-time scaling because it makes inference more expensive through generating more output tokens.

上述 CoT 方法可以被视为一种推理时扩展策略，因为它通过生成更多的输出 Token（Token）增加了推理的计算成本。

Another approach to inference-time scaling is the use of voting and search strategies. One simple example is majority voting where we have the LLM generate multiple answers, and we select the correct answer by majority vote. Similarly, we can use beam search and other search algorithms to generate better responses.

另一种在推理阶段进行优化扩展的方法是采用投票和搜索策略。一个简单的例子是多数投票，即让大语言模型（LLM）生成多个答案，然后通过多数投票来选择最合适的答案。类似地，我们还可以使用集束搜索（beam search）和其他搜索算法来生成更优质的回复。

I highly recommend the Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters paper that I described in my previous Noteworthy AI Research Papers of 2024 (Part Two) article (https://magazine.sebastianraschka.com/p/ai-research-papers-2024-part-2) for more details on these different strategies.

我强烈推荐这篇论文，它阐述了优化大语言模型（LLM/Large Language Model）测试时的计算资源分配（Scaling LLM Test-Time Compute Optimally）可能比扩大模型参数（Scaling Model Parameters）更有效。我在之前的 2024 年值得注意的 AI 研究论文（第二部分）的文章（https://magazine.sebastianraschka.com/p/ai-research-papers-2024-part-2）中介绍过这篇论文，你可以通过这篇文章了解更多关于这些策略的细节。

Fig: Different search-based methods rely on a process-reward-based model to select the best answer. Annotated figure from the LLM Test-Time Compute paper, https://arxiv.org/abs/2408.03314
The DeepSeek R1 technical report states that its models do not use inference-time scaling. However, this technique is often implemented at the application layer on top of the LLM, so it is possible that DeepSeek applies it within their app.

不同的基于搜索的方法依赖于一种基于过程奖励的模型来选择最佳答案。图示来自大语言模型（LLM）测试时计算论文，并带有注释，论文链接：https://arxiv.org/abs/2408.03314
DeepSeek R1 的技术报告指出，他们的模型没有采用推理时缩放（inference-time scaling）技术。但是，这项技术通常是在大语言模型（LLM）之上的应用层实现的，因此，DeepSeek 有可能在他们的应用中使用了这项技术。

[[2408.03314] Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters](https://arxiv.org/abs/2408.03314)

2025021Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters

I suspect that OpenAI's o1 and o3 models use inference-time scaling, which would explain why they are relatively expensive compared to models like GPT-4o. In addition to inference-time scaling, o1 and o3 were likely trained using RL pipelines similar to those used for DeepSeek R1. More on reinforcement learning in the next two sections below.

我怀疑 OpenAI 的 o1 和 o3 模型使用了推理时缩放（inference-time scaling），这解释了为什么它们比 GPT-4o 等模型更昂贵。除了推理时缩放，o1 和 o3 很可能还使用了与 DeepSeek R1 类似的强化学习（RL）流程进行训练。关于强化学习（reinforcement learning）的更多内容，请参见下面两节。

2) Pure reinforcement learning (RL)

纯粹强化学习（RL)

One of my personal highlights from the DeepSeek R1 paper is their discovery that reasoning emerges as a behavior from pure reinforcement learning (RL). Let's explore what this means in more detail.

DeepSeek R1 论文中，我个人认为最精彩的发现之一是：他们发现推理能力可以作为一种行为，从纯粹强化学习（RL）中涌现。让我们更深入地了解这意味着什么。

As outlined earlier, DeepSeek developed three types of R1 models. The first, DeepSeek-R1-Zero, was built on top of the DeepSeek-V3 base model, a standard pre-trained LLM they released in December 2024. Unlike typical RL pipelines, where supervised fine-tuning (SFT) is applied before RL, DeepSeek-R1-Zero was trained exclusively with reinforcement learning without an initial SFT stage as highlighted in the diagram below.

正如前面提到的，DeepSeek 开发了三种 R1 模型。第一种是 DeepSeek-R1-Zero，它基于 DeepSeek-V3 基础模型构建，后者是 DeepSeek 在 2024 年 12 月发布的标准预训练大语言模型（LLM）。与常见的强化学习（RL）流程不同，后者通常会在强化学习（RL）之前进行监督式微调（SFT），而 DeepSeek-R1-Zero 仅通过强化学习（RL）训练，没有经过初始的监督式微调（SFT）阶段，如下图所示。

Fig: The development process of DeepSeek-R1-Zero model.

DeepSeek-R1-Zero 模型的发展过程。

Still, this RL process is similar to the commonly used RLHF approach, which is typically applied to preference-tune LLMs. (I covered RLHF in more detail in my article, LLM Training: RLHF and Its Alternatives.) However, as mentioned above, the key difference in DeepSeek-R1-Zero is that they skipped the supervised fine-tuning (SFT) stage for instruction tuning. This is why they refer to it as "pure" RL. (Although, RL in the context of LLMs differs significantly from traditional RL, which is a topic for another time.)

这种强化学习（RL）过程与常用的 RLHF 方法类似，后者通常用于对大语言模型（LLM）进行偏好调整。（我在《大语言模型训练：RLHF 及其替代方案》 这篇文章中更详细地介绍了 RLHF。） 然而，正如前面提到的，DeepSeek-R1-Zero 的主要区别在于，他们省略了用于指令调整的有监督微调（SFT）阶段。这就是为什么他们称之为「纯粹」的强化学习（RL）。（不过，大语言模型（LLM）中的强化学习（RL）与传统强化学习（RL）有着显著区别，这又是另一个话题了。）

For rewards, instead of using a reward model trained on human preferences, they employed two types of rewards: an accuracy reward and a format reward.

对于奖励，他们没有使用基于人类偏好的奖励模型，而是采用了两种类型的奖励：准确性奖励和格式奖励。

1 The accuracy reward uses the LeetCode compiler to verify coding answers and a deterministic system to evaluate mathematical responses.

准确性奖励通过 LeetCode 编译器验证编码答案，并通过确定性系统评估数学响应。

2 The format reward relies on an LLM judge to ensure responses follow the expected format, such as placing reasoning steps inside <think> tags.

格式奖励依赖于大语言模型（LLM）评估模型，以确保响应遵循预期的格式，例如用 <think> 标签标注推理步骤。
	
Surprisingly, this approach was enough for the LLM to develop basic reasoning skills. The researchers observed an "Aha!" moment, where the model began generating reasoning traces as part of its responses despite not being explicitly trained to do so, as shown in the figure below.

令人惊讶的是，这种方法足以让大语言模型（LLM）发展基本的推理技能。研究人员观察到一个「顿悟」（Aha!）时刻，即模型开始在响应中生成推理轨迹，尽管它并没有经过明确的训练来生成这些轨迹，如下图所示。

A figure from the DeepSeek R1 technical report (https://arxiv.org/abs/2501.12948) showing the emergence of the "Aha" moment.

图来自 DeepSeek R1 技术报告（https://arxiv.org/abs/2501.12948），展示了「Aha」时刻的出现。

While R1-Zero is not a top-performing reasoning model, it does demonstrate reasoning capabilities by generating intermediate "thinking" steps, as shown in the figure above. This confirms that it is possible to develop a reasoning model using pure RL, and the DeepSeek team was the first to demonstrate (or at least publish) this approach.

尽管 R1-Zero 并非顶尖的推理模型，但它确实展现出推理能力，这体现在它能生成中间「思考」步骤，如上图所示。这证实了使用纯强化学习（Reinforcement Learning，RL）开发推理模型是可行的，并且 DeepSeek 团队是第一个展示（或至少公开）这一方法的。

3) Supervised finetuning and reinforcement learning (SFT + RL)

监督式微调和强化学习（SFT + RL)

Next, let's look at the development of DeepSeek-R1, DeepSeek’s flagship reasoning model, which serves as a blueprint for building reasoning models. This model improves upon DeepSeek-R1-Zero by incorporating additional supervised fine-tuning (SFT) and reinforcement learning (RL) to improve its reasoning performance.

接下来，让我们看看 DeepSeek-R1 的开发，这是 DeepSeek 的旗舰推理模型，并作为构建推理模型的蓝图。该模型通过结合额外的监督式微调（SFT）和强化学习（RL）来改进 DeepSeek-R1-Zero，从而提升其推理能力。

Note that it is actually common to include an SFT stage before RL, as seen in the standard RLHF pipeline. OpenAI's o1 was likely developed using a similar approach.

请注意，在强化学习（RL）之前，通常会先进行一个有监督微调（SFT）阶段，这在标准的人类反馈强化学习（RLHF）流程中很常见。OpenAI 的 o1 很可能也是通过类似方法开发的。

Fig: The development process of DeepSeek-R1 model.

DeepSeek-R1 模型的开发过程。

As shown in the diagram above, the DeepSeek team used DeepSeek-R1-Zero to generate what they call "cold-start" SFT data. The term "cold start" refers to the fact that this data was produced by DeepSeek-R1-Zero, which itself had not been trained on any supervised fine-tuning (SFT) data.

正如上图所展示的，DeepSeek 团队使用 DeepSeek-R1-Zero 来生成研究团队称之为「冷启动」的 SFT 数据。「冷启动」指的是这些数据由 DeepSeek-R1-Zero 生成，而 DeepSeek-R1-Zero 自身并没有经过任何监督式微调（Supervised Fine-Tuning，SFT）数据的训练。

Using this cold-start SFT data, DeepSeek then trained the model via instruction fine-tuning, followed by another reinforcement learning (RL) stage. This RL stage retained the same accuracy and format rewards used in DeepSeek-R1-Zero’s RL process. However, they added a consistency reward to prevent language mixing, which occurs when the model switches between multiple languages within a response.

利用这些冷启动的 SFT（Supervised Fine-Tuning）数据，DeepSeek 接下来通过指令微调（instruction fine-tuning）来训练模型，并在此之后引入了另一个强化学习（RL）阶段。这个强化学习阶段沿用了 DeepSeek-R1-Zero 的强化学习过程中所使用的准确性和格式奖励。除此之外，他们还增加了一致性奖励，以避免语言混合现象，即模型在回复过程中出现多种语言切换的情况。

The RL stage was followed by another round of SFT data collection. In this phase, the most recent model checkpoint was used to generate 600K Chain-of-Thought (CoT) SFT examples, while an additional 200K knowledge-based SFT examples were created using the DeepSeek-V3 base model.

在强化学习（RL）阶段之后，我们进行了新一轮的 SFT 数据收集。在这一阶段，我们利用最新的模型检查点生成了 60 万个思维链（Chain-of-Thought，CoT）的 SFT 示例。此外，还使用 DeepSeek-V3 基础模型额外创建了 20 万个基于知识的 SFT 示例。

These 600K + 200K SFT samples were then used for another round of RL. In this stage, they again used rule-based methods for accuracy rewards for math and coding questions, while human preference labels used for other question types.

这些总计 80 万条 SFT 样本随后被用于另一轮强化学习（RL）训练。在这一阶段，对于数学和编程问题，他们仍然采用基于规则的方法来评估准确性并给予奖励；而对于其他类型的问题，则使用人工标注的偏好标签。

The final model, DeepSeek-R1 has a noticeable performance boost over DeepSeek-R1-Zero thanks to the additional SFT and RL stages, as shown in the table below.

最终模型 DeepSeek-R1 的性能相比 DeepSeek-R1-Zero 有了显著提升，这得益于额外的监督微调（SFT，Supervised Fine-Tuning）和强化学习（RL，Reinforcement Learning）阶段，具体数据见下表。

Fig: Benchmark comparison of OpenAI A1 and DeepSeek R1 models. Annotated figure from the DeepSeek-R1 technical report (https://arxiv.org/abs/2501.12948).

OpenAI A1 和 DeepSeek R1 模型的基准测试对比。图例来自 DeepSeek-R1 技术报告（https://arxiv.org/abs/2501.12948）。

4) Pure supervised finetuning (SFT) and distillation

纯监督式微调（SFT）和蒸馏

So far, we have covered three key approaches to building and improving reasoning models:

目前为止，我们已经介绍了构建和改进推理模型的三个关键方法：

1 Inference-time scaling, a technique that improves reasoning capabilities without training or otherwise modifying the underlying model.

推理时调整（Inference-time scaling）是一种无需训练或修改模型本身，就能提升推理能力的技术。

2 Pure reinforcement learning (RL) as in DeepSeek-R1-Zero, which showed that reasoning can emerge as a learned behavior without supervised fine-tuning.

正如 DeepSeek-R1-Zero 所示，纯强化学习（RL）表明推理能力可以通过学习获得，而无需任何监督微调。

3 Supervised fine-tuning (SFT) plus RL, which led to DeepSeek-R1, DeepSeek’s flagship reasoning model.

通过监督微调（Supervised fine-tuning，SFT）结合强化学习（Reinforcement Learning，RL）技术，DeepSeek 打造了其旗舰推理模型 DeepSeek-R1。

So, what’s left? Model "distillation."

那么，还剩下什么？模型蒸馏。

Surprisingly, DeepSeek also released smaller models trained via a process they call distillation. However, in the context of LLMs, distillation does not necessarily follow the classical knowledge distillation approach used in deep learning. Traditionally, in knowledge distillation (as briefly described in Chapter 6 of my Machine Learning Q and AI book), a smaller student model is trained on both the logits of a larger teacher model and a target dataset.

出人意料的是，DeepSeek 还发布了规模更小的模型，这些模型通过一种他们称之为蒸馏（distillation）的方法进行训练。然而，在大语言模型（LLM）领域，这种蒸馏方法并不一定遵循深度学习中常用的经典知识蒸馏方法。传统上，知识蒸馏（knowledge distillation）(正如我的《机器学习 Q 和 AI》一书的第 6 章简要介绍的那样）会使用一个较大的教师模型输出的 logits（未经归一化的预测值）以及目标数据集来训练一个更小的学生模型。

Instead, here distillation refers to instruction fine-tuning smaller LLMs, such as Llama 8B and 70B and Qwen 2.5 models (0.5B to 32B), on an SFT dataset generated by larger LLMs. Specifically, these larger LLMs are DeepSeek-V3 and an intermediate checkpoint of DeepSeek-R1. In fact, the SFT data used for this distillation process is the same dataset that was used to train DeepSeek-R1, as described in the previous section.

这里所说的蒸馏，指的是使用较大规模的大语言模型（LLM/Large Language Model）生成的 SFT 数据集，对较小规模的大语言模型进行指令微调，例如 Llama 8B 和 70B，以及 Qwen 2.5 系列模型（0.5B 到 32B）。具体而言，我们使用了 DeepSeek-V3 和 DeepSeek-R1 的一个中间版本作为「教师模型」，生成训练数据。实际上，用于蒸馏的 SFT 数据集，与上一节中用于训练 DeepSeek-R1 的数据集完全相同。

To clarify this process, I have highlighted the distillation portion in the diagram below.

为了更清楚地展示这一过程，我在下图中特别标出了蒸馏部分。

Fig: The development process of DeepSeek-R1-Distill models.

Why did they develop these distilled models? In my opinion, there are two key reasons:

他们开发这些蒸馏模型的原因是什么？在我看来，主要有两个原因：

1 Smaller models are more efficient. This means they are cheaper to run, but they also can run on lower-end hardware, which makes these especially interesting for many researchers and tinkerers like me.

较小的模型效率更高。这意味着运行成本更低，并且可以在配置较低的硬件上运行，这使得它们对许多研究人员和像我这样的爱好者来说，尤其具有吸引力。

2 A case study in pure SFT. These distilled models serve as an interesting benchmark, showing how far pure supervised fine-tuning (SFT) can take a model without reinforcement learning.

纯粹监督微调（SFT）的案例研究。这些精馏模型充当了一个有趣的基准，展示了在没有强化学习的情况下，纯粹的监督微调（SFT）能将模型优化到何种程度。

The table below compares the performance of these distilled models against other popular models, as well as DeepSeek-R1-Zero and DeepSeek-R1.

下表比较了这些蒸馏模型的性能与其他流行的模型，以及 DeepSeek-R1-Zero 和 DeepSeek-R1。

| Model                          | AIME 2024   |          | MATH-500 | GPQA Diamond | LiveCode Bench | CodeForces |
|--------------------------------|-------------|----------|----------|--------------|----------------|------------|
|                                | pass@1      | cons@64  | pass@1   | pass@1       | pass@1         | rating     |
| GPT-4o-0513                   | 9.3         | 13.4     | 74.6     | 49.9         | 32.9           | 759        |
| Claude-3.5-Sonnet-1022        | 16.0        | 26.7     | 78.3     | 65.0         | 38.9           | 717        |
| OpenAI-o1-mini                | 63.6        | 80.0     | 90.0     | 60.0         | 53.8           | 1820       |
| QwQ-32B-Preview               | 50.0        | 60.0     | 90.6     | 54.5         | 41.9           | 1316       |
| DeepSeek-R1-Distill-QwQen-1.5B | 28.9        | 52.7     | 83.9     | 33.8         | 16.9           | 954        |
| DeepSeek-R1-Distill-QwQen-7B  | 55.5        | 83.3     | 92.8     | 49.1         | 37.6           | 1189       |
| DeepSeek-R1-Distill-QwQen-14B | 69.7        | 80.0     | 93.9     | 59.1         | 53.1           | 1481       |
| DeepSeek-R1-Distill-QwQen-32B | 72.6        | 83.3     | 94.3     | 62.1         | 57.2           | 1691       |
| DeepSeek-R1-Distill-Llama-8B  | 50.4        | 80.0     | 89.1     | 49.0         | 39.6           | 1205       |
| DeepSeek-R1-Distill-Llama-70B | 70.0        | 86.7     | 94.5     | 65.2         | 57.5           | 1633       |
| DeepSeek-R1-Zero              | 71.0        |          | 95.9     | 73.3         | 50.0           | 1444       |
| DeepSeek-R1                   | 79.8        |          | 97.3     | 71.5         | 65.9           | 2029       |

Fig: Benchmark comparison of distilled versus non-distilled models. Annotated figure from the DeepSeek-R1 technical report (https://arxiv.org/abs/2501.12948).

蒸馏模型与非蒸馏模型的基准比较。图表来自 DeepSeek-R1 技术报告（https://arxiv.org/abs/2501.12948）。

As we can see, the distilled models are noticeably weaker than DeepSeek-R1, but they are surprisingly strong relative to DeepSeek-R1-Zero, despite being orders of magnitude smaller. It's also interesting to note how well these models perform compared to o1 mini (I suspect o1-mini itself might be a similarly distilled version of o1).

可以看出，蒸馏模型明显弱于 DeepSeek-R1，但令人惊讶的是，尽管体积小几个数量级，它们相对于 DeepSeek-R1-Zero 仍然表现出色。另外，这些模型与 o1 mini 相比表现如何也值得关注（我怀疑 o1-mini 本身可能是一个与 o1 类似的蒸馏版本）。

Before wrapping up this section with a conclusion, there’s one more interesting comparison worth mentioning. The DeepSeek team tested whether the emergent reasoning behavior seen in DeepSeek-R1-Zero could also appear in smaller models. To investigate this, they applied the same pure RL approach from DeepSeek-R1-Zero directly to Qwen-32B.

在总结本节之前，还有一个有趣的对比值得一提。DeepSeek 团队测试了 DeepSeek-R1-Zero 中展现出的涌现推理行为，是否也会在更小的模型中出现。为此，他们将与 DeepSeek-R1-Zero 相同的纯强化学习（RL）方法直接应用于 Qwen-32B。

The results of this experiment are summarized in the table below, where QwQ-32B-Preview serves as a reference reasoning model based on Qwen 2.5 32B developed by the Qwen team (I think the training details were never disclosed). This comparison provides some additional insights into whether pure RL alone can induce reasoning capabilities in models much smaller than DeepSeek-R1-Zero.

下表总结了本次实验的结果，其中 QwQ-32B-Preview 作为参考推理模型，它基于 Qwen 团队开发的 Qwen 2.5 32B（我认为训练细节从未公开）。这一比较提供了一些额外的见解，以了解仅凭强化学习（Reinforcement Learning，RL）是否能单独地在比 DeepSeek-R1-Zero 小得多的模型中诱导推理能力。

| Model                         | AIME 2024   |          | MATH-500 | GPQA Diamond | LiveCodeBench |
|-------------------------------|-------------|----------|----------|--------------|---------------|
|                               | pass@1      | cons@64  | pass@1   | pass@1       | pass@1        |
| QwQ-32B-Preview               | 50.0        | 60.0     | 90.6     | 54.5         | 41.9          |
| DeepSeek-R1-Zero-QwQen-32B    | 47.0        | 60.0     | 91.6     | 55.0         | 40.2          |
| DeepSeek-R1-Distill-QwQen-32B | 72.6        | 83.3     | 94.3     | 62.1         | 57.2          |
| DeepSeek-R1-Zero              | 71.0        |          | 95.9     | 73.3         | 50.0          |
| DeepSeek-R1                   | 79.8        |          | 97.3     | 71.5         | 65.9          |

Fig: Benchmark comparison distillation and RL on a smaller 32B model. Annotated figure from the DeepSeek-R1 technical report (https://arxiv.org/abs/2501.12948).

基准测试对比：在较小的 32B 模型上进行知识蒸馏和强化学习。下图是来自 DeepSeek-R1 技术报告（https://arxiv.org/abs/2501.12948）的带有注释的图。

Interestingly, the results suggest that distillation is far more effective than pure RL for smaller models. This aligns with the idea that RL alone may not be sufficient to induce strong reasoning abilities in models of this scale, whereas SFT on high-quality reasoning data can be a more effective strategy when working with small models.

有趣的是，测试结果表明，对于较小的模型，知识蒸馏方法比单纯的强化学习方法有效得多。这印证了一种观点，即对于这种规模的模型，单纯使用强化学习可能不足以激发其强大的推理能力；而当处理小模型时，在高质量推理数据上进行有监督微调（SFT，Supervised Fine-Tuning）可能是更有效的策略。

For completeness, it would have been useful to see additional comparisons in the table:

为了更全面地评估，如果在表格中增加一些额外的对比将会更有价值：

1 Qwen-32B trained with SFT + RL, similar to how DeepSeek-R1 was developed. This would help determine how much improvement can be made, compared to pure RL and pure SFT, when RL is combined with SFT.

使用 SFT（Supervised Fine-Tuning，监督微调）+ RL（Reinforcement Learning，强化学习）训练的 Qwen-32B 模型，其训练方式与 DeepSeek-R1 类似。相比于纯粹使用 RL 或 SFT 的方法，这将有助于评估当 RL 与 SFT 结合使用时，能够带来多大的性能提升。

2 DeepSeek-V3 trained with pure SFT, similar to how the distilled models were created. This would allow for a direct comparison to see how effective RL + SFT is over pure SFT.

DeepSeek-V3 使用纯监督微调（Supervised Fine-tuning，SFT）训练，类似于创建蒸馏模型的方式。这将允许直接比较，以了解强化学习（Reinforcement Learning，RL）+ SFT 相对于纯 SFT 的效果。

### 05. Conclusion

结论

In this section, we explored four different strategies for building and improving reasoning models:

在本节中，我们探讨了四种用于构建和改进推理模型（reasoning models）的不同策略：

1 Inference-time scaling requires no additional training but increases inference costs, making large-scale deployment more expensive as the number or users or query volume grows. Still, it remains a no-brainer for improving the performance of already strong models. I strongly suspect that o1 leverages inference-time scaling, which helps explain why it is more expensive on a per-token basis compared to DeepSeek-R1.

推理阶段的扩展（inference-time scaling）不需要额外的训练，但会增加推理成本，随着用户数量或查询量的增长，这使得大规模部署的成本更高。尽管如此，对于提升现有强大模型的性能而言，它仍然是一个明智之举。我强烈怀疑 o1 利用了推理阶段的扩展，这或许可以解释为什么相比 DeepSeek-R1，它的每个 Token 的成本更高。

2 Pure RL is interesting for research purposes because it provides insights into reasoning as an emergent behavior. However, in practical model development, RL + SFT is the preferred approach as it leads to stronger reasoning models. I strongly suspect that o1 was trained using RL + SFT as well. More precisely, I believe o1 starts from a weaker, smaller base model than DeepSeek-R1 but compensates with RL + SFT and inference-time scaling.

纯强化学习（RL）(Reinforcement Learning）因其能提供对推理这种涌现行为的深刻见解，所以在研究方面颇具价值。然而，在实际的模型开发中，强化学习 + 有监督微调（SFT）(Supervised Fine-Tuning）才是更受青睐的方法，因为它能够训练出更强大的推理模型。我强烈怀疑 o1 模型也是通过强化学习 + 有监督微调的方式进行训练的。更准确地说，我认为 o1 模型的基础模型可能比 DeepSeek-R1 更弱、更小，但它通过强化学习 + 有监督微调以及推理时模型缩放等手段弥补了这一不足。

3 As mentioned above, RL + SFT is the key approach for building high-performance reasoning models. DeepSeek-R1 is a nice blueprint showing how this can be done.

如上所述，强化学习（RL）+ 有监督微调（SFT）是构建高性能推理模型的关键方法。DeepSeek-R1 是一个很好的范例，展示了如何做到这一点。

4 Distillation is an attractive approach, especially for creating smaller, more efficient models. However, the limitation is that distillation does not drive innovation or produce the next generation of reasoning models. For instance, distillation always depends on an existing, stronger model to generate the supervised fine-tuning (SFT) data.

知识蒸馏是一种颇具吸引力的方法，尤其是在构建更小、更高效的模型时。然而，这种方法的局限性在于它无法驱动创新，也无法催生下一代推理模型。例如，知识蒸馏总是依赖于一个现有的、更强大的模型来生成用于有监督微调（Supervised Fine-Tuning，SFT）的数据。

One interesting aspect I expect to see next is to combine RL + SFT (approach 3) with inference-time scaling (approach 1). This is likely what OpenAI o1 is doing, except it's probably based on a weaker base model than DeepSeek-R1, which explains why DeepSeek-R1 performs so well while remaining relatively cheap at inference time.

我期待接下来看到一个有趣的趋势，那就是将强化学习（RL）+ 有监督微调（SFT）(方法 3）与推理时缩放（方法 1）相结合。很有可能 OpenAI 的 o1 也在尝试类似的方法。不过，它所使用的基础模型可能不如 DeepSeek-R1 强大，这也解释了为什么 DeepSeek-R1 能够在推理时保持相对较低的成本，同时表现得非常出色。

### 06. Thoughts about DeepSeek R1

关于 DeepSeek R1 的思考

In recent weeks, many people have asked for my thoughts on the DeepSeek-R1 models. In short, I think they are an awesome achievement. As a research engineer, I particularly appreciate the detailed technical report, which provides insights into their methodology that I can learn from.

近几周，很多人询问我对 DeepSeek-R1 模型的看法。概括而言，我认为 DeepSeek-R1 模型是一项卓越的成就。作为一名研究工程师，我尤其赞赏其详尽的技术报告，报告中阐述的方法论提供了深刻的见解，我从中获益匪浅。

One of the most fascinating takeaways is how reasoning emerged as a behavior from pure RL. And it's impressive that DeepSeek has open-sourced their models under a permissive open-source MIT license, which has even fewer restrictions than Meta's Llama models.

其中一个最吸引人的发现是，推理能力竟然能从纯粹的强化学习（RL）中自发涌现。更令人印象深刻的是，DeepSeek 公司以非常宽松的 MIT 开源许可证发布了他们的模型。相比之下，这个许可证的限制甚至比 Meta 公司的 Llama 模型还要少。

How does it compare to o1?

它与 o1 相比表现如何？

Is DeepSeek-R1 better than o1? I’d say it’s roughly in the same ballpark. However, what stands out is that DeepSeek-R1 is more efficient at inference time. This suggests that DeepSeek likely invested more heavily in the training process, while OpenAI may have relied more on inference-time scaling for o1.

DeepSeek-R1 比 o1 更好吗？我认为它们的能力不相上下。然而，值得注意的是，DeepSeek-R1 在推理（inference）阶段的效率更高。这表明，DeepSeek 可能在训练阶段投入了更多的资源，而 OpenAI 可能更多地依赖于推理时规模扩展来实现 o1。

That said, it's difficult to compare o1 and DeepSeek-R1 directly because OpenAI has not disclosed much about o1. For instance, we don’t know:

也就是说，很难直接比较 o1 和 DeepSeek-R1，因为 OpenAI 没有公开关于 o1 的详细信息。例如，我们不知道：

1 Is o1 also a Mixture of Experts (MoE)?

o1 也是一个混合专家模型（Mixture of Experts，MoE）吗？

2 How large is o1?

o1 有多大？

3 Could o1 just be a slightly refined version of GPT-4o with minimal RL + SFT and only extensive inference-time scaling?

o1 会不会只是 GPT-4o 的一个轻微优化版本，只进行了最少的强化学习（Reinforcement Learning，RL）+ 监督微调（Supervised Fine-Tuning，SFT），并且仅在推理时进行了大规模扩展？

Without knowing these details, a direct comparison remains an apples-to-oranges comparison.

在不了解这些细节的情况下，直接比较仍然是风马牛不相及。

The cost of training DeepSeek-R1

DeepSeek-R1 的训练成本

Another point of discussion has been the cost of developing DeepSeek-R1. Some have mentioned a ~$6 million training cost, but they likely conflated DeepSeek-V3 (the base model released in December last year) and DeepSeek-R1.

另一个讨论的焦点是 DeepSeek-R1 的开发成本。有人提到训练成本约为 600 万美元，但他们可能将 DeepSeek-V3（去年 12 月发布的初始模型）与 DeepSeek-R1 混淆了。

The $6 million estimate is based on an assumed $2 per GPU hour and the number of GPU hours required for the final training run of DeepSeek-V3, which was originally discussed back in December 2024.

600 万美元的估算，是基于以下两个假设：一是 GPU 的使用成本为每小时 2 美元；二是 DeepSeek-V3 的最终训练所需要的 GPU 小时数，这个数据最初在 2024 年 12 月被提出。

However, the DeepSeek team has never disclosed the exact GPU hours or development cost for R1, so any cost estimates remain pure speculation.

然而，DeepSeek 团队从未公开 R1 的确切 GPU 运行时间或开发成本，因此任何成本估算都仍然纯粹是推测。

Either way, ultimately, DeepSeek-R1 is a major milestone in open-weight reasoning models, and its efficiency at inference time makes it an interesting alternative to OpenAI’s o1.

无论如何，最终，DeepSeek-R1 是具有开放权重的推理模型中的一个重要里程碑，并且它在推理效率使其成为 OpenAI 的 o1（可能是指 OpenAI 的某个具体模型）的一个有趣的替代方案。

### 07. Developing reasoning models on a limited budget

Developing a DeepSeek-R1-level reasoning model likely requires hundreds of thousands to millions of dollars, even when starting with an open-weight base model like DeepSeek-V3. This can feel discouraging for researchers or engineers working with limited budgets.

在有限的预算下开发推理模型开发一个达到 DeepSeek-R1 水平的推理模型，即使以 DeepSeek-V3 这样具有开源权重的基础模型为起点，也可能需要花费数十万甚至数百万美元。这对于预算有限的研究人员或工程师而言，无疑是一个不小的挑战。

The good news: Distillation can go a long way

好消息是：模型蒸馏潜力巨大

Fortunately, model distillation offers a more cost-effective alternative. The DeepSeek team demonstrated this with their R1-distilled models, which achieve surprisingly strong reasoning performance despite being significantly smaller than DeepSeek-R1. However, even this approach isn’t entirely cheap. Their distillation process used 800K SFT samples, which requires substantial compute.

幸运的是，模型蒸馏（model distillation）提供了一种更具成本效益的替代方案。DeepSeek 团队的 R1 蒸馏模型证明了这一点，该模型虽然比 DeepSeek-R1 小得多，但仍然实现了出人意料的强大推理性能。不过，即使是这种方法也并非完全经济。他们的蒸馏过程使用了 80 万个 SFT（Supervised Fine-tuning）样本，这需要大量的算力资源。

Interestingly, just a few days before DeepSeek-R1 was released, I came across an article about Sky-T1, a fascinating project where a small team trained an open-weight 32B model using only 17K SFT samples. The total cost? Just $450, which is less than the registration fee for most AI conferences.

有趣的是，就在 DeepSeek-R1 发布前几天，我偶然读到一篇关于 Sky-T1 的文章。这是一个非常吸引人的项目，一个小型团队仅用 1.7 万个 SFT（Supervised Fine-Tuning，监督微调）样本，就训练出了一个 32B 参数的开源模型。而总成本仅为 450 美元，甚至低于大多数 AI 会议的注册费用。

[Sky-T1: Train your own O1 preview model within $450](https://novasky-ai.github.io/posts/sky-t1/)

This example highlights that while large-scale training remains expensive, smaller, targeted fine-tuning efforts can still yield impressive results at a fraction of the cost.

这个例子强调，虽然大规模训练的成本依然高昂，但规模较小、目标明确的微调（fine-tuning）工作，仍然能以较低的成本，取得令人瞩目的成果。

Figure from the "Sky-T1: Train your own O1 preview model within $450" article, https://novasky-ai.github.io/posts/sky-t1/

图来自文章「Sky-T1：在 450 美元内训练你自己的 O1 预览模型（O1 preview model）」，https://novasky-ai.github.io/posts/sky-t1/

According to their benchmarks, Sky-T1 performs roughly on par with o1, which is impressive given its low training cost.

根据他们的基准测试，Sky-T1 的性能表现与 o1 大致相当，考虑到它极低的训练成本，这着实令人印象深刻。

Pure RL on a budget: TinyZero

纯粹强化学习（RL），经济之选：TinyZero

While Sky-T1 focused on model distillation, I also came across some interesting work in the "pure RL" space. One notable example is TinyZero, a 3B parameter model that replicates the DeepSeek-R1-Zero approach (side note: it costs less than $30 to train).

在 Sky-T1 专注于模型蒸馏的同时，我也发现了一些纯粹强化学习（RL）领域中很有意思的研究。其中一个值得关注的例子是 TinyZero，一个拥有 30 亿参数的模型，它复现了 DeepSeek-R1-Zero 的方法（顺便一提，它的训练成本不到 30 美元）。

Surprisingly, even at just 3B parameters, TinyZero exhibits some emergent self-verification abilities, which supports the idea that reasoning can emerge through pure RL, even in small models.

令人惊讶的是，即使只有 30 亿参数，TinyZero 也表现出一些初步的自我验证能力，这支持了纯强化学习（Reinforcement Learning，RL）也能使模型涌现推理能力的想法，即使是在小型模型中。

[Jiayi-Pan/TinyZero: Clean, minimal, accessible reproduction of DeepSeek R1-Zero](https://github.com/Jiayi-Pan/TinyZero/)

The TinyZero repository mentions that a research report is still work in progress, and I’ll definitely be keeping an eye out for further details.

TinyZero 的代码仓库表明，一份研究报告仍在撰写中，我将持续关注后续的详细信息。

A figure from the TinyZero repository (https://github.com/Jiayi-Pan/TinyZero) showing that the model is capable of self-verification. (It would have been interesting to see the response of the base model in comparison.)

图 1：来自 TinyZero 代码仓库（https://github.com/Jiayi-Pan/TinyZero）的图片，展示了该模型具备自我验证的能力。(如果能对比基础模型的回应，将会更有意思。)

The two projects mentioned above demonstrate that interesting work on reasoning models is possible even with limited budgets. While both approaches replicate methods from DeepSeek-R1, one focusing on pure RL (TinyZero) and the other on pure SFT (Sky-T1), it would be fascinating to explore how these ideas can be extended further.

以上两个项目都表明，即使在预算有限的情况下，构建优秀的推理模型依然是可行的。它们都复现了 DeepSeek-R1 中的方法，一个项目 TinyZero 侧重于纯粹的强化学习（RL），另一个项目 Sky-T1 则专注于纯粹的监督微调（SFT）。进一步探索如何扩展这些思路，将会非常有趣。

Beyond Traditional SFT: Journey Learning

超越传统 SFT：旅程学习

One particularly interesting approach I came across last year is described in the paper O1 Replication Journey: A Strategic Progress Report – Part 1. Despite its title, the paper does not actually replicate o1. Instead, it introduces an different way to improve the distillation (pure SFT) process.

去年，我偶然发现了一种特别有趣的方法，它在论文 O1 Replication Journey：A Strategic Progress Report – Part 1 中有所描述。尽管论文的标题似乎是关于复制 o1，但实际上它并没有这样做。相反，它提出了一种改进知识蒸馏（distillation，一种纯粹的 SFT）过程的新途径。

[[2410.18982] O1 Replication Journey: A Strategic Progress Report -- Part 1](https://arxiv.org/abs/2410.18982)

The key idea in the paper is "journey learning" as an alternative to "shortcut learning."

这篇论文的核心思想是「旅程学习」，它旨在替代「捷径学习」。

1 Shortcut learning refers to the traditional approach in instruction fine-tuning, where models are trained using only correct solution paths.

「捷径学习」指的是 Instruction fine-tuning（指令微调）中的传统方法，这种方法只用正确的解题步骤来训练模型。

2 Journey learning, on the other hand, also includes incorrect solution paths, allowing the model to learn from mistakes.

另一方面，过程学习（Journey learning）也包含了错误的解决方案路径，使模型能够从错误中学习。

This approach is kind of related to the self-verification abilities observed in TinyZero’s pure RL training, but it focuses on improving the model entirely through SFT. By exposing the model to incorrect reasoning paths and their corrections, journey learning may also reinforce self-correction abilities, potentially making reasoning models more reliable this way.

这种方法与 TinyZero 的纯 RL 训练中观察到的自我验证能力有相似之处，但它侧重于完全通过 SFT 来改进模型。通过使模型接触不正确的推理路径并进行纠正，过程学习（Journey learning）还有可能加强自我纠正能力，从而提高推理模型的可靠性。

Journey learning, as opposed to traditional shortcut learning, includes wrong solutions paths in the SFT data. Annotated figure from the O1 Replication Journey: A Strategic Progress Report – Part 1 (https://arxiv.org/abs/2410.18982)

旅程学习（Journey learning），与传统的捷径学习（shortcut learning）不同，在监督微调数据（SFT data）中包含了错误的解决方案路径。如图 O1 Replication Journey：A Strategic Progress Report – Part 1（https://arxiv.org/abs/2410.18982）所示。

This could be an exciting direction for future work, particularly for low-budget reasoning model development, where RL-based approaches may be computationally impractical.

这可能是一个令人兴奋的未来研究方向，特别是对于低预算的推理模型开发，其中基于强化学习（RL）的方法在计算资源上可能难以实现。

Anyways, a lot of interesting work is currently happening on the reasoning model front, and I'm sure we will see a lot more exciting work in the upcoming months!

总之，目前在推理模型方面涌现出大量有趣的研究，并且可以预见，未来几个月将涌现更多令人期待的成果！

## 宝玉的翻译

宝玉的分享

Published on 2025-02-07

以 DeepSeek R1 为例学习「推理型大语言模型 [译]

原文：Understanding Reasoning LLMs Methods and Strategies for Building and Refining Reasoning Models

导读：这是一篇相当棒的科普文章，作者以 DeepSeek R1 为核心案例，围绕「推理型大语言模型」（Reasoning LLMs）这一主题，深入探讨了其定义、应用场景、优劣势及主要实现方法。文章背景是 2024 年以来大型语言模型在专业化方向上的快速发展，尤其在解题、数学证明、代码生成等需要多步推理的复杂任务上，如何用 RL（强化学习）和 SFT（监督微调）等方法打造「会思考」的模型。文中还详细解读了 DeepSeek R1 模型训练流程，包括纯 RL、SFT+RL、以及利用蒸馏将大模型能力迁移到小模型。作者还介绍了一些低成本项目，如 Sky-T1、TinyZero 等，为有限资源下的研究者提供了新思路。通过这一系列方法对比，读者可以全面了解构建推理模型的关键技术、挑战与未来趋势。

理解推理型大语言模型（Reasoning LLMs）

构建与完善推理模型的方法与策略

本文将介绍构建「推理模型」（即如何增强大语言模型在推理方面的能力）所采用的四种主要方法。我希望这些内容能为你在这个快速发展的研究领域提供有价值的见解，并帮助你更好地理解和应对当下的热潮。

在 2024 年，大语言模型（LLM）领域出现了越来越多的专业化趋势。除了预训练和微调之外，我们还见证了诸多专用应用场景的兴起，从 RAG（Retrieval-Augmented Generation）到代码助手等。我预计到了 2025 年，这一趋势将更加明显，更多领域和应用场景会在基础模型的基础上进行深度优化（专业化）。

阶段 1-3 是常见的 LLM 开发流程，阶段 4 则是面向特定用例的专业化。

开发推理模型就是这样一种专业化，即对 LLM 进行精调，使其在那些需要中间推理步骤的复杂任务（如解谜、高级数学或编程挑战）上表现出色。不过，这种专门化并不会取代其他 LLM 应用场景。因为将 LLM 打造成推理模型的同时，也会带来一些缺点，稍后会讨论。

下面是本文将要涉及的内容，供你先行了解：

说明「推理模型」这一术语的含义

分析推理模型的优点与不足

概述 DeepSeek R1 的方法论

介绍构建与改进推理模型的四种主要思路

分享对 DeepSeek V3 与 R1 发布后，LLM 生态现状的看法

给出在预算有限的情况下开发推理模型的建议

希望这些内容能对你有所帮助。随着今年 AI 的高速发展，让我们拭目以待！

「推理模型」是什么？

在 AI（或更广泛的机器学习）领域，许多概念通常定义得不够明确，甚至有争议；「推理模型」也不例外。一个学术论文里可能对它做出正式定义，随后又会被下一个论文重新定义，反复迭代。

在本文中，我将「推理」定义为回答需要多步推理（中间思考步骤）的复杂问题的过程。例如，「法国的首都是哪里？」这类事实问答不涉及推理；但如果是「列车以每小时 60 英里的速度行驶，行驶 3 小时后会走多远？」就需要一些简单的推理，比如把速度、时间和距离关联起来，然后得出答案。

常规的 LLM 可能只给出简短的答案（左侧所示），而推理模型通常会包含中间推理步骤（右侧所示），展现一部分「思考」过程。（注意，很多未在推理任务上专门训练的 LLM 也可以在回答中呈现出一些推理思路。）

如今的大多数 LLM 都具备一定的基本推理能力，能够回答「列车时速 60 英里运行 3 小时走多远？」这类问题。所以，当我们现在谈及「推理模型」时，更常指那些在更复杂的推理任务（如解谜、猜谜或数学证明）上表现突出的 LLM。

另外，大部分被称为「推理模型」的 LLM，回答中通常会包含某种形式的「思考过程」或「思路」。至于它们是否在「真正思考」，这是另一个层面的问题。

在推理模型的回答中，中间推理步骤一般以两种方式呈现：

直接在最终回答里显示，比如上图示例那样，让用户看到全部推理过程。

有些推理 LLM（例如 OpenAI 的 o1），会在内部多次迭代，但并不向用户展示这些中间步骤。

「推理」在两个层面上被使用：1）模型在内部处理输入并生成多步推理；2）最终回答中是否显式展现出部分推理过程。

什么时候需要推理模型？

既然我们对推理模型有了初步定义，让我们先思考一个更关键的问题：我们在什么场景下才真的需要推理模型？在深入探讨技术实现前，先想想：什么时候「推理模型」才是合适的选择？

什么情况下应该使用推理模型？

推理模型专门用于应对那些需要复杂中间推理步骤的问题，比如解谜、高级数学题、具有挑战性的编程任务等。然而，对于诸如摘要、翻译、或者依靠知识检索的问答等更简单的任务，就未必需要推理模型了。

事实上，如果把推理模型用在所有场景，往往既低效又昂贵。因为推理模型通常更耗资源、输出也更冗长，有时还可能因为「过度思考」而出现错误。最简单的原则依然是：用对工具、用对类型的 LLM。

以下图总结了推理模型的一些主要优劣势。

推理模型的核心优势与局限。

简要概览 DeepSeek 的训练流程

在介绍构建与改进推理模型的四种方法之前，我想先简单介绍一下 DeepSeek R1 技术报告中描述的训练流程。一方面，这能当作一个有趣的案例，另一方面也能为如何打造推理型 LLM 提供一个蓝本。

需要注意的是，DeepSeek 并未只发布一个 R1 推理模型，而是一口气推出了三个不同版本：DeepSeek-R1-Zero、DeepSeek-R1 和 DeepSeek-R1-Distill。

他们在技术报告中对这三个模型做了较详细的介绍。下面这张图是我根据报告内容整理出来的流程概览。

DeepSeek 在 R1 技术报告中所讨论的三个推理模型的开发流程示意图。

接下来简要介绍上图中的流程，下一节我们再结合这四种主要构建思路做更深入讨论。

DeepSeek-R1-Zero

该模型基于 DeepSeek 在 2024 年 12 月发布的 671B 规模预训练基础模型 DeepSeek-V3。团队对其进行强化学习（RL）训练，并使用了两类奖励作为回报信号。由于没有进行监督微调（SFT），也就是常见「RLHF」流程中的 SFT 步骤被跳过，所以他们把这称为「冷启动」的方式（Cold Start）。

DeepSeek-R1

这是 DeepSeek 的主力推理模型，也是在 DeepSeek-R1-Zero 的基础上进一步引入额外的 SFT 阶段与更多轮的 RL 训练而成，性能优于「冷启动」的 R1-Zero。

DeepSeek-R1-Distill

他们还用前述训练过程中的 SFT 数据来微调了 Qwen 和 Llama 等较小模型，以提升这些模型的推理能力。虽然他们把这个过程称为「蒸馏」，但并不是传统意义上的知识蒸馏，更像是用大模型的输出数据去监督微调（SFT）小模型（包括 Llama 8B 和 70B，以及 Qwen 1.5B–30B）。

构建与改进推理模型的四种主要方式

本节将介绍当前用来提升 LLM 推理能力、并构建专门推理模型（如 DeepSeek-R1、OpenAI o1 & o3 等）的核心技术路线。

注：OpenAI 的 o1 和 o3 模型内部细节并未公开，但据传在推理和训练阶段都可能有类似的思路。

1）推理阶段的扩展（Inference-time scaling）

提升 LLM 推理能力的一种方法是推理阶段的扩展，即在推理时投入更多计算资源，以换取更高质量的输出结果。

形象类比：人类在面对复杂问题时，如果能有更多时间思考，往往会给出更好的答案。对 LLM 来说，我们可以在推理阶段用一些技术，让它「想得更多」，并且产出更高质量的回答。（至于模型是否真的在「思考」，这是另一个话题。）

推理阶段扩展的一种常见做法就是改进提示工程（prompt engineering）。其中的经典例子便是链式思考（Chain-of-Thought，CoT）提示。简单说，就是在输入提示中加入像「分步思考」或「一步一步想」等提示，引导模型产生中间推理步骤，而不是直接给出最终答案。这样往往（但并不总是）能在更复杂的问题上得到更准确的结果。（但对于诸如「法国首都是哪里」之类的简单问题，就没必要这样做 —— 这也再次印证了「用对模型、用对场景」这一原则。）

这是来自 2022 年论文 Large Language Models are Zero-Shot Reasoners 的经典 CoT 提示示例。

上面提到的 CoT，也可以视为一种推理时间扩展方式，因为需要生成更多的输出 Token，自然推理开销也更大。

另一个思路是用投票或搜索策略。最简单的例子是「多数投票」，即让 LLM 生成多个答案，最后以票数最多的答案作为结果。也可以用束搜索（beam search）等搜索算法来生成更优回答。

如果想更详细地了解这类方法，强烈推荐参阅我在另一篇文章中介绍过的 Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters 论文，该文对推理阶段的各种策略有深入分析。

一些基于搜索的推理方法通过对「过程 + 奖励」进行评估，以选择最佳答案。此图来自 Scaling LLM Test-Time Compute 论文，附有标注。

在 DeepSeek R1 技术报告中提到，他们的模型并未使用推理阶段扩展。不过，在实际应用时，很多 App 层面会加上类似功能，所以不排除 DeepSeek 在他们的应用中用了这个策略。

我个人猜测 OpenAI 的 o1 和 o3 模型中很可能使用了推理阶段扩展，这也能够部分解释为什么它们相较于 GPT-4o 来说价格更昂贵。除了推理阶段扩展，o1 和 o3 也可能在训练阶段采用了类似 DeepSeek R1 的强化学习管线，详情见下文。

2）纯强化学习（Pure Reinforcement Learning，RL）

DeepSeek R1 论文里最令我印象深刻的一点，是他们发现推理能力可以通过 ** 纯强化学习（RL）** 而涌现。具体是怎么做到的呢？

前面提到，DeepSeek 发布了三个 R1 系列模型，其中第一个 DeepSeek-R1-Zero 是基于基础预训练模型 DeepSeek-V3（671B），并通过纯强化学习训练而来。与常规的 RL 管线相比，他们跳过了最初的 SFT（通常是 RLHF 标准流程的一部分），因此称之为「纯」RL。也就是说没有事先的监督微调，就直接进行 RL。

DeepSeek-R1-Zero 的开发流程示意图。

不过，它跟传统的 RLHF 仍有共同之处，比如会用到奖励模型（reward）来指导训练。只不过，这里 DeepSeek-R1-Zero 没用人类偏好数据来训练 reward model，而是采用了两种奖励：

准确性奖励：利用 LeetCode 编译器来判定编程答案是否正确，以及用一套确定性系统来判定数学问题回答是否准确。

格式奖励：用一个 LLM 评估器来判断回答的格式是否符合要求，比如推理步骤是否出现在 <think> 标签中等。

令人惊喜的是，这种方式足以让模型学到一些基本的推理能力。研究团队提到在训练中出现了一个「顿悟时刻」（「Aha!」），模型开始在回答里自动生成推理线索，哪怕从来没有专门教它这样做。下图就是论文中展示的例子。

来自 DeepSeek R1 技术报告的插图，展示了模型突然学会显式生成推理过程的「顿悟时刻」。

虽然 R1-Zero 远称不上最强的推理模型，但它至少能在回答中展示一些中间思路，说明纯 RL 也能赋予模型基本的推理能力 ——DeepSeek 团队是率先把这一发现发表出来的先驱。

3）监督微调 + 强化学习（SFT + RL）

接下来看看 DeepSeek-R1，也就是 DeepSeek 的旗舰推理模型。它在 DeepSeek-R1-Zero 的基础上，通过额外的监督微调（SFT）与多轮 RL，取得了更高的推理水平。

需要指出的是，在 RL 阶段之前先做一轮 SFT，其实是很常见的做法，RLHF 中的标准流程也是如此。推测 OpenAI 的 o1 也很可能采用了类似的做法。

DeepSeek-R1 的开发流程示意图。

如上图所示，DeepSeek 团队先用 R1-Zero 生成了他们称作「冷启动」的 SFT 数据（即来自一个没有经过 SFT 的模型）。基于这批数据，他们进行了指令微调（Instruction Tuning），然后又进行了下一步 RL。此时 RL 使用的奖励类型仍是之前的准确性奖励和格式奖励，只不过多加了一个「语言一致性」奖励，防止模型在回答中中途切换语言。

完成这一步后，又进行了一轮 SFT 数据收集：

用最新的模型检查点，生成了 60 万条带有思维链（Chain-of-Thought，CoT）的 SFT 数据；

另外还用 DeepSeek-V3 基础模型生成了 20 万条知识型 SFT 数据。

接下来，这 80 万条（60 万 + 20 万）数据被再次用于 RL。在这一阶段，数学或编程问题依旧用基于规则的方法来衡量准确度，而对其他问题则采用了人类偏好打分。

最终得到的 DeepSeek-R1，比没经历过额外 SFT+RL 的 R1-Zero 拥有明显更高的推理性能。如下表所示（选自技术报告）。

DeepSeek-R1 技术报告（链接）中，OpenAI A1 与 DeepSeek R1 的基准测试对比。

4）纯监督微调（SFT）与「蒸馏」

前面我们已经讨论了三种思路：

推理阶段扩展（Inference-time scaling）：不需要额外训练模型就能提升推理性能，但会增加推理成本，面对大量用户或高并发时会很贵。不过对于性能需求较高的场景，仍然是「立竿见影」的做法。

纯强化学习（Pure RL）：在理论研究上很有趣，能看出推理能力有「涌现」特性。但在实际应用中，想要获得效果更好的模型，往往是「RL + SFT」结合起来才更理想。

SFT + RL：搭配使用能造就最强推理模型。DeepSeek-R1 可以视为这一思路的蓝本。

那么还剩下什么？答案就是模型「蒸馏」。

DeepSeek 也发布了若干更小的模型，并称之为「Distill（蒸馏）版」。不过，需要注意的是，他们所谓的「蒸馏」并不完全等同于传统深度学习里的知识蒸馏（knowledge distillation）。后者通常是让一个小模型去学习大模型输出的 logits，并结合原始目标数据来训练。

而在这里，「蒸馏」更像是拿大模型生成的指令数据（SFT 数据）来直接微调小模型，比如 Llama 8B、70B 或 Qwen 系列（0.5B~32B 等）。具体而言，DeepSeek-R1-Distill 所用到的训练数据，正是此前 DeepSeek-R1 与 DeepSeek-V3 产生的那批 SFT 数据。

为了更好理解这个流程，可以看下图中标示的「Distill」部分：

DeepSeek-R1-Distill 各模型的开发流程。

** 为什么要做这些蒸馏模型？** 我认为有两个主要原因：

更小的模型更高效，推理成本更低，也更容易部署在普通硬件上，对于研究者或爱好者而言很有吸引力。

这些模型也相当于一种「只用 SFT 能走多远」的实验对照，可以帮助研究者了解不借助 RL 时，SFT 到什么程度能赋予模型推理能力。

下表比较了这些经过蒸馏的小模型和市面上常见模型的性能，以及它们与 R1-Zero、R1 之间的差距。

DeepSeek-R1 技术报告（链接）中的基准对比，包含蒸馏模型与非蒸馏模型。

结果显示：和 DeepSeek-R1 相比，这些蒸馏模型确实要弱一些，但它们对比 R1-Zero 却表现不错，而且在规模上要小得多。在与 o1 mini 的对比中也很有意思（我猜 o1 mini 本身也许也是类似的蒸馏模型）。

此外，DeepSeek 团队还测试了若干关于小模型「纯 RL 能否诱发推理涌现」的实验 —— 即让 Qwen-32B 也照搬 R1-Zero 的纯 RL 思路来训练。他们把这个模型跟一个参考推理模型 QwQ-32B-Preview（由 Qwen 团队开发，训练细节不公开）做了对比，结果如下表：

DeepSeek-R1 技术报告（链接）中小模型蒸馏与纯 RL 的实验对比。

从结果看，对于较小的模型，纯 RL 并不如「蒸馏」管用。这说明单靠 RL 去训练数十亿参数级的模型，想获得强大的推理能力并不容易；而如果能拿到高质量的 SFT 数据，小模型也能通过纯 SFT 训练获得不错的效果。

若想更全面地对比，我个人倒还想看看：

直接在 Qwen-32B 上做 SFT + RL（类似 DeepSeek-R1 ），会不会更好？相较纯 RL、纯 SFT 提升有多大？

在 DeepSeek-V3 上只做纯 SFT，而不结合 RL，最终结果如何？这样能更直接地看出 RL+SFT 比纯 SFT 的增益。

小结

本节讨论了构建与改进推理模型的四种主要技术：

推理阶段扩展（Inference-time scaling）：不用改模型，但推理成本上升。如果用户量和请求量很大，总体费用会很高。尽管如此，它仍是增强已有强大模型的简单高效方法。我很怀疑 o1 中就有用到这种策略，这也是它比 DeepSeek-R1 贵的一个原因。

纯 RL：研究上有趣，可揭示推理是如何「涌现」的。但在实际开发中，如果要得到强推理能力，通常还是会在 RL 前后配合 SFT。o1 很大概率也是「RL + SFT」做出来的。我推测 o1 的起点可能是一个比 DeepSeek-R1 更弱（或更小）的基础模型，但通过大量 RL+SFT 以及推理阶段扩展来弥补。

RL + SFT：打造性能最强推理模型的关键方法。DeepSeek-R1 的训练思路可作范例。

蒸馏：即用已训练的大模型产生的 SFT 数据来微调小模型。这样能得到更小、更便宜的推理模型。但要注意，蒸馏本身并不会推动最前沿的能力突破 —— 因为它依赖于一个已经训练好、且更强的大模型来提供数据。

如果将上面第 3 点（RL + SFT）和第 1 点（推理阶段扩展）相结合，大概率会出现一个更强的方案。很多人猜测这正是 OpenAI 在 o1 上的做法，但它也可能仅基于一个较小的底模，所以在推理阶段要花更多算力，因而价格较高。

关于 DeepSeek R1 的一些看法

最近，不少人问我对 DeepSeek-R1 系列模型的看法。简单总结就是：它们堪称一次令人印象深刻的成就。作为研究工程师，我尤其欣赏他们发布的详实技术报告，从中能学到很多实操经验。

其中一个最让我感兴趣的点，就是「纯 RL 也能涌现出一定的推理能力」。另外，DeepSeek 也将这些模型在 MIT 许可下开源，相比 Meta 的 Llama 许可证更宽松，这点也十分难得。

与 o1 的比较

DeepSeek-R1 和 o1 谁更强？我个人感觉两者表现大体在同一层次。但 R1 在推理阶段更高效，说明 DeepSeek 在训练阶段投入了更多功夫，而 o1 可能更多依赖推理时间扩展，因此推理成本会更高。

不过，OpenAI 并未披露 o1 的更多信息，比如：

o1 是否是一个 Mixture of Experts（MoE）架构？

o1 的参数规模到底多大？

o1 可能是 GPT-4o 小修小改后再加上少量 RL+SFT，然后在推理阶段使用大规模算力？

因此，如果没有更多细节，o1 和 DeepSeek-R1 的对比仍然是「苹果和橙子」的比较。

DeepSeek-R1 训练成本

也有人提到它大约花了 600 万美元来训练，但其实很多人把这个数字混淆了：这是当初推算 DeepSeek-V3 训练成本时的估计。而 DeepSeek-R1 并未对外透露任何训练成本或具体 GPU 小时数，这部分也只能是猜测。

不管怎么说，DeepSeek-R1 确实是当前开源可用的推理模型中的里程碑，并且因为推理时效率较高，为它在与 o1 的竞争中增添了不少亮点。

在有限预算下开发推理模型的思考

像 DeepSeek-R1 这样大型推理模型，哪怕只是在开源基础上二次训练，依旧可能花费数十万美元到数百万美元的预算。对于资金不充裕的团队和研究者来说，这似乎让人望而却步。

好消息在于：蒸馏往往可以实现高性价比

正如前面所见，DeepSeek 通过蒸馏方式得到的 R1-Distill 小模型，尽管规模远小于 R1，本身性能也并不差。当然，这种方法也并非「零成本」，毕竟他们也用到了 80 万条 SFT 数据来做微调，对计算资源仍有一定要求。

但实际上，最近也有一些小规模、低成本的有趣项目。比如，就在 DeepSeek-R1 发布前几天，我偶然看到一个 Sky-T1 的案例：他们用仅仅 1.7 万条 SFT 数据，就训练了一个开源 32B 模型，总花费只有 450 美元 —— 这比参加一次 AI 学术会议的注册费还低。

更惊人的是，他们的基准测试显示 Sky-T1 的表现大致可以和 o1 相当。考虑到成本如此之低，这结果相当鼓舞人心。

来自「Sky-T1：Train your own O1 preview model within $450」这篇文章中的配图。

低成本「纯 RL」的尝试：TinyZero

如果说 Sky-T1 是在「纯 SFT」方向上的探索，那么还有一些项目则在纯 RL 上做实验。比如 TinyZero—— 一个 3B 参数大小的模型，用不到 30 美元的计算成本就复制了 DeepSeek-R1-Zero 的思路。

令人好奇的是，这个模型虽然只有 3B 参数，却也在某种程度上表现出了类似「自我验证」的推理能力，这进一步印证了通过纯 RL 也能在小模型里观察到一些推理涌现征兆。

TinyZero 的仓库目前说他们还在整理研究报告，我也会持续关注。

来自 TinyZero 仓库的图片，模型展示了某种「自我验证」能力。（如果能看到基准模型的对比效果会更有意思。）

这两者（Sky-T1、TinyZero）说明：即使没有大公司的预算，也能在推理模型上做出不错的尝试。一个是纯 SFT 思路，一个是纯 RL，都算是对 DeepSeek-R1 思路的复刻或简化。但未来如何把这两种方法结合起来，或者做得更进一步，还很值得探索。

超越传统 SFT：Journey Learning

再提一个我去年看到的有趣思路：论文 O1 Replication Journey：A Strategic Progress Report – Part 1 中介绍了一种名为「journey learning」的新方式，尝试在纯 SFT 框架里「学习模型改错」。

Shortcut Learning：传统 SFT 中只给模型正确的解决步骤，引导它走捷径；

Journey Learning：不仅给正确解法，也包括错误思路和纠正过程，让模型见识更多的完整「解题之旅」。

这在某种程度上与 TinyZero 那种能自我验证的「RL」训练思路有相通之处，但它完全依赖 SFT 数据来实现，不需要 RL。在这种「journey learning」模式中，模型能接触到「错误示例 + 纠正过程」，并学到更多纠正和自我检验的能力，或许能提高推理可靠性。

「Journey learning」不同于传统 SFT 的「shortcut learning」，它会在训练样本中同时包含正确与错误的推理过程。图片来源：O1 Replication Journey：A Strategic Progress Report – Part 1，带有标注。

对资金有限的人来说，RL 也许并不经济，这种「journey learning」或许是另一个有潜力的方向。让模型在学习过程中反复看到并纠正错误，有可能为推理能力提供类似 RL 的强化效果。

总之，推理模型的方向上还有很多有趣的研究正在发生。相信在不久的将来，我们会看到更多让人眼前一亮的新方法和成果！