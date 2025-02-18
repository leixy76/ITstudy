## 20250216o1-isnt-a-chat-model-and-thats-the-point

[o1 isn’t a chat model (and that’s the point)](https://www.latent.space/p/o1-skill-issue)

2025-01-12

o1 不是聊天模型（这才是关键所在)

How Ben Hylak turned from ol pro skeptic to fan by overcoming his skill issue.

Ben Hylak 如何克服技术难题，从资深怀疑者转变为忠实拥趸。

Since o1's launch in October and o1 pro/o3's announcement in December, many have been struggling to figure out their takes, both positive and negative. We took a strongly positive stance at the nadir of o1 Pro sentiment and mapped out what it would likely take for OpenAI to have a $2000/month agent product (rumored to be launched in the next few weeks). Since then, o1 has sat comfortably at #1 across ALL LMArena leaderboards (soon to have default Style Control as we discussed on pod).

自从 o1 在 10 月份发布，以及 o1 pro/o3 在 12 月份发布声明后，很多人都在试图理解各方的观点，既有赞扬也有批评。之前，当对 o1 Pro 的评价跌入谷底时，我们却持非常乐观的态度，并且分析了 OpenAI 若要推出每月收费 2000 美元的 AI 智能体产品（据传将在未来几周内发布），可能需要做哪些准备。从那时起，o1 已经稳定占据 LMArena 所有排行榜的首位（正如我们在播客里讨论的，未来还将加入默认的风格控制功能）。

We've been following Ben Hylak's work on the Apple VisionOS for a bit, and invited him to speak at the World's Fair. He has since launched Dawn Analytics, and continued to publish unfiltered thoughts about o1 — initially as a loud skeptic, and slowly becoming a daily user. We love mind-changers in both its meanings, and think this same conversation is happening all over the world as people struggle to move from the chat paradigm to the brave new world of reasoning and $x00/month prosumer AI products like Devin (spoke at WF, now GA). Here are our thoughts.

我们一直在关注 Ben Hylak 在 Apple VisionOS 上的工作，并邀请他参加世界博览会并发表演讲。之后，他创立了 Dawn Analytics，并持续发表关于 o1 的真实想法 —— 起初他强烈质疑 o1，之后逐渐成为了它的日常用户。我们喜欢能够改变想法的人，喜欢他们兼具深度思考和实践能力。我们认为，世界各地都在发生着类似的转变，人们正努力从传统的聊天模式，过渡到以推理为核心，以及像 Devin 这样每月花费 $x00 的专业级 AI 产品所代表的全新世界（Devin 曾在世界博览会（WF）上发表演讲，现在已全面上市（GA））。我们的观点如下。

PSA: Due to overwhelming demand (>15x applications:slots), we are closing CFPs for AI Engineer Summit tomorrow. Last call! Thanks, we'll be reaching out to all shortly!

公告：由于需求远超预期 （申请数量是名额的 15 倍以上），AI 工程师峰会的论文征集（Call for Papers，CFP）将于明日截止。截止日期临近！感谢您的参与，我们稍后会与各位联系！

### o1 isn't a chat model (and that's the point)

o1 不是聊天模型，这才是关键！

o1 的目标是成为一个实用的生成式 AI 智能体（AI Agent），而非另一个聊天机器人。这意味着，在设计上，o1 优先考虑的是可靠性、可重复性和可观察性，而非创造性或对话能力。

具体来说，这体现在以下几个方面：

1 o1 尽可能避免生成自由文本。相反，o1 优先使用各种工具，并以结构化的方式给出响应。当不可避免需要生成文本时，o1 会尽可能保持简洁和明确。

2 o1 尽可能避免不确定性。o1 的设计使其能够自信地识别自身知识的盲区，并在遇到不确定情况时明确地表达出来。

3 o1 力求完全透明和可观察。它的每一个行动都会被记录和注释，以便于充分理解和审查。

我们相信，这些设计选择使得 o1 成为一个更强大、更可靠，也最终更有用的 AI 智能体。

当然，这也意味着 o1 在某些方面不擅长。具体而言：

1 o1 不是一个优秀的聊天机器人。果您需要一个可以与您进行流畅对话的 AI，那么有其他比 o1 更好的选择。

2 o1 不擅长创造性的文本生成。如果您需要一个可以为您创作诗歌或故事的 AI，那么有其他比 o1 更好的选择。

