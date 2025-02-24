## 20250210Unsloth-Re-introducing-Unsloth

[Re-introducing Unsloth](https://unsloth.ai/blog/reintroducing)

Feb 10, 2025

By Daniel & Michael

Today, we’re the #1 trending repo on [GitHub](https://github.com/unslothai/unsloth)and it's all thanks to you! To celebrate, we want to take a moment to welcome anyone whether you’ve been with us from the beginning or just discovered Unsloth! 💖 

今天，我们荣登 [GitHub](https://github.com/unslothai/unsloth) 热榜第一名，这都归功于大家的支持！为了庆祝这一时刻，我们热烈欢迎每一位朋友，无论您是一直以来的忠实伙伴，还是刚刚认识 Unsloth 的新朋友！ 

But first, we wanted to thank each and everyone of you. We’re incredibly grateful for your support whether it’s reading our blogs, engaging with us, or contributing to our repo or just using/sharing Unsloth. Your support truly means the world to us and we wouldn't be here today without you guys! 

但首先，我们衷心感谢每一位朋友。非常感谢大家一直以来的支持，无论是阅读我们的博客、积极互动、为我们的代码仓库（repo）做出贡献，还是仅仅使用和分享 Unsloth。你们的支持对我们至关重要，没有大家的支持，就没有 Unsloth 的今天！

Also, we're also blown away by how much you guys enjoyed our [1.58-bit Dynamic](https://unsloth.ai/blog/deepseekr1-dynamic)DeepSeek-R1 and our latest [Reasoning](https://unsloth.ai/blog/r1-reasoning)release. But this is just the beginning - we’re not slowing down anytime soon! 

另外，大家对我们的 [1.58-bit Dynamic](https://unsloth.ai/blog/deepseekr1-dynamic) DeepSeek-R1 以及最新 [Reasoning](https://unsloth.ai/blog/r1-reasoning) 版本的热烈反响也让我们倍感振奋。但这仅仅是一个开端，我们前进的步伐绝不会停歇！

[Run DeepSeek-R1 Dynamic 1.58-bit](https://unsloth.ai/blog/deepseekr1-dynamic)

[Train your own R1 reasoning model locally (GRPO)](https://unsloth.ai/blog/r1-reasoning)

Here's a little bit about our journey so far: 

以下是关于我们目前为止的旅程的一点介绍：

### Unsloth Highlights 

Unsloth 亮点

1 Dec 2023: We launched Unsloth, making training 2x faster and 50% more memory-efficient. We built a custom autograd engine, rewrote all kernels in OpenAI's Triton, including the RoPE embeddings with optimized forward & backward passes and had our own custom Fast Cross Entropy Loss kernel.

2023 年 12 月：我们推出了 Unsloth，使训练速度提高 2 倍，内存效率提高 50%。我们构建了一个自定义的自动微分引擎（autograd engine），使用 OpenAI 的 Triton 重写了所有内核，包括具有优化正向和反向传递的 RoPE（Rotary Position Embedding）嵌入，并拥有我们自己的自定义快速交叉熵损失（Fast Cross Entropy Loss）内核。

[Unsloth update: Mistral support + more](https://unsloth.ai/blog/mistral-benchmark#Breakdown)

2 Jan 2024: We started uploading models to Hugging Face which has been downloaded by you amazing people millions of times! We also collabed with HF and are so thankful for their continued support. 

2024 年 1 月：我们开始将模型上传到 Hugging Face（HF），这些模型已被你们下载了数百万次！我们还与 HF 合作，非常感谢他们持续的支持。

[unsloth (Unsloth AI)](https://huggingface.co/unsloth)

[Make LLM Fine-tuning 2x faster with Unsloth and 🤗 TRL](https://huggingface.co/blog/unsloth-trl)

3 Mar 2024: We found & fixed 8 bugs in Google's incredible Gemma models. Thank you Andrej Karpathy for acknowledging our work and the Google team for their support!

2024 年 3 月：我们发现了并修复了 Google 的 Gemma 模型中的 8 个错误。感谢 Andrej Karpathy 对我们工作的认可，以及 Google 团队的支持！

[Unsloth Fixing Gemma bugs](https://unsloth.ai/blog/gemma-bugs)

[(1) X 上的 Andrej Karpathy：“Beautiful work / attention to detail trying to get Gemma to finetune correctly. There are so many foot guns here to be super careful with. All of these issues don't throw any errors, they silently make your network worse. A great example of what I wrote about in my "A Recipe for” / X](https://x.com/karpathy/status/1765473722985771335)

4 Apr 2024: We introduced Unsloth Gradient Checkpointing which allowed for 4x longer context lengths and 1.7x larger batch sizes. The epic Llama 3 models were released and we enabled the 70B model fit on 48GB of VRAM.

2024 年 4 月：我们推出了 Unsloth 梯度检查技术（Unsloth Gradient Checkpointing），它允许 4 倍更长的上下文长度和 1.7 倍更大的批量大小。史诗级的 Llama 3 模型发布，我们实现了在 48GB 显存（VRAM）上微调 70B 参数的 Llama 3 模型。

[Unsloth Gradient Checkpointing - 4x longer context windows](https://unsloth.ai/blog/long-context)

[Finetune Llama 3 with Unsloth](https://unsloth.ai/blog/llama3)

5 May 2024: We found & fixed many bugs in Llama 3 which greatly improved accuracy for training. The amazing Phi-3 model was released and we Llamafied it.

2024 年 5 月：我们发现了并修复了 Llama 3 中的许多错误，这大大提高了训练的准确性。令人惊叹的 Phi-3 模型发布，我们使其兼容 Llama 的架构。

[Finetune Phi-3 with Unsloth](https://unsloth.ai/blog/phi3)

6 Jul 2024: We fixed many bugs in Gemma 2 and introduced fine-tuning with CSV/Excel files and multiple columns.

2024 年 7 月：我们修复了 Gemma 2 中的许多错误，并推出了使用 CSV/Excel 文件和多列进行微调的功能。

[Finetune Gemma 2 with Unsloth](https://unsloth.ai/blog/gemma2)

[Finetune Mistral NeMo with Unsloth](https://unsloth.ai/blog/mistral-nemo)

7 Oct 2024: We fixed a universal issue in Gradient Accumulation that negatively impacted everyone's training runs (not just for Unsloth but everyone who was training models).

2024 年 10 月：我们修复了梯度累积（Gradient Accumulation）中的一个普遍问题，该问题对所有模型的训练都产生了负面影响。

[Bug Fixes in LLM Training - Gradient Accumulation](https://unsloth.ai/blog/gradient)

8 Nov 2024: 2x faster & 70% less VRAM Vision fine-tuning with Llama, Qwen, Pixtral and Llava support. We also found & fixed many Qwen 2.5 bugs.

2024 年 11 月：使用 Llama、Qwen、Pixtral 和 Llava 支持，视觉微调的速度提高 2 倍，显存占用减少 70%。我们还发现了并修复了许多 Qwen 2.5 错误。

[Llama 3.2 Vision Fine-tuning with Unsloth](https://unsloth.ai/blog/vision)

[(1) X 上的 Daniel Han：“Bug fixes &amp; analysis for Qwen 2.5: 1. Pad\_token should NOT be &lt;|endoftext|&gt; Inf gens 2. Base &lt;|im\_start|&gt; &lt;|im\_end|&gt; are untrained 3. PCA on embeddings has a BPE hierarchy 4. YaRN 128K extended context from 32B 5. Fixed versions + 128K GGUFs: https://t.co/DY3NvI2F2o Details: https://t.co/B8ogqObC0g” / X](https://x.com/danielhanchen/status/1856442699689414970)

9 Dec 2024: We introduced our Unsloth 4-bit Dynamic Quants which greatly increased accuracy compared to standard 4-bit by selectively avoiding quantizing certain layers. And we added support for 13x longer context lengths for Llama 3.3.

2024 年 12 月：我们推出了 Unsloth 4 比特动态量化技术（Unsloth 4-bit Dynamic Quants），通过选择性地避免量化某些层，与标准 4 比特量化相比，大大提高了准确性。并且我们增加了对 Llama 3.3 的 13 倍更长上下文长度的支持。

[Unsloth - Dynamic 4-bit Quantization](https://unsloth.ai/blog/dynamic-4bit)

[Fine-tune Llama 3.3 with Unsloth](https://unsloth.ai/blog/llama3-3)

10 Jan 2025: We released our 1.58-bit Dynamic R1 GGUF allowing you guys to run R1 on your local device and found & fixed many bugs in Phi-4.

2025 年 1 月：我们发布了我们的 1.58-bit Dynamic R1 GGUF，允许用户在本地设备上运行 R1，并发现了并修复了 Phi-4 中的许多错误。

11 Feb 2025: We introduced Reasoning in Unsloth and made GRPO work with QLoRA & LoRA, which previously did not work - allowing home users to train their own reasoning model like R1.

2025 年 2 月：我们在 Unsloth 中引入了推理能力（Reasoning），并使 GRPO 与 QLoRA 和 LoRA 配合使用，这在以前是行不通的，从而允许用户训练他们自己的推理模型，例如 R1。

[Train your own R1 reasoning model locally (GRPO)](https://unsloth.ai/blog/r1-reasoning)

### What's Next? 

未来展望

We're always trying to innovate and won't stop just yet. This year, you can expect even more exciting new cool stuff that will make creating your own custom models much easier and more accessible. 

我们始终致力于创新，探索的脚步永不停歇。今年，我们将推出更多令人期待的全新功能，让定制您专属的模型变得前所未有的轻松便捷。

And of course - multiGPU & Unsloth Studio are still on the way so don't worry - but we've got to support all models first which is coming pretty soon. Our goal is first and foremost open-source and Unslothing things for you guys, and nothing will ever change that so we hope you follow along this year for even more cool stuff!

当然，multiGPU 和 Unsloth Studio 仍在开发中，请不必担心。我们首要的任务是支持所有模型，这项工作很快就会完成。我们始终坚持开源，并致力于为大家简化 Unsloth 的相关流程。这一点永远不会改变，所以希望大家今年继续关注我们，期待更多精彩的内容！

### 参考

Andrej Karpathy
@karpathy

Beautiful work / attention to detail trying to get Gemma to finetune correctly. There are so many foot guns here to be super careful with. All of these issues don't throw any errors, they silently make your network worse.

A great example of what I wrote about in my "A Recipe for Training Neural Networks":
"""The "fast and furious" approach to training neural networks does not work and only leads to suffering. Now, suffering is a perfectly natural part of getting a neural network to work well, but it can be mitigated by being thorough, defensive, paranoid, and obsessed with visualizations of basically every possible thing. The qualities that in my experience correlate most strongly to success in deep learning are patience and attention to detail."""

And why I so emphasize the need for understanding all the parts of the deep learning stack in great detail. I exist in a perpetually terrified state of the remaining 20 silent bugs that certainly remain in my code.

你在努力让 Gemma 正确微调时展现出的细节把控令人赞叹。这个过程中存在许多看似无害却极具威胁的隐患，最危险的是这些问题不会产生任何错误提示，而是会悄无声息地降低模型性能。

这正好印证了我在《训练神经网络的秘诀》中所写的：

"""在训练神经网络时，采用 ' 快速冒进 ' 的方法注定失败，只会徒增痛苦。诚然，遭遇挫折是让神经网络达到理想效果过程中不可避免的，但我们可以通过全面严谨的态度、防御性的编程思维、极致的求证精神，以及对所有可能情况的可视化分析来减少这种痛苦。基于我的经验，在深度学习领域，最能带来成功的品质是耐心和对细节的专注。"""

这也解释了为什么我一直强调需要深入理解深度学习技术栈（deep learning stack）的每个组成部分。即便如此，我仍然时刻担忧着代码中那些潜伏着的、不会报错但会默默影响性能的 20 个问题。

---

Daniel Han
@danielhanchen

Bug fixes & analysis for Qwen 2.5:

1. Pad_token should NOT be <|endoftext|> Inf gens
2. Base <|im_start|> <|im_end|> are untrained
3. PCA on embeddings has a BPE hierarchy 
4. YaRN 128K extended context from 32B
5. Fixed versions + 128K GGUFs: http://huggingface.co/unsloth

Details:
1. Pad token bug - for finetuning, never use pad_token = EOS - this will result in infinite generations since finetuning will ignore them. Base model also has a chat template - remove this. 
@UnslothAI
 versions fixed them

2. Untrained tokens issues. Do NOT use the Qwen 2.5 chat template for the base version - <|im_start|>, <|im_end|> are untrained since Norm(<im_x>, pad_token) is close to 0. Instruct version have them trained.

3. PCA on embeddings for Base and Instruct show a BPE hierarchy. Less frequent tokens are obvious since they're ordered by ID. PCA shows <|im_x|> moving away from being untrained. Same phenomenon for Llama & more models.

4.  Uploaded native 128K extended YaRN GGUFs for Coder 0.5B all the way until 32B to https://huggingface.co/collections/unsloth/qwen-25-coder-all-versions-6732bc833ed65dd1964994d4. Use the 128K version for long contexts. Use the 32B native version for general chats.

Also, Unsloth can finetune 14B in a free Colab! Conversational style finetuning: https://colab.research.google.com/drive/18sN803sU23XuJV9Q8On2xgqHSer6-UZF?usp=sharing
Kaggle 14B notebook: https://kaggle.com/code/danielhanchen/kaggle-qwen-2-5-coder-14b-conversational

Unsloth can also finetune the 72B variants in a 48GB card!

Qwen 2.5 的问题修复和分析：

1. 填充词符 (pad_token) 不应设为文本结束符 (<|endoftext|>)，否则会导致模型无限输出
2. 基础版本中的对话标记 <|im_start|> 和 <|im_end|> 未经过训练
3. 对词嵌入进行主成分分析 (PCA) 发现了字节对编码 (BPE) 的层级特征
4. 使用 YaRN 技术将上下文长度从 32B 扩展到 128K
5. 修复版本和 128K GGUF 格式文件已上传至：http://huggingface.co/unsloth

详细说明：

1. 填充词符问题 - 在微调过程中，绝不要将填充词符设置为结束符 (EOS)，这会导致模型持续不断地生成内容，因为微调过程会忽略这些标记。基础模型中的对话模板也需要移除。@UnslothAI 的版本已修复这些问题。

2. 未训练词符问题。基础版本不要使用 Qwen 2.5 的对话模板 - 因为 <|im_start|> 和 <|im_end|> 这些标记未经训练（其与填充词符的范数接近于 0）。这些标记只在指令版本中经过了训练。

3. 对基础版和指令版的词嵌入进行主成分分析，揭示了字节对编码的层级结构。由于不常用的词符按 ID 排序，因此很容易识别。分析显示对话标记 <|im_x|> 正逐渐获得有意义的表示。这种现象在 Llama 等其他模型中也同样存在。

4. 我们已将支持 128K 长度的 YaRN 版本 GGUF 文件（包括从 0.5B 到 32B 的 Coder 版本）上传至 Hugging Face。建议在处理长文本时使用 128K 版本，日常对话则使用 32B 原生版本。

特别提醒：Unsloth 现在支持在免费版 Colab 上微调 140 亿参数的模型！对话式微调教程已上线。同时在 Kaggle 上也提供了 140 亿参数模型的训练示例。

更令人惊喜的是，Unsloth 甚至能够在配备 48GB 显存的显卡上微调 720 亿参数的模型变体！