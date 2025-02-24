## 20250120Run-Finetune-DeepSeek-R1

[Run Deepseek-R1 / R1 Zero](https://unsloth.ai/blog/deepseek-r1)

Jan 20, 2025

By Daniel & Michael

DeepSeek’s new R1 models sets new benchmarks in reasoning performance, matching OpenAI’s o1 model. It follows the recently launched [DeepSeek-V3](https://huggingface.co/collections/unsloth/deepseek-v3-all-versions-677cf5cfd7df8b7815fc723c), the most powerful open-source AI model to date. DeepSeek also distilled from R1 and fine-tuned it on Llama 3 and Qwen 2.5 models, meaning you can now also fine-tune the models out of the box with [Unsloth](https://github.com/unslothai/unsloth). 

DeepSeek 推出的全新 R1 模型在推理性能上设立了新的标杆，达到了与 OpenAI 的 o1 模型（具体名称未公开，此处沿用原文）相近的水平。在此之前，DeepSeek 刚刚发布了 [DeepSeek-V3](https://huggingface.co/collections/unsloth/deepseek-v3-all-versions-677cf5cfd7df8b7815fc723c）模型，后者是目前性能最强大的开源 AI 模型。不仅如此，DeepSeek 还对 R1 模型进行了提炼，并使用 Llama 3 和 Qwen 2.5 模型进行了微调，这意味着研究者和开发者现在可以使用 [Unsloth](https://github.com/unslothai/unsloth）快速、便捷地对这些模型进行微调，实现开箱即用的效果。

See our collection for all versions of the R1 model series including GGUF's, 4-bit and more! [huggingface.co/collections/unsloth/deepseek-r1](https://huggingface.co/collections/unsloth/deepseek-r1-all-versions-678e1c48f5d2fce87892ace5)

查看我们的 R1 模型系列的所有版本，其中包括 GGUF、4 比特（4-bit）模型等多种类型！ [huggingface.co/collections/unsloth/deepseek-r1](https://huggingface.co/collections/unsloth/deepseek-r1-all-versions-678e1c48f5d2fce87892ace5)

**Jan 27, 2025 update**: We've released 1.58-bit Dynamic GGUFs for DeepSeek-R1 allowing you to run R1 even better with a 80% size reduction: [1.58-bit Dynamic R1](https://unsloth.ai/blog/deepseekr1-dynamic)

**2025 年 1 月 27 日更新**：我们发布了用于 DeepSeek-R1 的 1.58-bit Dynamic GGUF（GGML Unified Files）格式文件，它能让您以更佳性能运行 R1 模型，并且体积缩小了 80%：[1.58-bit Dynamic R1](https://unsloth.ai/blog/deepseekr1-dynamic)

**Feb 6, 2025 update**: You can now train your own reasoning model like R1 using: [GRPO + Unsloth](https://unsloth.ai/blog/r1-reasoning)

**2025 年 2 月 6 日更新**：您现在可以通过 [GRPO + Unsloth](https://unsloth.ai/blog/r1-reasoning) 方案，训练出像 R1 这样具备推理能力的模型。

[Train your own R1 reasoning model locally (GRPO)](https://unsloth.ai/blog/r1-reasoning)


Train-your-own-R1-reasoning-model-locally-(GRPO)

Train-your-own-R1-reasoning-model-locally-GRPO

### 0.1 How to Run DeepSeek-R1 models 

如何运行 DeepSeek-R1 模型

Running DeepSeek-R1 comes with challenges: its unquantized 8-bit version is a massive 700GB, trained originally in FP8. Direct GGUF conversion is not feasible, as GGUF requires FP16 so we converted it to FP16 and made the GGUF versions available. Thankfully, the DeepSeek team has created R1 Llama and Qwen distilled models that are much smaller and can easily be run locally on your own device. 

运行 DeepSeek-R1 模型面临一些挑战：它未经量化的 8-bit 版本体积高达 700GB，并且最初使用 FP8 格式进行训练。由于 GGUF 格式需要 FP16 格式，因此无法直接进行 GGUF 转换。为此，我们将其转换为 FP16 格式，并提供 GGUF 版本。幸运的是，DeepSeek 团队创建了 R1 Llama 和 Qwen 的蒸馏版本模型，这些模型体积更小，可以轻松在本地设备上运行。

To run DeepSeek-R1 / R1-Zero, you'll need to install the open-source package [llama.cpp](https://github.com/ggerganov/llama.cpp), the original framework for using GGUF files. Hardware requirements: You do not need a GPU, a CPU with RAM will suffice, but make sure you have enough disk space. 

要运行 DeepSeek-R1 / R1-Zero，你需要安装开源包 [llama.cpp](https://github.com/ggerganov/llama.cpp），它是使用 GGUF 文件的原始框架。硬件要求：你不需要 GPU，一个带有 RAM 的 CPU 即可，但要确保你有足够的磁盘空间。

#### Using llama.cpp:

使用 llama.cpp：

These instructions work for the R1 distilled and non distilled models, however keep in mind that they will require different hardware requirements. See further below for R1 requirements. 

以下指令适用于 DeepSeek-R1 的优化版本和非优化版本，请注意不同版本对硬件的要求有所不同，具体要求请参考下文。

1 Do not forget about `<｜User｜>` and `<｜Assistant｜>` tokens! - Or use a chat template formatter

请务必注意 `<｜User｜>` 和 `<｜Assistant｜>` 这两个 Token（令牌)！ - 或者使用聊天模板格式化程序

2 You must obtain the latest `llama.cpp` version at: github.com/ggerganov/llama.cpp

请从 github.com/ggerganov/llama.cpp 获取最新版本的 `llama.cpp`

3 Example with Q8_0 K quantized cache **Notice -no-cnv disables auto conversation mode

以下是使用 Q8_0 K 量化（Quantized）缓存的示例 **注意：添加 -no-cnv 参数可以禁用自动对话模式**

4 

./llama.cpp/llama-cli \
 --model unsloth/DeepSeek-R1-Distill-Llama-8B-GGUF/DeepSeek-R1-Distill-Llama-8B-Q4_K_M.gguf \
 --cache-type-k q8_0 \
 --threads 16 \
 --prompt '<｜User｜>What is 1+1?<｜Assistant｜>' \
 -no-cnv
 
Example output:

<think>
 Okay, so I need to figure out what 1 plus 1 is. Hmm, where do I even start? I remember from school that adding numbers is pretty basic, but I want to make sure I understand it properly.
 Let me think, 1 plus 1. So, I have one item and I add another one. Maybe like a apple plus another apple. If I have one apple and someone gives me another, I now have two apples. So, 1 plus 1 should be 2. That makes sense.
 Wait, but sometimes math can be tricky. Could it be something else? Like, in a different number system maybe? But I think the question is straightforward, using regular numbers, not like binary or hexadecimal or anything.
 I also recall that in arithmetic, addition is combining quantities. So, if you have two quantities of 1, combining them gives you a total of 2. Yeah, that seems right.
 Is there a scenario where 1 plus 1 wouldn't be 2? I can't think of any...

5 If you have a GPU (RTX 4090 for example) with 24GB, you can offload multiple layers to the GPU for faster processing. If you have multiple GPUs, you can probably offload more layers.

如果你有一个配备 24GB 显存的 GPU（例如 RTX 4090），你可以将部分层卸载到 GPU 上以加速计算。如果你有多个 GPU，可以卸载更多的层。

./llama.cpp/llama-cli \
   --model unsloth/DeepSeek-R1-Distill-Llama-8B-GGUF/DeepSeek-R1-Distill-Llama-8B-Q4_K_M.gguf
   --cache-type-k q8_0 
   --threads 16 
   --prompt '<｜User｜>What is 1+1?<｜Assistant｜>'
   --n-gpu-layers 20 \
    -no-cnv

#### Hardware Requirements for R1 / Zero:

R1 / Zero 的硬件要求：

A GPU will not necessary. You’ll just need a CPU with at least 48GB of RAM and at least 250GB of disk space. 

不需要 GPU。只需要一个 CPU，但需要至少 48GB 的内存以及至少 250GB 的硬盘空间。

Although these are the minimum requirements, performance may be very slow. Expect less than 1.5 tokens per second on minimal hardware - but that doesn't mean you can't experiment! Using a GPU will make your inference faster. 

请注意，以上只是最低配置要求，性能可能会比较慢。在最低配置的硬件上，预计每秒处理的 Token（Token）不会超过 1.5 个。但这并不妨碍您进行尝试！使用 GPU 可以显著提升推理速度。

Below is a table of details for DeepSeek-R1 GGUF quants, including disk space requirements: 

以下表格展示了 DeepSeek-R1 GGUF 格式量化模型的详细信息，包括所需的磁盘空间：

R1 Quants Disk Size Details 

[Q2_K_XS](https://huggingface.co/unsloth/DeepSeek-R1-GGUF/tree/main/DeepSeek-R1-Q2_K_XS)207GB Q2 everything, Q4 embed, Q6 lm_head [Q2_K_L](https://huggingface.co/unsloth/DeepSeek-R1-GGUF/tree/main/DeepSeek-R1-Q2_K_L)228GB Q3 down_proj Q2 rest, Q4 embed, Q6 lm_head [Q3_K_M](https://huggingface.co/unsloth/DeepSeek-R1-GGUF/tree/main/DeepSeek-R1-Q3_K_M)298GB Standard Q3_K_M [Q4_K_M](https://huggingface.co/unsloth/DeepSeek-R1-GGUF/tree/main/DeepSeek-R1-Q4_K_M)377GB Standard Q4_K_M [Q5_K_M](https://huggingface.co/unsloth/DeepSeek-R1-GGUF/tree/main/DeepSeek-R1-Q5_K_M)443GB Standard Q5_K_M [Q6_K](https://huggingface.co/unsloth/DeepSeek-R1-GGUF/tree/main/DeepSeek-R1-Q6_K)513GB Standard Q6_K [Q8_0](https://huggingface.co/unsloth/DeepSeek-R1-GGUF/tree/main/DeepSeek-R1-Q8_0)712GB Standard Q8_0 

### 02. Fine-tuning DeepSeek R1 

Fine-tuning reasoning models is still a relatively new area of exploration. However, since DeepSeek's distilled models are built on Llama and Qwen architectures, they are fully compatible with Unsloth out of the box. 

微调（Fine-tuning）DeepSeek R1 模型仍然是一个相对较新的领域。不过，由于 DeepSeek 的蒸馏模型建立在 Llama 和 Qwen 架构之上，因此它们可以与 Unsloth 完美兼容，无需额外配置。

We will soon provide a dedicated example notebook for fine-tuning reasoning models. In the meantime, you can use our existing [Llama](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-Alpaca.ipynb)or [Qwen](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Qwen2.5_(7B)-Alpaca.ipynb)Colab notebooks for free fine-tuning. Simply update the model names to match the appropriate ones. For instance, replace 'unsloth/Meta-Llama-3.1-8B' with 'unsloth/DeepSeek-R1-Distill-Llama-8B-unsloth-bnb-4bit'. 

我们很快会提供专门的 Notebook 示例，用于对推理模型进行微调。在此期间，您可以先使用我们现有的 [Llama](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-Alpaca.ipynb）或 [Qwen](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Qwen2.5_(7B)-Alpaca.ipynb） Colab Notebook，它们可以免费用于微调。您只需更新模型名称，使其与目标模型相匹配即可。例如，将 'unsloth/Meta-Llama-3.1-8B' 替换为 'unsloth/DeepSeek-R1-Distill-Llama-8B-unsloth-bnb-4bit'。

You can view all our current free fine-tuning notebooks [here](https://docs.unsloth.ai/get-started/unsloth-notebooks). 

你可以在 [这里](https://docs.unsloth.ai/get-started/unsloth-notebooks）找到所有我们提供的免费微调 Notebook 哦。

[Unsloth Notebooks | Unsloth Documentation](https://docs.unsloth.ai/get-started/unsloth-notebooks)

[Llama3.1\_(8B)-GRPO.ipynb - Colab](https://colab.research.google.com/github/unslothai/notebooks/blob/main/nb/Llama3.1_(8B)-GRPO.ipynb#scrollTo=IWXjM1OCfJCv)
