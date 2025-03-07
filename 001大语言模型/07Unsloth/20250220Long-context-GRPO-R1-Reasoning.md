## 20250220Long-context-GRPO-R1-Reasoning

[Long-context GRPO (R1 Reasoning)](https://unsloth.ai/blog/grpo)

Feb 20, 2025

By Daniel & Michael

You can now train your own reasoning model with just **5GB VRAM**for Qwen2.5 (1.5B) - down from 7GB in our previous GRPO release 2 weeks ago! 

好消息！现在，只需 **5GB 显存**，你就能用 Qwen2.5（1.5B）训练自己的推理模型了！相比于两周前我们发布的 GRPO 版本，所需显存从 7GB 大幅降低！

Currently, achieving longer context lengths is one of GRPO's biggest challenges. Our newly derived Unsloth Efficient GRPO algorithm enables **10x longer context**lengths while using **90% less VRAM**vs. all other GRPO LoRA/QLoRA implementations, even those utilizing Flash Attention 2 (FA2). 

目前，如何实现更长的上下文长度是 GRPO 的一大难题。我们全新推出的 Unsloth Efficient GRPO 算法，能将上下文长度提升 **10 倍**，同时相比其他所有 GRPO LoRA/QLoRA 实现， 甚至包括那些使用了 Flash Attention 2（FA2）的实现，显存占用还能降低 **90%**！

With a GRPO setup using TRL + FA2, Llama 3.1 (8B) trai ning at 20K context length demands 510.8GB of VRAM. However, Unsloth’s 90% VRAM reduction brings the requirement down to just 54.3GB in the same setup. 

在使用 TRL + FA2 的 GRPO 设置下，训练上下文长度为 20K 的 Llama 3.1（8B）模型需要 510.8GB 的显存（VRAM）。然而，Unsloth 带来的 90% 显存占用减少，使得在相同设置下仅需 54.3GB 显存。

Try our free GRPO notebook with 10x longer context: [Llama 3.1 (8B) on Colab](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-GRPO.ipynb)
We'd highly recommend reading [our Guide](https://docs.unsloth.ai/basics/reasoning-grpo-and-rl)for everything on GRPO + reward functions/verifiers. 
View our GRPO notebooks featuring other models like Phi-4 [here](https://docs.unsloth.ai/). 

体验我们免费的 GRPO notebook 吧！它具有 10 倍于以往的上下文长度：[Llama 3.1（8B）on Colab](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-GRPO.ipynb)
我们强烈推荐您阅读 [我们的指南](https://docs.unsloth.ai/basics/reasoning-grpo-and-rl)，它详细介绍了 GRPO 及其奖励函数 / 验证器。
想了解更多？请点击 [这里](https://docs.unsloth.ai/)，查看包含 Phi-4 等其他模型的 GRPO notebooks。

P.S. If you enjoyed our work, don't forget to ⭐Star us: [github.com/unslothai/unsloth](https://github.com/unslothai/unsloth)

P.S. 如果您喜欢我们的工作，请不要忘记 ⭐Star 我们：[github.com/unslothai/unsloth](https://github.com/unslothai/unsloth)

### 90% less VRAM for long context 

处理长文本时，显存占用减少 90%

When you’re using Unsloth to do GRPO, we smartly reduce VRAM usage by over 90% when compared to standard implementations with Flash Attention 2 by using multiple tricks! On 20K context lengths for example with 8 generations per prompt, Unsloth uses only **54.3GB of VRAM for Llama 3.1 8B**, whilst standard implementations take **510.8GB (90% less for Unsloth)**. 

当您使用 Unsloth 进行 GRPO（Grouped Relative Position Output）时，与使用 Flash Attention 2 的标准实现相比，我们通过多种技巧，能够智能地将显存使用量减少 90% 以上！举例来说，对于上下文长度为 20K，每个提示生成 8 个结果的情况，Unsloth 仅需 **54.3GB 显存即可运行 Llama 3.1 8B 模型**，而标准实现则需要 **510.8GB（Unsloth 减少 90%)**。

1 Our new memory efficient linear algorithm for GRPO slashes memory usage by 8x or more. This shaves 68.5GB of memory, whilst being actually faster through the help of torch.compile for num_generations = 8 and 20K context length.

我们用于 GRPO（Grouped Relative Position Output）的新型内存高效线性算法，可以将内存使用量减少 8 倍甚至更多。在 `num_generations = 8`（生成数量为 8）和 20K 上下文长度的情况下，这节省了 68.5GB 的内存，并且在 `torch.compile` 的帮助下，速度实际上更快。

2 We leverage our smart Unsloth gradient checkpointing algorithm which we released a while ago. It smartly offloads intermediate activations to system RAM asynchronously whilst being only 1% slower. This shaves a whopping 372GB VRAM since we need num_generations = 8. We can reduce this memory usage even further through intermediate gradient accumulation.

我们利用之前发布的 Unsloth 高效梯度检查点（Gradient Checkpointing）算法。该算法能够巧妙地将中间激活（intermediate activations）异步卸载到系统内存中，速度仅降低 1%。由于 `num_generations = 8`（生成数量为 8），因此节省了高达 372GB 的显存。我们可以通过中间梯度累积（intermediate gradient accumulation）进一步减少内存使用。

3 Unsloth also uses the same GPU / CUDA memory space as the underlying inference engine (vLLM), unlike implementations in other packages. This shaves 16GB of VRAM.

与其他软件包中的实现不同，Unsloth 还与底层推理引擎（vLLM）共享 GPU / CUDA 内存空间。这样可以节省 16GB 的显存。

| Metric                               | 🦥 Unsloth           | TRL + FA2            |
| :----------------------------------- | :------------------ | :------------------- |
| Training Memory Cost (GB)            | 42GB                | 414GB                |
| GRPO Memory Cost (GB)                | 9.8GB               | 78.3GB               |
| Inference Cost (GB)                | 0GB                 | 16GB                 |
| Inference KV Cache for 20K context (GB) | 2.5GB               | 2.5GB                |
| Total Memory Usage                     | 54.3GB (90% less) | 510.8GB              |

In typical standard GRPO implementations, you need to create 2 logits of size (8, 20K) to calculate the GRPO loss. This takes 2 * 2 bytes * 8 (num generations) * 20K (context length) * 128256 (vocabulary size) = 78.3GB in VRAM. 

在典型的标准 GRPO 实现中，需要创建 2 个大小为（8，20K）的 logits（logits）来计算 GRPO 损失。这需要 2 * 2 字节（bytes）* 8（生成数量）* 20K（上下文长度）* 128256（词汇表大小）= 78.3GB 的显存（VRAM）。

Unsloth shaves 8x memory usage for long context GRPO, so we need only an extra 9.8GB in extra VRAM for 20K context lengths! 

Unsloth 将长上下文 GRPO 的内存占用降低了 8 倍，因此对于 20K 的上下文长度，我们只需要额外 9.8GB 的显存！

We also need to from the KV Cache in 16bit. Llama 3.1 8B has 32 layers, and both K and V are 1024 in size. So memory usage for 20K context length = 2 * 2 bytes * 32 layers * 20K context length * 1024 = 2.5GB per batch. We would set the batch size for vLLM to 8, but we shall leave it at 1 for our calculations to save VRAM. Otherwise you will need 20GB for the KV cache. 

我们还需要使用 16bit 的 KV 缓存（KV Cache）。Llama 3.1 8B 具有 32 层，其 K 和 V 的大小均为 1024。因此，对于 20K 上下文长度，内存使用量 = 2 * 2 字节 / 个 * 32 层 * 20K 上下文长度 * 1024 = 每个批次 2.5GB。虽然我们会将 vLLM 的批处理大小设置为 8，但为了节省显存，这里我们将其保留为 1 进行计算。否则，您将需要 20GB 用于 KV 缓存。

### Unsloth Efficient GRPO algorithm 

Unsloth 高效 GRPO 算法

We got inspired from Horace [He’s linear cross entropy](https://gist.github.com/Chillee/22cd93e11b887db1f596ab754d60a899)implementation, and managed to make it work for GRPO! We actually found a few surprising points: 

Unsloth 高效 GRPO 算法的灵感来自 Horace 的线性交叉熵（linear cross entropy）[实现](https://gist.github.com/Chillee/22cd93e11b887db1f596ab754d60a899)，并设法使其适用于 GRPO！我们实际上发现了一些令人惊讶的点：

1 The reference GRPO implementation uses the reverse KL divergence, not the forward KL divergence.

参考 GRPO 实现使用反向 KL 散度（KL divergence），而不是正向 KL 散度。

2 Naively implementing linear cross entropy on float16 mixed precision (and also float8) with automatic mixed precision scaling mechanisms will break if not handled properly.

如果处理不当，在具有自动混合精度缩放机制（automatic mixed precision scaling mechanisms）的 float16 混合精度（mixed precision)（以及 float8）上直接实现线性交叉熵将会失效。

3 We found other quirks in terms of the implementation of the GRPO loss - primarily in terms of the formulation of the reverse KL divergence.

我们在 GRPO 损失的实现方面发现了其他问题，主要是在反向 KL 散度的公式方面。

### Maths of GRPO & Issues Found 

GRPO 的数学原理及相关问题

GRPO was first introduced in [DeepSeek’s Math paper](https://arxiv.org/abs/2402.03300)back in February 2024 to April 2024 DeepSeek then leveraged the GRPO algorithm in creating DeepSeek R1, as mentioned in their [paper](https://arxiv.org/abs/2501.12948). 

GRPO 算法最早在 DeepSeek 发表于 2024 年 2 月至 4 月的 [数学论文](https://arxiv.org/abs/2402.03300)中被提出。之后，DeepSeek 在构建 DeepSeek R1 时采用了 GRPO 算法，相关细节可以参考他们的 [论文](https://arxiv.org/abs/2501.12948)。

[[2501.12948] DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](https://arxiv.org/abs/2501.12948)

We leverage Hugging Face’s TRL GRPO implementation [here](https://github.com/huggingface/trl/blob/main/trl/trainer/grpo_trainer.py). We see that the TRL implementation performs: 

我们使用了 Hugging Face 的 TRL 库中 GRPO 的实现，相关代码可以在 [这里](https://github.com/huggingface/trl/blob/main/trl/trainer/grpo_trainer.py)找到。TRL 的实现过程如下：

L = \frac{1}{n} \sum \beta D_{KL} (q \parallel p) + A

where we utilize the **reverse KL divergence**(not the forward KL divergence). Beta is a scaling factor set to 0.04, and A is the advantages obtained after considering all reward functions.Q is the new trained model, and P is the original reference model. 

在这个公式中，我们使用了 **反向 KL 散度**（Reverse KL Divergence，不是前向 KL 散度）。其中，Beta 是一个缩放因子，设置为 0.04；A 代表考虑所有奖励函数后获得的**优势（Advantage)**，可以理解为模型表现超越基线的程度；Q 代表新训练的模型，而 P 代表原始的参考模型。

We then notice interestingly that the implementation calculates the reverse KL divergence as: 

然后我们有趣地注意到，代码实现中反向 KL 散度（KL divergence）的计算方式如下：

$$
\begin{aligned}
p &= \sigma(f(x)) \\
q &= \sigma(f'(x)) \\
D_{KL}(q \parallel p)_i &= \exp(\log(p) - \log(q)) - (\log(p) - \log(q)) - 1 \\
&= \exp \left( \log \left(\frac{p}{q}\right) \right) - \log \left(\frac{p}{q}\right) - 1 \\
&= \frac{p}{q} - \log \left( \frac{p}{q} \right) - 1
\end{aligned}
$$

But is this actually correct? We first try to derive it, and collect like terms: 

其中，$D_{\text {KL}}\big（q \,\|\，p \big)_i$ 表示第 $i$ 个元素的 KL 散度。但这真的是正确的吗？我们首先尝试推导这个公式，并合并同类项：

$$
\begin{aligned}
D_{KL}(q \parallel p) &= \sum q \left[ \frac{p}{q} - \log\left( \frac{p}{q} \right) - 1 \right] \\
&= \sum q \frac{p}{q} - \sum q \log\left( \frac{p}{q} \right) - \sum q \\
&= \sum p - \sum q \log \left( \frac{p}{q} \right) - 1 \\
&= 1 - \sum q \log \left( \frac{p}{q} \right) - 1 \\
&= - \sum q \log \left( \frac{p}{q} \right) \\
D_{KL}(q \parallel p) &= \sum q \log \left( \frac{q}{p} \right)
\end{aligned}
$$

So what this means is that the implementation might be missing a multiplication by the Q (new distribution term)? 

上面的推导中，利用了概率分布的性质，$\sum q = 1$ 以及 $\sum p = 1$。那么，这意味着代码实现可能缺少与 $Q$（新分布项，具体含义需要根据上下文确定）的乘法吗？

But this seems to be correct as seen in the DeepSeek Math paper which first introduced GRPO on [page 14](https://arxiv.org/pdf/2402.03300). Likewise John [Schulman's blog](http://joschu.net/blog/kl-approx.html)also says that an unbiased estimator for the reverse KL term in fact does not need the extra Q term. We see in the blog that: 

但这个公式似乎又是正确的，正如 DeepSeek Math 论文中所述，该论文在 [第 14 页](https://arxiv.org/pdf/2402.03300)首次提出了 GRPO 算法。类似地，John Schulman 的博客(http://joschu.net/blog/kl-approx.html)也指出，反向 KL 散度的无偏估计量实际上并不需要额外的 Q 项。我们在该博客中看到：

$$
\begin{aligned}
r &= \frac{p(x)}{q(x)} \\
\text{KL}[q, p] &= (r - 1) - \log r \\
&= \frac{p}{q} - 1 - \log \frac{p}{q}
\end{aligned}
$$

We also found interestingly that: `torch.exp(q - q.detach()) * advantages.unsqueeze(1)`Is used, which should be evaluated to 1 right? 

我们还发现有趣的是，代码中使用了 `torch.exp（q - q.detach（)）* advantages.unsqueeze（1)`，这部分理论上应该等于 1，对吗？

We actually found this is necessary - it seems that the autograd engine might not be propagating gradients correctly. 

我们实际测试后发现，这部分代码是必要的。原因是 PyTorch 的自动求导引擎（autograd engine）可能没有正确地反向传播梯度（backpropagation gradients）。





So we perform 4 experiments: 
* Do normal GRPO via reference implementation (red line)
* Remove detach code (blue line)
* Full reverse KL with an extra term as discussed before (yellow line)
* Forward KL divergence instead (green line)

因此，我们进行了 4 个实验：
* 通过参考实现执行常规 GRPO（Gradient Ratio Policy Optimization，梯度比例策略优化）(红线)
* 移除用于切断梯度反向传播的 detach 代码（蓝线)
* 完整的反向 KL 散度（Kullback-Leibler divergence，库尔贝克 - 莱布勒散度），带有一个额外的项，如第 3.2 节讨论的（黄线)
* 使用前向 KL 散度（Kullback-Leibler divergence，库尔贝克 - 莱布勒散度）代替（绿线)

In general, removing detach definitely breaks all training, so we must leave it there - this will most likely need more investigation. It seems like all other implementations seem similar? We might need to run the model for longer to see different effects maybe. 

一般来说，移除 detach 操作一定会导致训练失败，所以必须保留它，但这可能需要更深入的调查。看起来其他的实现方法也类似？ 我们可能需要运行模型更长时间，才能观察到更明显的效果。

In all implementations, we also utilize the logsumexp trick: log ⁡ σ ⁡ ( x ) = log ⁡ exp ⁡ ( x ) ∑ exp ⁡ ( x ) = x − log ⁡ ∑ exp ⁡ ( x ) = x − logsumexp ⁡ ( x ) \begin{align}
\log\sigma(x) = \log{\frac{\exp(x)}{\sum{\exp(x)}}} &= x - \log\sum{\exp(x)} \\
&= x - \text{logsumexp}(x)
\end{align} 📈 Full Logging for GRPO We also provide full logging details for all reward functions now! Previously we only showed the total aggregated reward function itself. You also do not need to call functions to patch GRPO anymore! I.e. remove this at the top (we do it automatically): `from unsloth import PatchFastRL
PatchFastRL("GRPO", FastLanguageModel)`🖥️ vLLM inference options We also now allow you to use FP8 KV caches for vLLM, which allows for 2x less KV cache space usage on newer GPUs (RTX 3090, A100 and newer) `model, tokenizer = FastLanguageModel.from_pretrained(
 model_name = "meta-llama/meta-Llama-3.1-8B-Instruct",
 max_seq_length = max_seq_length,
 load_in_4bit = True, # False for LoRA 16bit
 fast_inference = True, # Enable vLLM fast inference
 max_lora_rank = lora_rank,
 gpu_memory_utilization = 0.6, # Reduce if out of memory
 float8_kv_cache = True, # Enable float8 KV cache
)`If you want to use min_p = 0.1, or other sampling params in vLLM, we also support passing anything in vLLM’s SamplingParams arguments! `max_prompt_length = 256
from trl import GRPOConfig, GRPOTrainer
from unsloth import vLLMSamplingParams
vllm_sampling_params = vLLMSamplingParams(
 min_p = 0.1,
 seed = 3407,
 ...
)
training_args = GRPOConfig(
 ...
 vllm_sampling_params = vllm_sampling_params,
 temperature = 1.5,
)`✨ Other Updates # 🦥 Run Unsloth Dynamic 4-bit directly with vLLM
You can now run and do inference with our dynamic quants directly in vLLM. This was due to an [accepted PR](https://github.com/vllm-project/vllm/pull/12974)we did for the vLLM repo. Read how our dynamic quants greatly increase accuracy than standard 4-bit with examples and benchmarks [here](https://unsloth.ai/blog/dynamic-4bit). # 🚀 Run Perplexity's R1-1776
You also now download our [R1-1776 Dynamic GGUFs](https://huggingface.co/unsloth/r1-1776-GGUF)for Perplexity AI’s new R1-1776 model which is a finetune of DeepSeek-R1 that removes all censorship whilst maintaining reasoning capabilities. Run them locally on your own device! # 🐱 GitHub Universe Interview
In October during GitHub's 2024 Universe, we did a wonderful interview with Andrea and now the video is out! We talk about our backgrounds from Australia, how we built Unsloth, how amazing all of you are and more! [Watch on YouTube](https://www.youtube.com/watch?v=lyVxD0bJDOk)

在所有实现中，我们还使用了 logsumexp 技巧：
\begin {align}
\log\sigma（x）= \log {\frac {\exp（x)}{\sum {\exp（x)}}} &= x - \log\sum {\exp（x)} \\
&= x - \text {logsumexp}(x)
\end {align}

📈 GRPO 全面日志记录：我们现在为所有奖励函数提供更详细的日志信息。之前，我们只展示了总体的聚合奖励函数。现在，你不再需要手动调用函数来修补 GRPO 了！相关代码（例如 `from unsloth import PatchFastRL; PatchFastRL（"GRPO」，FastLanguageModel)`）可以移除，我们会自动处理。

🖥️ vLLM 推理优化：我们现在支持在 vLLM 中使用 FP8 KV 缓存（FP8 KV cache），这可以在较新的 GPU（RTX 3090、A100 及更新型号）上减少 2 倍的 KV 缓存空间占用。使用方法如下：
```python
model，tokenizer = FastLanguageModel.from_pretrained（
 model_name =「meta-llama/meta-Llama-3.1-8B-Instruct",
 max_seq_length = max_seq_length,
 load_in_4bit = True，# False for LoRA 16bit
 fast_inference = True，# Enable vLLM fast inference
 max_lora_rank = lora_rank,
 gpu_memory_utilization = 0.6，# Reduce if out of memory
 float8_kv_cache = True，# Enable float8 KV cache
)
```如果你想在 vLLM 中使用`min_p = 0.1`或其他采样参数，我们也支持直接传递 vLLM 的`SamplingParams`参数来实现！示例：```python
max_prompt_length = 256
from trl import GRPOConfig，GRPOTrainer
from unsloth import vLLMSamplingParams
vllm_sampling_params = vLLMSamplingParams（
 min_p = 0.1,
 seed = 3407,
 ...
)
training_args = GRPOConfig（
 ...
 vllm_sampling_params = vllm_sampling_params,
 temperature = 1.5,
)
```

✨ 其他更新

*  🦥 ** 直接通过 vLLM 运行 Unsloth 动态 4 位（Unsloth Dynamic 4-bit)**

  现在，你可以直接在 vLLM 中使用我们的动态量化技术进行推理。这得益于我们为 vLLM 仓库提交的 [PR](https://github.com/vllm-project/vllm/pull/12974）并已被接受。想了解我们的动态量化技术如何显著提高 4 位量化的精度吗？请参考这篇 [文章](https://unsloth.ai/blog/dynamic-4bit），内含示例和基准测试。

*  🚀 ** 运行 Perplexity AI 的 R1-1776 模型 **

  现在，你可以下载我们提供的 [R1-1776 Dynamic GGUFs](https://huggingface.co/unsloth/r1-1776-GGUF），用于 Perplexity AI 的最新 R1-1776 模型。该模型基于 DeepSeek-R1 进行了微调，移除了所有审查机制，同时保留了强大的推理能力。快在你的设备上本地运行体验吧！

*  🐱 **Unsloth 团队 GitHub Universe 访谈 **

  在 2024 年 10 月举行的 GitHub Universe 大会上，我们和 Andrea 进行了一次愉快的访谈，视频已经发布！我们聊了聊来自澳大利亚的背景，Unsloth 的创建历程，以及我们对社区的感激之情！欢迎 [观看视频](https://www.youtube.com/watch?v=lyVxD0bJDOk）。
