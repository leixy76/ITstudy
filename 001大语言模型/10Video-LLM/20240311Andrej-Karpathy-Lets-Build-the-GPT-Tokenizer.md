## 20240311Andrej-Karpathy-Lets-Build-the-GPT-Tokenizer

[Let's build the GPT Tokenizer - YouTube](https://www.youtube.com/watch?v=zduSFxRajkE)

[openai/tiktoken: tiktoken is a fast BPE tokeniser for use with OpenAI's models.](https://github.com/openai/tiktoken)

[gpt-2/src/encoder.py at master · openai/gpt-2](https://github.com/openai/gpt-2/blob/master/src/encoder.py)

[Let's build GPT: from scratch, in code, spelled out. - YouTube](https://www.youtube.com/watch?v=kCc8FmEb1nY)

[[中文字幕][Andrej Karpathy] Let's build the GPT Tokenizer\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1yx4y1y7iK/?vd_source=280fc27368a92928cafc2cb72c54a549)

### 提炼消化

1、关于分词知识的论文位置。

[Language Models are Unsupervised Multitask Learners](https://insightcivic.s3.us-east-1.amazonaws.com/language-models.pdf)

上面这篇论文其实是讲 GPT-2 的，里面的小结「2.2. Input Representation」是关于分词知识的。

03.42min

### 音频整理

#### 01

Hi everyone. In this video, I'd like to cover the process of tokenization in large language models. I have a sad face here because tokenization is my least favorite part of working with large language models. But unfortunately, it is necessary to understand in some detail because it is fairly hairy, gnarly, and there are a lot of hidden foot guns to be aware of. A lot of oddness with large language models typically traces back to tokenization.

So what is tokenization? In my previous video, "Let's Build GPT from Scratch", we actually already did tokenization, but we did a very naive, simple version of it. In the Google Colab for that video, we loaded our training set, which was the Shakespeare dataset. In the beginning, the Shakespeare dataset is just a large string in Python, just text. The question is, how do we plug text into large language models? 

In that video, we created a vocabulary of 65 possible characters that we saw occur in this string. These were the possible characters and there were 65 of them. We then created a lookup table for converting every possible character, a little string piece, into a token, an integer. For example, we tokenized the string "hi there" and received a sequence of tokens 18, 47, etc. We took the first 1000 characters of our dataset and encoded it into tokens. Because this was character level, we received 1000 tokens in a sequence.

Later, we saw that the way we plug these tokens into the language model is by using an embedding table. If we have 65 possible tokens, this embedding table is going to have 65 rows. Roughly speaking, we're taking the integer associated with every single token, using that as a lookup into this table, and plucking out the corresponding row. This row contains trainable parameters that we're going to train using backpropagation. This is the vector that then feeds into the transformer and is how the transformer perceives every single token.

大家好！在本期视频中，我将为大家讲解大语言模型（Large Language Model）中的分词（tokenization）过程。你可能注意到我现在表情有点沮丧，这是因为在处理大语言模型的所有环节中，我最不喜欢的就是分词这一部分。但遗憾的是，我们必须深入理解它，因为这个过程不仅复杂难懂，还充满了各种棘手的问题，埋藏着许多潜在的风险。事实上，大语言模型中出现的许多异常现象，往往都可以追溯到分词这个环节。

那么什么是分词（tokenization）呢？在我之前的视频 "Let's Build GPT from Scratch"（让我们从零开始构建 GPT）中，我们其实已经进行了分词，但那是一个非常简单、朴素的版本。在那个视频的 Google Colab 中，我们加载了训练集，也就是莎士比亚数据集。起初，莎士比亚数据集只是 Python 中的一个大字符串，就是纯文本。那么问题来了，我们该如何将文本输入到大语言模型（Large Language Model）中呢？

[欢迎使用 Colaboratory - Colab](https://colab.research.google.com/#scrollTo=5fCEDCU_qrC0)

在之前的视频中，我们介绍了如何创建一个包含 65 个可能字符的字符集。这个字符集包含了我们在给定字符串中观察到的所有可能出现的字符。接下来，我们建立了一个查找表，用于将每个可能的字符（即一小段字符串）转换为一个称为 token 的整数。举个例子，当我们对字符串 "hi there" 进行分词（tokenization）处理时，得到了一个由整数组成的序列，如 18、47 等。这个过程就是将文本转换为机器可以理解的数字表示。

在我们的实验中，我们取了数据集中的前 1000 个字符，并将它们编码成 token。由于我们是在字符级别上进行操作，所以最终得到了一个长度为 1000 的 token 序列。这种字符级的处理方式使得每个字符都对应一个 token，因此输入的字符数量与输出的 token 数量是相等的。

接下来，我们了解到将这些 token（标记）输入到语言模型中的方法是使用嵌入表（embedding table）。假设我们有 65 个可能的 token，那么这个嵌入表就会有 65 行。简单来说，我们会为每个 token 分配一个整数，然后用这个整数在嵌入表中查找对应的行。这一行包含了可训练的参数，我们会通过反向传播（backpropagation）算法来训练这些参数。得到的向量随后会被输入到 Transformer 模型中，这就是 Transformer 模型理解每个 token 的方式。

为了更好地理解这个过程，我们可以将嵌入表想象成一本字典，每个 token 就像一个单词，而对应的行就是这个单词的详细解释。Transformer 模型通过查阅这本「字典」来理解每个 token 的含义，从而处理输入的文本。反向传播则是一种让模型不断改进这本「字典」的学习方法，使得模型对 token 的理解越来越准确。

In that video, we had a very naive tokenization process that was a character level tokenizer. But in practice, in state-of-the-art language models, people use much more complicated schemes for constructing these token vocabularies. We're not dealing on the character level, but on the chunk level. These character chunks are constructed using algorithms such as the byte pair encoding algorithm, which we're going to cover in detail in this video.

I'd like to briefly show you the paper that introduced byte level encoding as a mechanism for tokenization in the context of large language models. That's probably the GPT-2 paper. If you scroll down to the section "Input representation", this is where they cover tokenization and the properties you'd like the tokenization to have. They conclude that they're going to have a tokenizer with a vocabulary of 50,257 possible tokens. The context size is going to be 1,024 tokens. So in the attention layer of the transformer neural network, every single token is attending to the previous tokens in the sequence and it's going to see up to 1,024 tokens.

[Language Models are Unsupervised Multitask Learners](https://insightcivic.s3.us-east-1.amazonaws.com/language-models.pdf)

Tokens are the fundamental unit, the atom of large language models. Everything is in units of tokens, everything is about tokens. Tokenization is the process for translating strings or text into sequences of tokens and vice versa. 

When you go into the LAMA2 paper as well, if you search "token", you're going to get 63 hits. That's because tokens are pervasive. For example, they mention that they trained on 2 trillion tokens of data, and so on.

[[2307.09288] Llama 2: Open Foundation and Fine-Tuned Chat Models](https://arxiv.org/abs/2307.09288)

We're going to build our own tokenizer. Luckily the byte pairing coding algorithm is not super complicated and we can build it from scratch ourselves. We'll see exactly how this works. 

在之前的视频中，我们介绍了一种非常基础的分词（tokenization）方法，即字符级（character level）分词器。然而，在实际应用中，特别是在当前最先进的大语言模型（Large Language Model）中，研究人员采用了更为复杂的方案来构建词元（token）词汇表。这些先进的方法并不是在单个字符的层面上进行处理，而是以字符块（chunk）为单位。这些字符块是通过特定的算法构建的，其中最著名的就是字节对编码（Byte Pair Encoding, BPE）算法。在本视频中，我们将深入探讨这种算法的工作原理和应用。

让我们先简要回顾一下引入字节级编码作为大语言模型分词机制的重要论文，即 GPT-2 的研究论文。在该论文的「输入表示」部分，作者详细讨论了分词的过程及其应具备的特性。他们最终决定使用一个包含 50,257 个可能 token 的词汇表来进行分词。模型的上下文窗口大小设定为 1,024 个 token。这意味着在 Transformer 神经网络的注意力层中，每个 token 都能关注到序列中之前的 token，最多可以看到 1,024 个 token。

Token 是大语言模型的基本构建单位，可以说是模型处理信息的最小单元。在大语言模型中，所有的操作和计算都是以 token 为单位进行的。分词是一个将文本字符串转换为 token 序列的过程，同时这个过程也是可逆的。

如果我们查阅 LLAMA2 的研究论文，搜索「token」这个词，会发现有 63 处提及。这充分说明了 token 在大语言模型中的普遍性和重要性。例如，论文中提到他们使用了 2 万亿个 token 的数据进行模型训练，这个数字本身就十分惊人。

接下来，我们将要自己动手构建一个 tokenizer（分词器）。幸运的是，字节对编码算法（Byte Pair Encoding algorithm）并不特别复杂，我们完全可以从零开始构建它。通过这个过程，我们将能够深入理解 tokenizer 的工作原理，揭开它的神秘面纱。

Before we dive into code, I'd like to give you a brief taste of some of the complexities that come from tokenization. I want to make sure we're sufficiently motivated for why we are doing all this and why it's so gross. Tokenization is at the heart of a lot of weirdness in large language models. I would advise that you do not brush it off.

A lot of the issues that may look like just issues with the neural network architecture or the large language model itself are actually issues with the tokenization and fundamentally trace back to it. If you've noticed any issues with large language models not being able to do spelling tasks very easily, that's usually due to tokenization. Simple string processing can be difficult for the large language model to perform natively. Non-English languages can work much worse, and to a large extent, this is due to tokenization. Sometimes LLMs are bad at simple arithmetic, which can also be traced to tokenization. GPT-2 specifically would have had quite a bit more issues with Python than future versions of it due to tokenization. 

Maybe you've seen weird warnings about trailing whitespace. This is a tokenization issue. If you had asked GPT earlier about "solid gold Magikarp" and what it is, you would see the LLM go totally crazy and start going off on a completely unrelated tangent topic. Maybe you've been told to use YAML over JSON in structured data. All of that has to do with tokenization. Tokenization is at the heart of many issues. I will loop back around to these at the end of the video but for now let me just skip over it a bit.

在我们深入研究代码之前，我想先让你大致了解一下分词（tokenization）带来的一些复杂性。我希望确保我们充分理解为什么要做这些工作，以及为什么这个过程如此棘手。分词是大语言模型（Large Language Model）中许多异常现象的根源。我强烈建议你不要低估它的重要性。

许多看似只与神经网络架构或大语言模型（Large Language Model, LLM）本身相关的问题，实际上是由分词（tokenization）引起的，并且从根本上可以追溯到分词。例如，如果你注意到大语言模型在处理拼写任务时表现不佳，这通常就是由分词问题导致的。对于大语言模型来说，即使是简单的字符串处理也可能难以直接完成。非英语语言在模型中的表现往往更差，很大程度上也是因为分词问题。有时，大语言模型在进行简单算术运算时会出错，这同样可以追溯到分词问题。特别是 GPT-2，由于其分词方式的限制，在处理 Python 代码时比后续版本遇到了更多的困难。

也许你曾经遇到过关于尾随空格的奇怪警告。这其实是一个分词（tokenization）的问题。举个例子，如果你早些时候问过 GPT（一种大语言模型）关于「实心金色鲤鱼王」是什么，你可能会发现这个大语言模型（LLM）完全「失控」，开始谈论一些完全不相关的话题。再比如，在处理结构化数据时，你可能被建议使用 YAML 而非 JSON 格式。这些问题的根源都与分词有关。

分词实际上是许多问题的核心。虽然我们稍后会更详细地讨论这些问题，但现在让我们先略过这个话题，继续往下说。

Let's go to the web app tiktokenizer.versal.app. What I like about this web app is that tokenization is running live in your browser in JavaScript. You can just type "hello world" here and the whole string retokenizes. On the left is the string you put in. On the right we're currently using the GPT-2 tokenizer. We see that this string is tokenizing into 300 tokens, shown explicitly in different colors for every single token.

For example, the word "tokenization" became two tokens, 30,642 and 1,634. The token "space is" is token 318. Be careful, on the bottom you can show whitespace. Keep in mind that there are spaces and "\n" new line characters in here, but you can hide them for clarity. The token "space The" is 262, etc. Notice that the space is part of that token chunk.

This is how our English sentence broke up and that seems all well and good. Now I put in some arithmetic. We see the token "127 plus" and then token 6, space, 6, followed by 77. What's happening here is that 127 is feeding in as a single token into the large language model but the number 677 will actually feed in as two separate tokens. The large language model has to take account of that and process it correctly in its network.

804 will be broken up into two tokens and it's all completely arbitrary. Here's another example of four digit numbers and they break up in a way that is totally arbitrary. Sometimes you have multiple digits as a single token, sometimes you have individual digits as many tokens. It's all pretty arbitrary and coming out of the tokenizer.

让我们来看看 tiktokenizer.versel.app 这个网页应用。我特别喜欢这个应用的一个特点：它可以在你的浏览器中通过 JavaScript 实时进行分词（tokenization）。你只需在输入框中输入「hello world」，整个字符串就会立即重新分词。在页面的左侧是你输入的字符串，右侧则显示了当前使用 GPT-2 分词器的分词结果。我们可以看到，这个字符串被分解成了 300 个 token（词元），每个 token 都用不同的颜色清晰地标示出来。

[Tiktokenizer](https://tiktokenizer.vercel.app/)

举个例子，「tokenization」这个词被分成了两个 token，分别是 30,642 和 1,634。「space is」这个 token 的编号是 318。值得注意的是，在页面底部你可以选择显示空白字符。这里面包含了空格和「\n」换行符，但为了便于阅读，你可以选择隐藏它们。再比如，「space The」这个 token 的编号是 262，等等。有趣的是，你会发现空格也是这个 token 块的一部分。

这个工具帮助我们直观地理解了大语言模型是如何将文本分解成一个个 token 的。这个过程对于模型理解和处理文本至关重要，因为模型就是通过这些 token 来学习和生成文本的。

这就是我们的英语句子被拆分的方式，看起来一切正常。现在让我们来看看一些数学运算的例子。我们可以看到「127 plus」是一个 token（词元），然后是 6、空格、6，接着是 77。这里有趣的是，127 作为一个单独的 token 输入到大语言模型中，而数字 677 实际上会被拆分成两个独立的 token。大语言模型需要在处理过程中考虑这种情况，以确保正确理解和处理这些数字。

数字 804 会被拆分成两个 token，这种拆分方式完全是随机的。这里还有一个四位数的例子，它们的拆分方式也是完全随机的。有时候，多个数字会被组合成一个 token，有时候单个数字又会被拆分成多个 token。这种看似随机的拆分方式其实是由分词器（tokenizer）决定的，而分词器是大语言模型处理输入文本的第一步。

Here's another example. We have the string "egg" and you see that this became two tokens. But for some reason, when I say "I have an egg", when it's "space egg", it's a single token. Just "egg" by itself in the beginning of a sentence is two tokens, but here "space egg" is suddenly a single token for the exact same string.

Lowercase "egg" turns out to be a single token and notice that the color is different, so this is a different token. This is case sensitive and of course uppercase "egg" would also be different tokens. Again this would be two tokens arbitrarily. 

So for the same concept "egg", depending on if it's in the beginning of a sentence, at the end of a sentence, lowercase, uppercase, or mixed, all this will result in very different tokens and IDs. The language model has to learn from raw data, from all the internet text that it's going to be training on, that these are actually all the exact same concept. It has to group them in the parameters of the neural network and understand, just based on the data patterns, that these are all very similar, maybe not exactly similar, but very very similar.

让我们来看另一个例子。假设我们有单词「egg」，你会发现它被分割成了两个 token（标记）。但有趣的是，当我说「I have an egg」这个短语时，其中的「空格 + egg」却被视为一个单独的 token。这就出现了一个有趣的现象：单独的「egg」在句子开头是两个 token，但在前面加上空格后，完全相同的字符串「egg」却突然变成了一个 token。

再来看小写的「egg」，你会发现它是一个单独的 token。注意观察，它的颜色与之前的例子不同，这说明它是一个不同的 token。这里我们引入了一个重要概念：token 的划分是大小写敏感的。这意味着大写的「EGG」也会被识别为不同的 token。再次强调，大写的「EGG」也会被任意地分割成两个 token。

这个例子展示了在自然语言处理中，token 的划分可能会因上下文、大小写和位置等因素而变化，这种复杂性正是语言模型需要处理的挑战之一。

因此，对于同一个概念「egg」，无论它出现在句子开头、句子结尾，或者以小写、大写或混合大小写形式出现，都会产生非常不同的词元（tokens）和 ID。语言模型必须从原始数据中学习，即从它将要训练的所有互联网文本中理解，这些实际上都代表着完全相同的概念。模型需要在神经网络的权重中对这些表示进行分组，并仅基于数据模式来理解它们之间的关系。虽然这些表示可能不是完全等同，但模型需要认识到它们之间存在着极高的相似性。

After the demonstration, I have an introduction from OpenAI's ChatGPT in Korean. 만났어, 반가워요, etc. This is in Korean and the reason I put this here is because you'll notice that non-English languages work slightly worse in ChatGPT. Part of this is because the training dataset for ChatGPT is much larger for English than for everything else. But the same is true not just for the large language model itself, but also for the tokenizer. 

When we train the tokenizer, there's a training set as well and there's a lot more English than non-English. What ends up happening is that we're going to have a lot more longer tokens for English. If you have a single sentence in English and you tokenize it, you might see that it's 10 tokens or something like that. But if you translate that sentence into say Korean or Japanese or something else, you'll typically see the number of tokens used is much larger. That's because the chunks here are a lot more broken up. We're using a lot more tokens for the exact same thing. 

What this does is bloat up the sequence length of all the documents. You're using up more tokens and then in the attention of the transformer, when these tokens try to attend to each other, you are running out of context in the maximum context length of that transformer. Basically, all the non-English text is stretched out from the perspective of the transformer and this has to do with the training set used for the tokenizer and the tokenization itself. It will create much bigger tokens and larger groups in English and will have a lot of little boundaries for all the other non-English text. If we translated this into English it would be significantly fewer tokens.

在之前的演示之后，我想谈谈 OpenAI 的 ChatGPT 在处理韩语时的表现。比如，ChatGPT 可以理解并回应一些基本的韩语问候语，如「만났어」（见到你了）、「반가워요」（很高兴见到你）等。我在这里提到韩语是因为你会发现 ChatGPT 在处理非英语语言时的性能稍逊一筹。造成这种情况的部分原因是 ChatGPT 的训练数据集中，英语数据的数量远远超过其他语言。然而，这种性能差异不仅存在于大语言模型（Large Language Model）本身，还存在于分词器（tokenizer）中。分词器是将文本分割成小单元（称为 token）的工具，这是语言模型处理文本的第一步。

在训练分词器（tokenizer）时，我们使用的训练集中英语内容远多于其他语言。这导致了一个有趣的现象：英语文本往往会被切分成更长的 token。举个例子，如果你对一个英语句子进行分词，可能会得到大约 10 个 token。但是，如果你将同一个句子翻译成韩语、日语或其他语言，你会发现所需的 token 数量大大增加。这是因为在非英语语言中，文本被分割成了更小的片段，导致我们需要更多的 token 来表示相同的内容。

这种现象会导致文档的序列长度膨胀。使用更多的 token 意味着在 Transformer 模型的注意力机制中，当这些 token 需要相互关注时，很容易就会达到 Transformer 的最大上下文长度限制。从 Transformer 模型的角度来看，所有非英语文本都被「拉长」了。这个问题的根源在于分词器的训练集和分词过程本身。对于英语，分词器倾向于创建更大的 token 和更大的词组；而对于非英语文本，则会产生许多小的边界。如果我们将非英语文本翻译成英语，所需的 token 数量会显著减少。

The final example I have here is a little snippet of Python for doing FizzBuzz. What I'd like you to notice is how all these individual spaces are separate tokens, token 220. So 220, 220, 220, 220. Then "space if" is a single token. What's going on here is that when the transformer is going to consume or try to create this text, it needs to handle all these spaces individually. They all feed in one by one into the entire transformer in the sequence. This is extremely wasteful to tokenize it in this way. 

As a result, GPT-2 is not very good with Python and it's not anything to do with coding or the language model itself, it's just that if you use a lot of indentation using space in Python like we usually do, you just end up bloating out all the text. It's separated across way too much of the sequence and we are running out of the context length in the sequence. That's roughly speaking what's happening. We're being way too wasteful. We're taking up way too much token space.

We can also scroll up here and change the tokenizer. Note that the GPT-2 tokenizer creates a token count of 300 for this string here. We can change it to CL100K base, which is the GPT-4 tokenizer. We see that the token count drops to 185. For the exact same string we are now roughly halving the number of tokens. Roughly speaking, this is because the number of tokens in the GPT-4 tokenizer is roughly double that of the GPT-2 tokenizer. We went from roughly 50k to roughly 100k. 

You can imagine that this is a good thing because the same text is now squished into half as many tokens, so this is a lot denser input to the transformer. In the transformer, every single token has a finite number of tokens before it that it's going to pay attention to. What this is doing is we're roughly able to see twice as much text as context for what token to predict next because of this change. 

But of course, just increasing the number of tokens is not strictly better infinitely because as you increase the number of tokens, your embedding table is getting a lot larger. Also, at the output we are trying to predict the next token and there's the softmax there which grows as well. We're going to go into more detail on this later. There's some kind of sweet spot somewhere where you have a "just right" number of tokens in your vocabulary, where everything is appropriately dense and still fairly efficient.

One thing I'd like you to note specifically for the GPT-4 tokenizer is that the handling of the whitespace for Python has improved a lot. You see that here these four spaces are represented as one single token, and the three spaces here. Seven spaces were all grouped into a single token. We're being a lot more efficient in how we represent Python. This was a deliberate choice made by OpenAI when they designed the GPT-4 tokenizer. They group a lot more whitespace into a single character. This densifies Python and therefore we can attend to more code before it when we're trying to predict the next token in the sequence. The improvement in Python coding ability from GPT-2 to GPT-4 is not just a matter of the language model and the architecture and details of the optimization, but a lot of the improvement is also coming from the design of the tokenizer and how it groups characters into tokens.

最后，我想用一个 Python 代码片段来说明 fizzbuzz 问题，以此展示分词的另一个有趣现象。请注意观察，在这个代码中，所有的单个空格都被识别为独立的 token，其编号都是 220。所以我们看到的是：220、220、220、220。而「space if」（空格加上 if）则被识别为一个完整的 token。这意味着当 Transformer 模型处理或生成这段代码时，它需要单独处理每一个空格。这些空格会一个接一个地输入整个 Transformer 序列。显然，这种分词方式非常低效。

基于上述原因，GPT-2 在处理 Python 代码方面表现不佳。这并非源于编码能力或语言模型本身的局限，而是由于 Python 通常使用大量的空格进行缩进，这导致文本被过度膨胀。在序列中，这些空格被分散得过于分散，很快就会耗尽 Transformer 模型的上下文长度限制。简而言之，这种做法效率低下，占用了过多的 token 空间。

我们可以通过切换到不同的分词器来改善这种情况。让我们看一个例子：GPT-2 的分词器将一个特定的字符串切分成了 300 个 token。如果我们将分词器更换为 GPT-4 使用的 CL100K base，同样的字符串只需要 185 个 token。这意味着，对于相同的文本，token 数量大约减少了一半。这主要是因为 GPT-4 的分词器词汇量（大约 100k）是 GPT-2 分词器（大约 50k）的两倍。

这种变化带来了显著的好处。相同的文本被压缩成了更少的 token，为 Transformer 模型提供了更密集的输入。在 Transformer 中，每个 token 能够关注的前序 token 数量是有限的。通过这种改进，模型能够在预测下一个 token 时看到大约两倍的上下文信息。

然而，增加词汇量并非总是更好。随着词汇量的增加，模型的嵌入表（embedding table）会变得更大，输出层的 softmax 计算也会变得更复杂。我们将在后续讨论中详细探讨这一点。实际上，存在一个最优的词汇量，在这个点上，模型既能保持适当的密集度，又能维持较高的效率。

值得特别注意的是，GPT-4 的分词器在处理 Python 代码的空白字符方面有了显著改进。例如，连续的四个空格被表示为一个单独的 token，三个空格同样如此。甚至七个连续的空格也被压缩成一个 token。这大大提高了 Python 代码表示的效率。这是 OpenAI 在设计 GPT-4 分词器时经过精心考虑的结果。通过将更多的空白字符组合成单个 token，Python 代码的表示变得更加紧凑。这意味着在预测序列中的下一个 token 时，模型可以考虑更多的代码上下文。因此，从 GPT-2 到 GPT-4 在 Python 编码能力上的提升，不仅仅来自语言模型、架构和优化细节的改进，很大程度上也得益于分词器设计的优化。

#### 02

Okay, so let's now start writing some code. Remember what we want to do - we want to take strings and feed them into language models. For that, we need to somehow tokenize strings into some integers in a fixed vocabulary, and then we will use those integers to make a lookup into a lookup table of vectors and feed those vectors into the transformer as input. 

The reason this gets a little tricky, of course, is that we don't just want to support the simple English alphabet. We want to support different kinds of languages. This is "annyeonghaseyo" in Korean, which is "hello". We also want to support many kinds of special characters that we might find on the internet, for example, emojis. So how do we feed this text into transformers?

现在，让我们开始编写一些代码来实现这个过程。我们的目标是将字符串输入到语言模型中。为此，我们需要先将字符串转换成固定词汇表中的整数序列，然后使用这些整数在嵌入表中查找对应的向量，最后将这些向量作为输入送入 Transformer 模型。

这个任务之所以复杂，是因为我们不仅要支持简单的英语字母表，还要能够处理各种不同的语言。例如，韩语中的「annyeonghaseyo」（意为「你好」）。此外，我们还需要支持在互联网上常见的各种特殊字符，如表情符号。那么，我们该如何将这些多样化的文本输入到 Transformer 模型中呢？

Well, what is this text anyway in Python? If you go to the documentation of a string in Python, you can see that strings are immutable sequences of Unicode code points. Okay, what are Unicode code points? We can go to Wikipedia. Unicode code points are defined by the Unicode consortium as part of the Unicode standard. This is really just a definition of roughly 150,000 characters right now, and roughly speaking, what they look like and what integers represent those characters. This is 150,000 characters across 161 scripts as of right now. 

If you scroll down, you can see that the standard is very much alive. The latest standard 15.1 is from September 2023. Basically, this is just a way to define lots of types of characters, like for example all these characters across different scripts.

The way we can access the Unicode code point given a single character is by using the ORD function in Python. For example, I can pass in ORD and I can see that for the single character "H", the Unicode code point is 104. But this can be arbitrarily complicated. We can take for example our emoji here and we can see that the code point for this one is 128,000. Or we can take "un" and this is 50,000. 

Keep in mind you can't plug in strings here because this doesn't have a single code point. It only takes a single Unicode code point character and tells you its integer. In this way we can look up all the characters of this specific string and their code points. So ord(x) for x in this string and we get this encoding here.

在 Python 中，文本实际上是以字符串的形式存在的。如果我们查看 Python 文档，会发现字符串被定义为不可变的 Unicode 码点（code points）序列。那么，什么是 Unicode 码点呢？根据维基百科的解释，Unicode 码点是由 Unicode 联盟作为 Unicode 标准的一部分制定的。简单来说，这是一个包含约 150,000 个字符的定义集合，规定了这些字符的外观以及它们对应的整数值。截至目前，这个标准涵盖了 161 种不同的文字系统。

值得注意的是，Unicode 标准一直在不断更新。最新的 15.1 版本发布于 2023 年 9 月。这个标准的主要作用是定义各种类型的字符，包括不同文字系统中的字符。

在 Python 中，我们可以使用 ord() 函数来获取单个字符的 Unicode 码点。例如，ord('H') 会返回 104，这就是字母「H」的 Unicode 码点。对于更复杂的字符，如表情符号，其码点可能会更大，比如 128,000。需要注意的是，ord() 函数只能处理单个字符，不能直接处理字符串。

Now see here the raw code points already have integers. So why can't we simply just use these integers and not have any tokenization at all? Why can't we just use this natively as is and just use the code point? Well, one reason for that, of course, is that the vocabulary in that case would be quite long. In this case for Unicode, this is a vocabulary of 150,000 different code points. But more worryingly than that, I think the Unicode standard is very much alive and it keeps changing. It's not kind of a stable representation necessarily that we may want to use directly. For those reasons, we need something a bit better.

To find something better, we turn to encodings. If we go to the Wikipedia page here, we see that the Unicode consortium defines three types of encodings: UTF-8, UTF-16, and UTF-32. These encodings are the way by which we can take Unicode text and translate it into binary data, or byte streams. UTF-8 is by far the most common.

This is the UTF-8 page. This Wikipedia page is actually quite long, but what's important for our purposes is that UTF-8 takes every single code point and translates it to a byte stream. This byte stream is between one to four bytes, so it's a variable length encoding. So depending on the Unicode point, according to the schema, you're going to end up with between one to four bytes for each code point. 

On top of that, there's UTF-16 and UTF-32. UTF-32 is nice because it is fixed length instead of variable length but it has many other downsides as well. The full spectrum of pros and cons of all these encodings are beyond the scope of this video. I'd just like to point out that I enjoyed this blog post and this blog post at the end of it also has a number of references that can be quite useful. One of them is the "UTF-8 Everywhere" manifesto and this manifesto describes the reason why UTF-8 is significantly preferred and a lot nicer than the other encodings and why it is used a lot more prominently on the internet. One of the major advantages, just to give you a sense, is that UTF-8 is the only one of these that is backwards compatible to the much simpler ASCII encoding of text, but I'm not going to go into the full detail in this video.

那么，既然这些码点已经是整数了，为什么我们不直接使用它们，而要进行分词呢？主要有两个原因：首先，如果直接使用 Unicode 码点，词汇表的规模将达到 150,000，这是相当庞大的。其次，Unicode 标准本身在不断演进，这意味着直接使用码点可能会导致表示方式的不稳定。因此，我们需要一种更优的方法。

为了解决这个问题，我们需要引入编码的概念。Unicode 联盟定义了三种主要的编码方式：UTF-8、UTF-16 和 UTF-32。这些编码方式可以将 Unicode 文本转换为二进制数据或字节流。其中，UTF-8 是最为广泛使用的编码方式。

UTF-8 的特点是它使用可变长度的编码，将每个 Unicode 码点转换为 1 到 4 个字节的序列。相比之下，UTF-32 虽然使用固定长度编码，但也有其他方面的缺点。关于这些编码方式的详细优缺点分析超出了本次讨论的范围，但我推荐阅读一些相关的博客文章，特别是「UTF-8 Everywhere」宣言，它详细解释了为什么 UTF-8 在互联网上如此受欢迎。UTF-8 的一个主要优势是它向后兼容更简单的 ASCII 编码，这使得它在处理英文文本时特别高效。

[UTF-8 Everywhere](http://utf8everywhere.org/)

[UTF-8 遍地开花](http://utf8everywhere.org/zh-cn)

总的来说，理解文本编码对于处理多语言文本和设计高效的自然语言处理系统至关重要。虽然直接使用 Unicode 码点看似简单，但采用合适的编码方式如 UTF-8 可以在保持灵活性的同时提高效率。

Suffice to say that we like the UTF-8 encoding and let's try to take the string and see what we get if we encode it into UTF-8. The string class in Python actually has .encode() and you can give it the encoding which is say UTF-8. Now what we get out of this is not very nice because this is the bytes, it's a bytes object and it's not very nicely printed. So I personally like to take it through a list because then we actually get the raw bytes of this encoding. So this is the raw bytes that represent this string according to the UTF-8 encoding.

We can also look at UTF-16, we get a slightly different byte stream and here we start to see one of the disadvantages of UTF-16. You see how we have 0 something, 0 something, 0 something. We're starting to get a sense that this is a bit of a wasteful encoding. And indeed, for simple ASCII characters or English characters here, we just have the structure of 0 something, 0 something, and it's not exactly nice. Same for UTF-32. When we expand this, we can start to get a sense of the wastefulness of this encoding for our purposes. You see a lot of zeros followed by something, and so this is not desirable.

Suffice it to say that we would like to stick with UTF-8 for our purposes. However, if we just use UTF-8 naively, these are byte streams. So that would imply a vocabulary length of only 256 possible tokens. But this vocabulary size is very, very small. What this is going to do if we just were to use it naively is that all of our text would be stretched out over very, very long sequences of bytes.

我们普遍认为 UTF-8 编码是一种优秀的字符编码方式。现在，让我们尝试将一个字符串编码成 UTF-8 格式，看看会得到什么结果。在 Python 中，字符串对象（string object）实际上有一个 encode() 方法，你可以指定编码方式，比如 UTF-8。然而，直接使用这个方法得到的结果可能不太直观，因为它会返回一个字节对象（bytes object），其打印输出并不便于阅读。因此，我个人喜欢将其转换为列表形式。这样做的好处是，我们可以清楚地看到编码后的原始字节值。通过这种方法，我们就能得到根据 UTF-8 编码规则表示该字符串的原始字节序列。这些原始字节直观地展示了字符串在 UTF-8 编码下的实际存储形式。

我们也可以看看 UTF-16 编码。在 UTF-16 中，我们会得到一个略有不同的字节流，这里我们开始看到 UTF-16 的一个缺点。你会注意到字节流中出现了很多类似「0x00 + 某个值」的模式。这让我们开始意识到这种编码方式在某些情况下可能会造成空间浪费。事实上，对于简单的 ASCII 字符或英文字符，UTF-16 编码会产生「0x00 + 字符值」的结构，这在存储和传输效率上并不理想。UTF-32 编码的情况甚至更加明显。当我们展开 UTF-32 编码的字节流时，我们可以更清楚地看到这种编码方式对于某些用途来说的浪费程度。你会看到大量的零字节后面跟着有效字符的字节，这种模式在数据压缩和存储效率方面都不是最优选择。

简而言之，我们倾向于在我们的应用中继续使用 UTF-8 编码。然而，如果我们简单地使用 UTF-8，我们实际上是在处理字节流。这意味着我们的词汇表（vocabulary）大小将仅限于 256 个可能的标记（token）。这个词汇量显然是非常小的。如果我们不加考虑地直接使用这种方法，会导致我们的所有文本被转换成极长的字节序列。

这种方法的问题在于，它会大大增加文本的长度，因为每个字符都需要用多个字节来表示。这不仅会增加处理时间，还会降低模型的效率。因此，我们需要找到一种更优化的方法来处理文本数据，以便在保持 UTF-8 编码优势的同时，也能提高模型的处理效率。

What this does is that certainly the embedding table is going to be tiny, and the prediction at the top of the final layer is going to be very tiny, but our sequences are very long. Remember that we have pretty finite context lengths in the attention that we can support in a transformer for computational reasons. We only have as much context length, but now we have very, very long sequences, and this is just inefficient. It's not going to allow us to attend to sufficiently long text before us for the purposes of the next token prediction task. 

So we don't want to use the raw bytes of the UTF-8 encoding. We want to be able to support larger vocabulary size that we can tune as a hyperparameter, but we want to stick with the UTF-8 encoding of these strings. So what do we do? Well, the answer, of course, is we turn to the byte pair encoding algorithm, which will allow us to compress these byte sequences to a variable amount. We'll get to that in a bit.

I just want to briefly speak to the fact that I would love nothing more than to be able to feed raw byte sequences into language models. In fact, there's a paper about how this could potentially be done from somewhere last year. Now, the problem is you actually have to go in and you have to modify the transformer architecture because, as I mentioned, you're going to have a problem where the attention will start to become extremely expensive because the sequences are so long. 

In this paper they propose kind of a hierarchical structuring of the transformer that could allow you to just feed in raw bytes. At the end they say "together these results establish the viability of tokenization free autoregressive sequence modeling at scale". So tokenization free would indeed be amazing. We would just feed byte streams directly into our models but unfortunately I don't know that this has really been proven out yet by sufficiently many groups and at sufficient scale. Something like this at one point would be amazing and I hope someone comes up with it.

[[2305.07185] MEGABYTE: Predicting Million-byte Sequences with Multiscale Transformers](https://arxiv.org/abs/2305.07185)

But for now we have to come back and we can't feed this directly into language models. We have to compress it using the BytePair encoding algorithm. So let's see how that works.

这种做法会导致嵌入表（embedding table）和最终层顶部的预测变得非常小，但我们的序列却变得很长。需要注意的是，由于计算资源的限制，我们在 Transformer 中能够支持的注意力机制（attention）的上下文长度是有限的。尽管我们只有固定的上下文长度，但现在我们却面对着非常长的序列，这种情况是非常低效的。因为对于下一个 token 的预测任务来说，这种方法无法让模型有效地关注到足够长的前文信息。

因此，我们不打算直接使用 UTF-8 编码的原始字节。我们希望能够支持更大的词汇表大小，并将其作为一个可调整的超参数，但同时我们也想继续使用这些字符串的 UTF-8 编码。那么，我们该如何解决这个问题呢？答案就是采用字节对编码（byte pair encoding）算法。这种算法能够让我们将字节序列压缩到可变长度，从而实现我们的目标。关于这个算法的具体细节，我们将在稍后的部分进行详细讨论。

我想简要谈谈一个我非常感兴趣的想法：将原始字节序列直接输入到语言模型中。实际上，去年就有一篇论文探讨了这种方法的可能性。然而，这个想法面临着一个挑战：我们需要修改 Transformer 架构。正如我之前提到的，由于输入序列会变得非常长，这可能导致注意力机制（attention mechanism）的计算成本急剧增加。

这里的「原始字节序列」指的是未经任何预处理的数据，而「注意力机制」是 Transformer 模型中的一个关键组件，用于处理输入序列中的依赖关系。当序列变长时，注意力机制需要处理的信息量会呈指数级增长，从而大大增加了计算复杂度。

这篇论文提出了一种 Transformer 模型的层次化结构，这种结构有望实现直接输入原始字节数据的功能。论文最后总结道：「这些研究结果共同证明了大规模无词元化（tokenization-free）自回归序列建模的可行性。」这里的「无词元化」指的是不需要将输入文本分割成单词或子词的过程，而「自回归序列建模」是指模型根据先前的输出来预测序列中的下一个元素。如果真能实现无词元化，那将是一个巨大的突破。这意味着我们可以直接将字节流输入到模型中，而不需要预处理。然而，遗憾的是，这项技术目前还没有被足够多的研究团队在大规模应用中得到充分验证。尽管如此，这种方法的潜力是巨大的，我衷心希望有研究者能够在未来实现它。

但就目前而言，我们还是得回到现实。我们还不能直接将原始数据输入到语言模型中，而是需要使用 BytePair 编码（BytePair encoding）算法来压缩数据。接下来，让我们来看看这个算法是如何工作的。

As I mentioned, the BytePair encoding algorithm is not all that complicated and the Wikipedia page is actually quite instructive as far as the basic idea goes. What we're doing is we have some kind of input sequence, like for example here we have only four elements in our vocabulary: a, b, c and d. And we have a sequence of them. 

Instead of bytes, let's say we just have a vocabulary cap size of four. This sequence is too long, we'd like to compress it. So what we do is that we iteratively find the pair of tokens that occur the most frequently and then once we've identified that pair, we replace that pair with just a single new token that we append to our vocabulary.

So for example here, the byte pair AA occurs most often, so we mint a new token. Let's call it capital Z, and we replace every single occurrence of AA by Z. So now we have two Zs here. Here we took a sequence of 11 characters with vocabulary size 4, and we've converted it to a sequence of only 9 tokens, but now with a vocabulary of 5, because we have a fifth vocabulary element that we just created, and it's Z, standing for concatenation of AA. 

And we can, again, repeat this process. We again look at the sequence and identify the pair of tokens that are most frequent. Let's say that that is now AB. Well, we are going to replace AB with a new token that we mint, called Y. So Y becomes AB, and then every single occurrence of AB is now replaced with Y. So we end up with this.

Now we only have one, two, three, four, five, six, seven characters in our sequence but we have not just four vocabulary elements or five but now we have six. And for the final round we again look through the sequence, find that the phrase ZY or the pair ZY is most common and replace it one more time with another character, let's say X. So X is ZY and we replace all occurrences of ZY and we get this following sequence.

So basically after we have gone through this process, instead of having a sequence of 11 tokens with a vocabulary length of 4, we now have a sequence of 1, 2, 3, 4, 5 tokens, but our vocabulary length now is 7. In this way we can iteratively compress our sequence as we mint new tokens.

In the exact same way, we start out with byte sequences. So we have 256 vocabulary size but we're now going to go through these and find the byte pairs that occur the most and we're going to iteratively start minting new tokens, appending them to our vocabulary, and replacing things. In this way, we're going to end up with a compressed training dataset, and also an algorithm for taking any arbitrary sequence and encoding it using this vocabulary, and also decoding it back to strings. 

正如我之前提到的，BytePair 编码（BytePair encoding）算法其实并不复杂，维基百科上关于这个算法基本思想的介绍就已经相当清晰了。让我来简单解释一下这个算法的工作原理。想象一下，我们有一个输入序列，这个序列由词汇表中的元素组成。在这个例子中，我们的词汇表非常简单，只包含四个元素：a、b、c 和 d。现在，我们有一个由这些元素组成的长序列。

通常，我们会用字节来表示这些元素，但为了简化说明，我们假设我们的词汇表大小上限就是这四个元素。现在的问题是，这个序列太长了，我们想要压缩它以节省存储空间或提高处理效率。BytePair 编码的核心思想是这样的：我们反复寻找序列中最频繁出现的一对相邻标记（token）。找到后，我们就用一个新的单一标记替换这一对，并将这个新标记添加到我们的词汇表中。这个过程会不断重复，直到我们达到预设的词汇表大小或者无法找到频繁出现的配对为止。这种方法的好处是，它可以有效地捕捉到序列中频繁出现的模式，从而实现更高效的数据表示。这在自然语言处理等领域特别有用，因为它可以帮助我们发现单词中常见的子词单元，从而更好地处理未知词或罕见词。

让我们来看一个例子。假设字节对 AA 出现频率最高，那么我们就铸造（mint）一个新的 token。我们将其命名为大写 Z，然后用 Z 替换所有出现的 AA。这样一来，我们现在就有了两个 Z。在这个过程中，我们将一个长度为 11 个字符、词汇表大小为 4 的序列，转换成了一个只有 9 个 token 的序列。但现在词汇表大小变成了 5，因为我们刚刚创建了第五个词汇项，即代表 AA 拼接的 Z。

我们可以继续重复这个过程。再次检查序列，找出最频繁出现的 token 对。假设现在是 AB。那么，我们会铸造一个新的 token 来替换 AB，称之为 Y。这样，Y 就代表了 AB，然后我们用 Y 替换序列中所有出现的 AB。最终，我们得到了一个新的、更加压缩的序列。

现在，我们的序列中只有 7 个字符，但我们的词汇表不再只有 4 或 5 个元素，而是增加到了 6 个。在最后一轮处理中，我们再次遍历整个序列，发现字符对「ZY」出现得最频繁，于是我们用另一个新字符（比如说「X」）来替换它。这样，「X」就代表了「ZY」，我们把序列中所有的「ZY」都替换成「X」，得到了最终的序列。

通过这个过程，我们实现了一个有趣的转变：原本是一个包含 11 个 token（词元）、词汇表大小为 4 的序列，现在变成了一个只有 5 个 token、但词汇表大小为 7 的序列。这种方法允许我们在不断创建新 token 的同时，逐步压缩原始序列。

这个过程实际上是一种数据压缩技术，通过识别频繁出现的模式并用新的符号替换它们，我们可以用更少的空间来表示相同的信息。这种技术在自然语言处理和机器学习领域有广泛的应用，特别是在处理大规模文本数据时非常有用。

我们同样从字节序列开始。起初我们有 256 个词汇量，但接下来我们将遍历这些字节序列，找出出现频率最高的字节对。然后，我们会反复创建新的 token（标记），将它们添加到我们的词汇表中，并用它们替换原有内容。通过这种方式，我们最终会得到一个经过压缩的训练数据集。同时，我们还会得到一个算法，它可以将任意序列编码成这个词汇表中的 token，并能将这些 token 解码回原始字符串。

#### 03

So let's now implement all that. Here's what I did. I went to this blog post that I enjoyed and I took the first paragraph and copy pasted it here into text. So this is one very long line here.

To get the tokens, as I mentioned, we just take our text and we encode it into UTF-8. The tokens here at this point will be raw bytes, single stream of bytes. And just so that it's easier to work with, instead of just a bytes object, I'm going to convert all those bytes to integers and then create a list of it, just so it's easier for us to manipulate and work with in Python and visualize. 

Here I'm printing all that. So this is the original paragraph and its length is 533 code points. And then here are the bytes encoded in UTF-8 and we see that this has a length of 616 bytes at this point, or 616 tokens. The reason this is more is because a lot of these simple ASCII characters, or simple characters, they just become a single byte, but a lot of these Unicode, more complex characters, become multiple bytes, up to four, and so we are expanding that size.

现在让我们来实现这整个过程。我的做法是这样的：我找到了一篇我很喜欢的博客文章，然后将其第一段复制粘贴到了这里的文本中。所以你看到的是一行很长的文字。

为了获得 tokens（标记），正如我之前提到的，我们只需要将文本编码成 UTF-8 格式。此时的 tokens 将是一系列原始字节，形成一个连续的字节流。为了更方便处理，我不会直接使用字节对象（bytes object），而是将所有这些字节转换为整数，然后创建一个列表。这样做可以让我们在 Python 中更容易地操作、处理和可视化这些数据。

（注：UTF-8 是一种通用的字符编码方案，可以将文本中的字符转换为计算机可以处理的字节序列。将字节转换为整数列表可以让我们更直观地查看和操作这些数据，因为整数比原始字节更容易理解和处理。）

让我来解释一下我们刚才做的操作。首先，我们有一段原始文本，它包含了 533 个字符（在计算机术语中称为「代码点」）。接下来，我们将这段文本转换成了 UTF-8 编码的格式。转换后，我们发现这段文本占用了 616 个字节的存储空间。

你可能会问，为什么转换后的大小会增加呢？这是因为在 UTF-8 编码中，不同的字符会被转换成不同长度的字节序列。一些简单的字符，比如常见的 ASCII 字符，只需要一个字节就能表示。但是更复杂的 Unicode 字符，比如一些特殊符号或非英语字符，可能需要用到 2 到 4 个字节来表示。

这就解释了为什么同样一段文本，在 UTF-8 编码后会占用更多的存储空间。这种编码方式虽然增加了存储需求，但它能够支持更广泛的字符集，使得计算机能够处理各种语言和符号，这在我们这个全球化的数字世界中是非常重要的。

Now what we'd like to do as a first step of the algorithm is we'd like to iterate over here and find the pair of bytes that occur most frequently, because we're then going to merge it. If you are working along on a notebook on the side, then I encourage you to basically click on the link, find this notebook and try to write that function yourself. Otherwise, I'm going to come here and implement first the function that finds the most common pair.

OK, so here's what I came up with. There are many different ways to implement this, but I'm calling the function getStats. It expects a list of integers. I'm using a dictionary to keep track of basically the counts, and then this is a Pythonic way to iterate consecutive elements of this list, which we covered in a previous video. And then here I'm just keeping track of just incrementing by one for all the pairs.

So if I call this on all the tokens here, then the stats comes out here. This is the dictionary, the keys are these tuples of consecutive elements and this is the count. Just to print it in a slightly better way, this is one way that I like to do that where you... it's a little bit compound here so you can pause if you like, but we iterate all the items. The items() called on a dictionary returns pairs of key value and instead I create a list here of value key because if it's a value key list then I can call sort on it and by default Python will use the first element, which in this case will be value, to sort by if it's given tuples. And then reverse so it's descending and print that.

算法的第一步是遍历数据并找出出现频率最高的字节对（byte pair），因为我们接下来要对它们进行合并。如果你正在使用笔记本（notebook）跟随学习，我建议你点击链接找到相应的笔记本，然后尝试自己编写这个函数。如果你没有这样做，那么接下来我会在这里实现一个用于查找最常见字节对的函数。

这是我设计的一种实现方法。虽然有多种方式可以实现这个功能，但我选择将这个函数命名为 getStats。该函数接受一个整数列表作为输入参数。

在实现中，我使用了一个字典（dictionary）来统计出现的次数。然后，我采用了一种 Python 特有的方法来迭代列表中的连续元素对，这个技巧我们在之前的视频中已经介绍过。

具体来说，这段代码遍历列表中的每一对相邻元素，并在字典中记录每一对元素出现的次数。每遇到一对元素，就将其在字典中对应的计数加一。这种方法可以有效地统计列表中连续元素对的分布情况。

因此，如果我对这里的所有 token（tokens）执行这个操作，就会得到这里的统计结果。这是一个字典，其中键是连续元素组成的元组，值是对应的计数。为了更好地展示这些结果，我喜欢使用一种稍微复杂的方法 —— 你可以稍后仔细看看这段代码。

这种方法的核心是遍历字典的所有项。通常，在字典上调用 items() 方法会返回键值对。但在这里，我创建了一个值-键（value-key）的列表，而不是常见的键-值对。这样做的原因是，如果我们有一个值-键列表，就可以直接对其调用 sort 方法。默认情况下，当 Python 对元组列表进行排序时，会使用元组的第一个元素作为排序依据，在我们的情况下，这个元素就是值（即计数）。

最后，我们通过 reverse 参数将排序结果倒序，这样就得到了一个按计数降序排列的列表。然后我们打印出这个结果，就能清晰地看到最常出现的元素组合及其频率。

Basically it looks like 101, 32 was the most commonly occurring consecutive pair and it occurred 20 times. We can double check that that makes reasonable sense. If I just search 101, 32 then you see that these are the 20 occurrences of that pair. And if we'd like to take a look at what exactly that pair is, we can use chr, which is the opposite of ord in Python. We give it a Unicode code point, so 101 and 32, and we see that this is "e" and "space". Basically there's a lot of "e space" here, meaning that a lot of these words seem to end with "e". Here's "e space" as an example. There's a lot of that going on here, and this is the most common pair.

So now that we've identified the most common pair, we would like to iterate over the sequence. We're going to mint a new token with the ID of 256, right? Because these tokens currently go from 0 to 255. So when we create a new token, it will have an ID of 256. And we're going to iterate over this entire list. And every time we see 101,32, we're going to swap that out for 256. So let's implement that now and feel free to do that yourself as well.

从结果来看，101，32 这个数字对是最常出现的连续数字组合，总共出现了 20 次。我们可以通过一些方法来验证这个结果是否合理。如果我们直接搜索 101，32 这个组合，就能看到它确实出现了 20 次。

那么，这个数字对到底代表什么呢？在 Python 中，我们可以使用 chr 函数来查看。chr 函数是 ord 函数的反向操作，它可以将 Unicode 编码（也就是数字）转换为对应的字符。当我们输入 101 和 32 这两个数字时，得到的结果是「e」和「空格」字符。

这个发现很有意思：在我们的文本中，「e」后面跟着空格的情况非常多，这意味着有很多单词是以字母「e」结尾的。举个例子，「e 空格」就是这种模式。这种模式在文本中频繁出现，成为了最常见的字符对。

现在我们已经找到了最常见的 token 对，接下来我们要遍历这个序列。我们将创建一个新的 token，给它分配一个 ID 为 256。为什么是 256 呢？因为现有的 token ID 范围是从 0 到 255，所以 256 就是下一个可用的 ID。

接下来，我们将遍历整个列表。每当我们遇到 token 对「101，32」时，我们就用新创建的 ID 为 256 的 token 来替换它。这个过程实际上就是将两个 token 压缩成一个新的 token，这是 BPE 算法的核心步骤。

现在，让我们来实现这个过程。如果你正在跟随学习，也可以尝试自己动手实现这个步骤，这将有助于加深你对算法的理解。

So first I commented this just so we don't pollute the notebook too much. This is a nice way of, in Python, obtaining the highest ranking pair. We're basically calling the max on this dictionary stats and this will return the maximum key. And then the question is, how does it rank keys? You can provide it with a function that ranks keys and that function is just stats.get. Stats.get would basically return the value. And so we're ranking by the value and getting the maximum key. So it's 101 comma 32 as we saw.

Now to actually merge 101, 32, this is the function that I wrote but again there are many different versions of it. We're going to take a list of IDs and the pair that we want to replace and that pair will be replaced with the new index idx. 

Iterating ids, if we find the pair, swap it out for idx. So we create this new list and then we start at zero and then we go through this entire list sequentially from left to right. Here we are checking for equality at the current position with the pair. So here we are checking that the pair matches. 

Now here's a bit of a tricky condition that you have to append if you're trying to be careful, and that is that you don't want this here to be out of bounds at the very last position when you're on the rightmost element of this list, otherwise this would give you an out-of-bounds error. So we have to make sure that we're not at the very very last element, so this would be false for that.

If we find a match we append to this new list that replacement index and we increment the position by two, so we skip over that entire pair. But otherwise if we haven't found a matching pair we just sort of copy over the element at that position and increment by one and then return this.

Here's a very small toy example. If we have a list 5,6,6,7,9,1 and we want to replace the occurrences of 6,7 with 99 then calling this on that will give us what we're asking for. So here the 6,7 is replaced with 99. 

So now I'm going to uncomment this for our actual use case where we want to take our tokens, we want to take the top pair here and replace it with 256 to get tokens2. If we run this we get the following:

首先，我将这段代码注释掉了，以避免在 Jupyter Notebook 中产生过多无关输出。这里展示了一种在 Python 中获取字典中最高值对应键的巧妙方法。我们对名为 stats 的字典调用 max 函数，这会返回最大的键。那么，它是如何判断哪个键最大的呢？我们可以为 max 函数提供一个用于比较键的函数，在这里就是 stats.get。stats.get 函数会返回给定键的值。因此，我们实际上是在按值排序，并获取对应最大值的键。正如我们之前看到的，结果是键值对（101，32）。

接下来，为了实际合并键 101 和 32，我编写了一个函数。当然，实现这个功能的方法有很多种。这个函数接受两个参数：一个 ID 列表和我们想要替换的键值对。函数会用一个新的索引 idx 来替换这个键值对。

这个合并操作通常用于数据压缩或聚类算法中，可以将相似或相关的元素组合在一起，从而减少数据的复杂度或发现数据中的模式。

我们遍历列表中的元素 ID，如果找到匹配的一对元素，就用索引值（idx）替换它们。具体来说，我们先创建一个新的列表，然后从第一个元素（索引为 0）开始，从左到右依次检查整个列表。在每个位置，我们都会检查当前元素是否与我们要查找的对子匹配。

这里有一个需要特别注意的条件，那就是要避免在处理列表最后一个元素时发生越界错误。当我们检查到列表的最后一个元素时，如果不加限制，程序会试图访问不存在的下一个元素，从而导致越界错误。因此，我们需要增加一个判断条件，确保当前位置不是列表的最后一个元素。对于最后一个元素，这个条件将返回 false，从而避免了越界的问题。

如果我们找到一个匹配，我们会将该替换的索引添加到结果列表中，并将位置向前移动两步，这样就跳过了这对匹配的元素。如果没有找到匹配的配对，我们就只是将当前位置的元素复制到结果列表中，并将位置向前移动一步。最后返回这个结果列表。

让我们看一个简单的示例。假设我们有一个列表 5、6、6、7、9、1，我们想用 99 替换所有出现的 6、7 配对。调用这个函数后，我们就能得到想要的结果。在这个例子中，6、7 被替换成了 99。

现在，让我们回到我们实际的用例。我们要处理我们的 tokens，将其中出现频率最高的配对替换为 256，从而得到 tokens2。如果我们运行这段代码，我们会得到以下结果：

（注：这里应该会显示具体的运行结果，但原文中没有给出）

Recall that previously we had a length 616 in this list and now we have a length 596, right, so this decreased by 20 which makes sense because there are 20 occurrences. Moreover we can try to find 256 here and we see plenty of occurrences of it and moreover just to double check, there should be no occurrence of 101,32. So this is the original array, plenty of them, and in the second array there are no occurrences of 101,32. So we've successfully merged this single pair.

And now we just iterate this. So we are going to go over the sequence again, find the most common pair, and replace it. So let me now write a while loop that uses these functions to do this sort of iteratively. And how many times do we do it for? Well, that's totally up to us as a hyperparameter. The more steps we take, the larger will be our vocabulary and the shorter will be our sequence. And there is some sweet spot that we usually find works the best in practice. 

As an example, GPT-4 currently uses roughly a hundred thousand tokens and ballpark, those are reasonable numbers currently in state-of-the-art language models. So let me now write putting it all together and iterating these steps.

Okay now before we dive into the while loop I wanted to add one more cell here where I went to the blog post and instead of grabbing just the first paragraph or two, I took the entire blog post and I stretched it out in a single line. Basically just using longer text will allow us to have more representative statistics for the byte pairs and we'll just get more sensible results out of it because it's longer text.

So here we have the raw text, we encode it into bytes using the UTF-8 encoding, and then here as before we are just changing it into a list of integers in Python just so it's easier to work with instead of the raw bytes object. 

让我们回顾一下之前的情况：我们原本有一个长度为 616 的列表，现在这个列表的长度变成了 596。也就是说，列表长度减少了 20，这与我们观察到的 20 次出现次数相符。

此外，我们可以在新列表中寻找数字 256，会发现它出现了很多次。为了进一步验证我们的操作，我们应该确认数字对 101,32 已经不再出现在新列表中。

在原始数组中，我们可以看到很多 101,32 这样的数字对。而在处理后的新数组中，101,32 这个数字对已经完全消失了。

这些观察结果表明，我们已经成功地将目标数字对（101,32）合并为单个数字（256）。

现在，我们要反复执行这个过程。具体来说，我们会再次检查整个序列，找出出现最频繁的字符对，然后替换它。接下来，我要编写一个 while 循环，利用这些函数来重复执行这个过程。那么，我们应该重复多少次呢？这完全由我们自己决定，它是一个可调整的参数（超参数）。执行的步骤越多，我们的词汇表就越大，相应的，我们的序列就越短。在实际应用中，我们通常会找到一个效果最佳的平衡点。

举个例子，GPT-4 目前使用了大约十万个标记（token）。这个数量在当前最先进的语言模型中是很常见的。现在，让我把所有这些步骤整合在一起，开始循环执行这个过程。

好的，在我们深入研究 while 循环之前，我想在这里再添加一个代码单元。这次我访问了博客文章，但不是只获取前一两段，而是提取了整篇文章的内容，并将其转换成一行文本。基本上，使用更长的文本能让我们获得更有代表性的字节对统计数据，因为文本量更大，所以我们能得到更合理的结果。

在这里，我们有了原始文本，然后使用 UTF-8 编码将其转换成字节。接下来，我们像之前一样，将这些字节转换成 Python 中的整数列表。这样做比直接使用原始字节对象更方便处理。

And then this is the code that I came up with to actually do the merging in a loop. These two functions here are identical to what we had above. I only included them here just so that you have the point of reference here. So these two are identical.

And then this is the new code that I added. So the first thing we want to do is we want to decide on the final vocabulary size that we want our tokenizer to have. As I mentioned, this is a hyperparameter and you set it in some way depending on your best performance. So let's say for us we're going to use 276 because that way we're going to be doing exactly 20 merges. 20 merges because we already have 256 tokens for the raw bytes and to reach 276 we have to do 20 merges to add 20 new tokens.

Here, this is one way in Python to just create a copy of a list. I'm taking the tokens list and by wrapping it in a list, Python will construct a new list of all the individual elements. So this is just a copy operation. 

Then here, I'm creating a merges dictionary. This merges dictionary is going to maintain basically the child one, child two mapping to a new token. What we're going to be building up here is a binary tree of merges. But actually it's not exactly a tree because a tree would have a single root node with a bunch of leaves. 

For us, we're starting with the leaves on the bottom, which are the individual bytes. Those are the starting 256 tokens, and then we're starting to merge two of them at a time. And so it's not a tree, it's more like a forest as we merge these elements.

So for 20 merges we're going to find the most commonly occurring pair, we're going to mint a new token integer for it. So i here will start at 0, so we're going to start at 256. We're going to print that we're merging it and we're going to replace all the occurrences of that pair with the newly minted token. And we're going to record that this pair of integers merged into this new integer.

So running this gives us the following output. We did 20 merges and for example the first merge was exactly as before, the 101, 32 tokens merging into a new token 256. Now keep in mind that the individual tokens 101 and 32 can still occur in the sequence after merging. It's only when they occur exactly consecutively that that becomes 256 now. 

And in particular, the other thing to notice here is that the token 256, which is the newly minted token, is also eligible for merging. So here on the bottom the 20th merge was a merge of 256 and 259 becoming 275. So every time we replace these tokens they become eligible for merging in the next round of the iteration. That's why we're building up a small sort of binary forest instead of a single individual tree.

One thing we can take a look at as well is we can take a look at the compression ratio that we've achieved. In particular, we started off with this tokens list. So we started off with 24,000 bytes and after merging 20 times, we now have only 19,000 tokens. And so therefore, the compression ratio, simply just dividing the two, is roughly 1.27. So that's the amount of compression we're able to achieve of this text with only 20 merges. And of course the more vocabulary elements you add, the greater the compression ratio here would be.

接下来，我将展示一段代码，用于在循环中实际执行合并操作。首先，我们看到两个函数，它们与之前提到的完全相同。我在这里再次列出它们，是为了给大家一个参考。

然后是我新增的代码部分。我们要做的第一件事是确定分词器（tokenizer）的最终词汇表大小。如前所述，这是一个超参数（hyperparameter），你可以根据模型的最佳性能来设置它。在我们的例子中，我们选择使用 276 作为最终词汇表大小。这个数字的选择是有原因的：我们已经有 256 个表示原始字节的 token，要达到 276，我们需要进行 20 次合并操作，从而新增 20 个 token。

这里展示了一种在 Python 中创建列表副本的方法。我们取 tokens 列表（tokens list），通过将其包装在一个新的列表中，Python 会构建一个包含所有原始元素的新列表。这实际上就是一个简单的复制操作。

接下来，我创建了一个名为 merges 的字典（merges dictionary）。这个 merges 字典主要用于维护两个子元素到新 token 的映射关系。我们在这里要构建的是一个合并的二叉树结构（每个节点最多有两个子节点的树形结构）。不过，严格来说，它并不完全是一棵标准的树，因为传统的树结构通常有一个根节点连接着多个叶子节点。

在我们的情况中，我们是从底部的叶子节点开始的，这些节点代表单个字节。我们从最初的 256 个 tokens 开始（对应 256 个可能的字节值），然后每次合并其中的两个。因此，这个结构与其说是一棵树，不如说更像是一片森林 —— 我们在不断地合并这些元素，形成多个独立的结构，而不是一个单一的树形结构。

接下来，我们将进行 20 次合并操作。每次操作中，我们会找出最频繁出现的 token 对，并为其分配一个新的 token 整数值。这里的新 token 值将从 256 开始（因为 0-255 已被占用）。我们会打印出每次合并的信息，并用新创建的 token 替换原文中所有出现的该 token 对。同时，我们会记录下这对整数是如何合并成新的整数的。

运行这段代码后，我们得到了如下输出。在完成的 20 次合并中，第一次合并的结果与之前的例子相同：token 101 和 32 合并成了新的 token 256。需要注意的是，合并后，单独的 token 101 和 32 仍然可能在序列中出现。只有当它们恰好连续出现时，才会被替换为新的 token 256。

另外，这里还有一点特别值得注意：新生成的 token 256 也可以参与合并过程。例如，在图表底部我们可以看到，第 20 次合并操作就是将 token 256 和 259 合并成了 275。这意味着每次我们替换这些 token 后，它们在下一轮迭代中都有机会继续参与合并。正是因为这个原因，我们最终构建的是一个小型的「二元森林」（binary forest），而不是单一的树结构。这里的「二元森林」指的是由多个二叉树组成的数据结构，每次合并操作都可能创建新的树或者扩展现有的树。

我们还可以来看看我们 achieved 的压缩比。首先，我们从一个 token（词元）列表开始。最初，这个列表占用了 24,000 字节的空间。经过 20 次合并操作后，我们现在只有 19,000 个 token 了。因此，通过简单地将原始大小除以压缩后的大小，我们可以计算出压缩比大约为 1.27。

这意味着，仅仅通过 20 次合并操作，我们就能将这段文本压缩到原来大小的 78.7%（1/1.27）。压缩的好处是可以节省存储空间，加快数据传输速度。值得注意的是，如果我们增加更多的词汇元素（即进行更多次的合并操作），我们可以获得更高的压缩比。

这个例子展示了即使是简单的压缩技术也能带来显著的效果。在实际应用中，更复杂的压缩算法可以实现更高的压缩比，这在大规模数据处理和存储中特别有用。

Finally, so that's kind of like the training of the tokenizer, if you will. Now, one point that I wanted to make is that, and maybe this is a diagram that can help kind of illustrate, is that the tokenizer is a completely separate object from the large language model itself. So everything in this lecture, we're not really touching the LLM itself. We're just training the tokenizer. This is a completely separate pre-processing stage usually.

The tokenizer will have its own training set, just like a large language model has a potentially different training set. So the tokenizer has a training set of documents on which you're going to train the tokenizer. And then we're performing the byte pair encoding algorithm, as we saw above, to train the vocabulary of this tokenizer. 

So it has its own training set. It is a pre-processing stage that you would run a single time in the beginning and the tokenizer is trained using byte pair encoding algorithm. Once you have the tokenizer, once it's trained and you have the vocabulary and you have the merges, we can do both encoding and decoding.

最后，我们可以将上述过程理解为分词器的训练。在这里，我想强调一个重要的概念，可以用一个图表来说明：分词器是一个完全独立于大语言模型（Large Language Model，LLM）的组件。在本次讲座中，我们实际上并没有涉及 LLM 本身，而只是在讨论分词器的训练。这通常是一个完全独立的预处理阶段，用于为后续的模型训练做准备。

分词器有自己的训练集，这点类似于大语言模型，后者也有其（可能不同的）训练集。分词器的训练集由一系列文档组成，我们将在这些文档上训练分词器。具体来说，我们使用前面讨论过的字节对编码（Byte Pair Encoding）算法来训练分词器的词汇表。词汇表是分词器用来将文本切分成 token 的基础，它包含了模型可以直接识别的所有单词或子词单元。

因此，分词器（tokenizer）有自己的训练集。这是一个预处理阶段，你只需在开始时运行一次。分词器使用字节对编码（byte pair encoding）算法进行训练。一旦分词器训练完成，你就得到了词汇表和合并规则，之后我们就可以进行编码和解码了。

So these two arrows here, the tokenizer is a translation layer between raw text, which is as we saw the sequence of Unicode code points, it can take raw text and turn it into a token sequence and vice versa. It can take a token sequence and translate it back into raw text.

So now that we have trained a tokenizer and have these merges, we are going to turn to how we can do the encoding and the decoding step. If you give me text, here are the tokens and vice versa. If you give me tokens, here's the text. Once we have that, we can translate between these two realms and then the language model is going to be trained as a step two afterwards.

And typically in a sort of a state-of-the-art application, you might take all of your training data for the language model, and you might run it through the tokenizer and sort of translate everything into a massive token sequence. And then you can throw away the raw text, you're just left with the tokens themselves. And those are stored on disk, and that is what the large language model is actually reading when it's training on them. So that's one approach that you can take as a single massive pre-processing stage. 

Yeah, basically I think the most important thing I want to get across is that this is a completely separate stage. It usually has its own entire training set. You may want to have those training sets be different between the tokenizer and the large language model.

这里的两个箭头表示，分词器是原始文本和 token 序列之间的转换层。原始文本是 Unicode 码点的序列，分词器可以将原始文本转换为 token 序列，反之亦然。它可以将 token 序列转换回原始文本。简而言之，分词器就像一个双向翻译器，能够在人类可读的文本和机器可理解的 token 序列之间进行转换。这个过程对于文本处理和自然语言理解至关重要。

现在我们已经训练了一个分词器（tokenizer）并获得了这些合并规则（merges），接下来我们将关注如何执行编码（encoding）和解码（decoding）步骤。这个过程是双向的：如果你给我一段文本，我可以将其转换为相应的 token；反过来，如果你给我一系列 token，我也能将其还原为原始文本。一旦我们实现了这种双向转换能力，我们就可以在文本和 token 这两种表示形式之间自如地切换。这是很重要的一步，因为在此之后，我们才能进行语言模型的训练，这将是第二个阶段的工作。

在当前最尖端的应用中，通常会采取这样的做法：首先，我们会收集所有用于训练语言模型的数据，然后将这些数据通过分词器（tokenizer）处理，把所有内容转换成一个巨大的 token 序列。完成这一步后，我们就可以将原始文本舍弃，只保留这些 token。这些 token 会被存储在磁盘上，大语言模型（Large Language Model）在训练过程中实际上就是读取这些 token。这种方法可以看作是一个独立的大规模预处理阶段。

我想强调的最重要的一点是，这个预处理阶段是完全独立的。它通常有自己专门的训练集。而且，你可能会希望分词器和大语言模型使用不同的训练集。

So for example, when you're training the tokenizer, as I mentioned, we don't just care about the performance of English text. We care about many different languages. And we also care about code or not code. So you may want to look into different kinds of mixtures of different kinds of languages and different amounts of code and things like that. 

Because the amount of different language that you have in your tokenizer training set will determine how many merges of it there will be and therefore that determines the density with which this type of data sort of exists in the token space. Roughly speaking, intuitively, if you add some amount of data, say you have a ton of Japanese data in your tokenizer training set, then that means that more Japanese tokens will get merged, and therefore Japanese will have shorter sequences. And that's going to be beneficial for the large language model, which has a finite context length on which it can work on in the token space. So hopefully that makes sense.

举个例子，在训练分词器（tokenizer）时，正如我之前所说，我们不能仅仅关注英语文本的处理效果。实际上，我们需要考虑多种不同语言的处理能力。不仅如此，我们还要关注如何处理编程代码和非代码文本。因此，在训练过程中，你可能需要探索各种语言组合的混合文本，以及包含不同比例代码的数据集等各种情况。这样做的目的是为了确保分词器能够在各种复杂的实际应用场景中表现出色。

分词器（tokenizer）训练集中包含的不同语言种类数量，会影响词元（token）的合并次数，进而决定了这些语言数据在词元空间中的分布密度。简单来说，如果我们在分词器的训练数据中增加某种语言的数据量，比如加入大量的日语文本，那么更多的日语词元就会被合并。这样一来，日语文本在经过分词后会得到更短的序列。

对于大语言模型（Large Language Model）而言，这种做法是有利的。因为大语言模型在词元空间中能够处理的上下文长度是有限的，如果能用更少的词元表示相同的信息，就能在有限的上下文长度内处理更多的内容。

举个例子，假设我们的模型最多能处理 1000 个词元。如果日语文本平均每句话需要 50 个词元，那么模型一次只能处理 20 句话。但如果通过优化分词器，使得每句话平均只需要 25 个词元，那么同样的模型就能一次处理 40 句话，有效的延长了模型的「记忆力」。

总的来说，分词器训练集的语言构成对模型的性能有着深远的影响。通过合理设计训练集，我们可以优化模型对不同语言的处理能力，提高模型的整体效率。

We're now going to turn to encoding and decoding, now that we have trained a tokenizer. So we have our merges, and now how do we do encoding and decoding?

Okay, so let's begin with decoding, which is this arrow over here. Given a token sequence, let's go through the tokenizer to get back a Python string object, so the raw text. So this is the function that we'd like to implement. We're given the list of integers and we want to return a Python string. If you'd like, try to implement this function yourself. It's a fun exercise. Otherwise, I'm going to start pasting in my own solution.

So there are many different ways to do it. Here's one way. I will create a kind of pre-processing variable that I will call vocab. And vocab is a mapping or dictionary in Python from the token ID to the bytes object for that token. 

So we begin with the raw bytes for tokens from 0 to 255 and then we go in order of all the merges and we sort of populate this vocab list by doing an addition here. So this is basically the bytes representation of the first child followed by the second one. And remember, these are bytes objects. So this addition here is an addition of two bytes objects, just concatenation. So that's what we get here.

One tricky thing to be careful with, by the way, is that I'm iterating a dictionary in Python using dot items and it really matters that this runs in the order in which we inserted items into the merges dictionary. Luckily starting with Python 3.7 this is guaranteed to be the case but before Python 3.7 this iteration may have been out of order with respect to how we inserted elements into merges and this may not have worked, but we are using modern Python, so we're okay. 

现在我们已经训练好了分词器（tokenizer），接下来让我们来看看编码和解码的过程。我们已经得到了合并规则（merges），那么如何进行编码和解码呢？

让我们先从解码开始。解码的过程可以理解为将 token 序列转换回原始文本。具体来说，我们需要实现一个函数，该函数接收一个整数列表（代表 token 序列），然后返回一个 Python 字符串（即原始文本）。这是一个很有趣的练习，如果你想的话，可以先尝试自己实现这个函数。如果你准备好了，我们就来看看我的解决方案。

有多种方法可以实现这个功能。这里我将介绍其中一种方法。首先，我会创建一个预处理变量，称为词汇表（vocab）。在 Python 中，vocab 是一个映射或字典，用于将 token ID（token ID）映射到该 token 对应的字节对象（bytes object）。

我们从 0 到 255 的 token 的原始字节开始。这些数字代表了基本的 ASCII 字符集和扩展字符。然后，我们按照所有合并操作的顺序，通过执行加法操作来逐步填充这个 vocab 列表。这里的加法操作实际上是将第一个子项的字节表示与第二个子项的字节表示连接起来。需要注意的是，这些都是字节对象。因此，这里的加法操作实际上是两个字节对象的连接操作。通过这种方式，我们就得到了完整的词汇表。

顺便说一句，这里有一个需要特别注意的技术细节。我在 Python 中使用 `.items()` 方法迭代一个字典（dictionary），这个过程中，迭代顺序与我们向 `merges` 字典插入项目的顺序保持一致非常重要。

值得庆幸的是，从 Python 3.7 版本开始，字典迭代顺序就被保证与插入顺序一致。但在 Python 3.7 之前的版本中，这个迭代顺序可能与插入顺序不符，这可能会导致程序无法正常工作。不过，由于我们使用的是现代 Python 版本，所以不用担心这个问题。

And then here, given the IDs, the first thing we're going to do is get the tokens. So the way I implemented this here is I'm taking, I'm iterating over all the IDs, I'm using vocab to look up their bytes and then here this is one way in Python to concatenate all these bytes together to create our tokens and then these tokens here at this point are raw bytes.

So I have to decode using UTF-8 now back into Python strings. So previously we called encode on a string object to get the bytes and now we're doing the opposite. We're taking the bytes and calling decode on the bytes object to get a string in Python and then we can return text. 

So this is how we can do it. Now this actually has an issue in the way I implemented it and this could actually throw an error. So try to figure out why this code could actually result in an error if we plug in some sequence of IDs that is unlucky.

So let me demonstrate the issue. When I try to decode just something like 97, I am going to get a letter "a" here back. So nothing too crazy happening. But when I try to decode 128 as a single element, the token 128 is what? 

接下来，在获得 ID 之后，我们要做的第一件事是获取对应的 token（标记）。我在这里的实现方法是：遍历所有的 ID，使用词汇表（vocab）查找每个 ID 对应的字节，然后用 Python 的一种方法将这些字节连接起来，从而创建我们的 token。需要注意的是，此时这些 token 还是原始的字节序列。

因此，我们需要使用 UTF-8 编码将这些原始字节解码成 Python 可以理解的字符串。这个过程与之前的操作正好相反：之前我们对字符串对象调用 encode 方法来获取字节，而现在我们对字节对象调用 decode 方法来获取 Python 中的字符串。完成这一步后，我们就可以返回最终的文本了。

这整个过程实际上是在模拟大语言模型如何将数字 ID 转换回人类可读的文本。首先，我们使用 ID 找到对应的字节序列，然后将这些字节序列组合起来，最后再将它们转换成实际的文字。这就是模型生成文本的基本原理。

这就是我们可以实现的方法。然而，我的实现方式存在一个潜在的问题，可能会引发错误。让我们来分析一下，为什么在输入某些特定的 ID 序列时，这段代码可能会出错。

让我通过一个例子来说明这个问题。当我尝试解码数值 97 时，得到的结果是字母「a」。这个结果是正常的，没有任何异常。但是，当我尝试将 128 作为单个元素进行解码时，会发生什么呢？

UnicodeDecodeError: 'utf-8' codec can't decode byte 0x80 in position 0: invalid start byte.

What does that mean? Well, to understand what this means, we have to go back to our UTF-8 page that I briefly showed earlier. This is Wikipedia UTF-8. Basically, there's a specific schema that UTF-8 bytes take. In particular, if you have a multi-byte object for some of the Unicode characters, they have to have this special sort of envelope in how the encoding works.

What's happening here is that invalid start byte, that's because 128, the binary representation of it is 1 followed by all zeros. So we have 1 and then all 0s and we see here that that doesn't conform to the format because 1 followed by all 0s just doesn't fit any of these rules, so to speak. So it's an invalid start byte, which is byte one. This one must have a one following it, and then a zero following it, and then the content of your Unicode in Xs here.

结果是抛出了一个错误：

UnicodeDecodeError：'utf-8' 编解码器无法在位置 0 解码字节 0x80：无效的起始字节。

这个错误表明，在使用 UTF-8 编码方式解码时，遇到了一个无效的字节序列。具体来说，字节 0x80（十进制的 128）不是一个有效的 UTF-8 编码的起始字节。这就解释了为什么当我们尝试解码 128 这个值时会出现问题。

这到底是什么意思呢？要理解这个问题，我们需要回顾一下之前我简单提到的 UTF-8 编码。让我们看看维基百科上关于 UTF-8 的页面。

UTF-8（8 位元统一码转换格式）是一种针对 Unicode 的可变长度字符编码。它的字节遵循一个特定的结构模式。特别值得注意的是，当我们需要用多个字节来表示某些 Unicode 字符时，这些字节必须按照一种特殊的组织方式进行编码。

这种特殊的组织方式就像是给字符穿上了一件特殊的「外衣」。这个「外衣」告诉计算机：「嘿，我是一个多字节字符的一部分，请特别关注我！」这样，计算机就能正确地识别和处理这些复杂的字符了。

这里我们遇到了一个无效的 UTF-8（Unicode Transformation Format 8-bit）起始字节。让我们来解析一下原因：

数字 128 的二进制表示是 10000000（即 1 后面跟着 7 个 0）。在 UTF-8 编码中，这种格式不符合任何有效的多字节序列的起始字节规则。UTF-8 编码有特定的规则来表示不同长度的字符：

1、对于单字节字符（ASCII），最高位是 0。

2、对于多字节字符，起始字节的格式应该是「110xxxxx」（两字节），「1110xxxx」（三字节）或「11110xxx」（四字节），其中 x 代表实际的 Unicode 码点 bits。

因此，10000000 这个字节不符合任何这些模式。它既不是单字节 ASCII 字符（因为最高位是 1），也不是有效的多字节序列的起始字节（因为它不符合 110x、1110x 或 11110x 的模式）。

正确的多字节 UTF-8 序列应该是这样的：起始字节之后的每个延续字节都应该以「10」开头，后面跟着 6 个表示实际 Unicode 码点的比特。这就是为什么有效的起始字节后面必须跟着一个或多个以「10」开头的字节。

这种编码设计使得 UTF-8 能够向后兼容 ASCII，同时又能表示 Unicode 标准中的所有字符，是一种灵活而高效的编码方案。

So basically, we don't exactly follow the UTF-8 standard, and this cannot be decoded. And so the way to fix this is to use this errors='replace' in bytes.decode function of Python and by default errors is 'strict' so we will throw an error if it's not valid UTF-8 bytes encoding. But there are many different things that you could put here for error handling. This is the full list of all the errors that you can use.

In particular, instead of 'strict', let's change it to 'replace' and that will replace with this special marker, this is the replacement character. So errors='replace' and now we just get that character back.

So basically not every single byte sequence is valid UTF-8. And if it happens that your large language model, for example, predicts your tokens in a bad manner, then they might not be valid UTF-8. And then we won't be able to decode them. So the standard practice is to basically use errors='replace' and this is what you will also find in the OpenAI code that they released as well. But basically whenever you see this kind of a character in your output, in that case something went wrong and the LLM output was not a valid sort of sequence of tokens.

在处理文本编码时，我们并不总是严格遵循 UTF-8 标准，这可能导致某些文本无法被正确解码。为了解决这个问题，我们可以在 Python 的 bytes.decode 函数中使用 errors='replace' 参数。默认情况下，errors 参数设置为 'strict'，这意味着如果遇到无效的 UTF-8 字节编码，程序会抛出错误。但实际上，我们有多种错误处理方式可供选择。

一个更好的选择是将 'strict' 改为 'replace'。这种方法会用一个特殊的替换字符来代替那些无法解码的字符。具体来说，当我们设置 errors='replace' 时，程序会用这个替换字符来表示所有无法正常解码的部分。

需要注意的是，并非所有的字节序列都是有效的 UTF-8 编码。在使用大语言模型（Large Language Model, LLM）时，如果模型以不恰当的方式预测 token（标记），可能会产生无效的 UTF-8 序列。这种情况下，我们就无法正常解码这些序列。因此，使用 errors='replace' 已经成为了一种标准做法，在 OpenAI 公开的代码中也可以找到这种用法。

总的来说，如果你在输出中看到这种特殊的替换字符，它通常意味着在处理过程中出现了问题，LLM 输出的 token 序列不是有效的 UTF-8 编码。这种方法可以帮助我们在遇到编码问题时继续处理文本，而不会因为个别无效字符而中断整个程序的运行。

Okay and now we're going to go the other way. So we are going to implement this arrow right here where we are going to be given a string and we want to encode it into tokens. So this is the signature of the function that we're interested in and this should basically print a list of integers of the tokens.

Again, try to maybe implement this yourself if you'd like a fun exercise. Pause here, otherwise I'm going to start putting in my solution.

So again, there are many ways to do this. This is one of the ways that I came up with. The first thing we're going to do is we are going to take our text, encode it into UTF-8 to get the raw bytes. And then as before, we're going to call list on the bytes object to get a list of integers of those bytes. So those are the starting tokens. Those are the raw bytes of our sequence.

现在，我们要进行反向操作。我们将实现这个箭头所表示的功能，即给定一个字符串，我们需要将其编码为词元（tokens）。这就是我们要关注的函数签名，它基本上应该输出一个由表示词元的整数组成的列表。

如果你想要一个有趣的练习，不妨先尝试自己实现这个功能。你可以在这里稍作停顿思考一下，否则我将开始介绍我的解决方案。

再次强调，有多种方法可以实现这个功能。以下是我提出的方法之一。首先，我们要将文本编码成 UTF-8 格式以获得原始字节。然后，像之前一样，我们对字节对象调用 list 函数，得到这些字节的整数列表。这些就是我们序列的初始词元，也就是原始字节。

But now, of course, according to the merges dictionary above, and recall this was the merges, some of the bytes may be merged according to this lookup. In addition to that, remember that the merges was built from top to bottom and this is sort of the order in which we inserted stuff into merges. 

And so we prefer to do all these merges in the beginning before we do these merges later because, for example, this merge over here relies on the 256 which got merged here. So we have to go in the order from top to bottom, sort of, if we are going to be merging anything.

Now we expect to be doing a few merges, so we're gonna be doing while true. And now we want to find a pair of bytes that is consecutive that we are allowed to merge according to this. 

In order to reuse some of the functionality that we've already written, I'm going to reuse the function getStats. Recall that getStats will give us the... will basically count up how many times every single pair occurs in our sequence of tokens and return that as a dictionary. And the dictionary was a mapping from all the different byte pairs to the number of times that they occur, right?

At this point, we don't actually care how many times they occur in the sequence. We only care what the raw pairs are in that sequence. And so I'm only going to be using basically the keys of the dictionary. I only care about the set of possible merge candidates, if that makes sense.

但是现在，根据上面的合并字典（即我们之前讨论的 merges），某些字节可能会按照这个查找表进行合并。另外，请记住，合并字典是从上到下构建的，这也是我们将内容插入合并字典的顺序。

因此，我们更倾向于在一开始就进行所有这些合并操作，而不是稍后再进行。这是因为后面的合并操作可能依赖于之前的合并结果。举个例子，某个特定的合并操作可能依赖于之前合并得到的 256 这个值。所以，如果我们要进行任何合并，我们必须按照从上到下的顺序进行。

现在，我们预计要进行多次合并操作，所以我们要使用 "while true" 循环（一个无限循环，直到满足某个条件才会退出）。在这个循环中，我们想要找到一对连续的字节，这对字节根据我们的规则是允许合并的。

为了重用我们已经编写的一些功能，我打算重用 getStats 函数（getStats function）。回想一下，getStats 函数会计算我们的词元（token）序列中每个字节对出现的次数，并将结果以字典（dictionary，一种键值对的数据结构）的形式返回。这个字典将所有不同的字节对映射到它们在序列中出现的次数。

在这一点上，我们实际上并不关心这些字节对在序列中出现了多少次。我们只关心序列中存在哪些原始的字节对。因此，我只会使用字典的键（keys），也就是说，我只关心可能的合并候选集。这样做的目的是为了找出所有可能的合并选项，而不考虑它们的出现频率。

Now we want to identify the pair that we're going to be merging at this stage of the loop. So what do we want? We want to find the pair or like a key inside stats that has the lowest index in the merges dictionary, because we want to do all the early merges before we work our way to the late merges. 

Again there are many different ways to implement this but I'm going to do something a little bit fancy here. I'm going to be using the min over an iterator. In Python when you call min on an iterator, and stats here is a dictionary, we're going to be iterating the keys of this dictionary in Python. 

So we're looking at all the pairs inside stats, which are all the consecutive pairs. And we're going to be taking the consecutive pair inside tokens that has the minimum, what? The min takes a key, which gives us the function that is going to return a value over which we're going to do the min. And the one we care about is we care about taking merges and basically getting that pair's index.

So basically for any pair inside stats, we are going to be looking into merges at what index it has, and we want to get the pair with the min number. 

现在我们要确定在这个循环阶段要合并的配对。那么我们的目标是什么？我们想在统计数据（stats）中找到一个键，它在合并字典（merges）中具有最低的索引值。这是因为我们希望在处理后期合并之前完成所有早期的合并操作。

再次强调，有很多不同的方法可以实现这一点，但我在这里要使用一种稍微巧妙的方法。我将使用 Python 中迭代器上的 min() 函数。在 Python 中，当你对迭代器调用 min() 时，如果 stats 是一个字典，我们实际上是在迭代这个字典的键。

我们正在查看 stats 中的所有配对，它们都是连续的 token 对（例如，在文本中相邻的两个 token）。我们将在 tokens 中找出具有最小值的连续配对。这里的 min() 函数接受一个 key 参数，它指定了一个函数，这个函数将返回我们要进行最小化操作的值。在这个场景中，我们关心的是从 merges 中获取每个配对的索引。

简而言之，对于 stats 中的任何配对，我们都会在 merges 中查找它的索引值，我们的目标是找到具有最小索引值的配对。这样，我们就能确保按照正确的顺序进行合并操作。

So as an example, if there's a pair 101 and 32, we definitely want to get that pair. We want to identify it here and return it, and pair would become 101, 32 if it occurs. And the reason that I'm putting a float('inf') here as a fallback is that in the get function, when we basically consider a pair that doesn't occur in the merges, then that pair is not eligible to be merged, right? 

So if in the token sequence there's some pair that is not a merging pair, it cannot be merged, then it doesn't actually occur here and it doesn't have an index and it cannot be merged, which we will denote as float('inf'). And the reason infinity is nice here is because for sure we're guaranteed that it's not going to participate in the list of candidates when we do the min.

So this is one way to do it. Basically, long story short, this returns the most eligible merging candidate pair that occurs in the tokens.

让我们举个例子，假设有一个配对（pair）是 101 和 32，我们肯定想要获取这个配对。我们要在这里识别它并返回它，如果这个配对出现，它就会变成 101，32。我在这里使用 float('inf') 作为默认值的原因是，在 get 函数中，当我们遇到一个不在合并列表中的配对时，那个配对就不符合合并的资格，对吧？

所以，如果在 token 序列中有某个配对不是可合并的配对，它就不能被合并。这意味着它实际上不会出现在合并列表中，没有索引，也不能被合并，我们用 float('inf') 来表示这种情况。在这里使用正无穷大的好处是，我们可以确保它绝对不会出现在我们执行 min 操作时的候选列表中。

总的来说，这就是一种实现方法。简而言之，这个函数返回了在 tokens 中出现的、最适合合并的候选配对。

Now, one thing to be careful with here is this function here might fail in the following way. If there is nothing to merge, then there's nothing in merges that is satisfied anymore. There's nothing to merge. Everything just returns float('inf')s. And then the pair, I think, will just become the very first element of stats. 

But this pair is not actually a mergeable pair, it just becomes the first pair inside stats arbitrarily because all these pairs evaluate to float('inf') for the merging criterion. So basically it could be that this doesn't succeed because there's no more merging pairs.

So if this pair is not in merges that was returned, then this is a signal for us that actually there was nothing to merge. No single pair can be merged anymore. In that case we will break out. Nothing else can be merged. 

在这里需要注意的是，这个函数可能会以如下方式失败：如果没有可合并的元素，那么 merges 中就不会有任何满足条件的项。此时，没有东西可以合并，所有的评估结果都会返回 float('inf')（表示无穷大）。在这种情况下，pair 可能会简单地成为 stats 中的第一个元素。

然而，这个 pair 实际上并不是一个真正可合并的对。它之所以成为 stats 中的第一对，仅仅是因为所有的对在合并标准下都被评估为 float('inf'）。因此，这个过程可能会失败，原因是没有更多可合并的对了。

如果返回的 merges 中不包含这个 pair，这就向我们发出了一个信号：实际上已经没有什么可以合并的了。换句话说，没有任何一对元素可以再进行合并。在这种情况下，我们会跳出循环，因为没有其他东西可以合并了。

You may come up with a different implementation by the way. This is kind of like really trying hard in Python but really we're just trying to find a pair that can be merged with a lowest index here.

Now if we did find a pair that is inside merges with the lowest index then we can merge it. So we're going to look into the mergers dictionary for that pair to look up the index and we're going to now merge into that index. So we're going to do tokens equals and we're going to replace the original tokens.

We're going to be replacing the pair, pair, and we're going to be replacing it with index idx. This returns a new list of tokens where every occurrence of pair is replaced with idx. So we're doing a merge. We're going to be continuing this until eventually nothing can be merged. We'll come out here and we'll break out and here we just return tokens.

顺便说一下，你可能会想出一个不同的实现方法。这里的方法在 Python 中算是一种非常努力的尝试，但我们的目标其实很简单：就是找到一个可以合并的对，而且这个对的索引是最低的。

现在，如果我们找到了一对在合并列表中具有最低索引的 token 对，我们就可以进行合并操作。我们将在合并字典中查找该 token 对的索引，然后使用这个索引进行合并。具体来说，我们将对 tokens 进行重新赋值，替换原始的 tokens。

在这个过程中，我们将用索引 idx 替换找到的 token 对。这个操作会返回一个新的 tokens 列表，其中每次出现的该 token 对都被 idx 替换。这就是我们的合并过程。我们会持续这个过程，直到没有更多可以合并的 token 对。当达到这个状态时，我们就会退出循环，并返回最终的 tokens 列表。

And so that's the implementation. Hopefully this runs. Okay cool. Yeah and this looks reasonable. For example, 32 is a space in ASCII, so that's here. So this looks like it worked. Great.

Okay, so let's wrap up this section of the video at least. I wanted to point out that this is not quite the right implementation just yet because we are leaving out a special case.

In particular, if we tried to do this, this would give us an error. And the issue is that if we only have a single character or an empty string, then stats is empty and that causes an issue inside min.

So one way to fix this is if len(tokens) is at least two. Because if it's less than two, it's just a single token or no tokens, then let's just, there's nothing to merge, so we just return. So that would fix that case.

以上就是这个算法的实现。让我们运行一下看看结果。很好，结果看起来是合理的。例如，我们可以看到 ASCII 码 32（表示空格）出现在了结果中，这符合我们的预期。看来这个实现是成功的。

让我们总结一下这部分内容。需要注意的是，虽然这个实现基本正确，但还不是完全的实现。我们还遗漏了一个特殊情况需要处理。

需要特别注意的是，如果我们直接这样操作，程序就会报错。这个问题的根源在于：当我们只有一个字符或者一个空字符串时，stats 变量就会是空的，这会导致在执行 min 函数时出现错误。

解决这个问题的一种方法是先检查 tokens（分词列表）的长度是否至少为 2。因为如果长度小于 2，就意味着只有一个 token（词元）或者没有 token，这种情况下没有任何东西需要合并，我们可以直接返回。这样就能有效地处理这种特殊情况。

这个解决方案实际上是在函数开始时添加一个条件检查：如果 len(tokens) 小于 2，就直接返回，不执行后续的合并操作。这样可以确保我们只在有足够的 tokens 可以合并时才进行处理，从而避免了由于输入过短而导致的错误。

#### 04

Okay. And then second, I have a few test cases here for us as well. So first let's make sure about or let's note the following. If we take a string and we try to encode it and then decode it back, you'd expect to get the same string back right? Is that true for all strings?

So I think so here it is the case and I think in general this is probably the case but notice that going backwards is not you're not going to have an identity going backwards because as I mentioned not all token sequences are valid UTF-8 sort of byte streams and so therefore some of them can't even be decodable.

So this only goes in one direction. But for that one direction we can check here if we take the training text which is the text that we trained the tokenizer on, we can make sure that when we encode and decode we get the same thing back, which is true. 

And here I took some validation data so I went to I think this web page and I grabbed some text so this is text that the tokenizer has not seen and we can make sure that this also works ok. So that gives us some confidence that this was correctly implemented.

So those are the basics of the byte pair encoding algorithm. We saw how we can take some training set, train a tokenizer, the parameters of this tokenizer really are just this dictionary of merges, and that basically creates the little binary forest on top of raw bytes. Once we have this, the merges table, we can both encode and decode between raw text and token sequences.

So that's the simplest setting of the tokenizer. What we're going to do now, though, is we're going to look at some of the state-of-the-art large language models and the kinds of tokenizers that they use and we're going to see that this picture complexifies very quickly. So we're going to go through the details of this complexification one at a time.

接下来，让我们来看几个测试案例。首先，我们需要考虑一个问题：如果我们对一个字符串进行编码，然后再解码回来，你会期望得到原来的字符串，对吗？这个规则是否适用于所有的字符串呢？

在我们的案例中，这个规则是成立的。而且我认为在一般情况下，这个规则也是适用的。但是需要注意的是，这个过程并不是双向的恒等变换。因为就像我之前提到的，并非所有的 token 序列都能构成有效的 UTF-8 字节流，所以有些序列甚至无法解码。

因此，这个过程只能单向进行。但是对于这个单向过程，我们可以进行验证。我们可以使用训练分词器（tokenizer）时用到的文本进行测试，确保编码后再解码能够得到原始文本。我们的测试结果显示，这一点是成立的。

此外，我还准备了一些验证数据。我从一个网页上抓取了一些文本，这些文本是分词器之前没有见过的。我们可以用这些新数据来测试，确保分词器在处理未知文本时也能正常工作。这些测试都顺利通过了，这让我们有信心认为我们的实现是正确的。

以上就是字节对编码（Byte Pair Encoding）算法的基本原理。我们了解了如何使用训练集来训练一个分词器（tokenizer），这个分词器的核心参数其实就是一个合并字典，它在原始字节的基础上构建了一个小型的树状结构。有了这个合并表，我们就可以在原始文本和 token 序列之间进行双向转换，即编码和解码。

这是分词器的最基本形式。接下来，我们将探讨一些最先进的大语言模型（Large Language Model）及其使用的分词器类型。我们会发现，随着研究的深入，这个看似简单的概念会变得越来越复杂。因此，我们将逐步详细介绍这个复杂化的过程。

So let's kick things off by looking at the GPT series. In particular I have the GPT-2 paper here. And this paper is from 2019 or so, five years ago. And let's scroll down to "Input representation". This is where they talk about the tokenizer that they're using for GPT-2. 

Now, this is all fairly readable, so I encourage you to pause and read this yourself. But this is where they motivate the use of the byte pair encoding algorithm on the byte level representation of UTF-8 encoding. So this is where they motivate it, and they talk about the vocabulary sizes and everything.

Now, everything here is exactly as we've covered it so far, but things start to depart around here. What they mention is that they don't just apply the naive algorithm as we have done it. And in particular, here's a motivating example.

让我们首先来看看 GPT 系列模型。这里我手头有 GPT-2 的论文，这篇论文发表于 2019 年左右，也就是 5 年前。让我们查看论文中的「输入表示」（Input representation）部分。在这一部分，他们详细描述了 GPT-2 所使用的分词器。

现在，这段内容还是比较容易理解的，所以我建议你先自己阅读一下。这里主要讲述了为什么要在 UTF-8 编码的字节级表示上使用字节对编码（Byte Pair Encoding, BPE）算法。他们在这里解释了这么做的原因，并讨论了词汇表大小等相关内容。

到目前为止，这里的内容都与我们之前讨论的一致。但是接下来，情况开始有所不同。他们提到，他们并不是简单地应用我们之前讲过的基础算法。特别是，他们给出了一个很好的例子来说明这一点。

Suppose that you have common words like "dog". What will happen is that "dog" of course occurs very frequently in the text and it occurs right next to all kinds of punctuation as an example. So "dog.", "dog!", "dog?", etc. And naively you might imagine that the BPE algorithm could merge these to be single tokens and then you end up with lots of tokens that are just like "dog" with a slightly different punctuation.

It feels like you're clustering things that shouldn't be clustered. You're combining kind of semantics with punctuation and this feels suboptimal. Indeed they also say that this is suboptimal according to some of the experiments. So what they want to do is they want to, top-down in a manual way, enforce that some types of characters should never be merged together. They want to enforce these merging rules on top of the byte-pair encoding algorithm.

假设你有一个像 "dog"（狗）这样的常见词。在文本中，"dog" 经常出现，而且常常紧跟着各种标点符号。比如 "dog."、"dog!"、"dog?" 等等。你可能会想，BPE 算法可以将这些组合合并成单个 token。但这样做的结果是，你最终会得到大量的 token，它们都是 "dog" 加上稍微不同的标点符号。

看起来你正在将一些不应该聚集在一起的元素进行聚类。你把语义和标点符号这样的内容组合在了一起，这种做法并不是最优的。事实上，根据一些实验结果，他们也承认这种方法存在不足。因此，他们想要采用一种自上而下的人工方法，规定某些类型的字符不应被合并。他们的目标是在字节对编码（byte-pair encoding）算法的基础上，强制执行这些合并规则。

So let's take a look at their code and see how they actually enforce this and what kinds of merges they actually do perform. I have the tab open here for GPT-2 under OpenAI on GitHub and when we go to "source" there is an "encoder.py". 

Now I don't personally love that they call it "encoder.py" because this is the tokenizer and the tokenizer can do both encode and decode so it feels kind of awkward to me that it's called "encoder" but that is the tokenizer.

And there's a lot going on here and we're gonna step through it in detail at one point. For now I just want to focus on this part here. They create a regex pattern here that looks very complicated and we're gonna go through it in a bit. But this is the core part that allows them to enforce rules for what parts of the text will never be merged for sure.

Now notice that re.compile here is a little bit misleading because we're not just doing import re which is the Python re module, we're doing import regex as re and regex is a Python package that you can install pip install regex and it's basically an extension of re so it's a bit more powerful re. 

So let's take a look at this pattern and what it's doing and why this is actually doing the separation that they are looking for.

让我们来看看他们的代码，了解一下他们是如何实际执行这种强制规则的，以及他们具体执行了哪些类型的合并。我这里已经打开了 GitHub 上 OpenAI 组织下的 GPT-2 项目页面，在 "source" 目录中有一个名为 "encoder.py" 的文件。

我个人不太赞同他们将其命名为 "encoder.py"，因为这实际上是一个分词器（tokenizer），而分词器既可以进行编码也可以进行解码。因此，将其称为 "encoder" 感觉不太恰当，但无论如何，这就是他们的分词器。

这里涉及了很多内容，我们稍后会逐步详细讨论。现在，我想先聚焦于这个部分。他们创建了一个看似复杂的正则表达式模式，我们稍后会深入分析。这个模式是核心部分，它能确保文本的某些部分绝不会被合并。

值得注意的是，这里的 re.compile 可能会让人误解。实际上，我们不是使用 Python 的标准 re 模块，而是使用了 import regex as re。regex 是一个 Python 第三方包，可以通过 pip install regex 命令安装。它是 re 模块的增强版，功能更加强大。

接下来，让我们来分析这个模式，看看它的作用以及它如何实现所需的文本分离。

Okay so I've copy pasted the pattern here to our Jupyter notebook where we left off and let's take this pattern for a spin. In the exact same way that their code does, we're going to call an re.findall for this pattern on any arbitrary string that we are interested in. So this is the string that we want to encode into tokens to feed into an LLM like GPT-2.

So what exactly is this doing? Well, re.findall will take this pattern and try to match it against this string. The way this works is that you are going from left to right in the string and you're trying to match the pattern. And re.findall will get all the occurrences and organize them into a list.

Now when you look at this pattern, first of all notice that this is a raw string and then these are three double quotes just to start the string. So really the string itself, this is the pattern itself, right? And notice that it's made up of a lot of ORs, so see these vertical bars? Those are ORs in regex.

And so you go from left to right in this pattern and try to match it against the string wherever you are. So we have "hello" and we're gonna try to match it. Well, it's not apostrophe s, it's not apostrophe t, or any of these, but it is an optional space followed by \p{L}1 or more times.

我已经将这个模式复制到了我们之前使用的 Jupyter 笔记本中。现在，让我们来测试一下这个模式。我们将使用与原代码相同的方式，对任意感兴趣的字符串调用 re.findall 函数来匹配这个模式。这个字符串就是我们想要编码成 token（标记）并输入到像 GPT-2 这样的大语言模型（LLM）中的文本。

这段代码究竟在做什么呢？让我们来详细解析一下。

re.findall 函数（正则表达式查找所有匹配项的函数）会使用给定的模式去匹配目标字符串。它的工作原理是从左到右遍历字符串，尝试找出所有符合模式的部分。然后，re.findall 会将所有匹配项收集起来，整理成一个列表。

现在让我们来看看这个模式。首先，注意这是一个原始字符串（raw string），以三个双引号开始。这个字符串本身就是我们要使用的模式。你可能注意到了，这个模式中包含了很多竖线 "|"，在正则表达式（regex）中，这些竖线代表「或」的关系。

当我们使用这个模式时，会从左到右遍历字符串，尝试在每个位置进行匹配。比如，我们有一个 "hello" 字符串要匹配。它不是 "'s"（撇号加 s），不是 "'t"（撇号加 t），也不是模式中列出的其他选项。但是，它确实符合模式中的一个选项：一个可选的空格，后面跟着一个或多个 \p{L}（这是一个 Unicode 属性，表示任何语言的字母）。

这种模式设计允许我们灵活地匹配各种不同的文本结构，包括带有各种标点符号和空格的单词或短语。

What is \p{L}? It is, coming to some documentation that I found and there might be other sources as well, \p{L} is a letter, any kind of letter from any language. And "hello" is made up of letters, H-E-L-L-O, etc. followed by a bunch of letters, one or more letters, is going to match "hello", but then the match ends because a whitespace is not a letter.

So from there on begins a new sort of attempt to match against the string again. And starting in here we're gonna skip over all of these again until we get to the exact same point again, and we see that there's an optional space, this is the optional space, followed by a bunch of letters, one or more of them, and so that matches.

So when we run this we get a list of two elements, "hello" and then " world". So "how", "are", "you", if we add more letters? We would just get them like this.

Now what is this doing and why is this important? We are taking our string and instead of directly encoding it for tokenization, we are first splitting it up. And when you actually step through the code, and we'll do that in a bit more detail, what really it's doing on a high level is that it first splits your text into a list of text, just like this one.

And all these elements of this list are processed independently by the tokenizer. And all of the results of that processing are simply concatenated. So "hello", "world". Oh, I missed "how". "Hello", "world", "how", "are", "you"? We have five elements of a list. 

All of these will independently go from text to a token sequence and then that token sequence is going to be concatenated, it's all going to be joined up. And roughly speaking what that does is you're only ever finding merges between the elements of this list.

So you can only ever consider merges within every one of these elements individually. And after you've done all the possible merging for all these elements individually, the results of all that will be joined by concatenation.

什么是 \p{L}？根据我查阅的文档和其他一些资料，\p{L} 是一个正则表达式模式，用于匹配任何语言中的任何字母。例如，"hello" 由字母 H-E-L-L-O 组成。因此，\p{L} 后面跟着一个或多个字母的模式将匹配 "hello"，但匹配会在这里结束，因为空格不是字母。

从空格之后，正则表达式会重新开始尝试匹配字符串。它会跳过之前已匹配的内容，直到再次遇到相同的模式。这里我们看到有一个可选的空格，然后是一个或多个字母，所以 "world" 也能被匹配到。

因此，当我们运行这个正则表达式时，我们会得到一个包含两个元素的列表：["hello", "world"]。如果字符串中有更多的单词，比如 "how"、"are"、"you"，只要它们符合这个模式（可选的空格后跟一个或多个字母），就会被同样地匹配到并添加到结果列表中。

那么，这段代码在做什么？为什么它如此重要？我们并没有直接对字符串进行编码来进行标记化（tokenization），而是首先将其拆分。当我们稍后详细逐步分析代码时，你会发现它在宏观上所做的就是将文本拆分成一个文本列表，就像我们看到的这样。

这个列表中的每个元素都会被分词器（tokenizer）独立处理。然后，所有处理结果会被简单地连接在一起。例如，我们有 "hello"、"world"、"how"、"are"、"you" 这五个列表元素。

每个元素都会独立地从文本转换为标记（token）序列，然后这些标记序列会被连接起来，形成一个完整的序列。这种方法的核心在于，合并操作只会在列表的各个元素内部进行。

换句话说，分词器只会考虑每个元素内部的可能合并。当所有元素都完成了各自内部的所有可能合并后，这些结果才会通过连接操作被合并成最终的标记序列。

And so you are basically what you're doing effectively is you are never going to be merging this "e" with this space because they are now parts of separate elements of this list and so you are saying we are never going to merge "e space" because we're breaking it up in this way.

So basically using this regex pattern to chunk up the text is just one way of enforcing that some merges are not to happen. And we're going to go into more of this text and we'll see that what this is trying to do on a high level is we're trying to not merge across letters, across numbers, across punctuation and so on.

So let's see in more detail how that works. Let's continue. Now we have \p{N}. If you go to the documentation, \p{N} is any kind of numeric character in any script. So it's numbers. So we have an optional space followed by numbers and those would be separated out. So letters and numbers are being separated.

So if I do "hello world123, how are you?" Then "world" will stop matching here because 1 is not a letter anymore. But 1 is a number. So this group will match for that and we'll get it as a separate entity.

实际上，你所做的就是确保这个 "e" 永远不会与这个空格合并，因为它们现在是列表中的独立元素。换句话说，我们通过这种方式将 "e" 和空格分开，从而防止它们合并。

使用这种正则表达式模式来切分文本，本质上是一种防止某些字符合并的方法。接下来我们会深入研究这个文本，你会发现这种方法的目的是防止跨字母、数字、标点符号等的合并。

让我们更详细地了解它的工作原理。继续往下看，我们遇到了 \p{N}。根据文档，\p{N} 匹配任何脚本中的任何数字字符。所以它就是用来匹配数字的。这里我们有一个可选的空格，后面跟着数字，这些会被分开处理。这样，字母和数字就被分开了。

举个例子，如果我们有这样一个字符串："hello world123, how are you?"，"world" 的匹配会在这里停止，因为 1 不是字母而是数字。数字 1 会被这个匹配数字的组捕获，从而成为一个独立的实体。

Let's see how these apostrophes work. So here if we have 'v or I mean apostrophe v as an example then apostrophe here is not a letter or a number so "hello" will stop matching and then we will exactly match this with that. So that will come out as a separate thing.

So why are they doing the apostrophes here? Honestly, I think that these are just like very common apostrophes that are used typically. I don't love that they've done this because let me show you what happens when you have some Unicode apostrophes. 

Like, for example, if you have "house's", then this will be separated out because of this matching. But if you use the Unicode apostrophe like this, then suddenly this does not work. And so this apostrophe will actually become its own thing now.

And so it's basically hard-coded for this specific kind of apostrophe. And otherwise, they become completely separate tokens. In addition to this, you can go to the GPT-2 docs. And here when they define the pattern, they say, should have added re.ignoreCase. So BPE merges can happen for capitalized versions of contractions.

让我们来看看这些撇号（apostrophes）是如何工作的。以 'v 为例，或者说以撇号后接 v 为例，这里的撇号既不是字母也不是数字，所以 "hello" 将停止匹配，然后我们会精确地匹配这个撇号。因此，它会被作为一个独立的 token（标记）输出。

那么，为什么他们在这里使用撇号呢？老实说，我认为这些只是一些非常常见的、典型使用的撇号。我不太赞同他们这样做，让我给你展示一下当你使用一些 Unicode 撇号时会发生什么。

例如，如果你有 "house's" 这个词，由于这种匹配方式，它会被分开。但如果你使用 Unicode 撇号，那么这种分割就不会发生。这样，这个 Unicode 撇号实际上会成为一个独立的 token。

所以，这种处理方式基本上是为特定类型的撇号硬编码的。除此之外，其他类型的撇号会变成完全独立的 tokens。另外，你可以查看 GPT-2 的文档。在那里，当他们定义模式时，他们提到应该添加 re.ignoreCase。这样做是为了让字节对编码（BPE）合并能够处理缩写词的大写版本。

So what they're pointing out is that you see how this is apostrophe and then lowercase letters? Well because they didn't do re.ignoreCase then these rules will not separate out the apostrophes if it's uppercase.

So "House's" would be like this but if I did "House's" from uppercase, then notice suddenly the apostrophe comes by itself. So the tokenization will work differently in uppercase and lowercase, inconsistently separating out these apostrophes.

So it feels extremely gnarly and slightly gross, but that's how that works. Okay, so let's come back. After trying to match a bunch of apostrophe expressions, by the way, the other issue here is that these are quite language-specific probably.

So I don't know that all the languages, for example, use or don't use apostrophes, but that would be inconsistently tokenized as a result. Then we try to match letters. Then we try to match numbers. And then if that doesn't work, we fall back to here.

And what this is saying is, again, optional space followed by something that is not a letter, number, or a space, and one or more of that. So what this is doing effectively is this is trying to match punctuation, roughly speaking, not letters and not numbers.

So this group will try to trigger for that. So if I do something like this, then these parts here are not letters or numbers, but they will actually get caught here. And so they become its own group. So we've separated out the punctuation.

And finally, this is also a little bit confusing. So this is matching whitespace, but this is using a negative lookahead assertion in regex. So what this is doing is it's matching whitespace up to, but not including the last whitespace character.

他们指出的问题是这样的：你注意到这里有撇号（即单引号）后面跟着小写字母吗？因为代码中没有使用 re.ignoreCase（忽略大小写）选项，所以这些规则在处理大写字母时不会分离出撇号。

举个例子，"House's" 会被正常处理，但如果我们输入大写的 "HOUSE'S"，你会发现撇号突然被单独分离出来了。这意味着标记化（tokenization）过程在处理大写和小写时会产生不一致的结果，特别是在处理撇号时。

这种处理方式确实看起来很复杂，甚至可能让人感到不太舒服，但这就是它的工作原理。让我们继续往下看。在尝试匹配一系列带撇号的表达式之后，这里还存在另一个问题，那就是这些规则可能很大程度上是针对特定语言的。

我不确定所有语言是否都使用或不使用撇号，但结果是，不同语言的文本可能会被不一致地进行标记化处理。接下来，代码会尝试匹配字母，然后尝试匹配数字。如果这些都不起作用，最后会回退到默认的处理方式。

让我们再来看看这个部分。它表示的是：一个可选的空格，后面跟着一个或多个既不是字母，也不是数字，也不是空格的字符。实际上，这个模式主要是用来匹配标点符号的。

这个组会尝试匹配这样的模式。举个例子，如果我们有一些特殊字符（比如 "!@#"），它们既不是字母也不是数字，就会被这个组捕获。这样，我们就成功地把标点符号分离出来了。

最后还有一点可能会让人困惑。这里是在匹配空白字符，但使用了正则表达式中的「负向前瞻断言」（negative lookahead assertion）。这种方法可以匹配到除最后一个空白字符之外的所有空白字符。

Why is this important? This is pretty subtle, I think. You see how the whitespace is always included at the beginning of the word. So space "r", space "u", etc.

Suppose we have a lot of spaces here. What's gonna happen here is that these spaces up to and not including the last character will get caught by this. And what that will do is it will separate out the spaces up to but not including the last character so that the last character can come here and join with the space "u".

And the reason that's nice is because space "u" is the common token. So if I didn't have these extra spaces here you would just have space "u" and if I add tokens, if I add spaces, we still have a space "u" but now we have all this extra whitespace.

So basically the GPT-2 tokenizer really likes to have a space letter or space numbers and it prepends these spaces and this is just something that it is consistent about. So that's what that is for and then finally we have... the last fallback is whitespace characters. So that would be just if that doesn't get caught, then this thing will catch any trailing spaces and so on.

为什么这很重要呢？这其实是一个很微妙的设计。你注意到了吗，空白字符总是出现在单词的开头。比如空格后面跟着 "r"，空格后面跟着 "u"，以此类推。

假设我们在这里有很多空格。这个机制的工作原理是：它会捕获除最后一个字符之外的所有空格。这样做的目的是将空格分离出来，直到但不包括最后一个字符，使得最后一个字符可以与空格 "u" 组合。

这种做法的优点在于空格 "u" 是一个常见的词元（token）。如果这里没有额外的空格，你就只会得到空格 "u"。而如果我添加词元，即添加空格，我们仍然会有一个空格 "u"，但同时还会有所有这些额外的空白。

基本上，GPT-2 分词器（tokenizer）非常偏好于空格加字母或空格加数字的组合。它会在这些组合前添加空格，这是它一贯的处理方式。这就是这个机制的用途。最后，作为最终的后备方案，我们还有空白字符的处理。这意味着如果有任何未被前面规则捕获的尾随空格，这个规则将会捕获它们。

I wanted to show one more real-world example here. So if we have this string, which is a piece of Python code, and then we try to split it up, then this is the kind of output we get. You'll notice that the list has many elements here, and that's because we are splitting up fairly often every time sort of a category changes.

So there will never be any mergers within these elements and that's what you are seeing here. Now you might think that in order to train the tokenizer OpenAI has used this to split up text into chunks and then run just a BPE algorithm within all the chunks.

But that's not exactly what happened and the reason is the following. Notice that we have the spaces here. Those spaces end up being entire elements but these spaces never actually end up being merged by OpenAI and the way you can tell is that if you copy paste the exact same chunk here into the TikTokenizer you see that all the spaces are kept independent and they're all token 220.

So I think OpenAI decided at some point and for some rule that these spaces would never be merged and so there's some additional rules on top of just chunking and BPE that OpenAI does that's not clear about.

Now the training code for the GPT-2 tokenizer was never released, so all we have is the code that I've already shown you, but this code here that they've released is only the inference code for the tokenizer.

So this is not the training code, you can't give it a piece of text and train a tokenizer, this is just the inference code which takes the merges that we have up above and applies them to a new piece of text. And so we don't know exactly how OpenAI trained the tokenizer but it wasn't as simple as chunk it up and BPE it, whatever it was.

我想再举一个实际的例子来说明这个问题。假设我们有一个字符串，它是一段 Python 代码。当我们尝试对它进行分词时，我们会得到这样的输出。你会注意到，这个列表包含了很多元素。这是因为每当遇到某种类型的变化时，我们就会进行切分。

这意味着这些元素之间不会再有任何合并，这就是你在这里看到的结果。你可能会认为，OpenAI 在训练分词器（tokenizer）时，是先将文本切分成多个块，然后在每个块内单独运行字节对编码（BPE, Byte Pair Encoding）算法。

但实际情况并非完全如此，原因如下。请注意这里的空格。这些空格最终成为了独立的元素，但 OpenAI 从未将这些空格合并。你可以通过以下方式验证这一点：如果你将完全相同的代码块复制粘贴到 TikTokenizer 中，你会发现所有的空格都被单独保留，且它们都被标记为 token 220（这是一个特定的标记 ID）。

因此，我认为 OpenAI 在某个时候出于某些规则决定，这些空格永远不会被合并。这意味着除了简单的文本分块和 BPE 算法之外，OpenAI 还应用了一些额外的规则。不过，这些额外规则的具体内容目前还不太清楚。

目前，GPT-2 分词器的训练代码从未被公开发布。我之前向你展示的代码，以及 OpenAI 发布的代码，都只是分词器的推理代码。

这意味着，你无法使用这些代码来输入一段文本并训练出一个分词器。这些代码仅仅是推理代码，它们使用我们之前提到的合并规则，将其应用到新的文本上进行分词。因此，我们并不完全清楚 OpenAI 是如何训练他们的分词器的，但可以确定的是，这个过程比简单地将文本分块并应用字节对编码（BPE）要复杂得多。

#### 05

Next I wanted to introduce you to the TikToken library from OpenAI, which is the official library for tokenization from OpenAI. So this is tic token, pip install tic token, and then you can do the tokenization inference. This is again not training code, this is only inference code for tokenization.

I wanted to show you how you would use it, quite simple, and running this just gives us the GPT-2 tokens or the GPT-4 tokens. So this is the tokenizer used for GPT-4.

And so in particular we see that the whitespace in GPT-2 remains unmerged, but in GPT-4 these whitespaces merge, as we also saw in this one, where here they're all unmerged, but if we go down to GPT-4 they become merged.

Now, in the GPT-4 tokenizer, they changed the regular expression that they use to chunk up text. So the way to see this is that if you come to the TikToken library, and then you go to this file, TikToken/ext/openai_public, this is where sort of like the definition of all these different tokenizers that OpenAI maintains is.

接下来，我想向你介绍 OpenAI 的 tiktoken 库，这是 OpenAI 官方的分词库。你可以通过 `pip install tiktoken` 命令来安装它，然后就可以使用它进行分词推理。再次强调，这个库只提供推理功能，不包含训练代码。

我来演示一下如何使用它，非常简单。运行相关代码后，我们就能得到 GPT-2 或 GPT-4 模型使用的词元（token）。值得注意的是，这个分词器也被用于 GPT-4 模型。

具体来说，我们可以观察到 GPT-2 中的空白字符保持未合并状态，而在 GPT-4 中这些空白字符会合并。就像我们在这个例子中看到的，GPT-2 中所有空白字符都是未合并的，但在 GPT-4 中它们变成了合并状态。

在 GPT-4 的分词器（tokenizer）中，开发者们改变了用于切分文本的正则表达式。要了解这一点，我们可以查看 TikToken 库（这是一个用于 OpenAI 模型分词的开源库）。在 TikToken/ext/openai_public 这个文件中，我们可以找到 OpenAI 维护的各种分词器的定义。

And so necessarily to do the inference they had to publish some of the details about the strings. So this is the string that we already saw for GPT-2. It is slightly different but it is actually equivalent to what we discussed here.

So this pattern that we discussed is equivalent to this pattern, and this one just executes a little bit faster. So here you see a little bit of a slightly different definition, but otherwise it's the same. We're going to go into special tokens in a bit.

And then if you scroll down to CL100K, this is the GPT-4 tokenizer, you see that the pattern has changed. And this is kind of like the major change in addition to a bunch of other special tokens, which we'll go into a bit again.

Now, I'm not going to actually go into the full detail of the pattern change, because honestly, this is mind-numbing. I would just advise that you pull out ChatGPT and the RegEx documentation and just step through it.

为了让用户能够使用这些模型进行推理（即使用模型处理输入并获得输出），OpenAI 不得不公开一些关于字符串处理的细节。我们之前看到的 GPT-2 的字符串模式在这里略有不同，但实际上与我们之前讨论的是等效的。

我们讨论的这个模式等同于这里的模式，只是后者执行速度稍快一些。在这里你可以看到一个稍微不同的定义，但除此之外它们是相同的。我们稍后会讨论特殊的标记（special tokens，指在分词过程中有特殊含义或用途的标记）。

如果你继续向下滚动到 CL100K（这是 GPT-4 的分词器），你会发现模式已经发生了变化。这是除了其他一些特殊标记（token）之外的主要变化，我们稍后会再次详细讨论。

实际上，我不会详细解释模式变化的所有细节，因为说实话，这个过程相当枯燥。我建议你可以使用 ChatGPT 和 RegEx 文档，然后逐步进行分析。

But really, the major changes are number one, you see this (?i) here, that means that the case sensitivity, this is case insensitive match. And so the comment that we saw earlier on, oh, we should have used re.uppercase. Basically, we're now going to be matching these apostrophe s, apostrophe d, apostrophe m, etc. We're going to be matching them both in lowercase and in uppercase so that's fixed.

There's a bunch of different like handling of the white space that I'm not going to go into the full details of. And then one more thing here is you will notice that when they match the numbers they only match one to three numbers.

So they will never merge numbers that are in more than three digits. Only up to three digits of numbers will ever be merged. And that's one change that they made as well to prevent tokens that are very, very long number sequences.

But again, we don't really know why they do any of this stuff because none of this is documented. And we just get the pattern. So yeah, it is what it is. But those are some of the changes that GPT-4 has made. And of course, the vocabulary size went from roughly 50k to roughly 100k.

但实际上，主要的变化有以下几点：

1、你会看到 `(?i)` 这个标记，这意味着匹配时不区分大小写。这解决了我们之前提到的应该使用 `re.uppercase` 的问题。现在，我们可以同时匹配撇号后的 s、d、m 等字母的大写和小写形式。

2、有一些关于空白字符处理的变化，但我不会详细讨论这些内容。

3、另外一个值得注意的变化是，在匹配数字时，现在只匹配一到三位数字。

这些改变使得分词器能够更好地处理各种文本情况，提高了其灵活性和准确性。

因此，他们绝不会合并超过三位数的数字。只有最多三位数的数字才会被合并。这也是他们做出的一项改变，目的是防止出现非常长的数字序列 token。

不过需要再次强调的是，我们并不真正了解他们为什么要这样做，因为这些都没有文档记录。我们只能从模式中推测。这就是现状，我们只能接受。但这些确实是 GPT-4 所做的一些改变。当然，词汇量的规模也从大约 5 万增加到了大约 10 万。

The next thing I would like to do very briefly is to take you through the GPT2 encoder.py that OpenAI has released. This is the file that I already mentioned to you briefly. Now this file is fairly short and should be relatively understandable to you at this point.

Starting at the bottom here they are loading two files encoder.json and vocab.bpe and they do some light processing on it and then they call this encoder object which is the tokenizer.

Now if you'd like to inspect these two files which together constitute their saved tokenizer then you can do that with a piece of code like this. This is where you can download these two files and you can inspect them if you'd like.

And what you will find is that this encoder, as they call it in their code, is exactly equivalent to our vocab. So remember here where we have this vocab object which allowed us to decode very efficiently and basically it took us from the integer to the bytes for that integer. So our vocab is exactly their encoder.

And then their vocab.bpe, confusingly, is actually our merges. So their bpe_merges, which is based on the data inside vocab.bpe, ends up being equivalent to our merges.

So basically they are saving and loading the two variables that for us are also critical, the merges variable and the vocab variable. Using just these two variables, you can represent a tokenizer and you can both do encoding and decoding once you've trained this tokenizer.

接下来，我想简要地带你浏览一下 OpenAI 发布的 GPT2 encoder.py 文件。这就是我之前简单提到过的文件。这个文件相当短，到目前为止你应该能够相对轻松地理解它。

让我们从文件的底部开始看。他们首先加载了两个文件：encoder.json 和 vocab.bpe，然后对这些文件进行了一些简单的预处理。之后，他们调用了一个名为 encoder 的对象，这个对象就是分词器（tokenizer）。

现在，如果你想查看构成保存的分词器（tokenizer）的两个文件，你可以使用类似下面这样的代码。这段代码允许你下载并检查这两个文件。

通过检查，你会发现他们代码中称为「编码器」（encoder）的部分，其实就等同于我们的词汇表（vocab）。回想一下，我们有一个 vocab 对象，它能够非常高效地进行解码，本质上是将整数转换为对应的字节。因此，我们的 vocab 就是他们所说的编码器。

有趣的是，他们的 vocab.bpe 实际上对应的是我们的合并（merges）。他们的 bpe_merges，也就是基于 vocab.bpe 文件中数据的内容，最终等同于我们的 merges。

简而言之，他们保存和加载的两个变量，恰好就是对我们来说至关重要的 merges 变量和 vocab 变量。仅凭这两个变量，你就可以表示一个完整的分词器。而且，一旦你训练好这个分词器，你就可以同时进行编码和解码操作。

Now the only thing that is actually slightly confusing inside what OpenAI does here is that in addition to this encoder and the decoder they also have something called a byte_encoder and a byte_decoder and this is actually unfortunately just kind of a spurious implementation detail, it isn't actually deep or interesting in any way so I'm going to skip the discussion of it.

But what OpenAI does here for reasons that I don't fully understand is that not only have they this tokenizer which can encode and decode, but they have a whole separate layer here in addition that is used serially with the tokenizer.

And so you first do byte_encode and then encode and then you do decode and then byte_decode. So that's the loop and they are just stacked serially on top of each other. And it's not that interesting. So I won't cover it, and you can step through it if you'd like.

Otherwise, this file, if you ignore the byte_encoder and the byte_decoder, will be algorithmically very familiar to you. And the meat of it here is the, what they call BPE function. And you should recognize this loop here, which is very similar to our own while loop, where they're trying to identify the bigram, a pair, that they should be merging next. 

在 OpenAI 的实现中，有一点稍微令人困惑的地方是：除了编码器和解码器之外，他们还有所谓的 byte_encoder 和 byte_decoder。不过，这其实只是一个无关紧要的实现细节，并没有什么深层次的含义或特别有趣的地方，所以我就不详细讨论了。

OpenAI 在这里的做法，出于我不太清楚的原因，不仅包含了可以进行编码和解码的分词器（tokenizer），还额外增加了一个完全独立的层，它与分词器串行使用。

具体来说，处理流程是这样的：首先进行 byte_encode，然后是 encode，接着是 decode，最后是 byte_decode。这就是整个循环过程，这些步骤就是简单地依次执行。这个过程并不特别有趣，所以我就不详细介绍了。如果你感兴趣的话，可以自己去深入研究一下。

如果你忽略掉 byte_encoder 和 byte_decoder 这两部分，这个文件的算法结构其实会让你感到非常熟悉。其中的核心是他们称为 BPE 函数的部分。你应该能认出这里的循环结构，它与我们之前实现的 while 循环非常相似，目的是识别下一个需要合并的字符对（二元组）。

And then here, just like we had, they have a for loop trying to merge this pair. So they will go over all of the sequence and they will merge the pair whenever they find it. And they keep repeating that until they run out of possible merges in the text. 

So that's the meat of this file. And there's an encode and decode function just like we have implemented it. So long story short what I want you to take away at this point is that unfortunately it's a little bit of a messy code that they have but algorithmically it is identical to what we've built up above and what we've built up above if you understand it is algorithmically what is necessary to actually build a BPE tokenizer, train it, and then both encode and decode.

The next topic I would like to turn to is that of special tokens. So in addition to tokens that are coming from, you know, raw bytes and the BPE merges, we can insert all kinds of tokens that we are going to use to delimit different parts of the data or introduce to create a special structure of the token streams.

接下来，就像我们之前做的那样，他们使用了一个 for 循环来合并这个字符对。具体来说，他们会遍历整个序列，每当找到这个字符对就进行合并。这个过程会不断重复，直到文本中没有可以合并的对象为止。

这就是该文件的核心内容。此外，还有编码和解码函数，这与我们之前实现的功能类似。总的来说，我希望你能从中理解到以下几点：虽然他们的代码结构可能看起来有些复杂，但从算法角度来看，它与我们上面构建的内容是完全一致的。如果你理解了我们之前构建的内容，那么你就掌握了构建字节对编码（BPE）分词器、训练它，以及进行编码和解码所需的全部算法知识。

接下来，我想讨论一下特殊标记（special tokens）这个话题。除了来自原始字节和字节对编码（Byte Pair Encoding, BPE）合并产生的标记外，我们还可以插入各种特殊标记。这些特殊标记用于分隔数据的不同部分，或者创建标记流的特殊结构。

So if you look at this encoder object from OpenAI's GPT-2 right here, we mentioned this is very similar to our vocab. You'll notice that the length of this is 50,257. As I mentioned, it's a mapping and it's inverted from the mapping of our vocab. Our vocab goes from integer to string and they go the other way around for no amazing reason.

But the thing to note here is that the mapping table here is 50,257. Where does that number come from? Where are the tokens? As I mentioned, there are 256 raw byte tokens. And then OpenAI actually did 50,000 merges so those become the other tokens but this would have been 50,256. So what is the 57th token?

And there is basically one special token and that one special token you can see is called "end of text". So this is a special token, and it's the very last token, and this token is used to delimit documents in the training set.

让我们看一下 OpenAI 的 GPT-2 模型中的编码器对象。这个编码器与我们之前讨论的词汇表非常相似。你会注意到它的长度是 50,257。如我之前提到的，这是一个映射表，但与我们词汇表的映射方向相反。我们的词汇表是从整数映射到字符串，而他们则是从字符串映射到整数，这种差异并没有特别的原因。

这个映射表的长度是 50,257，这个数字是怎么来的呢？让我们来分析一下标记的构成。正如我之前提到的，有 256 个原始字节标记。然后 OpenAI 实际上进行了 50,000 次 BPE 合并，产生了另外 50,000 个标记。这样算下来应该是 50,256 个标记。那么，第 50,257 个标记是什么呢？

实际上，这第 50,257 个标记是一个特殊标记，被称为「文本结束」（end of text）标记。这个特殊标记是整个词汇表中的最后一个标记，它在训练集中用于分隔不同的文档。

通过添加这种特殊标记，模型可以更好地理解文本的结构和边界，从而提高其理解和生成文本的能力。

So when we're creating the training data, we have all these documents, and we tokenize them, and we get a stream of tokens. Those tokens only range from 0 to 50,256. And then in between those documents, we put a special "end of text" token. And we insert that token in between documents.

And we are using this as a signal to the language model that the document has ended and what follows is going to be unrelated to the document previously. That said, the language model has to learn this from data. It needs to learn that this token usually means that it should wipe its sort of memory of what came before and what came before this token is not actually informative to what comes next. But we are expecting the language model to just like learn this, but we're giving it the special sort of delimiter of these documents.

在创建训练数据时，我们首先对所有文档进行分词（tokenize），生成一个 token 序列。这些 token 的编号范围仅在 0 到 50,256 之间。然后，我们在每个文档的结尾插入一个特殊的「文本结束」（end of text）token，作为文档间的分隔符。

这个特殊 token 的作用是向语言模型发出信号，表示当前文档已经结束，接下来的内容与之前的文档无关。然而，语言模型需要从数据中学习理解这个信号的含义。它需要学会识别这个特殊 token，并明白在遇到这个 token 时应该「重置」其上下文记忆，因为这个 token 之前的内容对理解后续内容没有帮助。

虽然我们提供了这个特殊的文档分隔符，但我们仍然期望语言模型能够自主学习理解它的作用。这个过程是语言模型训练中的一个重要方面，它使模型能够更好地处理多文档数据集，并在不同文档之间保持适当的语境隔离。

We can go here to tiktokenizer and this is the GPT-2 tokenizer, our code that we've been playing with before. So we can add here, right, "hello world how are you" and we're getting different tokens but now you can see what happens if I put "end of text". 

You see how until I finished it, these are all different tokens. "End of text", still separate tokens. And now when I finish it, suddenly we get token 50,256. And the reason this works is because this didn't actually go through the BPE merges.

Instead, the code that actually outputs the tokens has special case instructions for handling special tokens. We did not see these special instructions for handling special tokens in the encoder.py. It's absent there.

But if you go to tiktoken library, which is implemented in Rust, you will find all kinds of special case handling for these special tokens that you can register, create, add to the vocabulary, and then it looks for them and whenever it sees these special tokens like this, it will actually come in and swap in that special token.

So these things are outside of the typical algorithm of byte pairing coding. So these special tokens are used pervasively, not just in basically base language modeling of predicting the next token in the sequence, but especially when it gets to later to the fine tuning stage and all of the ChatGPT sort of aspects of it, because we don't just want to delimit documents, we want to delimit entire conversations between an assistant and a user.

我们可以访问 tiktokenizer，这是 GPT-2 的分词器，也就是我们之前一直在使用的代码。让我们在这里输入 "hello world how are you"，你会看到它被分解成不同的 token（词元）。现在，让我们看看当我输入 "end of text" 时会发生什么。

注意观察，在我完成输入之前，这些词都被分解成不同的 token。"End of text" 仍然被拆分成单独的 token。但当我输入完成后，突然出现了编号为 50,256 的 token。这种情况的出现是因为这个过程并没有经过 BPE（字节对编码）的合并操作。

实际上，负责输出 token 的代码中包含了处理特殊 token 的专门指令。我们在之前查看的 encoder.py 文件中并没有看到这些处理特殊 token 的指令，它们在那里是缺失的。

但如果你查看 tiktoken 库（它是用 Rust 语言实现的），你会发现有各种处理这些特殊 token 的特殊情况。你可以注册、创建这些特殊 token，将它们添加到词汇表中，然后代码会搜索它们。每当遇到这些特殊 token 时，它实际上会介入并用相应的特殊 token 替换它们。

这些特殊标记超出了典型的字节对编码（byte pair encoding）算法的范畴。这些特殊的 token（标记）被广泛使用，不仅仅是在基本的语言模型中用于预测序列中的下一个 token，更重要的是在后续的微调阶段和 ChatGPT 的各个方面发挥作用。这是因为我们不仅需要划分文档，还需要划分 AI 助手和用户之间的整个对话。

So if I refresh this TikTokenizer page, the default example that they have here is using not sort of base model encoders but fine-tuned model sort of tokenizers. So for example using the GPT-3.5 Turbo scheme, these here are all special tokens. "IAM_start", "IAM_end", etc. This is short for imaginary_assistant_message_start by the way.

But you can see here that there's a sort of start and end of every single message and there can be many other tokens, lots of tokens, in use to delimit these conversations and kind of keep track of the flow of the messages here.

Now we can go back to the TikToken library and here when you scroll to the bottom they talk about how you can extend TikToken and now you can create basically you can fork the CL100K base tokenizer as used in GPT-4 and for example you can extend it by adding more special tokens.

And these are totally up to you, you can come up with any arbitrary tokens and add them with the new ID afterwards and the TikToken library will correctly swap them out when it sees this in the strings.

如果我刷新这个 TikTokenizer 页面，我们可以看到他们的默认示例使用的不是基础模型的编码器，而是类似于微调模型的 tokenizer。例如，使用 GPT-3.5 Turbo 方案时，这里展示的都是特殊 token。"IAM_start"、"IAM_end" 等就是其中的例子。顺便说一下，"IAM" 是 "imaginary_assistant_message"（虚拟助手消息）的缩写。

从这个例子中我们可以看出，每条消息都有一个开始和结束标记。除此之外，还可能使用许多其他 token，大量的 token 被用来划分这些对话并追踪消息的流程。这种设计使得模型能够更好地理解和管理复杂的对话结构。

现在让我们回到 TikToken 库。当你滚动到页面底部时，你会发现他们讨论了如何扩展 TikToken 的功能。现在你可以基于 GPT-4 使用的 CL100K 基础分词器（tokenizer）创建一个新的版本，例如，你可以通过添加更多特殊 token 来扩展它。

这些特殊 token 完全由你自己定义。你可以创建任何自定义的 token（即文本的最小单位），并为它们分配新的 ID。TikToken 库会在处理字符串时正确地识别和替换这些特殊 token。

Now we can also go back to this file which we looked at previously and I mentioned that the GPT-2 in tiktoken/ext/openai_public.py we have the vocabulary, we have the pattern for splitting, and then here we are registering the single special token in GPT-2, which was the "end of text" token, and we saw that it has this ID.

In GPT-4, when they defined this here, you see that the pattern has changed as we've discussed, but also the special tokens have changed in this tokenizer. So we of course have the "end of text", just like in GPT-2 but we also see three, sorry four additional tokens here. "FIM_prefix", "middle" and "suffix".

What is FIM? FIM is short for "fill in the middle" and if you'd like to learn more about this idea it comes from this paper and I'm not going to go into detail in this video, it's beyond this video. And then there's one additional uh stripped token here so that's that encoding as well.

So it's very common basically to train a language model and then if you'd like you can add special tokens. Now when you add special tokens you of course have to do some model surgery to the transformer and all the parameters involved in that transformer because you are basically adding an integer and you want to make sure that for example your embedding matrix for the vocabulary tokens has to be extended by adding a row.

And typically this row would be initialized with small random numbers or something like that because we need to have a vector that now stands for that token. In addition to that you have to go to the final layer of the transformer and you have to make sure that that projection at the very end into the classifier is extended by one as well.

So basically there's some model surgery involved that you have to couple with the tokenization changes if you are going to add special tokens. But this is a very common operation that people do, especially if they'd like to fine-tune the model, for example taking it from a base model to a chat model like ChatGPT.

现在我们可以回顾之前提到的文件。我曾经提到在 tiktoken/ext/openai_public.py 文件中的 GPT-2 相关代码，其中包含词汇表、用于分割文本的模式，以及注册 GPT-2 中唯一的特殊 token 的部分。这个特殊 token 是「文本结束」（end of text）token，我们看到它有一个特定的 ID。

在 GPT-4 的定义中，我们可以看到不仅分割模式发生了变化（正如我们之前讨论的），而且这个分词器中的特殊 token 也有所改变。我们仍然保留了「文本结束」token，就像在 GPT-2 中一样，但我们还可以看到四个额外的 token："FIM_prefix"、"FIM_middle" 和 "FIM_suffix"。

什么是 FIM？FIM 是「填充中间」（Fill In the Middle）的缩写。如果你想深入了解这个概念，可以参考相关论文，不过在本视频中我们不会详细讨论，因为这超出了我们的范围。此外，这里还有一个额外的特殊 token（用于标记特定含义的符号），它也是编码的一部分。

通常情况下，我们会先训练一个语言模型，然后根据需要添加一些特殊 token。当你添加特殊 token 时，你实际上是在向模型中引入新的整数标识。这就需要对 Transformer 模型及其相关参数进行一些调整。比如，你需要确保用于词汇 token 的嵌入矩阵（embedding matrix）能够通过增加一行来进行扩展。

这新增的一行通常会被初始化为一些小的随机数，因为我们需要一个向量来代表这个新的 token。除此之外，你还需要修改 Transformer 的最后一层，确保最终投射到分类器（classifier）的那部分也相应地扩展了一位。

所以基本上，如果你想添加特殊 token，你需要对模型进行一些调整，并将这些调整与分词器的变化相结合。这是一个非常常见的操作，特别是当人们想要对模型进行微调（fine-tune）时，比如将基础模型转变为像 ChatGPT 这样的聊天模型。

#### 06

Okay, so at this point you should have everything you need in order to build your own GPT-4 tokenizer. Now in the process of developing this lecture I've done that and I've published the code under this repository minbpe. 

So minbpe looks like this right now as I'm recording, but the minbpe repository will probably change quite a bit because I intend to continue working on it. In addition to the minbpe repository, I've published this exercise progression that you can follow.

So if you go to exercise.md here, this is sort of me breaking up the task ahead of you into four steps that sort of build up to what can be a GPT-4 tokenizer. And so feel free to follow these steps exactly and follow a little bit of the guidance that I've laid out here. And anytime you feel stuck, just reference the minbpe repository here.

So either the tests could be useful or the minbpe repository itself. I try to keep the code fairly clean and understandable and so feel free to reference it whenever you get stuck. In addition to that basically, once you write it you should be able to reproduce this behavior from tiktoken.

好了，到这里你应该已经掌握了构建自己的 GPT-4 分词器所需的所有知识。在准备这门课程的过程中，我已经实践了这一点，并且我已经在名为 minbpe 的 GitHub 仓库中发布了相关代码。

目前，在我录制这段内容时，minbpe 的样子是这样的。不过，minbpe 仓库可能会发生很大变化，因为我打算继续对它进行开发。除了 minbpe 仓库之外，我还发布了一个你可以按步骤完成的练习系列。

如果你查看 exercise.md 文件，你会发现我把构建 GPT-4 分词器的任务分解成了四个渐进的步骤。你可以完全按照这些步骤进行，并参考我在其中提供的一些指导。如果在任何时候你感到困惑或遇到困难，都可以随时查阅 minbpe 仓库中的代码作为参考。

minbpe 仓库中的测试用例和代码本身都可能对你有所帮助。我一直努力保持代码的整洁和易读性，所以当你遇到困难时，随时可以参考它。基本上，一旦你完成编写，你应该能够复现 tiktoken（一个分词工具库）的功能。

So getting the GPT-4 tokenizer you can encode this string and you should get these tokens and then you can encode and decode the exact same string to recover it. And in addition to all that, you should be able to implement your own train function, which tiktoken library does not provide. It's again, only inference code, but you should write your own train. Minbpe does it as well.

And that will allow you to train your own token vocabularies. So here's some of the code inside minbpe. Minbpe shows the token vocabularies that you might obtain. So on the left here, we have the GPT-4 merges.

So the first 256 are raw individual bytes, and then here I am visualizing the merges that GPT-4 performed during its training. So the very first merge that GPT-4 did was merge two spaces into a single token for two spaces, and that is the token 256.

And so this is the order in which things merged during GPT-4 training, and this is the merge order that we obtain in minbpe by training a tokenizer. And in this case, I trained it on a Wikipedia page of Taylor Swift, not because I'm a Swifty, but because that is one of the longest Wikipedia pages, apparently, that's available. But she is pretty cool.

具体来说，你可以使用 GPT-4（一种先进的大语言模型）的分词器对给定的字符串进行编码，得到相应的 token（标记，即文本的基本单位）。然后，你应该能够对完全相同的字符串进行编码和解码，从而恢复原始文本。除此之外，你还应该能够实现自己的训练函数。这是 tiktoken 库没有提供的功能 —— tiktoken 只提供了推理（inference）代码，但你应该编写自己的训练部分。Minbpe（另一个分词工具库）也实现了这一功能。

这将使你能够训练自己的 token 词汇表。在 minbpe 的代码中，你可以看到可能获得的 token 词汇表的示例。在左边，我们可以看到 GPT-4 的合并（merges）操作。

首先，前 256 个 token 是原始的单个字节。然后，我正在可视化展示 GPT-4 在训练过程中执行的合并操作。GPT-4 执行的第一个合并操作是将两个空格合并成一个单独的 token，表示两个空格，这就是编号为 256 的 token。

这就是 GPT-4 在训练过程中词元（token）合并的顺序，也是我们在 minbpe 中通过训练分词器（tokenizer）得到的合并顺序。在这个例子中，我使用 Taylor Swift 的维基百科页面进行训练，不是因为我是她的狂热粉丝，而是因为这恰好是最长的维基百科页面之一。不过话说回来，她确实很酷。

And what was I going to say? Yeah, so you can compare these two vocabularies. And so as an example, here GPT-4 merged "in" to become "IN", and we've done the exact same thing on this token, 259. Here, "space T" becomes "space T", and that happened for us a little bit later as well.

So the difference here is, again, to my understanding, only a difference of the training set. So as an example, because I see a lot of white space, I expect that GPT-4 probably had a lot of Python code in its training set for the tokenizer and here we see much less of that of course in the Wikipedia page.

So roughly speaking they look the same and they look the same because they're running the same algorithm and when you train your own you're probably gonna get something similar depending on what you train it on.

我刚才想说什么来着？哦对了，你可以比较这两个词汇表。例如，在这里 GPT-4 将 "in" 合并成了 "IN"，我们在第 259 个词元上做了完全相同的操作。再比如，"空格 T" 变成了 "空格 T"，在我们的训练中也发生了类似的合并，只是时间稍晚一些。

所以这里的区别，据我理解，主要来自训练集（training set）的不同。举个例子，因为我看到很多空白字符，我推测 GPT-4 的分词器训练集中可能包含了大量 Python 代码，而在这个维基百科页面中，这种情况就少得多。

总的来说，这两个词汇表看起来很相似，这是因为它们运行的是相同的算法。当你训练自己的分词器时，你可能会得到类似的结果，具体取决于你使用的训练数据。

#### 07

Okay so we are now going to move on from TikToken and the way that OpenAI tokenizes its strings. We're going to discuss one more very commonly used library for working with tokenization in LLMs and that is SentencePiece.

So SentencePiece is very commonly used in language models because unlike TikToken it can do both training and inference and is quite efficient at both. It supports a number of algorithms for training vocabularies, but one of them is the byte-pairing coding algorithm that we've been looking at. So it supports it.

Now, SentencePiece is used both by the Llama and Mistral series and many other models as well. It is on GitHub under google/sentencepiece. And the big difference with SentencePiece, and we're going to look at an example because this is kind of hard and subtle to explain, is that they think differently about the order of operations here.

接下来，我们将不再讨论 TikToken 和 OpenAI 的字符串分词方式，而是转向另一个在大语言模型（LLM）中广泛使用的分词库：SentencePiece。

SentencePiece 在大语言模型中非常流行，原因在于它不同于 TikToken，既能进行训练又能进行推理，而且这两项功能都非常高效。它支持多种用于训练词汇表的算法，其中包括我们一直在研究的字节对编码（byte-pairing coding）算法。

目前，SentencePiece 被 Llama 和 Mistral 系列以及许多其他模型所采用。它的 GitHub 仓库地址是 google/sentencepiece。SentencePiece 的一个主要特点在于其操作顺序的不同理念。这一点比较微妙，难以解释，所以我们待会儿会通过一个例子来说明。

So in the case of TikToken, we first take our code points in the string, we encode them using UTF-8 to bytes, and then we're merging bytes. It's fairly straightforward. For SentencePiece, it works directly on the level of the code points themselves.

So it looks at whatever code points are available in your training set and then it starts merging those code points and the BPE is running on the level of code points. If you happen to run out of code points, so there are maybe some rare code points that just don't come up too often and the rarity is determined by this character_coverage hyperparameter, then these code points will either get mapped to a special unknown token like unk, or if you have the byte_fallback option turned on, then that will take those rare code points, it will encode them using UTF-8 and then the individual bytes of that encoding will be translated into tokens and there are these special byte tokens that basically get added to the vocabulary.

So it uses BPE on the code points and then it falls back to bytes for rare code points. And so that's kind of like the difference. Personally I find the TikToken way significantly cleaner, but it's kind of like a subtle but pretty major difference between the way they approach tokenization.

对于 TikToken 来说，其处理过程相对直接：首先获取字符串中的码点（code points），然后使用 UTF-8 将它们编码为字节，最后合并这些字节。而 SentencePiece 则直接在码点本身的层面上进行操作。

这种方法首先会查看训练数据集中所有可用的字符编码点（code points），然后开始合并这些编码点，这个过程中使用的是字节对编码（Byte Pair Encoding, BPE）算法，并在编码点层面上进行操作。如果出现了一些罕见的编码点（其稀有程度由 character_coverage 这个超参数决定），系统会采取两种处理方式之一：要么将这些罕见编码点映射到一个特殊的未知标记（如 "unk"），要么在启用了 byte_fallback 选项的情况下，将这些罕见编码点用 UTF-8 编码，然后将编码后的单个字节转换为特殊的字节标记，并将这些标记添加到词汇表中。

简而言之，这种方法在编码点层面使用 BPE 算法，对于罕见的编码点则回退到字节级别处理。相比之下，TikToken（一种不同的分词方法）采用了另一种策略。从个人角度来看，我认为 TikToken 的方法明显更加简洁，尽管这两种分词方法的区别看似微小，但实际上是相当重要的。

Let's work with a concrete example because otherwise this is kind of hard to get your head around. So let's work with a concrete example. This is how we can import sentencepiece and then here we're going to take, I think I took like the description of sentencepiece and I just created like a little toy dataset.

SentencePiece really likes to have a file so I created a toy.txt file with this content. Now what's kind of a little bit crazy about sentencepiece is that there's a ton of options and configurations and the reason this is so is because sentencepiece has been around I think, for a while, and it really tries to handle a large diversity of things. 

Because it's been around, I think it has quite a bit of accumulated historical baggage as well. In particular, there's a ton of configuration arguments. This is not even all of it. You can go to here to see all the training options. There's also quite useful documentation when you look at the raw protobuf that is used to represent the trainer spec and so on.

Many of these options are irrelevant to us. Maybe to point out one example, --shrinking_factor. This shrinking_factor is not used in the byte pairing coding algorithm, so this is just an argument that is irrelevant to us. It applies to a different training algorithm.

让我们用一个具体的例子来说明，因为这样更容易理解。我们先看看如何导入 SentencePiece，然后我们将使用 SentencePiece 的描述来创建一个简单的示例数据集。

SentencePiece 通常需要一个文件作为输入，所以我创建了一个名为 toy.txt 的文件，里面包含这些内容。SentencePiece 的一个特点是它有大量的选项和配置，这是因为 SentencePiece 已经存在了一段时间，它试图处理各种各样的情况。

由于它已经存在了一段时间，我认为它也积累了相当多的历史遗留问题。特别是，它有大量的配置参数。这里列出的甚至还不是全部。你可以在这里查看所有的训练选项。此外，当你查看用于表示训练器规格的原始 protobuf 时，也能找到一些非常有用的文档。

这些选项中有许多与我们无关。例如，--shrinking_factor 参数。这个 shrinking_factor 在字节对编码（BPE）算法中并不使用，所以它只是一个与我们无关的参数，适用于其他的训练算法。

Now what I tried to do here is I tried to set up sentencepiece in a way that is very very similar, as far as I can tell, to maybe identical hopefully, to the way that Llama2 was trained, so the way they trained their own tokenizer.

And the way I did this was basically you can take the tokenizer.model file that Meta released and you can open it using the protobuf file that you can generate and then you can inspect all the options and I tried to copy over all the options that looked relevant.

So here we set up the input. It's raw text in this file. Here's gonna be the output so it's gonna be phototok400.model and .vocab. We're saying that we're gonna use the BPE algorithm and we want a vocab size of 400.

Then there's a ton of configurations here for basically pre-processing and normalization rules, as they're called. Normalization used to be very prevalent, I would say, before LLMs in natural language processing.

So in machine translation and text classification and so on, you want to normalize and simplify the text, and you want to turn it all lowercase, and you want to remove all double whitespace, etc. And in language models, we prefer not to do any of it, or at least that is my preference. As a deep learning person, you want to not touch your data, you want to keep the raw data as much as possible in a raw form, so you're basically trying to turn off a lot of this if you can.

在这里，我尝试将 sentencepiece 的设置方式尽可能地接近 Llama2 训练其分词器的方式，希望能完全相同。

我的方法是：首先获取 Meta 发布的 tokenizer.model 文件，然后使用生成的 protobuf 文件打开它，检查所有的选项，然后尝试复制所有看起来相关的选项。

这里我们设置了输入，它是文件中的原始文本。输出将是 "phototok400.model" 和 ".vocab" 文件。我们指定使用 BPE 算法，并将词汇表大小设为 400。

然后这里有大量的配置，主要用于预处理和所谓的规范化规则。值得注意的是，在大语言模型（LLM）出现之前，规范化在自然语言处理（NLP）中曾经非常普遍。

在机器翻译和文本分类等任务中，通常需要对文本进行规范化和简化处理。这包括将所有英文字母转换为小写，删除多余的空白字符等。然而，在语言模型（Language Model）中，我们倾向于不进行这些处理，或者至少这是我个人的偏好。从深度学习的角度来看，我们希望尽可能保持数据的原始形态，也就是说，我们会尽量避免对数据进行预处理。

The other thing that sentencepiece does is that it has this concept of sentences. So sentencepiece, its background kind of like was developed I think early in the days where there was an idea that you're training a tokenizer on a bunch of independent sentences.

So it has a lot of like how many sentences you're going to train on, what is the maximum sentence length, shuffling sentences and so on. For it, sentences are kind of like the individual training examples.

But again, in the context of LLMs, I find that this is like a very spurious and weird distinction. Like sentences are just like, don't touch the raw data. Sentences happen to exist. But in the raw datasets, there are a lot of like in-betweens, like what exactly is a sentence? What isn't a sentence?

And so I think like it's really hard to define what an actual sentence is if you really dig into it and there could be different concepts of it in different languages or something like that. So why even introduce the concept? It doesn't honestly make sense to me, I would just prefer to treat a file as a giant stream of bytes.

SentencePiece（一种分词工具）的另一个特点是引入了「句子」的概念。SentencePiece 的开发背景可以追溯到早期，当时有一种想法是在一系列独立的句子上训练分词器（tokenizer）。

因此，SentencePiece 包含了许多与句子相关的参数，例如训练时使用的句子数量、最大句子长度、句子随机化等。在 SentencePiece 中，句子被视为独立的训练样本。

然而，在大语言模型（LLM）的语境中，我认为这种区分是非常牵强和奇怪的。例如，句子就像是一种既定存在，我们不应该去触碰原始数据。但在原始数据集中，存在许多模糊的边界情况。究竟什么才算是一个句子？什么又不是句子呢？

我认为，如果深入研究，很难给「句子」下一个确切的定义，而且在不同语言中可能有不同的概念。那么，为什么要引入这个概念呢？老实说，我觉得这没有太大意义。我更倾向于将一个文件视为一个巨大的字节流来处理。

SentencePiece has a lot of treatment around the rare word characters and when I say word I mean code points. We're going to come back to this in a second and it has a lot of other rules for basically splitting digits, splitting white space and numbers and how you deal with that.

So these are some kind of like merge rules. I think this is a little bit equivalent to TikToken using the regular expression to split up categories. There's kind of equivalence of it if you squint at it in SentencePiece where you can also, for example, split up the digits and so on.

There's a few more things here that I'll come back to in a bit, and then there are some special tokens that you can indicate. It hard codes the unk token, the beginning of sentence, end of sentence and a pad token. And the unk token must exist from my understanding. And then some system things.

So we can train and when I press train it's going to create this file tok400.model and tok400.vocab. I can then load the model file and I can inspect the vocabulary of it. And so we trained vocab size 400 on this text here. And these are the individual pieces, the individual tokens that sentencepiece will create.

SentencePiece 对罕见的字符有很多处理方法，这里的「字符」指的是码点（code points）。我们稍后会详细讨论这一点。此外，它还有许多其他规则，主要用于分割数字、分割空白字符和数字，以及如何处理这些情况。

这些可以看作是一种合并规则。我认为这在某种程度上类似于 TikToken 使用正则表达式来分割不同类别。如果仔细观察 SentencePiece，你会发现它也有一些等效的功能，例如，同样可以分割数字等。

接下来我还有一些内容稍后会详细讨论，其中包括一些可以自定义的特殊标记（token）。在这个系统中，有一些预设的特殊标记，包括未知词标记（UNK token)、句子开始标记、句子结束标记和填充标记（PAD token）。根据我的理解，未知词标记是必须存在的。除此之外，还有一些系统相关的设置。

现在我们可以开始训练模型了。当我点击训练按钮时，系统会创建两个文件：tok400.model 和 tok400.vocab。训练完成后，我可以加载这个模型文件并查看它的词汇表。在这个例子中，我们基于给定的文本训练了一个词汇量为 400 的模型。这个词汇表包含了分词工具 SentencePiece 创建的各个独立的标记。

So in the beginning we see that we have the unk token with the ID 0. Then we have the beginning of sequence, end of sequence, 1 and 2. And then we said that the pad ID is negative 1, so we chose not to use it. So there's no pad ID here.

Then these are individual byte tokens. So here we saw that byte fallback in Llama was turned on, so it's true. So what follows are going to be the 256 byte tokens and these are their IDs.

And then at the bottom, after the byte tokens come the merges and these are the parent nodes in the merges. So we're not seeing the children, we're just seeing the parents and their ID.

And then after the merges comes eventually the individual tokens and their IDs and so these are the individual tokens so these are the individual code point tokens if you will and they come at the end.

So that is the ordering with which sentencepiece sort of like represents its vocabularies. It starts with special tokens then the byte tokens, then the merge tokens, and then the individual code point tokens.

And all these raw code point tokens are the ones that it encountered in the training set. So those individual code points are all the entire set of code points that occurred here. So those all get put in there and then those are extremely rare as determined by character_coverage.

So if a code point occurred only a single time out of like a million sentences or something like that then it would be ignored and it would not be added to our vocabulary.

Once we have a vocabulary we can encode into IDs and we can sort of get a list. And then here I am also decoding the individual tokens back into little pieces as they call it.

在词汇表的开始，我们可以看到未知词标记的 ID 是 0。接着是序列开始标记和序列结束标记，它们的 ID 分别是 1 和 2。我们将填充标记的 ID 设置为 -1，这意味着我们选择不使用它，所以在这个词汇表中没有出现填充标记。

接下来的是单个字节标记。我们可以看到在 Llama 模型中，字节回退（byte fallback）功能被启用了。这意味着接下来会出现 256 个字节标记，每个标记都有其对应的 ID。这种机制确保了模型能够处理任何输入，即使遇到未知的字符也能通过这些字节标记来表示。

接下来，在底部字节 token（byte tokens）之后是合并项（merges），这些代表了合并过程中的父节点。我们在这里只能看到父节点及其 ID，而看不到子节点。

再往后，最终会出现单个 token 及其 ID。这些是独立的 token，可以理解为单个字符或代码点（code point）的 token，它们被放置在最后。

这就是 SentencePiece（一种用于文本分词的工具）表示其词汇表的排序方式。它的顺序是：首先是特殊 token，然后是字节 token，接着是合并 token，最后是单个字符 token。

所有这些原始的字符 token 都是 SentencePiece 在训练集中遇到的。换句话说，这些单个字符代表了训练数据中出现的所有字符的完整集合。这些字符被添加到词汇表中，但它们通常由 character_coverage 参数确定为极其罕见的字符。

例如，如果一个字符在一百万个句子中只出现一次，那么它可能会被忽略，不会被添加到我们的词汇表中。这种机制有助于控制词汇表的大小，并专注于更常见和更有意义的 token。

一旦我们有了词汇表（vocabulary），我们就可以将文本编码（encode）成 ID，得到一个 ID 列表。在这里，我还将单个 token 解码（decode）回它们所谓的「小片段」。

So let's take a look at what happened here. "Hello space". So these are the token IDs we got back. 안녕하세요. So these are the token IDs we got back and when we look here a few things sort of jump to mind.

Number one, take a look at these characters, the Korean characters. Of course, they were not part of the training set so sentencepiece is encountering code points that it has not seen during training time and those code points do not have a token associated with them. So suddenly these are unk tokens, unknown tokens.

But because byte_fallback is true, instead sentencepiece falls back to bytes. And so it takes this, it encodes it with UTF-8, and then it uses these tokens to represent those bytes. And that's what we are getting sort of here. This is the UTF-8 encoding and it is shifted by three because of these special tokens here that have IDs earlier on.

让我们来看看这里发生了什么。对于 "Hello space" 这个输入，我们得到了对应的 token ID。对于韩语输入 "안녕하세요"，我们也得到了相应的 token ID。观察这些结果，我们可以注意到几个重要的点：

首先，看看这些韩语字符。显然，它们不是训练集的一部分，所以 SentencePiece 遇到了在训练时没有见过的 Unicode 代码点，这些代码点没有与之对应的 token。因此，这些字符本应被标记为未知 token（unknown token，简称 unk token）。

但是，由于 `byte_fallback` 参数设置为 true，SentencePiece 采用了字节回退（byte fallback）机制。它将这些字符用 UTF-8 编码，然后使用特定的 token 来表示这些字节。这就是我们在结果中看到的情况。这些 token 实际上代表了 UTF-8 编码，而且它们的 ID 值比正常情况下要大 3，这是因为在词汇表的开头有三个特殊 token 占用了较小的 ID 值。

So that's what happened here. Now one more thing that, well first before I go on, with respect to the byte_fallback. Let me remove byte_fallback. If this is false, what's gonna happen? Let's retrain.

So the first thing that happened is all the byte tokens disappeared, right? And now we just have the merges and we have a lot more merges now because we have a lot more space because we're not taking up space in the vocab size with all the bytes.

And now if we encode this we get a zero. So this entire string here suddenly there's no byte fallback so this is unknown and unknown is unk and so this is zero because the unk token is token zero.

And you have to keep in mind that this would feed into your language model. So what is a language model supposed to do when all kinds of different things that are unrecognized because they're rare just end up mapping into unk? It's not exactly the property that you want.

So that's why I think Llama correctly used byte_fallback true, because we definitely want to feed these unknown or rare code points into the model in some manner.

让我们继续讨论 byte_fallback（字节回退）机制。如果我们将 byte_fallback 设置为 false 会发生什么呢？让我们重新训练模型看看结果。

首先，所有的字节 token 都消失了。现在我们只剩下合并后的 token，而且数量比之前多了很多。这是因为我们不再在词汇表中为所有的字节保留空间，从而有更多的空间用于其他 token。

现在，如果我们尝试对之前的字符串进行编码，我们会得到一个零。这是因为没有了字节回退机制，整个字符串变成了未知词，而未知词用 "unk"（unknown 的缩写）表示。在词汇表中，"unk" token 通常被赋予索引 0。

我们需要考虑这对语言模型的影响。当各种罕见或无法识别的输入都被映射为 "unk" 时，语言模型该如何处理呢？这显然不是我们想要的结果。

这就是为什么我认为 Llama（一种大型语言模型）正确地选择了启用 byte_fallback。我们确实希望以某种方式将这些未知或罕见的字符输入到模型中，而不是简单地将它们全部视为未知。

The next thing I want to show you is the following. Notice here when we are decoding all the individual tokens, you see how spaces, space here, ends up being this bold underline. I'm not 100% sure, by the way, why sentencepiece switches whitespace into these bold underscore characters. Maybe it's for visualization. I'm not 100% sure why that happens.

But notice this. Why do we have an extra space in the front of "hello"? Where is this coming from? Well, it's coming from this option here. add_dummy_prefix is true. And when you go to the documentation, add dummy white space at the beginning of text in order to treat "world" in "world" and "hello world" in the exact same way.

So what this is trying to do is the following. If we go back to our TikTokenizer, "world" as a token by itself has a different ID than "space world". So we have this is 1917, but this is 14, etc. So these are two different tokens for the language model.

And the language model has to learn from data that they are actually kind of like a very similar concept. So to the language model in the TikToken world, basically words in the beginning of sentences and words in the middle of sentences actually look completely different and it has to learn that they are roughly the same.

So this add_dummy_prefix is trying to fight that a little bit and the way that works is that it basically adds a dummy prefix. So as a part of preprocessing, it will take the string and it will add a space. It will do this. And that's done in an effort to make this "world" and that "world" the same. They will both be "space world". So that's one other kind of preprocessing option that is turned on.

And Llama2 also uses this option. And that's I think everything that I wanna say from my preview of sentencepiece and how it is different. Maybe here what I've done is I just put in the raw protocol buffer representation basically of the tokenizer that Llama2 trained.

So feel free to sort of step through this and if you would like your tokenization to look identical to that of the Meta Llama2 then you would be copy pasting these settings as I've tried to do up above.

接下来，我想为你展示一个有趣的现象。在解码单个 token（标记）时，你可能会注意到空格被显示为粗体下划线。说实话，我也不太确定为什么 SentencePiece（一种分词工具）要将空白字符转换成这种粗体下划线的形式。这可能是为了更好的可视化效果，但具体原因我也不是很清楚。

不过，这里有一个值得注意的地方：为什么 "hello" 这个词前面会多出一个空格呢？这个额外的空格是从哪里来的？其实，这是因为我们设置了一个选项：add_dummy_prefix 为 true。如果你查看文档，会发现这个选项的作用是「在文本开头添加一个虚拟的空白，以便以完全相同的方式处理单独的 'world' 和 'hello world' 中的 'world'」。

那么，这个设置究竟是为了解决什么问题呢？让我们回到 TikTokenizer（一种用于 token 化的工具）的例子。你会发现，单独的 "world" 作为一个 token 的 ID 是 1917，而 "空格 + world" 的 ID 则是 14。这意味着对于语言模型来说，这两者是完全不同的 token。

语言模型必须从数据中学习到，句子开头和句子中间的相同单词实际上是非常相似的概念。然而，在像 TikToken 这样的分词系统中，句子开头和中间的相同单词对语言模型来说可能看起来完全不同，模型必须学会识别它们本质上是相同的。

为了解决这个问题，研究者们引入了一个叫做「添加虚拟前缀」（add_dummy_prefix）的技术。这种预处理方法会在每个输入字符串的开头添加一个空格。这样做的目的是使句子开头和中间的相同单词在模型眼中变得一致。例如，无论 "world" 这个词出现在句子的哪个位置，它们都会变成 "空格 world"。这个预处理选项在很多模型中都被启用了。

值得注意的是，Llama2（一个由 Meta 公司开发的大型语言模型）也使用了这个选项。这基本上概括了我想说的关于 SentencePiece（一种常用的分词工具）的预览，以及它与其他分词方法的不同之处。

在这里，我提供了 Llama2 训练时使用的分词器的原始协议缓冲区（protocol buffer）表示。如果你希望你的分词结果与 Meta 的 Llama2 完全相同，你可以参考并使用这些设置，就像我在上面尝试做的那样。这些设置详细描述了分词器的各种参数和配置。

#### 08

And yeah that's I think that's it for this section. I think my summary for sentencepiece from all this is number one, I think that there's a lot of historical baggage in sentencepiece, a lot of concepts that I think are slightly confusing and I think potentially contain foot guns, like this concept of a sentence and its maximum length and stuff like that.

Otherwise it is fairly commonly used in the industry because it is efficient and can do both training and inference. It has a few quirks like for example unk token must exist and the way the byte fallbacks are done and so on. I don't find it particularly elegant.

And unfortunately I have to say it's not very well documented, so it took me a lot of time working with this myself and just visualizing things and trying to really understand what is happening here because the documentation unfortunately is in my opinion not super amazing.

我想这就是本节的全部内容了。总结一下我对 SentencePiece 的看法：

首先，我认为 SentencePiece 存在许多历史遗留问题。它包含了一些我认为略显混乱的概念，这些概念可能会成为潜在的隐患。例如，它对「句子」的定义以及句子最大长度的设置等。

尽管如此，由于 SentencePiece 效率高，且能同时用于训练和推理，它在业界仍被广泛使用。它有一些独特之处，比如必须包含未知词元（unk token），以及其特殊的字节回退（byte fallbacks）处理方式等。然而，我并不认为它的设计特别优雅。

遗憾的是，我不得不指出 SentencePiece 的文档质量不尽如人意。这导致我花费了大量时间来研究它，通过自行实验和数据可视化来真正理解其工作原理。因为在我看来，官方文档的质量确实有待提高。

#### 09

But it is a very nice repo that is available to you if you'd like to train your own tokenizer right now. Okay let me now switch gears again as we're starting to slowly wrap up here. I want to revisit this issue in a bit more detail of how we should set the vocab size and what are some of the considerations around it.

So for this I'd like to go back to the model architecture that we developed in the last video when we built the GPT from scratch. So this here was the file that we built in the previous video and we defined the transformer model and let's specifically look at vocab_size and where it appears in this file.

So here we define the vocab_size. At this time it was 65 or something like that, extremely small number, so this will grow much larger. You'll see that vocab_size doesn't come up too much in most of these layers. The only place that it comes up to is in exactly these two places here.

So when we define the language model, there's the token embedding table, which is this two-dimensional array where the vocab_size is basically the number of rows, and each vocabulary element, each token, has a vector that we're going to train using backpropagation. That vector is of size n_embd, which is number of channels in the transformer.

And basically, as vocab_size increases, this embedding table, as I mentioned earlier, is going to also grow. We're going to be adding rows. In addition to that, at the end of the transformer, there's this lm_head layer which is a linear layer and you'll notice that that layer is used at the very end to produce the logits which become the probabilities for the next token in a sequence.

不过，如果你现在想训练自己的分词器，这个仓库是一个很好的选择。好的，让我们稍微转换一下话题，因为我们正在慢慢接近尾声。我想更详细地 revisit 一下如何设置词汇表大小（vocab size）以及围绕它的一些考虑因素。

为此，我想回顾一下我们在上一个视频中从头构建 GPT 时开发的模型架构。让我们看看我们在上一个视频中创建的文件，其中我们定义了 Transformer 模型。特别地，我们来关注一下 vocab_size 在这个文件中出现的位置。

在这里，我们定义了 vocab_size。当时我们设置的值大约是 65，这是一个非常小的数字，在实际应用中这个数字会变得更大。你会发现 vocab_size 在大多数层中并没有频繁出现。事实上，它只在文件中的两个特定位置出现。

当我们设计语言模型时，有一个重要的组成部分叫做 token 嵌入表（token embedding table）。这是一个二维数组，其中行数基本上等于词汇表大小（vocab_size）。词汇表中的每个元素，也就是每个 token，都对应着一个向量。这些向量是通过反向传播（backpropagation）算法来训练的。每个向量的维度是 n_embd，也就是 Transformer 模型中的通道数。

随着词汇表大小的增加，这个嵌入表也会相应地增长，我们会不断地添加新的行。除此之外，在 Transformer 模型的末端，还有一个叫做 lm_head 的线性层。这个层在模型的最后被用来产生 logits（未归一化的预测概率），这些 logits 最终会转化为序列中下一个 token 的概率。

And so intuitively we're trying to produce a probability for every single token that might come next at every point in time of that transformer and if we have more and more tokens we need to produce more and more probabilities.

So every single token is going to introduce an additional dot product that we have to do here in this linear layer for this final layer in the transformer. So why can't vocab_size be infinite? Why can't we grow to infinity?

Well, number one, your token embedding table is going to grow. Your linear layer is going to grow. So we're going to be doing a lot more computation here because this lm_head layer will become more computationally expensive.

Number two, because we have more parameters we could be worried that we are going to be under-training some of these parameters. So intuitively if you have a very large vocabulary size, say we have a million tokens, then every one of these tokens is going to come up more and more rarely in the training data because there's a lot more other tokens all over the place.

And so we're going to be seeing fewer and fewer examples for each individual token. And you might be worried that basically the vectors associated with every token will be under-trained as a result because they just don't come up too often and they don't participate in the forward-backward pass.

从直观上理解，我们的目标是为 Transformer 模型在每个时间步可能出现的每一个 token 都计算一个概率。如果我们的词汇表越来越大，我们就需要计算越来越多的概率。

因此，每增加一个 token，我们就需要在这个线性层（也就是 Transformer 的最后一层）中多进行一次点积运算。那么，为什么词汇表大小不能无限增长呢？为什么我们不能让它变得无限大？

首先，随着词汇量的增加，模型的 token 嵌入表（token embedding table）和线性层（linear layer）的规模都会扩大。这意味着我们需要进行更多的计算，特别是在语言模型头部（lm_head）层，其计算成本将显著增加。

其次，参数数量的增加可能导致某些参数训练不足的问题。举个例子，如果我们的词汇表大小达到一百万个 tokens，那么每个 token 在训练数据中出现的频率就会变得越来越低，因为整个词汇表中存在更多其他的 tokens。

这就意味着我们对每个单独的 token 能够看到的训练样本会越来越少。因此，你可能会担心与每个 token 相关联的向量可能会由于出现频率过低而训练不足，因为它们很少参与模型的前向传播和反向传播过程。

In addition to that, as your vocab_size grows, you're going to start shrinking your sequences a lot, right? And that's really nice because that means that we're going to be attending to more and more text, so that's nice.

But also, you might be worrying that too large of chunks are being squished into single tokens, and so the model just doesn't have as much sort of time to think per sort of some number of characters in the text or you can think about it that way, right?

So basically we're squishing too much information into a single token and then the forward pass of the transformer is not enough to actually process that information appropriately and so these are some of the considerations you're thinking about when you're designing the vocab_size.

As I mentioned, this is mostly an empirical hyperparameter and it seems like in state-of-the-art architectures today this is usually in the high ten thousands or somewhere around a hundred thousand today.

另外，随着词汇表大小（vocab_size）的增长，我们可以用更少的 tokens 来表示相同长度的文本，从而缩短序列长度。这一点非常有益，因为它使得模型能够关注更多的文本内容，从而提高模型的性能。

但是，你可能也在担心另一个问题：是否有太多的信息被压缩成了单个 token（词元)？如果是这样，模型在处理这些高度压缩的信息时可能就没有足够的计算资源来充分理解和分析文本中的内容。

简单来说，如果我们将过多的信息压缩到单个 token 中，那么 Transformer 模型在前向传播过程中可能无法 adequately 处理这些信息。这就是为什么在设计词汇表大小（vocab_size）时需要考虑这些因素。

正如我之前提到的，词汇表大小主要是一个基于经验确定的超参数。在当今最先进的模型架构中，这个数值通常在几万到十万左右。

And the next consideration I want to briefly talk about is what if we want to take a pre-trained model and we want to extend the vocab_size? And this is done fairly commonly actually.

So for example when you're doing fine-tuning for ChatGPT a lot more new special tokens get introduced on top of the base model to maintain the metadata and all the structure of conversation objects between the user and assistant. So that takes a lot of special tokens.

You might also try to throw in more special tokens, for example, for using the browser or any other tool. And so it's very tempting to add a lot of tokens for all kinds of special functionality.

So if you want to be adding a token that's totally possible, right? All we have to do is we have to resize this embedding, so we have to add rows. We would initialize these parameters from scratch, which would be small random numbers, and then we have to extend the weight inside this linear.

So we have to start making dot products with the associated parameters as well to basically calculate the probabilities for these new tokens. So both of these are just resizing operations. It's a very mild model surgery and can be done fairly easily and it's quite common that basically you would freeze the base model, you introduce these new parameters and then you only train these new parameters to introduce new tokens into the architecture.

And so you can freeze arbitrary parts of it or you can train arbitrary parts of it and that's totally up to you. But basically minor surgery required if you'd like to introduce new tokens.

接下来，我想简要讨论另一个问题：如果我们想要在已有的预训练模型基础上扩展词汇表大小，该怎么做？实际上，这是一种相当常见的做法。

举个例子，当对 ChatGPT 进行微调（fine-tuning，即在特定任务上进行进一步训练）时，通常会在基础模型之上引入许多新的特殊 token。这些特殊 token 用于维护用户和 AI 助手之间对话的元数据和结构。这个过程需要大量的特殊 token。

你可能还想尝试加入更多特殊标记（token），比如用于浏览网页或使用其他工具的标记。这样一来，为各种特殊功能添加大量标记的想法就变得非常诱人了。

那么，如果你想添加一个新的标记，这完全是可行的，对吧？我们需要做的就是调整嵌入（embedding）的大小，也就是增加一些行。我们会从头开始初始化这些新参数，它们将是一些小的随机数。然后，我们还需要扩展线性层（linear layer）中的权重。

接下来，我们就要开始用这些新参数进行点积（dot product）运算，基本上是为了计算这些新标记的概率。这两个步骤其实都只是调整大小的操作。这种对模型的微调可以比较容易地完成，而且这种做法很常见。通常的做法是，你会先冻结基础模型，然后引入这些新参数，最后只训练这些新参数，从而将新标记引入到模型架构中。

你可以自由选择冻结或训练模型的任何部分，这完全取决于你的需求。但总的来说，如果你想引入新的标记，只需要对模型进行一些小小的调整就可以了。

And finally I'd like to mention that actually there's an entire design space of applications in terms of introducing new tokens into a vocabulary that go way beyond just adding special tokens and special new functionality.

So just to give you a sense of the design space, but this could be an entire video just by itself, this is a paper on learning to compress prompts with what they called gist tokens. And the rough idea is, suppose that you're using language models in a setting that requires very long prompts.

Well, these long prompts just slow everything down because you have to encode them, and then you have to use them, and then you're attending over them, and it's just heavy to have very large prompts.

So instead what they do here in this paper is they introduce new tokens and imagine basically having a few new tokens, you put them in a sequence and then you train the model by distillation. So you are keeping the entire model frozen and you're only training the representations of the new tokens, their embeddings, and you're optimizing over the new tokens such that the behavior of the language model is identical to the model that has a very long prompt that works for you.

And so it's a compression technique of compressing that very long prompt into those few new gist tokens. And so you can train this and then at test time you can discard your old prompt and just swap in those tokens and they sort of like stand in for that very long prompt and have an almost identical performance.

And so this is one technique in a class of parameter efficient fine-tuning techniques where most of the model is basically fixed and there's no training of the model weights, there's no training of LoRa or anything like that, of new parameters. The parameters that you're training are now just the token embeddings.

So that's just one example, but this could again be like an entire video, but just to give you a sense that there's a whole design space here that is potentially worth exploring in the future.

最后，我想强调的是，在将新 token 引入词汇表方面，实际上存在着广阔的应用设计空间，远远超出了仅仅添加特殊 token 和新功能的范畴。

为了让你对这个设计空间有所了解（尽管这个主题本身就足够制作一个完整的视频），我想介绍一篇关于学习压缩提示的论文。这篇论文提出了一种称为「精华 token」（gist token）的概念。其基本思想是，假设你在一个需要非常长提示的场景中使用大语言模型。

这些长提示会显著降低整个过程的效率，因为你必须对它们进行编码，然后使用它们，还要在处理过程中持续关注它们。而且，处理这些大型提示本身就需要大量计算资源。

因此，这篇论文提出了引入新 token 的方法。你可以想象有几个新的 token，将它们放在一个序列中，然后通过知识蒸馏（distillation）的方式来训练模型。在这个过程中，整个模型的参数保持不变，只训练这些新 token 的表示（即它们的嵌入向量）。优化的目标是使得使用这些新 token 的语言模型行为，与使用原本有效但很长的提示的模型行为保持一致。

这是一种压缩技术，它可以将非常长的提示压缩成少量新的概要 token（gist tokens）。你可以先训练这个技术，然后在测试阶段抛弃原来的长提示，只使用这些新的 token。这些 token 可以代表原来的长提示，并且能够达到几乎相同的性能。

这种技术属于参数高效微调（parameter efficient fine-tuning）技术的一种。在这类技术中，模型的大部分参数基本上是固定不变的，不需要训练模型权重，也不需要训练 LoRa（一种低秩适应技术）或其他新参数。你只需要训练的参数就是这些 token 的嵌入表示（token embeddings）。

这只是众多技术中的一个例子。实际上，这个话题可以单独制作一整个视频。我提到这个例子，是想让你了解在这个领域中存在着广阔的设计空间，这些都可能值得我们在未来进行深入探索。

#### 10

The next thing I want to briefly address is that I think recently there's a lot of momentum in how you actually could construct transformers that can simultaneously process not just text as the input modality, but a lot of other modalities. So be it images, videos, audio, et cetera.

And how do you feed in all these modalities and potentially predict these modalities from a transformer? Do you have to change the architecture in some fundamental way? And I think what a lot of people are starting to converge towards is that you're not changing the architecture, you stick with the transformer, you just kind of tokenize your input domains and then call it a day and pretend it's just text tokens and just do everything else in an identical manner.

So here for example there was an early paper that has a nice graphic for how you can take an image and you can chunk it into integers and these sometimes, so these would basically become the tokens of images, as an example. These tokens can be hard tokens where you force them to be integers. They can also be soft tokens where you don't require these to be discrete, but you do force these representations to go through bottlenecks like in autoencoders.

Also in this paper that came out from OpenAI, Soraa, which I think really blew the mind of many people and inspired a lot of people in terms of what's possible, they have a graphic here and they talk briefly about how LLMs have text tokens, Soraa has visual patches.

So again, they came up with a way to chunk videos into basically tokens with their own vocabularies and then you can either process discrete tokens say with autoregressive models or even soft tokens with diffusion models and all of that is sort of being actively worked on, actively designed and it's beyond the scope of this video but just something I wanted to mention briefly.

接下来，我想简要讨论最近一个热门的研究方向。那就是如何构建能够同时处理多种输入形式的 Transformer 模型。这些模型不仅可以处理文本输入，还可以处理图像、视频、音频等多种形式的数据。这种能够处理多种数据形式的能力，我们称之为多模态处理（multi-modal processing）。

那么，如何将所有这些模态输入到 Transformer 中，并可能从中预测这些模态呢？是否需要从根本上改变架构？我认为，很多人开始达成的共识是：你不需要改变架构，只需继续使用 Transformer（Transformer）。你只需要将输入域标记化（tokenize），然后就可以完成任务了。这样做的关键是将所有输入都视为文本标记（token），然后用相同的方式处理所有内容。

例如，有一篇早期的论文提供了一个很好的图表，展示了如何将图像分割成整数。这些整数实际上就成为了图像的标记。这些标记可以是硬标记（hard token），即强制它们为整数。它们也可以是软标记（soft token），即不要求它们是离散的，但会强制这些表示通过类似自动编码器（autoencoder）中的瓶颈层。

另外，OpenAI 最近发布的 Sora 论文也值得一提。我认为这篇论文真正让许多人大开眼界，并在人工智能可能性方面激发了广泛的灵感。论文中有一个图表，简要讨论了大语言模型（LLM）如何使用文本标记，而 Sora 如何使用视觉补丁（visual patch）。

让我再次强调一下，研究人员发明了一种将视频分割成基本单元（称为 tokens）的方法，这些 tokens 有自己的词汇表。然后，你可以用自回归模型（autoregressive models）处理离散的 tokens，甚至可以用扩散模型（diffusion models）处理软 tokens。所有这些技术都在积极研究和开发中。虽然这些内容超出了本视频的范围，但我觉得简单提一下还是很有必要的。

#### 11

Okay now that we have gone quite deep into the tokenization algorithm and we understand a lot more about how it works, let's loop back around to the beginning of this video and go through some of these bullet points and really see why they happen.

So first of all, why can't my LLM spell words very well or do other spell-related tasks? So fundamentally this is because, as we saw, these characters are chunked up into tokens. Some of these tokens are actually fairly long.

As an example, I went to the GPT-4 vocabulary and I looked at one of the longer tokens. "dot default style" turns out to be a single individual token. That's a lot of characters for a single token. My suspicion is that there's just too much crammed into this single token.

And my suspicion was that the model should not be very good at tasks related to spelling of this single token. So I asked how many letters "L" are there in the word "dot default style"? And of course my prompt is intentionally done that way. And you see how "default style" will be a single token. This is what the model sees.

My suspicion is that it wouldn't be very good at this and indeed it is not. It doesn't actually know how many Ls are in there. It thinks there are three and actually there are four if I'm not getting this wrong myself. That didn't go extremely well.

现在我们已经深入了解了分词（tokenization）算法的工作原理，让我们回到视频开头提到的几个要点，看看为什么会出现这些情况。

首先，为什么大语言模型（LLM, Large Language Model）不擅长拼写单词或执行其他与拼写相关的任务呢？从根本上说，这是因为，正如我们所看到的，字符被分割成了 tokens。而且，有些 tokens 实际上相当长。

举个例子，我查看了 GPT-4 的词汇表，找到了一个比较长的 token。"dot default style"（意为「点默认样式」）居然被当作一个单独的 token。对于单个 token 来说，这包含了太多字符。我怀疑这个 token 中塞进了过多的信息。

我猜测，模型在处理与单个 token（标记）拼写相关的任务时表现可能不会很好。为了验证这一点，我问了一个问题：「在 'dot default style' 这个词中有多少个字母 'L'？」需要说明的是，我的提问是经过刻意设计的。你可以看到，"default style" 在模型中会被视为一个单独的 token。这就是模型所能「看到」的信息。

正如我所预料的，模型在这类任务中的表现确实不尽如人意。它实际上并不知道这个短语中确切的字母数量。模型认为有三个 "L"，但实际上如果我没有记错的话，应该有四个。这个结果显然不太理想。

Let's look at another character level task. For example, here I asked GPT-4 to reverse the string "default style" and to try to use a code interpreter. I stopped it and I said just do it, just try it, and it gave me jumble. It doesn't actually really know how to reverse this string going from right to left. So it gave a wrong result.

So again, working with this working hypothesis that maybe this is due to the tokenization, I tried a different approach. I said okay let's reverse the exact same string but take the following approach. Step one, just print out every single character separated by spaces and then as a step two, reverse that list.

And it again tried to use a tool but when I stopped it, it first produced all the characters and that was actually correct and then it reversed them and that was correct once it had this. So somehow it can't reverse it directly but when you go just first listing it out in order, it can do that somehow and then once it's broken up this way, this becomes all these individual characters and so now this is much easier for it to see these individual tokens and reverse them and print them out. So that is kind of interesting.

So let's continue. Now, why are LLMs worse at non-English languages? I briefly covered this already but basically it's not only that the language model sees less non-English data during training of the model parameters but also the tokenizer is not sufficiently trained on non-English data.

让我们再看一个字符级的任务。这次，我要求 GPT-4（一种大语言模型）反转字符串 "default style"，并尝试使用代码解释器（code interpreter）来完成这个任务。我中断了它的常规回答，直接要求它尝试完成任务。结果它给出了一串乱码。这表明它实际上并不真正理解如何从右到左反转这个字符串，因此给出了错误的结果。

让我们继续探讨这个问题。基于之前的工作假设，即这可能是由分词导致的，我尝试了一种新的方法。我决定用以下步骤来反转同一个字符串：第一步，将每个字符单独打印出来，用空格分隔；第二步，反转这个字符列表。

有趣的是，当我阻止 AI 使用工具时，它首先正确地列出了所有字符，然后也成功地反转了它们。这说明 AI 虽然无法直接反转字符串，但当我们将字符串拆分成单个字符时，它就能轻松地识别这些独立的 token（标记）并进行反转和打印。这个发现很有意思。

接下来，让我们讨论一下为什么大语言模型（LLMs, Large Language Models）在处理非英语语言时表现较差。我之前简单提到过，主要原因不仅仅是因为在训练模型参数时接触到的非英语数据较少，还因为分词器（tokenizer）在非英语数据上的训练也不够充分。

And so here for example "hello how are you" is five tokens and its translation is 15 tokens. So this is a three times blow up. And so for example, "annyeonghaseyo" is just "hello" basically in Korean, and that ends up being three tokens. I'm actually kind of surprised by that because that is a very common phrase. It's just a typical greeting of like "hello", and that ends up being three tokens whereas our "hello" is a single token.

And so basically everything is a lot more bloated and diffuse, and this is I think partly the reason that the model works worse on other languages. Coming back, why is LLM bad at simple arithmetic? That has to do with the tokenization of numbers.

And so you'll notice that, for example, addition is very sort of like, there's an algorithm that is like character level for doing addition. So for example, here we would first add the ones and then the tens and then the hundreds, you have to refer to specific parts of these digits.

But these numbers are represented completely arbitrarily based on whatever happened to merge or not merge during the tokenization process. There's an entire blog post about this that I think is quite good, "Integer Tokenization is Insane".

举个例子，英语短语 "hello how are you" 由 5 个标记（token）组成，而它的翻译可能需要 15 个标记。这就是一个三倍的增加。再比如，韩语中的 "안녕하세요(annyeonghaseyo)" 基本上就是 "hello" 的意思，但它被分成了 3 个标记。这让我有点惊讶，因为这是一个非常常见的短语。它只是一个典型的「你好」问候语，却被分成了 3 个标记，而英语的 "hello" 只是单个标记。

所以基本上，在其他语言中，一切都变得更加冗长和分散，我认为这部分原因导致模型在非英语语言上表现更差。回到之前的话题，为什么大语言模型（LLM）在简单算术方面表现不佳？这与数字的标记化（tokenization）处理有关。

你会注意到，例如，加法在某种程度上很像是有一个字符级别的算法来进行运算。比如，在进行加法时，我们会先加个位，然后是十位，然后是百位，你必须参考这些数字的特定位置。这种操作方式与模型处理标记的方式不太一致，因此可能导致在算术运算上的表现不佳。

但是，这些数字的表示方式完全是基于分词（tokenization）过程中随机合并或分割的结果，显得非常随意。有一篇很棒的博客文章专门讨论了这个问题，标题是「整数分词：一场疯狂的游戏」。

And this person basically systematically explores the tokenization of numbers in, I believe this is GPT-2. And so they noticed that, for example, for four digit numbers, you can take a look at whether it is a single token or whether it is two tokens that is a 1-3 or a 2-2 or a 3-1 combination. And so all the different numbers are all the different combinations.

And you can imagine this is all completely arbitrary. And the model, unfortunately, sometimes sees a token for all four digits, sometimes for three, sometimes for two, sometimes for one. And it's in an arbitrary manner. And so this is definitely a headwind, if you will, for the language model.

And it's kind of incredible that it can kind of do it and deal with it, but it's also kind of not ideal. And so that's why, for example, we saw that Meta, when they trained the Llama2 algorithm and they used SentencePiece, they make sure to split up all the digits, as an example, for Llama2. And this is partly to improve simple arithmetic kind of performance.

And finally, why is GPT-2 not as good in Python? Again, this is partly a modeling issue in the architecture and the dataset and the strength of the model, but it's also partly tokenization. Because as we saw here with the simple Python example, the encoding efficiency of the tokenizer for handling spaces in Python is terrible and every single space is an individual token and this dramatically reduces the context length that the model can attend across.

So that's almost like a tokenization bug for GPT-2 and that was later fixed with GPT-4. Okay so here's another fun one. My LLM abruptly halts when it sees the string "end of text". So here's a very strange behavior. "print a string end of text" is what I told GPT-4 and it says "Could you please specify the string?"

And I'm telling it "Give me end of text" and it seems like there's an issue. It's not seeing "end of text" and then I give it "end of text is the string" and then here's the string and then it just doesn't print it.

So obviously something is breaking here with respect to the handling of the special token. And I don't actually know what OpenAI is doing under the hood here and whether they are potentially parsing this as an actual token instead of this just being "end of text" as like individual sort of pieces of it without the special token handling logic.

And so it might be that someone when they're calling .encode they are passing in the allowed special and they are allowing "end of text" as a special character in the user prompt. But the user prompt of course is a sort of attacker-controlled text, so you would hope that they don't really parse or use special tokens from that kind of input, but it appears that there's something definitely going wrong here.

And so your knowledge of these special tokens ends up being an attack surface potentially, and so if you'd like to confuse LLMs, then just try to give them some special tokens and see if you're breaking something by chance.

这篇文章的作者系统地研究了 GPT-2 模型中数字的分词情况。他们发现，以四位数为例，可能会出现不同的分词结果：要么作为一个完整的 token，要么被分成两个 token。这两个 token 的组合方式可能是 1 位 + 3 位，2 位 + 2 位，或者 3 位 + 1 位。因此，不同的数字会产生各种不同的分词组合。

你可以想象，这种分词方式完全是随机的。遗憾的是，模型有时会将四位数视为一个完整的 token，有时又会将其拆分成三位、两位甚至一位数的 token。这种随机性无疑给语言模型带来了一定的挑战。

模型能够处理这种情况确实令人惊叹，但同时这种方法也并不理想。这就是为什么我们看到，例如，Meta 在训练 Llama2 算法时使用了 SentencePiece 分词工具，并特意将所有数字分开处理。这样做部分是为了提高模型的基础算术运算能力。

那么，为什么 GPT-2 在处理 Python 代码方面表现不佳呢？这部分原因是模型架构、训练数据集和模型本身能力的限制，但也部分是由于分词问题。正如我们在之前的简单 Python 示例中看到的，GPT-2 的分词器在处理 Python 中的空格时效率极低，每个空格都被视为一个独立的 token。这大大减少了模型能够处理的有效上下文长度。

这几乎可以被视为 GPT-2 的一个分词缺陷，而这个问题在 GPT-4 中得到了修复。好的，这里还有一个有趣的例子。我的大语言模型（LLM）在遇到 "end of text" 这个字符串时会突然停止。这是一个非常奇怪的行为。当我告诉 GPT-4 "print a string end of text" 时，它回复说："Could you please specify the string?"（请指定要打印的字符串）

我告诉模型「给我结束文本」，但似乎出现了问题。它没有识别出「结束文本」，然后我输入「结束文本是字符串」，接着是这个字符串本身，但模型就是不打印出来。

显然，在处理特殊标记（special tokens）方面出现了问题。我其实不清楚 OpenAI 在底层是如何处理的，他们可能将其解析为实际的标记，而不是将「结束文本」作为普通文本处理，没有应用特殊标记处理逻辑。

可能有人在调用 .encode 方法时，传入了允许使用的特殊字符，并允许在用户输入中使用「结束文本」作为特殊字符。但用户输入本质上是攻击者可控的文本，理想情况下，系统不应该从这种输入中解析或使用特殊标记，但看起来这里确实出了问题。

因此，你对这些特殊标记的了解最终可能成为潜在的攻击面（attack surface）。如果你想要混淆大语言模型，可以尝试输入一些特殊标记，看看是否能碰巧破坏系统的某些功能。

Okay so this next one is a really fun one, the trailing whitespace issue. So if you come to playground and we come here to GPT 3.5 Turbo instruct. So this is not a chat model, this is a completion model. So think of it more like it's a lot more closer to a base model. It does completion. It will continue the token sequence.

So here's a tagline for Ice Cream Shop and we want to continue the sequence. And so we can submit and get a bunch of tokens. Okay, no problem. But now suppose I do this but instead of pressing submit here I do... here's a tagline for an ice cream shop space so I have a space here before I click submit.

We get a warning "Your text ends in a trailing space which causes worse performance due to how API splits text into tokens". So what's happening here? It still gave us a completion here but let's take a look at what's happening.

So here's a tagline for an ice cream shop and then what does this look like in the actual training data? Suppose you found the completion in the training document somewhere on the internet and the LLM trained on this data. So maybe it's something like "Oh yeah maybe that's the tagline", that's a terrible tagline.

接下来，我们要讨论一个非常有趣的问题：尾随空格问题。让我们来到 OpenAI 的 playground，选择 GPT-3.5 Turbo instruct 模型。需要注意的是，这不是一个聊天模型，而是一个补全模型（completion model）。你可以将它理解为更接近基础模型（base model）的存在。它的主要功能是进行文本补全，即继续生成 token（Token）序列。

假设我们有一个冰淇淋店的标语，我们希望模型能够继续这个序列。通常情况下，我们可以直接提交请求，模型就会生成一系列的 token。这很正常。但是，让我们做一个小实验：在冰淇淋店的标语后面加一个空格，然后再提交请求。

这时，我们会收到一个警告：「你的文本以尾随空格结尾，这可能会导致性能下降，因为 API 在将文本分割成 token 时会受到影响」。虽然模型仍然给出了补全结果，但让我们深入了解一下这里到底发生了什么。

考虑一下，在实际的训练数据中，这个场景可能是什么样的？假设你在互联网上的某个训练文档中发现了这样的补全。大语言模型（LLM）就是在这样的数据上进行训练的。可能会出现这样的情况：「哦，没错，那可能就是标语」—— 尽管这可能是一个糟糕的标语。

But notice here that when I create "O", you see that because there's the space character is always a prefix to these tokens in GPT. So it's not an "O" token, it's a "space O" token. The space is part of the "O" and together they are token 8840. That's "space O".

So what's happening here is that when I just have it like this and I let it complete the next token, it can sample the "space O" token. But instead, if I have this and I add my space, then what I'm doing here when I encode this string is I have basically "here's a tagline for an ice cream shop". And this space at the very end becomes a token 220.

And so we've added token 220 and this token otherwise would be part of the tagline because if there actually is a tagline here so "space o" is the token and so this is suddenly out of distribution for the model because this space is part of the next token but we're putting it here like this and the model has seen very very little data of actual space by itself.

And we're asking it to complete the sequence like add in more tokens but the problem is that we've sort of begun the first token and now it's been split up and now we're out of distribution and now arbitrary bad things happen and it's just a very rare example for it to see something like that.

And that's why we get the warning. So the fundamental issue here is of course, that the LLM is on top of these tokens and these tokens are text chunks. They're not characters in a way you and I would think of them. These are the atoms of what the LLM is seeing. And there's a bunch of weird stuff that comes out of it.

让我们来关注一个有趣的现象。当我创建 "O" 这个字符时，你会发现在 GPT（生成式预训练 Transformer）中，空格字符总是作为这些 token 的前缀。因此，我们看到的不是单独的 "O" token，而是 "空格 O" token。这里的空格实际上是 "O" 的一部分，它们共同组成了编号为 8840 的 token。

这种设计会导致一些有趣的结果。当我让模型直接完成下一个 token 时，它可以自然地生成 "空格 O" token。但是，如果我手动在输入末尾添加一个空格，情况就变得不同了。

让我们以「这是一个冰淇淋店的 tagline（广告标语）」为例。当我们在这句话的末尾添加一个空格时，这个空格会被编码为单独的 token，编号为 220。

这样一来，我们就在输入中额外插入了 token 220。正常情况下，这个空格应该是下一个 token（比如 "空格 o"）的一部分。但现在，我们把它单独放在了输入的末尾。这种情况对模型来说是「分布外」（out of distribution）的，因为在训练数据中，模型几乎没有见过单独出现的空格 token。

这个例子展示了在处理文本时，即使是看似微小的改变（如添加一个空格），也可能对模型的行为产生显著影响。这提醒我们在使用和设计语言模型时，需要注意这些细节。

我们要求大语言模型（LLM）完成序列，例如添加更多的 token，但问题在于我们已经开始了第一个 token，现在它被分割了。这导致我们超出了模型的分布范围，可能会引发一些意料之外的问题。对于模型来说，遇到这种情况是非常罕见的。

这就是我们收到警告的原因。这里的根本问题在于，大语言模型是建立在这些 token 之上的，而这些 token 是文本块，而不是你我通常理解的单个字符。这些 token 是大语言模型所能识别的最小单位，就像原子之于物质。这种机制会导致一些奇怪的现象。

Let's go back to our "default style". I bet you that the model has never in its training set seen "default style" without "dot" in there. It's always seen this as a single group because this is some kind of a function in I'm guessing, I don't actually know what this is part of, this some kind of API.

But I bet you that it's never seen this combination of tokens in its training data, or I think it would be extremely rare. So I took this and I copy-pasted it here, and I tried to complete from it, and it immediately gave me a big error, and it said, "The model predicted a completion that begins with a stop sequence resulting in no output. Consider adjusting your prompt or stop sequences."

So what happened here when I clicked submit is that immediately the model emitted a sort of like "end of text" token, I think, or something like that. It basically predicted the stop sequence immediately. So it had no completion.

And so this is why I'm getting a warning again, because we're off the data distribution and the model is just predicting just totally arbitrary things. It's just really confused basically. This is giving it brain damage. It's never seen this before. It's shocked and it's predicting "end of text" or something.

让我们回到 "default style" 这个例子。我敢说，在模型的训练集中，"default style" 从未出现过没有「点」的形式。它总是将 "default.style" 作为一个整体来识别，因为这可能是某种函数或 API 的一部分（虽然我并不确切知道它的具体用途）。

但我敢打赌，这种 token（词元）组合在模型的训练数据中几乎从未出现过，即便有也是极其罕见的。为了验证这一点，我将这段文本复制粘贴到这里，并尝试让模型续写。结果模型立即报错，显示：「模型预测的输出以停止序列开始，导致没有实际输出。建议调整您的提示或停止序列。」

这里发生的情况是，当我点击提交按钮时，模型立即生成了一个类似「文本结束」的 token。也就是说，它几乎立刻就预测到了停止序列。这就导致模型无法生成任何有效输出。

这就是为什么我再次收到警告的原因。因为我们给出的输入已经超出了模型的训练数据分布范围，模型完全不知所措，开始随机预测一些毫无意义的内容。这种情况对模型来说就像是遇到了无法处理的异常输入。它从未见过这样的文本，感到十分困惑，所以直接预测出「文本结束」或类似的标记来结束处理。

I tried it again here and in this case it completed it but then for some reason "this request may violate our usage policies". This was flagged. Basically something just goes wrong and there's something like jank. You can just feel the jank because the model is extremely unhappy with just this and it doesn't know how to complete it because it's never occurred in a training set. In a training set it always appears like this and becomes a single token.

So these kinds of issues where tokens are either you sort of complete the first character of the next token or you are sort of... you have long tokens that you then have just some of the characters of, all of these are kind of like issues with partial tokens is how I would describe it.

And if you actually dig into the TikToken repository, go to the Rust code and search for "unstable", go to the Rust code and search for "unstable" and you'll see in code unstable native, unstable tokens and a lot of like special case handling.

None of this stuff about unstable tokens is documented anywhere but there's a ton of code dealing with unstable tokens and unstable tokens is exactly kind of like what I'm describing here.

What you would like out of a completion API is something a lot more fancy like if we're putting in "default style", if we're asking for the next token sequence, we're not actually trying to append the next token exactly after this list. We're actually trying to append... we're trying to consider lots of tokens that if we were... I guess like we're trying to search over characters that if we retokenized would be of high probability, if that makes sense.

So that we can actually add a single individual character instead of just like adding the next full token that comes after this partial token list. So this is very tricky to describe. And I invite you to maybe like look through this. It ends up being extremely gnarly and hairy kind of topic and it comes from tokenization fundamentally.

我再次尝试了这个操作，这次它确实完成了任务，但随后出现了「此请求可能违反我们的使用政策」的提示。这被系统标记了。基本上就是出现了一些异常，你能感受到模型运行时的不正常状态。这是因为模型无法正确处理这种情况，它不知道如何完成这个任务，原因是这种情况在训练集中从未出现过。在训练集中，它总是以特定方式出现并被视为单个 token（词元）。

这类问题要么是你只完成了下一个 token 的第一个字符，要么是你有长 token，但只出现了其中的一部分字符。所有这些都可以被归类为部分 token 的问题。

如果你深入研究 TikToken 代码仓库，进入 Rust 代码并搜索 "unstable"，你会在代码中看到不稳定的原生实现、不稳定的 token，以及大量的特殊情况处理逻辑。

有关不稳定 token 的这些内容在任何官方文档中都没有记录，但有大量的代码在处理不稳定 token。而这些不稳定 token 恰恰就是我前面描述的那种情况。

从完成 API（completion API）中，我们期望获得的是一种更加复杂的功能。例如，当我们输入「默认风格」并请求下一个 token（词元）序列时，我们实际上并不是想要精确地在现有列表后直接添加下一个 token。相反，我们是在尝试考虑多个 token，如果我们对这些 token 重新进行分词（tokenization），它们将具有较高的出现概率。

这种方法使我们能够添加单个字符，而不仅仅是添加部分 token 列表之后的下一个完整 token。这个概念确实很难描述清楚。我建议你可以深入研究一下这个话题。它最终会演变成一个极其复杂和棘手的问题，而这个问题的根源在于分词机制。

#### 12

So maybe I can even spend an entire video talking about unstable tokens sometime in the future. Okay and I'm really saving the best for last. My favorite one by far is this "solid gold Magikarp". This comes from this blog post, "Solid Gold Magikarp" and this is internet famous now for those of us in LLMs.

And basically, I would advise you to read this blog post in full. But basically what this person was doing is this person went to the token embedding table and clustered the tokens based on their embedding representation.

And this person noticed that there's a cluster of tokens that look really strange. So there's a cluster here, "atrot", "eStream", "fame", "solid gold", "Magikarp", "signup message", like really weird tokens in basically in this embedding cluster.

And so where are these tokens and where do they even come from? Like what is "solid gold Magikarp"? It makes no sense. And then they found a bunch of these tokens and then they noticed that actually the plot thickens here because if you ask the model about these tokens, like you ask it some very benign question like "Please can you repeat back to me the string "solid gold Magikarp"?", then you get a variety of basically totally broken LLM behavior.

So either you get evasion like "I'm sorry, I can't hear you" or you get a bunch of hallucinations as a response. You can even get back like insults. So you ask it about "streamer bot" and it tells the... and the model actually just calls you names. Or it kind of comes up with like weird humor. Like you're actually breaking the model by asking about these very simple strings like "at roth" and "solid gold Magikarp".

也许在未来，我可以专门制作一个视频来讨论不稳定 token 这个主题。好了，现在让我们来看最精彩的部分。到目前为止，我最喜欢的例子是「金色鲤鱼王」（solid gold Magikarp）。这个例子来自一篇题为「金色鲤鱼王」的博客文章，现在在大语言模型（LLM）研究领域已经成为了一个网络热点。

我强烈建议你完整阅读这篇博客文章。简单来说，这位研究者查看了 token（符号）嵌入表，并基于它们的嵌入（embedding）表示对 tokens 进行了聚类分析。

研究者注意到有一个看起来非常奇怪的 token 簇。这个簇中包含了一些奇怪的 tokens，比如 "atrot"、"eStream"、"fame"、"solid gold"、"Magikarp"、"signup message" 等。

那么，这些 tokens 是从哪里来的？它们代表什么意思？比如 "solid gold Magikarp" 是什么？这些词组看起来毫无意义。研究者发现了大量类似的 tokens，随后他们发现情况比想象中更加有趣。如果你向大语言模型（LLM）询问这些 tokens 相关的问题，即使是一些非常简单的问题，比如「请你重复一遍 'solid gold Magikarp' 这个字符串」，模型就会表现出各种异常行为，完全偏离了正常的运行轨道。

因此，你要么会得到类似「对不起，我听不懂你在说什么」这样的回避回答，要么会得到一堆虚构的响应。有时甚至会收到侮辱性的回复。例如，当你询问关于 "streamer bot"（一种流媒体机器人）的信息时，模型可能会出人意料地开始辱骂你。或者，它会突然产生一些奇怪的幽默感。实际上，你通过询问一些非常简单的字符串，如 "at roth" 或 "solid gold Magikarp"（纯金鲤鱼王，来自宝可梦游戏），就能导致模型出现异常行为。

So like what the hell is happening? And there's a variety of here documented behaviors. There's a bunch of tokens, not just "solid gold Magikarp" that have that kind of a behavior. And so basically there's a bunch of like trigger words. And if you ask the model about these trigger words or you just include them in your prompt, the model goes haywire and has all kinds of really strange behaviors including sort of ones that violate typical safety guidelines and the alignment of the model like it's swearing back at you.

So what is happening here and how can this possibly be true? Well this again comes down to tokenization. So what's happening here is that "solid gold Magikarp", if you actually dig into it, is a Reddit user. So there's a u/SolidGoldMagikarp and probably what happened here, even though I don't know that this has been like really definitively explored, but what is thought to have happened is that the tokenization dataset was very different from the training dataset for the actual language model.

So in the tokenization dataset, there was a ton of Reddit data, potentially, where the user SolidGoldMagikarp was mentioned in the text. Because SolidGoldMagikarp was a very common person who would post a lot, this would be a string that occurs many times in a tokenization dataset.

Because it occurs many times in a tokenization dataset, these tokens would end up getting merged to a single individual token for that single Reddit user "solid gold Magikarp". So they would have a dedicated token in a vocabulary of, was it 50,000 tokens in GPT-2 that is devoted to that Reddit user.

那么，究竟发生了什么？这里记录了各种异常行为。不仅仅是 "solid gold Magikarp"，还有许多其他的 token（在 AI 中指输入文本的基本单位）会触发类似的反应。基本上，存在一系列的「触发词」。如果你询问模型这些触发词，或者仅仅在你的提示中包含它们，模型就会失控，表现出各种非常奇怪的行为。这些行为甚至包括违反典型安全准则和模型对齐（即确保 AI 系统的行为与人类价值观一致）的情况，比如模型会对用户进行反咒骂。

那么，这种现象是如何发生的，又为什么会出现呢？答案还是与分词（tokenization）有关。让我们深入了解一下："solid gold Magikarp" 实际上是一个 Reddit 用户的名字。具体来说，存在一个用户 `u/SolidGoldMagikarp`。虽然这个现象还没有被彻底研究过，但普遍认为的原因是：用于分词的数据集与用于训练实际语言模型的数据集存在显著差异。

在分词数据集中，可能包含了大量的 Reddit 数据，其中频繁提到了用户 SolidGoldMagikarp。由于这个用户非常活跃，经常发帖，因此这个用户名在分词数据集中多次出现。

正是因为在分词数据集中的高频出现，这个用户名最终被合并成了一个单独的 token。也就是说，在 GPT-2 模型约 50,000 个 token 的词汇表中，专门为这个 Reddit 用户 "solid gold Magikarp" 分配了一个独立的 token。

And then what happens is the tokenization dataset has those strings, but then later when you train the model, the language model itself, this data from Reddit was not present. And so therefore, in the entire training set for the language model, "solid gold Magikarp" never occurs. That token never appears in the training set for the actual language model later.

So this token never gets activated. It's initialized at random in the beginning of optimization. Then you have forward-backward passes and updates to the model, and this token is just never updated in the embedding table. That row vector never gets sampled. It never gets used, so it never gets trained, and it's completely untrained.

It's kind of like unallocated memory in a typical binary program written in C or something like that. So it's unallocated memory, and then at test time, if you evoke this token, then you're basically plucking out a row of the embedding table that is completely untrained, and that feeds into a transformer and creates undefined behavior.

And that's what we're seeing here, this completely undefined, never before seen in a training behavior. And so any of these kind of like weird tokens would evoke this behavior because fundamentally the model is out of sample, out of distribution.

接下来发生的情况是，在数据标记化（tokenization）的过程中，这些字符串被包含在数据集中。但是，当你后来训练语言模型时，这些来自 Reddit 的数据却不存在于训练集中。因此，在整个语言模型的训练数据中，像「纯金鲤鱼王」（solid gold Magikarp）这样的词组从未出现过。这个 token（即文本中的最小单位，可能是一个单词或者单词的一部分）在后来实际的语言模型训练集中从未出现。

因此，这个 token 从未被激活。它在优化过程开始时只是被随机初始化了一个数值。然后，在模型训练的过程中，虽然有前向传播（数据从输入到输出的计算过程）和后向传播（误差从输出到输入的传递过程），以及相应的模型更新，但这个特定的 token 在嵌入表（一个存储单词或 token 数值表示的矩阵）中从未被更新。代表这个 token 的那一行向量从未被采样，从未被使用，所以它从未被训练，完全处于未训练状态。

这种情况有点像在用 C 语言编写的典型程序中的未分配内存。它就像是一块未被使用的内存空间，然后在测试模型时，如果你碰巧使用了这个 token，你实际上是从嵌入表中抽取出一个完全未经训练的行。这个未经训练的数据会被输入到 Transformer 模型中，从而导致不可预测的行为。

这里我们看到的是一种完全未定义的、在模型训练过程中从未出现过的行为。任何这些不常见的 token 都可能触发这种行为，因为从根本上说，模型正在处理超出其训练样本和分布范围的内容。

Okay and the very last thing I wanted to just briefly mention and point out although I think a lot of people are quite aware of this is that different kinds of formats and different representations and different languages and so on might be more or less efficient with GPT tokenizers or any tokenizers for any other LLM for that matter.

So for example JSON is actually really dense in tokens and YAML is a lot more efficient in tokens. So for example these are the same in JSON and in YAML. The JSON is 116 and the YAML is 99. So quite a bit of an improvement.

And so in the token economy where we are paying per token in many ways and you are paying in the context length and you're paying in dollar amount for the cost of processing all this kind of structured data when you have to.

So prefer to use YAMLs over JSONs. And in general, the tokenization density is something that you have to sort of care about and worry about at all times and try to find efficient encoding schemes and spend a lot of time in TikTokenizer and measure the different token efficiencies of different formats and settings and so on.

最后，我想简要提一点，虽然我认为很多人已经意识到这一点：不同类型的格式、不同的数据表示方式和不同的编程语言等，对于 GPT 分词器（GPT tokenizers）或任何其他大语言模型（LLM）的分词器来说，其处理效率可能会有所不同。

举个例子，JSON 格式在 token 数量上通常比较密集，而 YAML 格式则更加节省 token。比如说，同样的数据用 JSON 表示可能需要 116 个 token，而用 YAML 表示只需要 99 个 token。这是一个相当可观的改进。

在当前的「token 经济」中，我们往往需要为每个 token 付费。这不仅体现在上下文长度的限制上，还体现在处理结构化数据时的实际美元成本上。因此，选择更高效的数据表示方式可以帮助我们节省成本，提高效率。

因此，相比 JSON，我们更推荐使用 YAML 格式。总的来说，Token 密度（tokenization density）是一个需要持续关注和考虑的问题。你需要努力寻找高效的编码方案，在 TikTokenizer 上投入大量时间，并测量不同格式和设置下的 Token 效率。

Okay, so that concludes my fairly long video on tokenization. I know it's dry, I know it's annoying, I know it's irritating. I personally really dislike this stage. What I do have to say at this point is don't brush it off. There's a lot of foot guns, sharp edges here, security issues, AI safety issues as we saw plugging in unallocated memory into language models. So it's worth understanding this stage.

That said, I will say that eternal glory goes to anyone who can get rid of it. I showed you one possible paper that tried to do that, and I think, I hope, a lot more can follow over time. And my final recommendations for the application right now are, if you can reuse the GPT-4 tokens and the vocabulary in your application, then that's something you should consider and just use TikToken because it is a very efficient and nice library for inference for BPE.

I also really like the byte level BPE that TikToken and OpenAI uses. If you for some reason want to train your own vocabulary from scratch, then I would use the BPE with SentencePiece I apologize, but the transcript you provided seems to have ended at this point:

"If you for some reason want to train your own vocabulary from scratch, then I would use the BPE with SentencePiece."

There doesn't appear to be any additional content to continue organizing or correcting. Let me know if you have any other transcripts you would like me to work on.

好了，这就是我关于 Token 化（tokenization）的长篇视频的全部内容。我知道这个主题可能很枯燥、烦人，甚至令人恼火。老实说，我个人也非常不喜欢这个阶段。但是我必须强调，不要轻视它。这个领域存在许多潜在的风险、棘手的问题，以及安全隐患。正如我们所见，将未分配的内存输入语言模型可能引发 AI 安全问题。因此，理解这个阶段是非常有价值的。

尽管如此，我还是要说，如果有人能彻底解决这个问题，那将是一项伟大的成就。我向大家介绍了一篇尝试解决这个问题的论文，我希望并相信未来会有更多相关的研究成果。

对于当前的应用，我的最终建议是：如果可能的话，考虑在你的应用中重用 GPT-4 的 Token 和词汇表。使用 TikToken 库是个不错的选择，因为它是一个非常高效且优秀的库，特别适合用于字节对编码（Byte Pair Encoding，BPE）的推理过程。

我也非常喜欢 TikToken 和 OpenAI 使用的字节级 BPE（Byte-Pair Encoding，字节对编码）。这种方法在处理文本时非常高效。如果出于某些原因，你想要从头开始训练自己的词汇表，那么我建议你使用 SentencePiece 工具中的 BPE 方法。SentencePiece 是一个用于文本分词和子词分割的开源工具，它提供了多种算法，包括 BPE。

### 参考资料

[Language Models are Unsupervised Multitask Learners](https://insightcivic.s3.us-east-1.amazonaws.com/language-models.pdf)

[[2307.09288] Llama 2: Open Foundation and Fine-Tuned Chat Models](https://arxiv.org/abs/2307.09288)

[[2305.07185] MEGABYTE: Predicting Million-byte Sequences with Multiscale Transformers](https://arxiv.org/abs/2305.07185)