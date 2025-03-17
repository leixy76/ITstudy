## 20250307Run-Finetune-QwQ-32B-with-Bug-Fixes

[Run & Finetune QwQ-32B with Bug Fixes](https://unsloth.ai/blog/qwq-32b)

[Tutorial: How to Run QwQ-32B effectively | Unsloth Documentation](https://docs.unsloth.ai/basics/tutorial-how-to-run-qwq-32b-effectively)

运行与微调 QwQ-32B，并修复 Bug

Mar 7, 2025

By Daniel & Michael

Qwen released QwQ-32B, a powerful reasoning model with performance comparable to DeepSeek-R1 across multiple benchmarks. You may have encountered issues such as infinite loops, repetitions, <think> token errors, and fine-tuning challenges, which do not reflect the model’s true quality. We hope this blog will help debug and fix most issues! [View Tutorial](https://unsloth.ai/blog/qwq-32b#Tutorial%20QwQ)

Qwen 发布了 QwQ-32B，这是一个强大的推理模型（reasoning model），在多个基准测试中，其性能可以与 DeepSeek-R1 相媲美。您可能遇到过一些问题，比如无限循环、重复、<think> Token 错误以及微调方面的问题，但这些并不能完全展现 QwQ-32B 的真实水平。我们希望这篇博客能帮助您调试并解决大部分问题！[查看教程](https://unsloth.ai/blog/qwq-32b#Tutorial%20QwQ)

Our model uploads include bug fixes and work for fine-tuning, vLLM and Transformers, however if you're using llama.cpp and engines that use llama.cpp as backend you might have experienced issues. To solve the issues follow our tutorial below or read our detailed guide + analysis in our [docs here](https://docs.unsloth.ai/basics/tutorial-how-to-run-qwq-32b-properly). 

我们上传的模型包括错误修复、微调工作，以及对 vLLM 和 Transformers 的支持。但是，如果您使用的是 llama.cpp 或以 llama.cpp 为后端的引擎，则可能遇到问题。要解决这些问题，请按照我们下面的教程进行操作，或阅读我们详细的指南及分析，请参阅我们的文档：[docs here](https://docs.unsloth.ai/basics/tutorial-how-to-run-qwq-32b-properly)。

See all Unsloth fixed QwQ-32B uploads including [GGUF](https://huggingface.co/unsloth/QwQ-32B-GGUF)& dynamic 4-bit on [here](https://huggingface.co/collections/unsloth/qwen-qwq-32b-collection-676b3b29c20c09a8c71a6235). 

[Tutorial: How to Run QwQ-32B effectively | Unsloth Documentation](https://docs.unsloth.ai/basics/tutorial-how-to-run-qwq-32b-effectively)

[unsloth/QwQ-32B-GGUF · Hugging Face](https://huggingface.co/unsloth/QwQ-32B-GGUF)

[Qwen QwQ-32B Collection - a unsloth Collection](https://huggingface.co/collections/unsloth/qwen-qwq-32b-collection-676b3b29c20c09a8c71a6235)

点击 [这里](https://huggingface.co/collections/unsloth/qwen-qwq-32b-collection-676b3b29c20c09a8c71a6235)，查看所有 Unsloth 修复的 QwQ-32B 模型上传，包括 [GGUF](https://huggingface.co/unsloth/QwQ-32B-GGUF)格式以及动态 4 位量化（dynamic 4-bit）版本。

### QwQ-32B Bug Fixes 

QwQ-32B 缺陷修复

We found a few issues as well specifically impacting finetuning! The EOS token is correct, but the PAD token should probably rather be "<|vision_pad|>" We updated it in here.

我们发现了一些问题，尤其会影响模型的微调！句末 Token（EOS Token）是正确的，但填充 Token（PAD Token）应该为「<|vision_pad|>」。我们已在此处更新：

"eos_token": "<|im_end|>",
"pad_token": "<|endoftext|>",

### Official Recommended Settings 

官方推荐设置

According to Qwen, these are the recommended settings for inference:

根据 Qwen 官方建议，以下是推理时推荐使用的设置：

[Qwen/QwQ-32B · Hugging Face](https://huggingface.co/Qwen/QwQ-32B)

1 Temperature of 0.6

Top_K of 40 (or 20 to 40)

Min_P of 0.0

Top_P of 0.95

温度（Temperature）设置为 0.6，Top_K 设置为 40（或 20 到 40），Min_P 设置为 0.0，Top_P 设置为 0.95。

2 Repetition Penalty of 1.0. (1.0 means disabled in llama.cpp and transformers)

重复惩罚（Repetition Penalty）设置为 1.0（在 llama.cpp 和 transformers 中，1.0 表示禁用该功能）。

3 Chat template: <|im_start|>user\nCreate a Flappy Bird game in Python.<|im_end|>\n<|im_start|>assistant\n<think>\n

聊天模板：<|im_start|>user\n 用 Python 创建一个 Flappy Bird 游戏。<|im_end|>\n<|im_start|>assistant\n<think>\n

### Recommended settings for llama.cpp 

llama.cpp 优化建议

We noticed many people use a Repetition Penalty greater than 1.0. For example 1.1 to 1.5. This actually interferes with llama.cpp's sampling mechanisms. The goal of a repetition penalty is to penalize repeated generations, but we found this doesn't work as expected.

我们发现许多用户在使用大于 1.0 的重复惩罚。例如，1.1 到 1.5。但实际上，这会影响 llama.cpp 的采样机制。重复惩罚（Repetition Penalty）的目的是为了避免模型重复生成内容，但实验结果表明，这种方式并没有达到预期的效果。

Turning off Repetition Penalty also works (ie setting it to 1.0), but we found using it to be useful to penalize endless generations.

虽然关闭重复惩罚（设置为 1.0）也能避免重复生成，但我们发现，适当使用重复惩罚来避免无限生成是有帮助的。

To use it, we found you must also edit the ordering of samplers in llama.cpp to before applying Repetition Penalty, otherwise there will be endless generations. So add this:

为了达到最佳效果，您还需要调整 llama.cpp 中采样器的顺序，确保在应用重复惩罚之前完成采样。具体来说，添加以下参数：

--samplers "top_k;top_p;min_p;temperature;dry;typ_p;xtc"

By default, llama.cpp uses this ordering:

默认情况下，llama.cpp 使用的采样器顺序为：

--samplers "dry;top_k;typ_p;top_p;min_p;xtc;temperature"

We reorder essentially temperature and dry, and move min_p forward. This means we apply samplers in this order:

我们调整了 temperature 和 dry 的顺序，并将 min_p 提前。调整后的采样顺序如下：

top_k=40
top_p=0.95
min_p=0.0
temperature=0.6
dry
typ_p
xtc

### Tutorial: Run QwQ-32B with Fixes 

教程：修复 QwQ-32B 模型运行问题

#### 1. For llama.cpp & engines that use llama.cpp:

1 适用于 llama.cpp 及其相关引擎：

You can read our complete guide in our docs here. Obtain the latest llama.cpp at: github.com/ggml-org/llama.cpp. You can follow the build instructions below as well. Change -DGGML_CUDA=ON to -DGGML_CUDA=OFF if you don't have a GPU or just want CPU inference.

您可以在我们的文档中找到完整指南：[完整指南](https://unsloth.ai/blog/qwq-32b)。访问 [github.com/ggml-org/llama.cpp](https://github.com/ggml-org/llama.cpp) 获取最新版本的 llama.cpp。您也可以参考下面的构建步骤。如果您没有 GPU，或者只想使用 CPU 进行推理，请将 `-DGGML_CUDA=ON` 修改为 `-DGGML_CUDA=OFF`。

[ggml-org/llama.cpp: LLM inference in C/C++](https://github.com/ggml-org/llama.cpp)

`apt-get update
apt-get install build-essential cmake curl libcurl4-openssl-dev -y
git clone https://github.com/ggerganov/llama.cpp
cmake llama.cpp -B llama.cpp/build \
 -DBUILD_SHARED_LIBS=ON -DGGML_CUDA=ON -DLLAMA_CURL=ON
cmake --build llama.cpp/build --config Release -j --clean-first --target llama-quantize llama-cli llama-gguf-split
cp llama.cpp/build/bin/llama-* llama.cpp`

#### 2. Download the model + Test

2 下载模型并进行测试安装

Download the model via (after installing pip install huggingface_hub hf_transfer ). You can choose Q4_K_M, or other quantized versions (like BF16 full precision). Other variants: huggingface.co/unsloth/QwQ-32B-GGUFThen run Unsloth's Flappy Bird test, which will save the output to Q4_K_M_yes_samplers.txt

`pip install huggingface_hub hf_transfer` 后，您可以通过以下方式下载模型。可以选择 `Q4_K_M`，或者其他量化版本（如 `BF16` 全精度）。更多模型变体请访问：[huggingface.co/unsloth/QwQ-32B-GGUF](https://huggingface.co/unsloth/QwQ-32B-GGUF)。下载完成后，运行 Unsloth 提供的 Flappy Bird 测试脚本，测试结果将保存到 `Q4_K_M_yes_samplers.txt` 文件中。

[unsloth/QwQ-32B-GGUF · Hugging Face](https://huggingface.co/unsloth/QwQ-32B-GGUF)

`# !pip install huggingface_hub hf_transfer
import os
os.environ["HF_HUB_ENABLE_HF_TRANSFER"] = "1"
from huggingface_hub import snapshot_download
snapshot_download(
 repo_id = "unsloth/QwQ-32B-GGUF",
 local_dir = "unsloth-QwQ-32B-GGUF",
 allow_patterns = ["*Q4_K_M*"], # For Q4_K_M
)`

#### 3. Test/Evaluate

3 测试与评估

Edit --threads 32 for the number of CPU threads, --ctx-size 16384 for context length, --n-gpu-layers 99 for GPU offloading on how many layers. Try adjusting it if your GPU goes out of memory. Also remove it if you have CPU only inference.We use --repeat-penalty 1.1 and --dry-multiplier 0.5 which you can adjust.

根据您的 CPU 线程数、上下文长度和 GPU 显存大小，调整以下参数：`--threads 32`（CPU 线程数），`--ctx-size 16384`（上下文长度），`--n-gpu-layers 99`（用于 GPU 加速的层数）。如果 GPU 显存不足，请尝试减小 `--n-gpu-layers` 的值。如果只使用 CPU 进行推理，则移除此参数。建议使用 `--repeat-penalty 1.1` 和 `--dry-multiplier 0.5`，您可以根据实际情况进行调整。

`./llama.cpp/llama-cli \
 --model unsloth-QwQ-32B-GGUF/QwQ-32B-Q4_K_M.gguf \
 --threads 32 \
 --ctx-size 16384 \
 --n-gpu-layers 99 \
 --seed 3407 \
 --prio 2 \
 --temp 0.6 \
 --repeat-penalty 1.5 \
 --repeat-penalty 1.1 \
 --dry-multiplier 0.5 \
 --min-p 0.0 \
 --top-k 40 \
 --top-p 0.95 \
 -no-cnv \
 --samplers "top_k;top_p;min_p;temperature;dry;typ_p;xtc" \
 --prompt "<|im_start|>user\nCreate a Flappy Bird game in Python. You must include these things:\n1. You must use pygame.\n2. The background color should be randomly chosen and is a light shade. Start with a light blue color.\n3. Pressing SPACE multiple times will accelerate the bird.\n4. The bird's shape should be randomly chosen as a square, circle or triangle. The color should be randomly chosen as a dark color.\n5. Place on the bottom some land colored as dark brown or yellow chosen randomly.\n6. Make a score shown on the top right side. Increment if you pass pipes and don't hit them.\n7. Make randomly spaced pipes with enough space. Color them randomly as dark green or light brown or a dark gray shade.\n8. When you lose, show the best score. Make the text inside the screen. Pressing q or Esc will quit the game. Restarting is pressing SPACE again.\nThe final game should be inside a markdown section in Python. Check your code for errors and fix them before the final markdown section.<|im_end|>\n<|im_start|>assistant\n<think>\n" \
 2>&1 | tee Q4_K_M_yes_samplers.txt`
 
See example final Python output here. The full input is:
 
最终 Python 代码示例如下。完整的 Prompt 内容如下：

[Tutorial: How to Run QwQ-32B effectively | Unsloth Documentation](https://docs.unsloth.ai/basics/tutorial-how-to-run-qwq-32b-effectively)

`<|im_start|>user
Create a Flappy Bird game in Python. You must include these things:
1. You must use pygame.
2. The background color should be randomly chosen and is a light shade. Start with a light blue color.
3. Pressing SPACE multiple times will accelerate the bird.
4. The bird's shape should be randomly chosen as a square, circle or triangle. The color should be randomly chosen as a dark color.
5. Place on the bottom some land colored as dark brown or yellow chosen randomly.
6. Make a score shown on the top right side. Increment if you pass pipes and don't hit them.
7. Make randomly spaced pipes with enough space. Color them randomly as dark green or light brown or a dark gray shade.
8. When you lose, show the best score. Make the text inside the screen. Pressing q or Esc will quit the game. Restarting is pressing SPACE again.
The final game should be inside a markdown section in Python. Check your code for errors and fix them before the final markdown section.<|im_end|>
<|im_start|>assistant
<think>`
	
When running it, we get a runnable game!

运行后，您将得到一个可以正常运行的 Flappy Bird 游戏！

#### 4. Try without our Fixes:

4 不使用修复方案进行尝试：

Now try the same without our fixes! So remove --samplers "top_k;top_p;min_p;temperature;dry;typ_p;xtc" This will save the output to Q4_K_M_no_samplers.txt

现在，让我们尝试在不应用上述修复方案的情况下运行相同的测试！移除 `--samplers"top_k;top_p;min_p;temperature;dry;typ_p;xtc"`参数，并将输出保存到`Q4_K_M_no_samplers.txt`文件中。

./llama.cpp/llama-cli \
 --model unsloth-QwQ-32B-GGUF/QwQ-32B-Q4_K_M.gguf \
 --threads 32 \
 --ctx-size 16384 \
 --n-gpu-layers 99 \
 --seed 3407 \
 --prio 2 \
 --temp 0.6 \
 --repeat-penalty 1.5 \
 --repeat-penalty 1.1 \
 --dry-multiplier 0.5 \
 --min-p 0.1 \
 --top-k 40 \
 --top-p 0.95 \
 -no-cnv \
 --prompt "<|im_start|>user\nCreate a Flappy Bird game in Python. You must include these things:\n1. You must use pygame.\n2. The background color should be randomly chosen and is a light shade. Start with a light blue color.\n3. Pressing SPACE multiple times will accelerate the bird.\n4. The bird's shape should be randomly chosen as a square, circle or triangle. The color should be randomly chosen as a dark color.\n5. Place on the bottom some land colored as dark brown or yellow chosen randomly.\n6. Make a score shown on the top right side. Increment if you pass pipes and don't hit them.\n7. Make randomly spaced pipes with enough space. Color them randomly as dark green or light brown or a dark gray shade.\n8. When you lose, show the best score. Make the text inside the screen. Pressing q or Esc will quit the game. Restarting is pressing SPACE again.\nThe final game should be inside a markdown section in Python. Check your code for errors and fix them before the final markdown section.<|im_end|>\n<|im_start|>assistant\n<think>\n" \
 2>&1 | tee Q4_K_M_no_samplers.txt
 
You will get some looping, but problematically incorrect Python syntax and many other issues. For example the below looks correct, but is wrong! Ie line 39 pipes.clear() ### <<< NameError: name 'pipes' is not defined. Did you forget to import 'pipes'? See our example which shows totally incorrect results here

您会发现模型生成的内容存在循环，以及不正确的 Python 语法和其他问题。例如，以下代码片段看起来正确，但实际上存在错误！在第 39 行，`pipes.clear()`会抛出 `NameError：name 'pipes' is not defined` 错误。这是因为代码中缺少 `import pipes` 语句。更多错误示例请参考 [链接]。

[Tutorial: How to Run QwQ-32B effectively | Unsloth Documentation](https://docs.unsloth.ai/basics/tutorial-how-to-run-qwq-32b-effectively)

If you use --repeat-penalty 1.5, it gets even worse and more obvious, with actually totally incorrect syntax.

如果您使用`--repeat-penalty 1.5`，问题会更加严重，模型会生成完全无效的语法。

You might be wondering maybe it's Q4_K_M? B16 ie full precision should work fine right? Incorrect - the outputs again fail if we do not use our fix of --samplers "top_k;top_p;min_p;temperature;dry;typ_p;xtc" when using a Repetition Penalty.

也许您会认为问题出在`Q4_K_M`量化模型上？使用`BF16`全精度模型应该没问题吧？答案是否定的。如果不使用 `--samplers "top_k;top_p;min_p;temperature;dry;typ_p;xtc"` 修复方案，即使是全精度模型也会生成错误的输出。

### <think> token not shown? 

关于 `<think>` Token 显示问题的说明

Some people are reporting that because <think> is default added in the chat template, some systems are not outputting the thinking traces correctly. You will have to manually edit the Jinja template from:

有用户报告说，由于聊天模板默认添加了 `<think>`，导致某些系统无法正确显示推理过程。您需要手动修改 Jinja 模板，删除以下代码段中的 `<think>\n`：

`{%- if tools %} {{- '<|im_start|>system\n' }} {%- if messages[0]['role'] == 'system' %} {{- messages[0]['content'] }} {%- else %} {{- '' }} {%- endif %} {{- "\n\n# Tools\n\nYou may call one or more functions to assist with the user query.\n\nYou are provided with function signatures within <tools></tools> XML tags:\n<tools>" }} {%- for tool in tools %} {{- "\n" }} {{- tool | tojson }} {%- endfor %} {{- "\n</tools>\n\nFor each function call, return a json object with function name and arguments within <tool_call></tool_call> XML tags:\n<tool_call>\n{\"name\": <function-name>, \"arguments\": <args-json-object>}\n</tool_call><|im_end|>\n" }} {%- else %} {%- if messages[0]['role'] == 'system' %} {{- '<|im_start|>system\n' + messages[0]['content'] + '<|im_end|>\n' }} {%- endif %} {%- endif %} {%- for message in messages %} {%- if (message.role == "user") or (message.role == "system" and not loop.first) %} {{- '<|im_start|>' + message.role + '\n' + message.content + '<|im_end|>' + '\n' }} {%- elif message.role == "assistant" and not message.tool_calls %} {%- set content = message.content.split('</think>')[-1].lstrip('\n') %} {{- '<|im_start|>' + message.role + '\n' + content + '<|im_end|>' + '\n' }} {%- elif message.role == "assistant" %} {%- set content = message.content.split('</think>')[-1].lstrip('\n') %} {{- '<|im_start|>' + message.role }} {%- if message.content %} {{- '\n' + content }} {%- endif %} {%- for tool_call in message.tool_calls %} {%- if tool_call.function is defined %} {%- set tool_call = tool_call.function %} {%- endif %} {{- '\n<tool_call>\n{"name": "' }} {{- tool_call.name }} {{- '", "arguments": ' }} {{- tool_call.arguments | tojson }} {{- '}\n</tool_call>' }} {%- endfor %} {{- '<|im_end|>\n' }} {%- elif message.role == "tool" %} {%- if (loop.index0 == 0) or (messages[loop.index0 - 1].role != "tool") %} {{- '<|im_start|>user' }} {%- endif %} {{- '\n<tool_response>\n' }} {{- message.content }} {{- '\n</tool_response>' }} {%- if loop.last or (messages[loop.index0 + 1].role != "tool") %} {{- '<|im_end|>\n' }} {%- endif %} {%- endif %} {%- endfor %} {%- if add_generation_prompt %} {{- '<|im_start|>assistant\n<think>\n' }} {%- endif %}`

to another by removing the <think>\n at the end. The model will now have to manually add <think>\n during inference, which might not always succeed. DeepSeek also edited all models to default add a <think> token to force the model to go into reasoning model.

So change {%- if add_generation_prompt %} {{- '<|im_start|>assistant\n<think>\n' }} {%- endif %} to {%- if add_generation_prompt %} {{- '<|im_start|>assistant\n' }} {%- endif %} ie remove <think>\nSee full jinga template with removed <think>\n part here.

也就是说，移除`<think>\n`。修改后，模型需要在推理过程中手动添加`<think>\n`，但这可能不会总是成功。DeepSeek 修改了所有模型，默认添加`<think>`Token，以强制模型进入推理模式。查看已移除`<think>\n` 的完整 Jinja 模板 [链接]。

[Tutorial: How to Run QwQ-32B effectively | Unsloth Documentation](https://docs.unsloth.ai/basics/tutorial-how-to-run-qwq-32b-effectively)

### Experimental Results + Notes 

实验结果与注意事项

We first thought maybe:

最初，我们认为问题可能出在：

1 QwQ's context length was not natively 128K, but rather 32K with YaRN extension. We tried overriding llama.cpp's YaRN handling, but nothing changed. For example in the QwQ-32B readme file we see the below:

{
  ...,
  "rope_scaling": {
    "factor": 4.0,
    "original_max_position_embeddings": 32768,
    "type": "yarn"
  }
}

QwQ 的上下文长度并非原生支持 128K，而是通过 YaRN 扩展在 32K 的基础上实现的。我们尝试修改 llama.cpp 中关于 YaRN 的处理方式，但没有产生效果。例如，在 QwQ-32B 的 readme 文件中，我们可以看到如下信息：

2 We also thought maybe the RMS Layernorm epsilon was wrong - not 1e-5 but maybe 1e-6. For example this has rms_norm_eps=1e-06, whilst this has rms_norm_eps=1e-05 . We also overrided it, but it did not work:

我们还怀疑可能是 RMS Layernorm 的 epsilon 值（RMS Layernorm epsilon）设置有误，本应为 1e-5 却被设置为了 1e-6。例如，这个模型文件的 `rms_norm_eps` 参数值为 1e-06，而另一个模型文件的该参数值为 1e-05。我们尝试修改这个值，但问题依旧没有解决：

3 We also tested if tokenizer IDs matched between llama.cpp and normal Transformers courtesy of @kalomaze. They matched, so this was not the culprit. We provide our experimental results in our docs.

此外，在 @kalomaze 的帮助下，我们还测试了 llama.cpp 和标准的 Transformer 模型之间，tokenizer 的 ID 是否一致。结果显示它们是匹配的，因此可以排除 tokenizer 的问题。详细的实验结果请参考我们的文档。

### Dynamic 4-bit Quants 

动态 4 位量化（Dynamic 4-bit Quants)

We also uploaded dynamic 4-bit quants which increase accuracy vs naive 4-bit quantizations! We uploaded dynamic 4-bit quants to here. We attached the QwQ quantization error plot analysis for both activation and weight quantization errors below:

我们上传了动态 4 位量化版本，相比于简单的 4 位量化，它能够显著提高模型精度。点击 [链接] 即可获取我们上传的动态 4 位量化模型。下方是我们对激活和权重进行 QwQ 量化后的误差分析图：

[Unsloth - Dynamic 4-bit Quantization](https://unsloth.ai/blog/dynamic-4bit)

[unsloth/QwQ-32B-unsloth-bnb-4bit · Hugging Face](https://huggingface.co/unsloth/QwQ-32B-unsloth-bnb-4bit)

Since vLLM 0.7.3 (2025 Feb 20), vLLM now supports loading Unsloth dynamic 4-bit quants!

自 vLLM 0.7.3（2025 年 2 月 20 日）起，vLLM 开始支持加载 Unsloth 的动态 4 位量化模型！

[Release v0.7.3 · vllm-project/vllm](https://github.com/vllm-project/vllm/releases/tag/v0.7.3)

### Finetuning QwQ-32B

QwQ-32B1xL4 24GB13xlonger context
QwQ-32B1xL4 24GB2xfaster
QwQ-32B1xL4 24GB>70%less VRAM

QwQ-32B finetuning fits with Unsloth in under 20GB of VRAM! It’s also 2x faster, and default uses our dynamic 4-bit quants for superior accuracy for QLoRA. 

使用 Unsloth 进行 QwQ-32B 微调，仅需不到 20GB 的显存！速度还能提升 2 倍。并且，为了保证 QLoRA 的精度，我们默认使用了动态 4 位量化。

Due to the model size, unfortunately the model does not fit on free Google Colab 16GB VRAM GPUs so you will need a GPU with at least 20GB VRAM. To view the rest of our notebooks and model uploads, please visit our [documentation](https://docs.unsloth.ai/get-started/unsloth-notebooks). 

由于模型体积较大，该模型无法在免费的 Google Colab 提供的 16GB VRAM GPU 上运行，因此您需要至少 20GB VRAM 的 GPU。要查看我们的其他 notebook 示例和上传的模型，请访问我们的 [documentation](https://docs.unsloth.ai/get-started/unsloth-notebooks)。

[Unsloth Notebooks | Unsloth Documentation](https://docs.unsloth.ai/get-started/unsloth-notebooks)

### Performance benchmarks

| Model | VRAM | 🦥Unsloth speed | 🦥VRAM reduction | 🦥Longer context | 🤗Hugging Face+FA2 |
|---|---|---|---|---|---|
| QwQ-32B | 24GB | 2x | 70% | 13x longer | 1x |

We tested using the Alpaca Dataset, a batch size of 2, gradient accumulation steps of 4, rank = 32, and applied QLoRA on all linear layers (q, k, v, o, gate, up, down). 

我们使用 Alpaca Dataset 进行了测试，批量大小（batch size）为 2，梯度累积步数（gradient accumulation steps）为 4，秩（rank）为 32。我们对所有线性层（q、k、v、o、gate、up、down）应用了 QLoRA 技术。