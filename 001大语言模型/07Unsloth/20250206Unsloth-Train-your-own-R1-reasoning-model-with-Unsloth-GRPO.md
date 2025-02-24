## 20250206Unsloth-Train-your-own-R1-reasoning-model-with-Unsloth-GRPO

[Train your own R1 reasoning model locally (GRPO)](https://unsloth.ai/blog/r1-reasoning)

[Blog](https://unsloth.ai/blog)

Feb 6, 2025

By Daniel & Michael

Today, we're excited to introduce reasoning in [Unsloth](https://github.com/unslothai/unsloth)! DeepSeek’s R1 research revealed an “aha moment” where R1-Zero autonomously learned to allocate more thinking time without human feedback by using Group Relative Policy Optimization (GRPO). 

今天，我们很高兴介绍 [Unsloth](https://github.com/unslothai/unsloth) 中的推理功能！DeepSeek 的 R1 研究揭示了一个重要的发现：R1-Zero 通过使用群体相对策略优化（GRPO，Group Relative Policy Optimization），在没有人为干预的情况下，自主地学会了分配更多的时间用于思考。

We've enhanced the entire GRPO process, making it use 80% less VRAM than Hugging Face + FA2. This allows you to reproduce R1-Zero's "aha moment" on just 7GB of VRAM using Qwen2.5 (1.5B). 

我们对整个 GRPO 流程进行了优化，使其 VRAM（显存）使用量相比 Hugging Face + FA2 减少了 80%。这意味着，你现在只需 7GB 显存，并使用 Qwen2.5（1.5B）模型，就能重现 R1-Zero 的「灵光乍现」时刻。

Try our free GRPO notebook: [Llama 3.1 (8B) on Colab](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-GRPO.ipynb)
For [our Guide](https://docs.unsloth.ai/basics/reasoning-grpo-and-rl)and GRPO notebooks featuring other models like Phi-4, visit our [docs](https://docs.unsloth.ai/basics/reasoning-grpo)

不妨试试我们免费的 GRPO notebook：[Llama 3.1（8B）on Colab](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-GRPO.ipynb)
想要了解更多信息，例如 [我们的指南](https://docs.unsloth.ai/basics/reasoning-grpo-and-rl)以及包含 Phi-4 等其他模型的 GRPO notebook，请访问我们的[文档](https://docs.unsloth.ai/basics/reasoning-grpo)

[Llama3.1\_(8B)-GRPO.ipynb - Colab](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-GRPO.ipynb)

[Reasoning - GRPO & RL | Unsloth Documentation](https://docs.unsloth.ai/basics/reasoning-grpo-and-rl)

P.S. thanks for the love on our R1 Dynamic [1.58-bit](https://unsloth.ai/blog/deepseekr1-dynamic)GGUF last week & don't forget to ⭐Star us: [github.com/unslothai/unsloth](https://github.com/unslothai/unsloth)

P.S. 感谢各位上周对 R1 Dynamic [1.58-bit](https://unsloth.ai/blog/deepseekr1-dynamic)GGUF 的支持，请不要忘记 ⭐Star 我们的项目：[github.com/unslothai/unsloth](https://github.com/unslothai/unsloth)

### Main Details 

主要细节：

1 With 15GB VRAM, Unsloth allows you to transform any model up to 15B parameters like Llama 3.1 (8B), Phi-4 (14B), Mistral (7B) or Qwen2.5 (7B) into a reasoning model

仅需 15GB 显存（VRAM），Unsloth 就能将任何高达 150 亿参数的模型，例如 Llama 3.1（8B）、Phi-4（14B）、Mistral（7B）或 Qwen2.5（7B），转化为强大的推理模型。

2 Minimum requirement: Just  7GB VRAM is enough to train your own reasoning model locally.

最低配置：只需 7GB 显存（VRAM），即可在本地训练您专属的推理模型。

3 The incredible team at Tiny-Zero demonstrated that you could achieve your own "aha" moment with Qwen2.5 (1.5B) - but it required 2xA100 GPUs (160GB VRAM). Now, with Unsloth, you can achieve the same "aha" moment using just a single 7GB VRAM GPU

Tiny-Zero 团队的研究表明，使用 Qwen2.5（1.5B）可以实现模型能力的跃升。过去，这需要 2 块 A100 GPU（160GB 显存（VRAM)）。现在，借助 Unsloth，仅用一块 7GB 显存（VRAM）的 GPU 就能实现同样的效果。

4 Previously, GRPO was only supported for full fine-tuning, but we've made it work with QLoRA and LoRA

过去，GRPO 仅支持完整模型的微调，现在我们已将其与 QLoRA 和 LoRA 技术相适配。

5 Please note, this isn’t fine-tuning DeepSeek’s R1 distilled models or using distilled data from R1 for tuning which Unsloth already supported. This is converting a standard model into a full-fledged reasoning model using GRPO.

请注意，这与微调 DeepSeek 的 R1 蒸馏模型或使用 R1 蒸馏数据进行训练不同，Unsloth 已经支持这些功能。这里的重点是使用 GRPO 将普通模型转化为具有完整推理能力的模型。

6 Use cases for GRPO include: If you want to make a customized model with rewards (say for law, medicine etc.), then GRPO can help.If you have input and output data (like questions and answers), but do not have the chain of thought or reasoning process, GRPO can magically create the reasoning process for you! + much more

GRPO 的应用场景包括：如果您希望创建具备奖励机制的定制模型（例如，应用于法律、医学等领域），GRPO 将大有帮助。如果您拥有输入和输出数据（比如问题和答案），但缺乏中间的推理过程，GRPO 能够神奇地补全推理链！更多应用等你探索。

---

[X 上的 Jiayi Pan：“We reproduced DeepSeek R1-Zero in the CountDown game, and it just works Through RL, the 3B base LM develops self-verification and search abilities all on its own You can experience the Ahah moment yourself for &lt; $30 Code: https://t.co/B2IsN1PrXV Here's what we learned 🧵 https://t.co/43BVYMmS8X” / X](https://x.com/jiayi_pirate/status/1882839370505621655)


We reproduced DeepSeek R1-Zero in the CountDown game, and it just works 

Through RL, the 3B base LM develops self-verification and search abilities all on its own 

You can experience the Ahah moment yourself for < $30 

Code:

[Jiayi-Pan/TinyZero: Clean, minimal, accessible reproduction of DeepSeek R1-Zero](https://github.com/Jiayi-Pan/TinyZero)

Here's what we learned 🧵

### GRPO + The "aha" moment 

GRPO +「啊哈」时刻 

DeepSeek’s researchers observed an "aha moment" when training R1-Zero with pure reinforcement learning (RL). The model learned to extend its thinking time by reevaluating its initial approach, without any human guidance or predefined instructions. 

DeepSeek 研究人员在使用纯强化学习（RL）训练 R1-Zero 时，观察到了一个「啊哈」时刻。R1-Zero 模型无需任何人工指导或预设指令，就学会了通过重新评估初始方案来延长思考时间。

In a test example, even though we only trained Phi-4 with 100 steps using GRPO, the results are already clear. The model without GRPO does not have the thinking token, whilst the one trained with GRPO does and also has the correct answer. 

在一个测试例子中，即使我们只使用 GRPO 训练了 Phi-4 模型 100 步，结果已经非常明显。未使用 GRPO 的模型没有用于思考的 Token，而使用 GRPO 训练的模型既有思考的 Token，而且答案也是正确的。

This magic could be recreated through GRPO, a RL algorithm that optimizes responses efficiently without requiring a value function, unlike Proximal Policy Optimization (PPO) which relies on a value function. In our notebooks, we train a model with GRPO, aiming for it to develop its own self-verification and search abilities autonomously - creating a mini "aha moment". 

这种能力可以通过 GRPO 这种强化学习（RL）算法重现。与依赖价值函数的近端策略优化（Proximal Policy Optimization，PPO）不同，GRPO 无需价值函数，就能高效地优化响应。在我们的 Notebook 中，我们使用 GRPO 训练一个模型，目标是让它自主发展自我验证和搜索能力，从而创造一个微型的「啊哈时刻」。

How it works: 

工作原理如下：

1 The model generates groups of responses.

模型生成若干组响应。

2 Each response is scored based on correctness or another metric created by some set reward function rather than an LLM reward model.

每一个响应都基于正确性，或者其他由奖励函数设定的指标进行评分，这里不使用大语言模型（LLM）奖励模型。

3 The average score of the group is computed.

计算每组响应的平均分。

4 Each response's score is compared to the group average.

将每个响应的得分与该组的平均分进行比较。

5 The model is reinforced to favor higher-scoring responses.

模型会学习并倾向于选择得分更高的响应。

As an example, assume we want a model to solve: 
What is 1+1? >> Chain of thought/working out >> The answer is 2. 
What is 2+2? >> Chain of thought/working out >> The answer is 4. 

例如，假设我们希望一个模型解决以下问题：
1+1 是多少？>> 思维链 / 计算步骤 >> 答案是 2。
2+2 是多少？>> 思维链 / 计算步骤 >> 答案是 4。

Originally, one had to collect large swathes of data to fill the working out / chain of thought process. But GRPO (the algorithm DeepSeek uses) or other RL algorithms can steer the model to automatically exhibit reasoning capabilities and create the reasoning trace. Instead, we need to create good reward functions or verifiers. For example, if it gets the correct answer, give it a score of 1. If some words are mis-spelt, minus 0.1. And so on! We can provide many many functions to reward the process. 

最初，人们必须收集大量数据来完善模型的推理过程，也就是思维链（chain of thought）。但是 GRPO（DeepSeek 使用的算法）或其他强化学习（Reinforcement Learning，RL）算法可以引导模型自动展现推理能力，并生成推理过程的轨迹。现在，我们更需要创建良好的奖励函数或验证器。例如，如果模型给出了正确的答案，就奖励 1 分；如果某些单词拼写错误，则扣 0.1 分。我们可以设计多种多样的函数来奖励模型的推理过程。

### GRPO in Unsloth

Unsloth 中的 GRPO

If you're using GRPO with Unsloth locally, please "pip install diffusers" as well as it is a dependency. 

如果在本地使用 Unsloth 运行 GRPO，请先执行「pip install diffusers」命令，因为它是必要的依赖。

Wait for at least 300 steps for the reward to actually increase and please use the latest version of vLLM. Keep in mind that our example on Colab was just trained in an hour so the results are subpar. In order to get good results, you will need to train for at least 12 hours (this is how GRPO works), but keep in mind this isn't compulsory as you can stop at anytime. 

请至少等待 300 步，以便奖励值能够真正开始提升。同时，请使用最新版本的 vLLM。需要注意的是，我们在 Colab 上提供的示例仅仅训练了一个小时，因此实验结果可能不够理想。为了获得更好的实验结果，您需要至少训练 12 个小时（这是 GRPO 的典型训练时长）。当然，这并非强制要求，您可以随时根据实际情况停止训练。

It's [advised](https://x.com/jiayi_pirate/status/1882839487417561307/photo/1)to apply GRPO to a model at least 1.5B in parameters to correctly generate thinking tokens as smaller models may not. If you’re using a base model, ensure you have a chat template. Training loss tracking for GRPO is now built directly into Unsloth, eliminating the need for external tools like wandb etc. 

建议将 GRPO（Gradient Ratio Policy Optimization）应用于参数量至少达到 15 亿的模型，以便能够正确生成「思维 Token」—— 即模型在推理过程中用于思考和决策的内部表征 [advised](https://x.com/jiayi_pirate/status/1882839487417561307/photo/1)。参数量较小的模型可能无法有效生成这些 Token。如果您使用的是基础模型，请确保配备了「聊天模板」，这是一种预定义的对话结构，能够引导模型生成更连贯、更符合语境的回复。现在，GRPO 的训练损失跟踪功能已直接集成到 Unsloth 中，无需使用像 wandb 这样的外部工具（wandb 是一个常用的机器学习实验跟踪平台）。Unsloth 集成训练损失跟踪功能，使得用户可以更方便地监控和调试训练过程。

In addition to adding GRPO support, we subsequently have support for Online DPO, PPO and RLOO as well! More details can be seen in [Keith’s post](https://www.linkedin.com/feed/update/urn:li:activity:7290108099607097344/)and [blog](https://substack.com/home/post/p-154490380)that includes the Github fork on how he got Online DPO working. The initial draft of GRPO changes on Google Colab can be seen in [Joey’s tweet](https://x.com/shxf0072/status/1886085377146180091)as well! Both of their contributions allowed us to also make support for the other generation based RL methods. See below for a graph comparison of Unsloth's Online DPO VRAM consumption vs standard Hugging Face + FA2. 

除了支持 GRPO 之外，Unsloth 还增加了对在线 DPO（Direct Preference Optimization）、PPO（Proximal Policy Optimization）和 RLOO（Reinforcement Learning from Online Observations）的支持！更多详细信息，请参考 [Keith's post](https://www.linkedin.com/feed/update/urn:li:activity:7290108099607097344/) 和 [blog](https://substack.com/home/post/p-154490380)，其中包含了关于他是如何实现 Online DPO 的 Github 分支。您还可以在 [Joey's tweet](https://x.com/shxf0072/status/1886085377146180091) 中找到 Google Colab 上 GRPO 更改的初始草案！他们的贡献使得我们能够支持其他基于生成的强化学习（RL）方法（即通过生成内容来优化策略的 RL 方法）。请参阅下图，了解 Unsloth 的在线 DPO 显存（VRAM）消耗与标准 Hugging Face + FA2 的比较。

### Unsloth x vLLM # 

Unsloth x vLLM

#### 20x more throughput, 50% VRAM savings:

吞吐量提高 20 倍，显存（VRAM）节省 50%:

You can now use [vLLM](https://github.com/vllm-project/vllm/i) directly in your finetuning stack, which allows for much more throughput and allows you to finetune and do inference on the model at the same time! On 1x A100 40GB, expect **4000 tokens / s**or so with Unsloth’s dynamic 4bit quant of Llama 3.2 3B Instruct. On a 16GB Tesla T4 (free Colab GPU), you can get 300 tokens / s. 

现在，您可以直接在微调堆栈（即用于模型微调的工具和库的集合）中使用 [vLLM](https://github.com/vllm-project/vllm/i)，从而显著提高吞吐量，并允许您同时对模型进行微调和推理！在一块 A100 40GB 显卡上，使用 Unsloth 的 Llama 3.2 3B Instruct 模型的动态 4bit 量化，预计可以达到约 **4000 个 Token/s** 的处理速度。在 16GB Tesla T4（免费 Colab GPU）上，您可以获得 300 个 Token/s 的处理速度。

[vllm-project/vllm: A high-throughput and memory-efficient inference and serving engine for LLMs](https://github.com/vllm-project/vllm)

We also magically **removed double memory usage**when loading vLLM and Unsloth together, allowing for savings of 5GB or so for Llama 3.1 8B and 3GB for Llama 3.2 3B (thanks to inspiration from [Boris](https://github.com/borisshapa)). Unsloth could originally finetune Llama 3.3 70B Instruct in 1x 48GB GPU with Llama 3.3 70B weights taking 40GB of VRAM. If we do not remove double memory usage, then we’ll need >= 80GB of VRAM when loading Unsloth and vLLM together. 

我们还巧妙地**解决了同时加载 vLLM 和 Unsloth 时内存占用翻倍的问题**。这一改进为 Llama 3.1 8B 模型节省了约 5GB 显存，为 Llama 3.2 3B 模型节省了 3GB 显存（灵感来自 [Boris](https://github.com/borisshapa)）。最初，Unsloth 能够在单张 48GB 显存的 GPU 上微调 Llama 3.3 70B Instruct 模型，其中 Llama 3.3 70B 的模型权重会占用 40GB 显存（VRAM）。如果没有解决内存占用翻倍的问题，同时加载 Unsloth 和 vLLM 时，则至少需要 80GB 显存（VRAM）。

But with Unsloth, you can still finetune and get the benefits of fast inference in one package in under 48GB of VRAM! To use fast inference, first install vllm, and instantiate Unsloth with fast_inference: 

但是有了 Unsloth，你仍然可以在一个包中微调并获得快速推理的好处，并且只需要低于 48GB 的显存（VRAM)！要使用快速推理，首先安装 vllm，并使用 fast_inference 实例化 Unsloth：

pip install unsloth vllm
from unsloth import FastLanguageModel
model, tokenizer = FastLanguageModel.from_pretrained(
 model_name = "unsloth/Llama-3.2-3B-Instruct",
 fast_inference = True,
)
model.fast_generate(["Hello!"])`

#### vLLM Findings in Unsloth

Unsloth 中使用 vLLM 的发现

1 vLLM can now load Unsloth Dynamic 4-bit quants. Just like our 1.58bit Dynamic R1 GGUF, we showed that dynamically quantizing certain layers to 4-bit and some to 16-bit can dramatically improve accuracy whilst keeping the model small.

vLLM 现在可以加载 Unsloth Dynamic 4-bit quants（动态 4-bit 量化）。就像我们的 1.58bit Dynamic R1 GGUF（超量化技术）一样，我们发现将某些层动态量化到 4-bit，而将另一些层量化到 16-bit，可以显著提高准确性，同时保持模型体积较小。

2 We auto select multiple parameters to account for RAM, VRAM efficiency and maximum throughput (like # of chunked prefill tokens, # max sequences etc). We enable -O3 in vLLM by default and enable prefix caching. We found Flashinfer on old GPUs to be actually 10% slower. FP8 KV cache makes things 10% slower, but doubles throughput potential.

我们自动选择多个参数来兼顾 RAM、VRAM 效率和最大吞吐量，例如分块预填充 Token（Token）的数量、最大序列数等。我们默认在 vLLM 中启用 -O3 优化并启用前缀缓存。我们发现，在旧 GPU 上使用 Flashinfer 实际上会降低 10% 的速度。FP8 KV 缓存会使速度降低 10%，但能使吞吐量潜力翻倍。

3 We allow LoRA loading in vLLM via parsing a state dict instead of loading from disk - this can make your GRPO training runs 1.5x faster. An active area of research is to somehow directly edit the LoRA adapters in vLLM (I’m not sure how to yet). This can boost speeds a lot, since we’re doing unnecessary GPU data movement now.

我们允许在 vLLM 中通过解析 state dict（模型权重状态字典）而不是从磁盘加载来加载 LoRA（Low-Rank Adaptation）—— 这可以使你的 GRPO（Group Recursive Partitioning Optimization）训练运行速度提高 1.5 倍。目前一个活跃的研究领域是如何直接在 vLLM 中编辑 LoRA 适配器（LoRA adapters）(我还不确定具体方法）。如果能实现这一点，可以大大提高速度，因为现在我们正在进行不必要的 GPU 数据移动，从而导致效率降低。

4 vLLM will have random VRAM spikes weirdly, especially during batched generation. We added a batched generate function to reduce memory spikes.

vLLM 尤其是在批量生成期间，会奇怪地出现随机 VRAM 峰值。我们添加了一个批量生成函数（batched generate function）来减少内存峰值。

### 参考

[X 上的 Jiayi Pan：“Quick ablations on CountDown: Base model quality is key: We run Qwen-2.5-Base 0.5B, 1.5B, 3B to 7B. 0.5B guess a solution and stop. From 1.5B, the model start learning to search, to self-verify and to revise its solutions, enabling them to achieve much higher scores. https://t.co/BNhx9e4Sv4” / X](https://x.com/jiayi_pirate/status/1882839487417561307)

Jiayi Pan
@jiayi_pirate

1月25日

We reproduced DeepSeek R1-Zero in the CountDown game, and it just works 

Through RL, the 3B base LM develops self-verification and search abilities all on its own 

You can experience the Ahah moment yourself for < $30 

Code: http://github.com/Jiayi-Pan/TinyZero

Here's what we learned 🧵

Jiayi Pan
@jiayi_pirate

1月25日

The recipe: 

We follow DeepSeek R1-Zero alg -- Given a base LM, prompts and ground-truth reward, we run RL. 

We apply it to CountDown: a game where players combine numbers with basic arithmetic to reach a target number.

Jiayi Pan
@jiayi_pirate

1月25日

The results: It just works! 

Model start from dummy outputs but gradually develop tactics such as revision and search. 

In the following sample, the model propose a solution, self-verify, and iteratively revise it until it works. 

Full experiment log: https://wandb.ai/jiayipan/TinyZero

Jiayi Pan
@jiayi_pirate

Quick ablations on CountDown: 

Base model quality is key: 

We run Qwen-2.5-Base 0.5B, 1.5B, 3B to 7B. 0.5B guess a solution and stop. From 1.5B, the model start learning to search, to self-verify and to revise its solutions, enabling them to achieve much higher scores.

上午1:14 · 2025年1月25日

Jiayi Pan
@jiayi_pirate

1月25日

Either base or instruct model works 

- Instruct model learns faster, but converges to about same performance as base 
- Instruct model's output are more structured and readable

So extra instruction tuning isn't necessary, which supports R1-Zero's design decision

Jiayi Pan
@jiayi_pirate

1月25日

The specific RL alg doesn't matter much

We tried PPO, GRPO and PRIME. Long cot all emerge and they seem all work well. We haven't got the time to tune the hyper-parameters, so don't want to make quantitative conclusions about which alg works better.
Jiayi Pan
@jiayi_pirate

1月25日

Model's reasoning behavior is very task dependent: 

- For countdown, the model learns to do search and self-verificatoin 
- For number multiplicatoin, the model instead learns to break down the problem using distirbution rule and solve it step by step.
Jiayi Pan
@jiayi_pirate

1月25日

Everything's open at http://github.com/Jiayi-Pan/TinyZero  

And it costs < $30 to train the model! We hope this project helps to demystify the emerging RL scaling research and make it more accessible!

来自 github.com
Jiayi Pan
@jiayi_pirate

1月25日
One caveat, of course, is that it's validated only in the Countdown task but not the general reasoning domain. We are now bounded by compute, and please reach out if you wanna help!

Jiayi Pan
@jiayi_pirate

1月25日

A wild ride with 

@JunjieZhang12
 
@xingyaow_
 
@lifan__yuan