3 o1 不擅长猜测或即兴发挥。如果您需要一个可以在信息缺失时进行推断，或在不确定情况下进行大胆尝试的 AI，那么有其他比 o1 更好的选择。

总而言之，我们相信 o1 的独特优势使其成为各种任务的宝贵工具，尤其是在那些对可靠性、可重复性和可观察性有较高要求的场景中。我们期待看到社区如何使用它！

---

How did I go from hating o1 to using it everyday for my most important questions?

我是如何从一开始讨厌 o1，到后来每天用它来解决我最关键的问题的呢？

I learned how to use it.

答案是：我学会了如何正确地使用它。

When o1 pro was announced, I subscribed without flinching. To justify the $200/mo price tag, it just has to provide 1-2 Engineer hours a month (the less we have to hire at dawn, the better!)

当 o1 pro 宣布推出时，我立刻就订阅了。为了对得起每月 200 美元的价格，它只需要每月提供 1-2 个工程师的工作量 （这样我们就不用总是在紧急情况下雇佣工程师了！）。

But at the end of a day filled with earnest attempts to get the model to work — I concluded that it was garbage.

但在认真尝试让模型运行了一整天后，我的结论是 —— 它表现很糟糕。

Every time I asked a question, I had to wait 5 minutes only to be greeted with a massive wall of self-contradicting gobbledygook, complete with unrequested architecture diagrams + pro/con lists.

每次我提出问题，都需要等待 5 分钟，最终得到的却是一大段自相矛盾的无意义信息，其中还包括未经要求的架构图和优缺点分析。

I tweeted as much and a lot of people agreed — but more interestingly to me, some disagreed vehemently. In fact, they were mind-blown by just how good it was.

我发了推特，很多人都同意 —— 但对我来说更有趣的是，有些人强烈反对。事实上，他们对它竟然这么好感到震惊。

Sure, people often get very hypey about OpenAI after launches (it's the second best strategy to go viral, right after being negative.)

当然，人们在 OpenAI 发布产品后经常会变得非常兴奋（这是仅次于负面评价 / 批评的第二好的爆火策略，是吧？）

But this felt different — these takes were coming from folks deep in the trenches.

The more I started talking to people who disagreed with me, the more I realized I was getting it completely wrong:

I was using o1 like a chat model — but o1 is not a chat model.

### How to use o1 in anger

如果 o1 不是一个聊天模型 —— 那它是什么呢？

If o1 is not a chat model — what is it?

I think of it like a "report generator." If you give it enough context, and tell it what you want outputted, it'll often nail the solution in one-shot.

我更倾向于把它看作一个「报告生成工具」。只要你提供充分的背景信息，并明确告知它所需的输出格式，它通常能够一步到位地给出解决方案。

> swyx's Note: OpenAI does publish advice on prompting o1, but we find it incomplete, and in a sense you can view this article as a "Missing Manual" to lived experience using o1 and o1 pro in practice.

swyx 笔记：OpenAI 确实发布了一些关于提示词 o1 的建议，但我们认为这些建议不够完善。在某种程度上，你可以将本文看作是实际使用 o1 和 o1 pro 的经验总结，一份「缺失的手册」。

[Reasoning models - OpenAI API](https://platform.openai.com/docs/guides/reasoning#advice-on-prompting)

#### 1. Don't Write Prompts; Write Briefs

不要撰写提示词，而要编写概要提供丰富的背景信息。

Give a ton of context. Whatever you think I mean by a "ton" — 10x that.

无论你认为的「丰富」是多少，都请在此基础上增加十倍。

When you use a chat model like Claude 3.5 Sonnet or 4o, you often start with a simple question and some context. If the model needs more context, it'll often ask you for it (or it'll be obvious from the output).

当你使用像 Claude 3.5 Sonnet 或 4o 这样的聊天模型时，你通常从一个简单的问题和一些背景信息（context）开始。如果模型需要更多的背景信息，它通常会主动向你提问（或者从返回的结果中可以明显看出来）。

> (Putting context at the end is better for OpenAI models - per OpenAI's own docs)

（根据 OpenAI 官方文档，将上下文信息置于末尾，能更好地服务于 OpenAI 的模型。）

You iterate back and forth with the model, correcting it + expanding on requirements, until the desired output is achieved. It's almost like pottery. The chat models essentially pull context from you via this back and forth. Overtime, our questions get quicker + lazier — as lazy as they can be while still getting a good output.

你需要与模型进行反复交互，不断纠正模型的输出并细化需求，最终获得符合预期的结果。这个过程很像制作陶器：通过不断地调整和精雕细琢，最终得到满意的作品。聊天模型本质上就是通过这种反复的交流来理解你所提供的上下文信息。随着使用时间的积累，为了在保证输出质量的前提下，我们提问的方式会变得更加简洁高效。

o1 will just take lazy questions at face value and doesn't try to pull the context from you. Instead, you need to push as much context as you can into o1.

o1 只会简单地理解问题的表面含义，不会主动挖掘你想表达的深层内容。因此，你需要主动提供尽可能详细的背景信息。

Even if you're just asking a simple engineering question:

即使你只是在咨询一个简单的技术问题，也要：

1 Explain everything that you've tried that didn't work

详细说明你之前尝试过但失败的所有解决方案

2 Add a full dump of all your database schemas

提供所有数据库结构的完整信息

3 Explain what your company does, how big it is (and define company-specific lingo)

介绍你的公司业务、规模大小（同时解释公司内部使用的专业术语）

In short, treat o1 like a new hire. Beware that o1's mistakes include reasoning about how much it should reason. Sometimes the variance fails to accurately map to task difficulty. e.g. if the task is really simple, it will often spiral into reasoning rabbit holes for no reason. Note: the o1 API allows you to specify low/medium/high reasoning_effort, but that is not exposed to ChatGPT users.

简单来说，可以把 o1 当作一个新来的员工。需要注意的是，o1 有时会犯一些错误，比如它不太能准确判断需要进行多少推理。也就是说，它对任务难度的估计有时不太准确。举个例子，如果任务非常简单，它也可能会过度分析，钻牛角尖。注意：o1 API 允许你设置推理强度（reasoning_effort），分为低、中、高三个等级，但 ChatGPT 用户无法使用这个功能。

> Tips to make it easier giving o1 context

让提供 o1 上下文更轻松的小技巧：

I suggest using the Voice Memos app on your mac/phone. I just describe the entire problem space for 1-2 minutes, and then paste that transcript in.

我建议在你的 Mac / 手机上使用语音备忘录应用。你可以用 1-2 分钟描述整个问题，然后粘贴录音的文本。我自己会专门用一个笔记来保存这些上下文信息，方便重复使用。

I actually have a note where I keep long segments of context to re-use.

swyx: I use Careless Whisper by Sarav from the LS DiscordThe AI assistants that are popping up inside of products can often make this extraction easier. For example, if you use Supabase, try asking the Supabase Assistant to dump/describe all of the relevant tables/RPC's/etc.

swyx：我用的是 LS Discord 里 Sarav 写的 Careless Whisper。现在很多产品里都自带 AI 助手，它们通常能更方便地提取信息。比如，如果你用 Supabase，可以试试让 Supabase 助手导出（dump）并描述所有相关的表（table）、RPC 等。

Twitter:

Another insight i had today: spend 100x more in prompting if you expect 100x more in output quality.

我今天又有一个新的见解：如果你期望产出质量提高 100 倍，就在提示词工程（prompting）上多投入 100 倍。

o1 can do alot, but it still can't read your mind.

即使像 o1 这样强大的模型，它仍然无法读取你的想法。

With the improvements in longer test time compute (planning and reasoning), the returns to crafting prompts and giving context also magnify 100-fold.

随着更长的测试时间所带来的计算能力提升（用于规划和推理），精心设计提示（prompt）和提供背景信息所带来的收益也显著增加，甚至可达百倍。

so I'm using o1 in a totally different way, not starting a convo but just telling it my entire situation and saying what i'm unhappy with about it. this is much much closer to using o1 as an advisor than just a chatbot. and that means spending the time to give context, clarify goals, and specify constraints, much more than enjoying a simple conversation.

所以我使用 o1 的方式截然不同，不是发起对话，而是直接将我的完整情况告知于它，并详细说明我对现状的不满之处。相比于仅仅将 o1 当作聊天机器人使用，这种方式更像是将其作为一位顾问。这意味着需要投入更多的时间来提供上下文、明确目标，并详细设定约束条件，而不仅仅是进行轻松的对话。

Bonus tip: always ask for alternative approaches. The thing is searching thru options anyway, might as well get it to spell out each option so you can take a final executive decision.

实用建议：记得询问所有可能的解决方案。既然系统本身就会分析各种可能性，不如让它详细列举每种方案的优劣，这样你就能做出更明智的决策判断。

#### 2. Focus on Goals: describe exactly WHAT you want upfront, and less HOW you want it

关注目标：开门见山地说明*你想要什么*，而不是*怎么做*

Once you've stuffed the model with as much context as possible — focus on explaining what you want the output to be.

一旦你给模型提供了尽可能多的背景信息 —— 重点说明你期望的输出结果。

With most models, we've been trained to tell the model how we want it to answer us. e.g."You are an expert software engineer. Think slowly + carefully"

对于大多数模型，我们通常需要训练它们，告诉模型我们期望的回答方式。例如，我们会告诉模型：「你是一位专业的软件工程师，请缓慢而仔细地思考」。

This is the opposite of how I've found success with o1. I don't instruct it on the how — only the what. Then let o1 take over and plan and resolve its own steps. This is what the autonomous reasoning is for, and can actually be much faster than if you were to manually review and chat as the "human in the loop".

但我在使用 o1 时发现，更有效的方法恰恰相反。我不告诉它如何做，只告诉它做什么。然后，让 o1 自主接管，规划并解决它自己的步骤。这正是自主推理的目的所在。实际上，这种方式可能比您手动检查，并以「人机协作」的方式进行对话更快。

> swyx's pro tip: developing really good criteria for what you consider to be "good" vs "bad" helps you give the model a way to evaluate its own output and self-improve/fix its own mistakes. Essentially you're moving the LLM-as-Judge into the prompt and letting o1 run it whenever needed. As a bonus, this eventually gives you LLM-as-Judge evaluators you can use for Reinforcement Finetuning when it is GA.

swyx 的建议：为「好」与「坏」制定明确的标准，能帮助你为模型提供一种评估自身输出、自我改进并修复自身错误的方法。本质上，你是将大语言模型（LLM）的评判能力融入到提示中，并根据需要随时运行。此外，当强化微调（Reinforcement Finetuning）技术成熟时，你最终可以获得可用于强化微调的、大语言模型（LLM）评判器。

This requires you to really know exactly what you want (and you should really ask for one specific output per prompt — it can only reason at the beginning!)

这要求你必须准确知道自己的需求（而且每次提问时最好只专注于一个具体目标 —— 因为系统只能在对话开始时进行分析和判断！）

Sounds easier than it is! Did I want o1 to implement a specific architecture in production, create a minimal test app, or just explore options and list pros/cons? These are all entirely different asks.

这件事看似简单，实则不然！比如当我们在使用 o1 时，目标可能是：在生产环境中实现某个特定架构、创建一个基础的测试程序、或者仅仅是研究各种可能性并分析其利弊。这些都是性质完全不同的任务。

o1 often defaults to explaining concepts with a report-style syntax — completely with numbered headings and subheadings. If you want to skip the explanations and output complete files — you just need to explicitly say that.

o1 经常默认采用类似报告的格式来解释概念 —— 带有编号的标题和子标题。如果你想跳过这些解释，直接生成完整的文件 —— 你只需要明确地提出要求。

Since learning how to use o1, I've been pretty mind-blown by its ability to generate the right answer the first time. It's really pretty much better in every single way (besides cost/latency). Here are a few little moments where this has particularly stood out:

自从我开始学习使用 o1 以来，它第一次就能给出正确答案的能力让我印象深刻。除了成本和延迟之外，它几乎在所有方面都表现得更好。下面分享几个让我觉得特别惊艳的瞬间：

#### 3. Know what o1 does and does not do well

了解 o1 的优势与局限

What o1 does well:

o1 的优势：

1 Perfectly one-shotting entire/multiple files: This, by far, is o1's most impressive ability. I copy/paste a ton of code in, a ton of context about what I'm building, and it'll completely one-shot the entire file (or files!), usually free of errors, following existing patterns I have in my codebase.

能够完美地一次性生成完整 / 多个文件：这是 o1 目前最令人惊叹的功能。我复制粘贴大量的代码，以及关于我正在构建内容的大量背景信息，该模型就能完全一次性地生成整个文件（或者多个文件），并且通常没有错误，还能遵循我代码库中已有的编码模式。

2 Hallucinates Less: In general, it just seems to confuse things less. For example, o1 really nails bespoke query languages (like ClickHouse and New Relic), where Claude often confuses the syntax for Postgres.

减少胡编乱造：总的来说，它似乎不太容易混淆事情。例如，o1 在处理定制查询语言方面表现出色（如 ClickHouse 和 New Relic），而 Claude 常常会把 Postgres 的语法搞混。

3 Medical Diagnoses: My girlfriend is a dermatologist — so whenever any friend or anyone in my extended family has any sort of skin issue, they're sure to send her a picture! Just for fun, I started asking o1 in parallel. It's usually shockingly close to the right answer — maybe 3/5 times. More useful for medical professionals — it almost always provides an extremely accurate differential diagnosis.

医学诊断：我的女朋友是位皮肤科医生，因此亲朋好友们一遇到皮肤问题，总是会给她发照片求助！我觉得好玩，就开始同步询问 o1（具体指代内容需要补充说明）。它给出的答案通常非常接近正确诊断，大概有 60% 的准确率。对于医疗专业人员而言，o1 更有价值，因为它几乎总能提供极其精确的鉴别诊断。

4 Explaining Concepts: I've found that it is very good at explaining very difficult engineering concepts, with examples. It's almost like it generates an entire article.When I'm working on difficult architectural decisions, I will often have o1 generate multiple plans, with pros/cons for each, and even compare those plans. I'll copy/paste the responses as PDF's, and compare them — almost like I'm considering proposals.

概念阐释：我发现它非常擅长解释复杂的工程概念，并且能够给出相应的示例。它几乎可以像写一篇完整的文章那样进行阐述。在进行困难的架构决策时，我经常会让 o1 生成多个方案，并列出每个方案的优缺点，甚至对这些方案进行比较分析。我会将这些结果复制并粘贴成 PDF 文件，然后进行对比，就像在评估不同的提案一样。

5 Bonus: Evals. I have historically been very skeptical of using LLM as a Judge for Evals, because fundamentally the judge model often suffers from the same failure modes as what generated the outputs in the first place. o1, however, shows a ton of promise — it is often able to determine if a generation is correct or not with very little context.

额外发现：评估（Evals）。我一直对使用大语言模型（LLM）作为评估的裁判持怀疑态度，因为裁判模型通常会遇到与生成输出内容的大语言模型（LLM）相同的错误。然而，o1 展示出了巨大的潜力 —— 它常常能够在极少背景信息的情况下判断生成的内容是否正确。

What o1 doesn't do well (yet):

o1 目前还不擅长的方面：

1 Writing in specific voices/styles: No, I did not use o1 to write this post :)I've found that it's pretty bad at writing anything, especially in specific voices or styles. It has a very academic/corporate report style that it wants to follow. I think that there are just so many reasoning tokens biasing the tone in that direction, it's very hard to break free from that.Here's an example of me trying to get it to write this post — this is after much back and forth — it just wants to produce a bland school report.

以特定语气 / 风格写作：不，我没有用 o1 来写这篇文章。我发现它不太擅长写作，尤其是在使用特定的语气或风格时。它倾向于使用非常学术化 / 公司报告的风格。我认为是因为有太多的用于推理的 Token 让其语气偏向这个方向，很难摆脱这种影响。这里有一个我尝试让它写这篇文章的例子 —— 经过多次尝试 —— 它只会生成平淡的学校报告。

2 Building an Entire App: o1 is mindblowingly good at one-shotting entire files. that being said, despite some of the more… optimistic… demos you might see on twitter — o1 is not going to build an entire SaaS for you, at least not with a lot of iteration. But it can pretty much one-shot entire features, especially if they're front-end or simple backend features.

构建整个应用程序：o1 在快速处理整个文件方面表现惊艳。尽管如此，即使你在 Twitter 上看到一些非常乐观的演示，o1 也不会直接为你构建一个完整的 SaaS 应用，至少在经过大量迭代之前是这样。但是，它可以快速实现整个功能，特别是前端或简单的后端功能。

### Aside: Designing Interfaces for Report Generators

题外话：报告生成器的界面设计

Latency fundamentally changes our experience of a product.

延迟会显著影响用户体验，这是报告生成器设计需要考虑的关键因素。

> swyx: we agree - as much as 6 grades of AI latency are common now. Inference, Fast and SlowNovember 5, 2024Read full story

swyx：我们都同意 —— 目前常见的 AI 延迟通常分为 6 个等级。推理：速度的快与慢，2024 年 11 月 5 日。

Consider the differences between mail, email and texting — it's mainly just latency. A voice message vs. a phone call — latency. A video vs a Zoom — latency. And so on.

想想邮件、电子邮件和短信的区别 —— 主要就在于延迟。语音留言和电话的区别在于延迟，视频和 Zoom 的区别也在于延迟。以此类推。

I call o1 a "report generator" because it's clearly not a chat model — it feels a lot more like email.

我把 o1 叫做「报告生成器」，因为它明显不是聊天模型，用起来更像是电子邮件。

This hasn't yet manifested in o1's product design. I would love to see the design more honestly reflected in the interface.

这一点还没有在 o1 的产品设计上体现出来。我希望在用户界面上能更直接地看到这种设计理念。

Here are some specific AI UX tips for anyone building o1-based products:

以下是一些为构建基于 o1 的产品的开发者提供的 AI 用户体验（UX）建议：

1 Make it easier to see the hierarchy of the response (think a mini table of contents)

让用户更容易理解响应的层级结构（可以将其视为一个迷你目录）。

2 Similarly, make the hierarchy more easily navigable. Since every request is usually larger than the height of the window, I would take a Perplexity like approach where each question/answer page gets a section vs. freeform scroll. Within an answer, things like sticky headers, collapsible headers, etc. could really help)

类似地，为了让层级结构更易于浏览，可以参考 Perplexity 的做法。鉴于每个请求的篇幅通常都超过窗口高度，建议将每个问题和答案页面划分成独立的章节，避免自由滚动式的浏览方式。在答案内部，还可以使用粘性标题、可折叠标题等功能，以提升阅读体验 ）。

3 Make it easier to manage and see the context you're providing to the model. (Ironically Claude's UI does a much better job of this — when you paste in a long piece of text, it renders as a little attachment). I also find that ChatGPT Projects don't work nearly as well as Claude's, so I'm copying and pasting stuff a lot.

让管理和查看您提供给模型的信息上下文变得更加容易（具有讽刺意味的是，Claude 的用户界面在这方面表现更出色 —— 当你粘贴一大段文字时，它会显示为一个小的附件）。我还发现 ChatGPT 项目的使用体验不如 Claude，所以我不得不频繁地复制和粘贴内容。

Side note:

Separately ChatGPT is REALLY buggy when it comes to o1. The descriptions of reasoning are comical, it often completely fails to generate, and most often doesn't work on the mobile app.A beautiful day in… Kenya??

### What's next?

接下来是什么？

I'm really excited to see how these models actually get used. 

我非常期待看到这些模型在实际应用中的表现。

I think o1 will make certain products possible for the first time — for example, products that can benefit from high-latency, long running background intelligence.

我认为 o1 将首次催生某些前所未有的产品 —— 例如，那些能够受益于高延迟、长时间运行的后台智能的产品。

What sort of tasks is a user willing to wait 5 minutes for? An hour? A day? 3-5 business days?

用户愿意等待多久来完成特定的任务？5 分钟？1 小时？ 1 天？甚至 3-5 个工作日？

A bunch, I think, if it's designed correctly.

我认为，如果经过精心设计，用户愿意等待的任务有很多。

As models get more expensive, experimentation gets harder to justify. It's easier than ever to waste $1000s of dollars in just minutes.

随着模型成本的不断攀升，实验的成本效益也变得更难评估。仅仅几分钟内就可能耗费数千美元，这种情况比以往任何时候都更容易发生。

o1-preview and o1-mini support streaming, but they don't support structured generation or system prompts. o1 supports structured generation and system prompts, but not streaming yet.

o1-preview 和 o1-mini 支持流式传输（streaming，即实时数据传输），但不支持结构化生成（structured generation，即按照预定格式生成内容）或系统提示（system prompts，即预设的角色或指令）。o1 支持结构化生成和系统提示，但目前尚不支持流式传输。

Given how long a response takes, streaming feels like a requirement.

考虑到生成回复所需的时间，流式传输（streaming）几乎是不可或缺的。

It will be very cool to see what developers actually do with the model as they get to work in 2025.

展望 2025 年，开发者们开始实际应用该模型后，他们会如何利用它，这将会非常令人期待。