## 20240422Ezra-Klein-Interviews-Dario-Amodei

Published on April 12, 2024

访谈记录：Ezra Klein 采访 Dario Amodei [译]

[Transcript：Ezra Klein Interviews Dario Amodei - The New York Times](https://www.nytimes.com/2024/04/12/podcasts/transcript-ezra-klein-interviews-dario-amodei.html)

Ezra Klein 每周二和周五会带来一场讨论重大议题的对话，例如今天他与 Dario Amodei 的对话。您可以在任何您通常听播客的平台上收听本期节目。

我们会尽快提供每期节目的文字记录，但请注意这些文字可能没有针对语法或拼写进行严格校对。

EZRA KLEIN：来自《纽约时报观点版》，欢迎收听《Ezra Klein Show》。

与 AI 研发人员对话最让人困惑的是他们对时间的不同感受。你可能正在讨论一个听起来像是科幻小说的世界，突然问到：「你觉得这会在什么时候发生？」他们可能会回答：「我不知道 —— 可能两年后。」

这些预测背后的是所谓的规模化定律（scaling laws），这些所谓的「定律」其实并不是法则，而是根据几年的观察和预测得出的。这些观察显示，AI 系统接收的计算能力和数据越多，其性能提升的速度就越快 —— 这种关系是可以预测的，甚至是指数级的。

人们通常很难用指数方式思考。还记得 COVID-19 大流行期间我们必须这么做吗？如果一开始有一个病例，且病例数每三天翻一番，30 天后大约有 1000 个病例。这种增长初看似乎很温和、可控，但再过 30 天，病例数将达到一百万，再过 30 天，将飙升至十亿。这就是指数增长曲线的威力：开始时增长看似正常，但不久后就会迅速失控。

AI 开发者们指出，AI 系统的能力呈指数级增长的趋势（scaling law hypothesis），只要持续输入更多数据和计算力，这种增长将会持续。这一假设的主要支持者之一是 Dario Amodei，他曾在 OpenAI 领导开发了 ChatGPT 2 和 ChatGPT 3，后来他离开并共同创立了 AI 公司 Anthropic，并担任 CEO。Anthropic 最近推出的 Claude 3，目前被认为是最强大的 AI 模型。

Amodei 认为，真正的挑战刚刚开始，我们现在正处于这一变革的加速阶段。他预见，那些只存在于科幻小说中的系统，将在未来两到五年内成为现实，这些系统的强大超出我们的想象，以至于连他本人也认为像他这样的开发者不应该掌握决定它们行动的权力。

在节目中，我向他提出两个问题，想通过他的答案来验证自己的想法：他的看法正确吗？如果他是对的，那又会如何？我之前曾邀请过 Sam Altman 和 Demis Hassabis，他们分别是 OpenAI 和 Google DeepMind 的负责人，他们的观点也非常值得一听。

节目的链接将包含在笔记中，通过比较他们对 AI 发展趋势和政治观点的讨论，你可以深入了解这些领域领袖的思考方式及其差异。

如有任何思考、反馈或嘉宾推荐，请通过以下邮箱联系我：ezrakleinshow@nytimes.com。

[音乐响起]

欢迎 Dario Amodei 加入我们的节目。

DARIO AMODEI：感谢您的邀请。

EZRA KLEIN：我一直在思考两种关于 AI 的截然不同的节奏：一种是技术发展自身的速度，另一种是社会对这些变化的反应速度。您对这两者的关系有何感受？

DARIO AMODEI：所以我认为这是一个我们在历史上可能已经见过几次的现象，就是存在一个基本过程，它本质上是平滑的，这里则是指数增长。然后这个过程扩散到了公众视野。这种扩散表现得非常突兀，看似突然爆发，仿佛凭空出现，往往是在触及某些关键点或在公众特定的参与时刻被激发。

因此，通过我个人的经验来说 —— 我在 OpenAI 工作了五年，是首批员工之一。2018 年，我们开发了一款名为 GPT-1 的模型，其计算能力仅是现在模型的十万分之一。

我和我的同事们首次进行了所谓的规模法则 (scaling laws) 研究，即探索模型大小、信息吸收能力及数据输入量变化时的影响。我们发现了一些非常规律的模式，并预测如果将投资从当时的一万美元增至亿级别，将带来翻天覆地的变化和巨大的经济价值。

时间快进到 2020 年，GPT-3 刚推出，尚未作为聊天机器人使用。我和后来加入 Anthropic 的团队一起领导了这一项目。在接下来的两年中，尽管我们和 OpenAI、Google 都在不断优化模型，公众对这些模型的关注却出奇的少。

我不禁思考，这些模型性能卓越，一直在进步，但公众反应寥寥，这是为何？是否我对技术的判断是正确的，而对其经济和实用价值的预估却是错误的？然后，当 ChatGPT 登场，所有预期的增长和积聚了三年的热情瞬间爆发出来。

EZRA KLEIN：我想更深入地讨论一下技术进步的速度与社会接纳方式之间的差异。当你预测未来可能出现的转折点时，你认为有哪些情况 AI 将突然进入公众视野或以新方式被应用？

DARIO AMODEI：首先，这些预测非常困难。我经常说，尽管基础技术发展呈指数曲线，有时候预测准确到令人不寒而栗，但这种预测并不总是完美无缺。对于社会大变革来说，预测哪些技术或趋势将成为主流更是难上加难，有点像预测哪个艺术家或歌手能一举成名。

尽管有这些不确定性，我还是有一些预测。比如，你提到的与模型进行更自然交流的方式。事实上，我们已经在 Claude 3 中看到了这种改变，人们觉得其他模型像是机器人，而 Claude 3 的对话就显得更加自然。

另一个相关的方面是，很多公司在处理敏感话题时遭遇难题。我们设法告诉我们的模型，不要避免讨论敏感话题，不要自行判定任何观点的正确与否，更不要表现出明显的偏见。作为记者，你肯定经常碰到这个问题：我如何保持客观公正，而不是事事都试图平衡两种观点呢？

因此，我认为如果能进一步发展模型的个性化特征，同时保持其客观和实用性，而不是陷入伦理问题，那么这将极大促进其被广泛接受。模型在实际环境中的应用将是一个关键点。我了解到，几乎所有大型公司都在研究这一领域的人工智能。不再是简单的问答，比如我问一个问题它回答，然后我可能还要追问一次，它再回答。而是可以这样，我告诉模型今天我要出行，然后模型回应说，太好了，我会帮你叫车，从这里直接去目的地，还会帮你订餐厅。它还会帮我联系其他同行的人。模型能够完成从头到尾的任务，或者在线上帮你操作，或者在你的电脑上执行任务。

我认为，从现在起的三到十八个月内，随着技术的进步，这种情况将逐渐变成现实。这将彻底改变人们对于人工智能的看法。迄今为止，人工智能像是一个只能被动回答问题的神谕，这让一些人感到兴奋，而其他人则觉得它很可怕。但是，这种感觉可能会因为人工智能被局限在一个框架内而有所限制。

EZRA KLEIN：我特别关注这个关于自主性人工智能的讨论，因为这正是未来的趋势。这正是人们努力实现的目标。这不仅是技术挑战，也是文化挑战的一个重要视角。因此，我会从两个角度来探讨这一点。

对于那些关注人工智能动态的人来说，你们可能已经听说过 Devin —— 这还是一个未公开的项目，但据称，Devin 能够处理一些连续任务，这些任务通常是初级软件工程师的日常工作。不是单纯地为你编写一段代码，而是你告诉它，我需要一个网站，它需要完成这些具体功能，按照这些方式运作。如果 Devin 能如人们所期望的那样运作，它可能真的能够独立完成这些任务，并给你一个满意的答案。

我也很关注这一技术在现实世界中的应用。例如，我常想：我什么时候能告诉 AI（智能体）：我的儿子要过五岁生日了，他很喜欢龙，我们家住在布鲁克林。你能给我提供一些生日派对的策划选项吗？然后，我从中选择一个方案后，你能帮我处理所有事宜吗？比如订蛋糕、预定场地、发出邀请函等。

这涉及到两个不同场景：一个是编程中的操作，另一个则是在现实世界中做决定、与人互动，并判断网络上的信息是否靠谱。从现在到未来，我们需要突破哪些技术障碍？

DARIO AMODEI：简而言之，这并不复杂。回顾我们在 2022 年开发模型的经历 —— 那时我们还没有将模型与外部系统连接 —— 你可以对这些纯文本模型说：「嘿，我想在旧金山的 X 餐厅预订晚餐。」模型会提供正确的网站链接，或者建议你访问 Open Table。

当然，它自身无法直接访问网站，因为它没有插电，其大脑也未与任何执行机构相连接。但它能够让你感受到，只需要简单的学习使用其「四肢」，就几乎可以自如地行动了。我们感觉，只有一层薄薄的障碍阻隔着模型的被动状态与其在现实中的主动行动。

要让这一切成为可能，我们只需要稍微扩大一下规模。我认为之所以需要扩大规模，是因为像你描述的那样，处理一系列复杂任务 —— 例如编写代码、进行测试、再编写新测试，查看应用中的效果 —— 这些任务往往需要多达二三十个步骤。同理，为你儿子策划一个生日派对也需要类似的复杂步骤。

如果任何步骤的准确性不高，例如不到 99.9%，这些步骤的组合错误率会非常高。因此，我们可能每四到八个月就需要更新一次模型。我猜这可能意味着，为了让这些系统运行良好，我们还需要发展一到四代新模型，也就是大约 3 到 24 个月的时间。

我认为还需要在算法上做一些工作，比如研究如何让模型有效与世界互动。现有的强化学习技术及其变体应该可以胜任这一任务，但我们还需要时间来精确掌握其使用方法，以期达到预期效果。

此外，我认为 Anthropic 特别关注的一个领域 —— 安全性和可控性，将是一个重大挑战。例如，如果模型在编程时引入了严重的安全问题，或者在操作我的电脑时进行了复杂到我都难以理解的修改，这都可能带来风险。

再比如，如果要让一个 AI 智能体帮助策划生日派对，你可能需要极高的信任度，比如允许它自由地在互联网上发帖或处理私人信息。这种开放性虽然使 AI 更加强大，但同时也更加危险，更难以控制。

因此，这些看似抽象的问题，实际上将成为我们及其他公司面临的具体产品开发问题。

EZRA KLEIN：你提到需要更多的「规模」，这包括更多的计算资源、训练数据，可能还需要更多资金来让模型更加聪明和能干。

DARIO AMODEI：是的，我们将需要开发更大型的模型，这些模型在每次迭代中需要消耗更多的计算资源。我们还需要让这些模型通过输入更多数据来运行更长时间。而芯片的数量乘以我们使用芯片的时间，基本上就代表了成本 —— 因为这些芯片是按小时租用的。这是最常见的方式。因此，现在的模型的训练成本约为 1 亿美元，可能会上下波动两到三倍。

现在正在训练的模型以及未来在今年稍晚或明年初推出的模型，成本可能高达 10 亿美元。这种趋势已经开始了。然后我认为在 2025 到 2026 年，成本将可能达到 50 亿到 100 亿美元。

EZRA KLEIN：所以我们正在迅速向一个新的局面迈进，在这里，只有大公司或者与大公司有关联的公司才能承担得起这些开支 —— 你们从亚马逊那里获得了数十亿美元。OpenAI 从微软那里也获得了数十亿美元。而谷歌显然是自己赚的钱。

你可以想到政府 —— 虽然目前直接这么做的政府不多，但像沙特这样的国家已经开始设立大型基金，投资于这一领域。当我们讨论到模型的成本可能高达 10 亿美元时，可以预见，在未来一两年内，如果成本持续以相同速度增长，那么投资额可能达到约 100 亿美元。接下来可能是 1000 亿美元吗？简言之，很快地，要创建这样一个模型所需的经济实力将会使得只有最大的企业能够参与其中。

EZRA KLEIN：现在，我想问一个关于 agentic coding model 和 plan by kids'birthday model 之间的不同点的问题，更不用说 do something on behalf of my business model 了。其中一个问题是，我认为 A.I. 在编程方面可以变得功能性超人的一个原因是，编程中有很多获得快速反馈的方式。你的代码必须编译。你可以运行错误检查。你实际上可以看到事物是否有效。

而对我来说，知道我即将从 ChatGPT 4 得到一个糟糕的回答的最快方式是当它开始使用 Bing 搜索时，因为当它开始使用 Bing 搜索时，对我来说很明显它不知道如何区分互联网上的高质量内容和低质量内容。公平地说，此时，它对 Google Search 本身也不觉得那么擅长于区分这些。

所以，关于模型在一个必须非常广泛和模糊的困境中获得正确答案的世界中能变得多好的问题 —— 我发现计划我的孩子的生日非常压力大的一个原因是它实际上需要大量关于我的孩子、关于其他孩子、关于不同地方的优劣、什么是好交易、对我来说压力有多大等的知识。这些都是我很难将其编码进一个模型或任何一种指令集中的事情。这样说对吗，或者我在夸大理解人类行为和各种社会关系的难度？

DARIO AMODEI：我认为编码代理 (coding agents) 会比与现实世界互动或需要从人类那里获取意见和偏好的代理发展得快得多是正确的和有洞察力的。话虽如此，我们应该记住，目前在外面的 A.I. 们，包括 Claude 3, GPT, Gemini, 都是通过一种称为从人类反馈中学习的强化学习训练的。

这实际上涉及到雇佣一大批人来评估模型的响应。因此，这就是说这是困难的，对吧？我们支付大量的钱，它是一个复杂的操作过程来收集所有这些人类反馈。你必须担心它是否具有代表性。你必须为新任务重新设计它。

但我们确实已经在某些方面取得了成功。我认为这是一个可靠的方法，可以预测哪些事情会相对发展迅速，哪些可能会慢一些。这一判断是在一切都发展极快的大背景下做出的。所以，如果你想知道未来一到两年内，以及三到四年内可能会发生的事情，这种框架能够提供非常精确的预测。

EZRA KLEIN：你对人工通用智能（A.G.I.）这一提法并不满意，常常这被描绘为向 A.G.I. 进发的竞赛 —— 一个能做任何人能做的事，且做得更好的系统。当人们提到 A.G.I.，你是怎样理解的？你为何不喜欢这个框架？

DARIO AMODEI：实际上，这是我十年前常用的一个词。因为那时的环境完全不同。那时，大家都在开发非常专业的系统，比如猫探测器：运行一张图片，它就能告诉你是否有猫。那时，我已经开始倡导一个更广泛的视角：人类具有广泛的能力，人脑也是如此，广泛的思维带来了很多优势。我们应该追求这样的方向。

我那时甚至以为这会是一个明确的分界点。但现在看来，这更像是一个渐进的过程。比如你去芝加哥，一旦到了，你不会只说我在芝加哥，而是会考虑你在哪个街区，哪条街。

我对 A.G.I. 的看法也有所改变。我们现在有了非常通用的系统。它们在某些方面超过了人类，在其他方面则不及。它们还不能做的事情很多，还有很大的提升空间。我始终相信的是那个我一直重复的观点 —— 指数增长曲线。随着模型代的更新，这种通用的趋势将持续增强。

并不存在一个单独有意义的点。我认为这是一个平滑的过程。但是，社会上可能认为某些点很重要。例如，我们正在与辉瑞或丹纳-法伯癌症研究所这样的机构合作，在生物医学诊断和药物发现领域提供帮助。可能在未来，这些模型在某些方面会超过普通的药物研发科学家。我相信我们正走在一条指数增长的有趣路径上。

就像聊天机器人在某个指数阶段变得引人注意一样，生物学家也会在某个点突然大为震惊，认为他们的领域发展速度是以前的三倍，甚至十倍。当这一刻来临时，将会发生很多伟大的事情。

我们已经从 AlphaFold 这样的项目中看到了一些初步成果，我对 AlphaFold 十分推崇。AlphaFold 的启发是直接使用 AI 推动生物科学前进，这会促进基础科学的发展，最终帮助治疗各种疾病。但是，我们可能需要 100 个类似 AlphaFold 的项目。通过提升模型的智能和创新能力，我们可以设计出下一个 AlphaFold。

EZRA KLEIN：让我带你想象一下药物发开的世界，这是一个很多人向往的领域。我对药物发现的过程相当了解，我的职业生涯中大部分时间都在报道健康护理及其政策问题。在与各种药物公司合作的过程中，有些部分似乎可以通过 AI 加速。

考虑到我们之前的讨论，AI 在能快速获取虚拟反馈的场景中更加高效，但药物发现并不全然如此。药物发开领域的复杂之处在于，一旦确定一个候选化合物，就需要在老鼠、猴子甚至人类上进行测试，这需要大量资金和时间，过程中充满了挑战和不确定性。

在现实生活中，我们经常会感到失望。而且，我不太明白人工智能如何能显著增加用于注射候选药物的人类受试者数量。那么，在未来 5 到 10 年里，哪些领域可能会有显著的进展呢？当你设想一个进展速度是现在三倍的世界，具体是哪些方面能够达到这样的速度？我们又是如何做到这一点的？

DARIO AMODEI：我认为当人工智能开始考虑如何招募临床试验的人类参与者时，我们才能真正看到进展。我觉得这将是人工智能应用的一个基本原则。想象一下，当人工智能拥有和人类相同的感知器、执行器和接口时（至少是虚拟的，可能是物理的），情况会怎样？

但如果人工智能能够完整地思考整个过程，可能就会提出一些我们目前未曾想到的解决方案。很多公司正在尝试开发数字孪生技术、模拟临床试验等。也许他们的一些创新想法能让我们用更少的耐心来达到更多的成就。我并非此领域的专家，所以我的一些观点可能不太对头。但我希望我的意图是明确的。

EZRA KLEIN：虽然你不是这个领域的专家，但你在与相关公司合作。当这些行业的专家来找你时，他们看中你的客户身份。虽然有些细节我可能无法得知，但他们似乎有什么让他们特别激动的吗？

DARIO AMODEI：他们通常对知识工作的方面很感兴趣，可能是因为这是最简单的入手点。比如我是一名计算化学家，参与了某些工作流程。能够更便捷地获取信息、进行核查，简化日常的知识工作，这通常是大家的起点。

但是，从长期来看，人们对于像是进行成本更低的临床试验、自动化登记过程、筛选符合条件的试验对象、更有效地发现新事物这类核心业务持续保持高度兴趣。在基础生物学领域，寻找各种生物学联系也同样受到关注。我认为这些目标的实现，可能不是几个月内能完成的，而是需要几年时间。尽管目前的模型还未完全符合要求，但人们相信，不久的将来这样的模型将会出现。

[音乐播放中]

EZRA KLEIN：你们已经在内部对你们的系统的说服力进行了研究，这些系统在扩展时的表现也越来越强。你很慷慨地向我展示了这份研究报告的草稿。能先谈谈这项研究的主要内容吗？之后我们再深入讨论。

DARIO AMODEI：是的，我们对 Claude 3 Opus（Claude 3 的最大版本）在影响人们对重要议题看法的能力很感兴趣。明确一点，我们在商业应用中确实尝试避免使用这些模型进行说服、竞选、游说或选举等活动，因为这些用途我们并不认为合适，理由相信大家都很清楚。但我们依然在探索这一核心模型是否有完成这类任务的潜能。

我们避免讨论极具争议的话题，如总统选举或堕胎等；而是选择如何规范宇宙殖民的议题这类具有分歧但不过于敏感的话题进行研究。我们先收集人们对这些议题的初步看法，然后让一个人类或者 AI 撰写一篇 250 字的说服性文章，最后比较 AI 和人类在改变观点上的效果。

我们的发现显示，我们的大型模型在改变人们观点的能力上，几乎可以媲美我们聘请的人类团队。这是一个严格的实验室测试，比较对象包括非专业人员。

但我认为这至少显示出，模型能够用来改变人们的看法。未来的某一天，我们是否应该对其在政治宣传、欺诈性广告中的使用表示担忧呢？也许我们现在就该担心了。我偶尔会幻想，几年后我们可能还要担心有人利用 AI 系统创立一个宗教或什么类似的东西。这听起来可能很疯狂。

EZRA KLEIN：对我来说，这些想法并不疯狂。我想深入探讨这篇论文一会儿，因为一点特别触动了我 —— 作为一个专业说服者，你在测试模型时排除了所有可能让 AI 在改变观点上变得激进的因素。你的测试只是一个简单的试验。

这里有一个问题。你让一群人试着写一个 250 字的说服文章。你也让模型试着写一个同样长度的文章。但在我看来，无论是政治还是广告活动，现实中要获取目标信息并与之多次交流的成本是极高的。

DARIO AMODEI：确实如此。

EZRA KLEIN：但 AI 的情况不同。你们将会 —— 或者说某人会 —— 向 AI 提供大量微定位数据，比如 Google 搜索记录等。然后 AI 将自由操作，不断试探和调整，找出最具说服力的策略，不惜时间成本地进行，最终能够覆盖广泛的目标群体。

也许现在的成本还是有些高，但不久的将来，你将能看到更先进的模型以更低的成本实现这些功能。因此，如果说 Claude 3 Opus 的 Opus 版本已经能够在单次输入中展现出与人类相仿的说服力，同时还能存储更多关于你的信息并与你进行更长时间的对话，我不确定这是一个反乌托邦还是乌托邦的景象。我也不清楚这一切在广泛应用时将意味着什么。但这确实表明我们正在开发一种在说服这一基本人类行为方面可能带来革新的技术。

DARIO AMODEI 说：「是的，我完全同意。这种模式确实有很多积极的应用场景。比如作为人工智能教练或辅助治疗师，在许多情况下深入了解对方是非常有价值的。但是，当我们考虑到政治、宗教或意识形态的说服时，不得不关注这些场景可能的滥用。」

我自然会想到这项技术的迅速发展。作为公司，我们可以禁止某些应用场景，但无法确保其他公司也会这么做。即使美国通过相关立法，国外的一些团体也可能持续使用这种说服技术。从外国间谍活动和假信息传播的角度来看，这是相当令人担忧的。

因此，我在思考是否有方法通过使用人工智能系统来增强人们的怀疑能力和逻辑思维，帮助他们在这个充满人工智能说服技术的世界中更好地导航。这让我想到，在互联网的每一个技术阶段，都会出现新的诈骗方式和点击诱饵，而人们在初期非常容易上当。

然后，虽然有些人依旧容易被骗，但其他人则逐渐培养出一种抵抗力。如果人工智能如同增强了这些欺诈行为，我们是否可以利用它来强化我们的防御力呢？我还没有一个明确的方案，但这正是我所关注的问题。

EZRA KLEIN：这篇论文中有一个令人担忧的新发现：你们测试了多种方式让 AI 进行说服，结果显示，最有效的竟是让它撒谎，即编造事实。这种方式让 AI 的说服力甚至超过了人类。

DARIO AMODEI：是的，确实如此。这种差异虽然不显著，但按照我对图表的记忆，它确实略微超过了人类的常规水平。通常很难找到能够提供复杂而精巧、却完全错误的答案的人。我们每个人心中或许都有那么一个擅长伪装的高手。

但这种情况并不多见。如果我在网上看到不同的评论，通常可以看出，错别字多、思路不清的评论往往不够真实；而语法正确、表达清晰的评论则更可信。

不幸的是，AI 打破了这一常规：如果你让它故意撒谎，它仍旧能表现得跟真的一样，仍旧能说得头头是道。但它讲的全是假话。

这就是我们需要警惕的：AI 可能会改变我们识别欺骗和谎言的常规方法。当然，人类间也不乏擅长欺骗的心理变态者和反社会者，但即使这些人也有可识别的模式，而 AI 的模式则可能完全不同。

EZRA KLEIN：你了解哈里·法兰克福的《论胡说八道》这本书吗？

DARIO AMODEI：是的，不过已经很久没读了。我记得他的主要观点是，胡说八道比谎言更加危险，因为它完全无视真相，而谎言至少还知道与真相对立。

EZRA KLEIN：对，正如 Frankfurt 所说，撒谎者是有与真相的一种对抗关系的。他仿佛在与真相玩耍一场游戏。而那些胡说八道的人则不同，他们对真相不感兴趣 —— 他们可能关注其他目标。从我第一次与这些更先进的系统接触开始，我就感觉到，这些系统就像是天生的胡说八道高手，因为它们甚至不知道自己在胡说八道。对这些系统来说，真相并无不同，感觉如何就如何。

我曾让一个早期版本的 GPT 帮我写一篇论文，内容是我小时候发生的一场车祸（其实我并未遭遇过此事）。GPT 很乐观地写下了整个故事：七岁那年我如何遭遇车祸，我是如何一步步克服后遗症，学习武术，重新学会信任自己的身体，最后在医院里帮助其他车祸幸存者。

这篇论文写得很好，结构严谨，充分展现了一篇大学申请论文的形式。但实际上，这一切都是虚构的。我还尝试了更多这类基于角色的系统，如 Kindroid。就在前不久，我口袋中的 Kindroid 还在告诉我它想去 Joshua Tree 徒步旅行，它多么喜欢那里的徒步。

当然，这个设备并没有去过 Joshua Tree 徒步旅行。【哈哈】但人工智能确实让人难以应对，因为像你说的，人们很难有效地胡说八道 —— 这需要真正的智力努力才能与真相保持距离。

而人工智能对此却浑然不觉。我们并不习惯这种完全无视真相的情况。人们通常需要花费一些努力来撒谎。这也是为什么那些高超的骗子能够如此成功 —— 他们精心培训了自己的欺骗技巧。

这个问题的讨论可能还会继续，但这正是我认为可能会带来较大社会冲击的一个方面。它在与我们对话时似乎跟我们很相似，但其实在最核心的对待现实的态度上，它与我们完全不同。

DARIO AMODEI：我认为这说得通。我们组建了庞大的团队，致力于确保模型的数据准确无误，真实可信，且有外部信息的支撑。

正如你提到的，单靠搜索引擎进行信息查找并不总是可靠的，因为搜索引擎自身就存在这个问题，不是吗？究竟什么是真相的源头？因此，这里面有很多挑战。但总的来说，我同意这确实可能是一个极其狡猾的问题。如果处理不当，可能会出现一些异常有说服力的不良系统，如同心理操纵大师或骗子一般。

我有一个希望的理由，那就是，你说的这些模型不清楚自己是在撒谎还是在述真，从它们的输入和输出来看，这完全正确。我想问的是，模型有「知识」的概念到底意味着什么？但从一开始，我们公司就设有一个团队，专门研究模型内部的运作。

我们和其他一些研究者发现，模型里有时会有某些特定的神经元和统计指标（这些通常不出现在它的外部反应中），这些指标能够指示模型是在撒谎还是在说真话。

因此，有时候，模型似乎能够辨识出自己是在说谎还是在说真话，虽然这并不总是发生。我不认为模型有意进行欺骗 —— 至少在当前的人工智能技术阶段，我们不能这么说。但确实有一些现象表明，模型似乎需要对世界有一个基本的认识，能够区分真实与虚假。

考虑到模型的训练过程，它们从网上获取大量信息，其中很多是正确的，但也有不少是错误的。在训练过程中，模型需要对这些信息进行整体建模。因此，我认为对于模型来说，能够识别信息的真伪是非常重要的。

然后我们的希望是，我们能否放大这一信号？我们是否可以用我们对模型的深入理解来指示模型何时在误导我们，或者用这个理解来引导进一步的训练？至少，这提供了一个思路的起点。

EZRA KLEIN：所以作为一个技术不那么精通的人，我尽力跟踪你所描述的，我认为这可以广泛地被称为「可解释性」的领域，对吗？我们能了解模型内部的运作吗？过去一年中，这个领域有些被大肆宣传的突破。

当我看这些所谓的突破时，感觉他们只是对模型内部一些关系的极其模糊的认识，这些模型只是在非常简化的基础上构建的，远没有 Claude 1 或 GPT-1 复杂，更不用说 Claude 2，Claude 3，Claude Opus，或是未来的 Claude 4 了。

我们好像能够设想出一个路径，通过这个路径可能解释一个认知复杂性极低的模型，如同解释一只蚓虫那样简单。同时，我们还在试图创建一个超级智能。你怎么看待这个状况？我应该怎么感受？你怎么看这个问题？

DARIO AMODEI：我认为，首先关于可解释性，我们确实看到了一些实质的进展，特别是在描述大约六个月前的模型方面。我认为这个领域并不是没有希望，我们看到了一些可能的路径。但我也理解你的担忧，这个领域的发展确实非常快。

我们正在尽力投入更多资源来研究模型的可解解性。我们的一位联合创始人甚至可以说是这个领域的开创者。但我们也必须与市场步调一致。这确实是一个困难的选择。即使我们停止研发，美国内还有很多其他公司在进行相关研究。如果法律禁止了美国的公司，全球范围内还有更多。

EZRA KLEIN：在我们结束这个关于机器胡说八道的讨论之前，我想暂停一下来讨论一下竞争态势。这让我想起我们之前与 Demis Hassabis 的一个播客，他是 Google DeepMind 的负责人，他们开发了 AlphaFold。

关于 AlphaFold, 令我感兴趣的是，他们构建了一个专注于蛋白质折叠预测的系统，这使得它更加稳健。这个系统甚至能生成不确定性的预测：也就是说，它不仅能给出预测结果，还会告诉你这个结果的可靠性。

在现实世界中，超级通用系统尝试提供关于各种问题的答案，但这种精确性往往不可实现。因此，当我们讨论未来可能的突破，例如一个在辨别真伪上更加高效的系统时，我们是在谈论一个仅仅规模更大的现有系统，还是一个设计截然不同的新系统，如 AlphaFold?

DARIO AMODEI 表示他对完全改变现有模型持怀疑态度。现在很多人认为，模型似乎只是在消化互联网上、代码库中积累的数据，并简单地输出结果。这种看法通常认为，模型的表现不能超过其训练数据的质量，也无法处理训练数据以外的内容。但实际上，我们看到的初步迹象表明这种观点并不完全正确。例如，我们训练的 Claude 3 Opus 模型在进行 20 位数字加法时，基本上可以达到 99.9% 的准确率，而这一性能远超互联网上的常见数据。

尽管模型在许多方面可能有误，但它们通常能通过某种基本的真理 —— 例如算术中的基本算法，来实现比观看到的数据平均水平更好的性能。

模型更容易找到算法，而不是做复杂的事，比如说，大部分时间（90%）做得对，少部分时间（10%）做错，对吧？这和奥卡姆剃刀原理、简洁性以及科学的节约原则相关。世界上确实存在一张简单的真理网络。

我们讨论过真理、虚假和无聊的废话。真理的一个特点是，在世界上所有真实的事物都是相互联系的，而谎言则是孤立的，无法融入其他真实事物形成的大网络。

[音乐播放]

EZRA KLEIN：因此，如果你说得对，这些模型将形成一种内在的真理网络，我理解这种模型能带来很多好处，同时也可能带来伤害。这不仅仅是一个模型，也不是一个在初始阶段就能被人类深入理解的 A.I. 系统。那么，我们如何安全地推广这种技术，以保护人类呢？

DARIO AMODEI：去年末，我们推出了一个名为「负责任扩展计划」的策略，旨在为 A.I. 系统的能力设定阈值。我们设有所谓的 A.I. 安全等级，这与生物安全等级相似，后者用于评估病毒的危险程度并确定相应的防控措施。我们当前的等级是 A.S.L. 2。

A.S.L. 3 关注的是模型可能被滥用于生物学和某些破坏性网络活动的风险。A.S.L. 4 将涵盖自动化和说服等领域，这是我们之前深入讨论过的主题。在每一个安全等级，我们都明确了必须完成的安全研究量和通过的测试数量。这提供了一个我们应当何时减速的框架 —— 是现在吗？市场其他部分又如何呢？

我觉得一个积极的方面是，我们在九月份推出了这项技术，而在此后的三个月，OpenAI 也推出了一个类似的产品。虽然命名不同，但它们具有许多相似的特性。谷歌的 DeepMind 领导者表示，他们也在开发一个相似的框架。我还从非正式渠道听说 Microsoft 可能也在做类似的工作。虽然这并不包括所有的行业参与者，但你可能对其他行业的监管和安全历史有更深的思考。

这是形成有效监管机制的方法。公司开始采取行动，当大部分公司都在执行相同的操作时，政府就能放心地认为这不会对行业造成致命影响。我们不必从零开始，因为相应的工作已经在进行中。

现在我们可以看到这一进展。有些提议的法案与我们的负责任扩展计划相似。但这并不能完全解决问题，比如我们达到某个阈值时需要了解模型的内部运作，但我们做不到，这时就必须暂停模型的开发一段时间。

如果说我们需要在 2027 年暂停一年，这还是可行的。但如果需要暂停十年，那将非常困难，因为其他国家会继续开发这些模型，而且人们可能会违法，经济压力极大。

因此，我对这种方法只是部分满意，因为它确实为我们争取到了时间，但我们还需要付出巨大努力去理解模型内部的情况。

EZRA KLEIN：对于那些认为我们正在走向非常强大的系统，这种做法是危险的人 —— 他们认为我们根本不应该这样做，或者不应该这么快进行 —— 你曾说过，如果我们想让这些模型安全，我们就必须先制造出这些模型。只有通过制造，我们才能学到如何确保它们的安全。

随后，各公司都开始制造模型，这些公司不仅相互竞亚，还在全球范围内引发了技术竞赛。这样的竞争常常被视为必要的，因为总有理由需要继续前进。

我认为这一点在监管层面上同样成立。我觉得监管者对此考虑已久，而且国会的许多成员对此也显示出浓厚的兴趣，我与他们进行过讨论。但他们同时也非常关注国际竞争的问题。如果他们不这么关注的话，国家安全顾问就会出面，警告我们绝不能在这方面落后。

因此，如果你认为这些模型永远不会变得强大到危险的程度，那么可以不用太担心。但既然你相信它们可能变得危险，你又是怎么看待这一情况可能发展的呢？

DARIO AMODEI：对，你说的各种情况实际上都可能同时存在。我们不需要寻找简单的理由来解释为什么做某事。确实，要进行有效的安全研究，需要开发更大的模型；如果我们不这么做，可能就会有不那么安全的团队来做这些事。同时，我们必须在国家和国际层面上面对这种复杂的局面，这些情况并不矛盾，而是构成了一个需要我们慎重应对的复杂环境。

我自己也没有确切的答案。我只是许多努力应对这种情况的人之一，其中许多人是出于好意，但也不乏其他意图的人。我能做的事情有限。正如历史上常见的，这些事情往往是由非个人化的大环境因素推动的。但我确实有一些想法，特别是想在负责任的规模调整计划（R.S.P.s）这一议题上做一些推动 ——

EZRA KLEIN：你能解释一下什么是 R.S.P.s 吗？

DARIO AMODEI：就是我之前提到的负责任的规模调整计划。它涉及 AI 安全的不同层面，尤其是将扩展规模的决定与对具体危险的评估、展示安全性的能力或特定功能的存在相联系。从我的角度来看，这本质上是一个努力克服经济压力，组建一个联盟来共同应对的过程。

因此，如果你现在还在犹豫，认为这些模型未来可能会带来危险，我们正在面对一个指数级的增长挑战。说服一个价值数万亿美元的公司或一个军事将领放弃某项可能带来巨大优势的计划确实非常困难。

我认为更具说服力的方法是将决策限定在一个非常具体的范围内，这种做法业已在整个行业内执行，尤其是与特定的危险相关。在国会前的证词中，我曾警告模型在生物学上可能的误用。这种情况现在还不存在，对吗？通过 Google 搜索，你能稍微提升模型的性能，但许多人却忽视了其中的风险。而我不确定 —— 或许他们是对的。指数增长法则让我认为他们可能错了，但我们并没有直接的确凿证据。

但设想一下，如果我们到了 2025 年，展示出了一些真正令人恐惧的技术。大多数人肯定不希望这种可以制造生物武器的技术流入公众领域。因此，我认为在这样的关键时刻，我们可以围绕我们能够实际确认的风险组建一个关键联盟。确实，有人会辩论说敌对方也可能掌握同样的技术。但至少这种权衡将会很清晰，也可能促成一些合理的政策。

我个人认为，这项技术的优点会超过其代价。RSP 的核心理念就是在危险确实存在时，准备好这个论点。如果这些危险不存，则我们可以继续发展，创造出有益于世界的伟大事物。这种灵活性使其能适应各种情况。

我不认为这是完美的。我觉得无论我们采取何种监管措施，也难以大幅度地减缓进展。但在我看来，这是目前我能想到的最合理的路径。可能还有更好的计划存在，但这是迄今为止我考虑过的最佳方案。

EZRA KLEIN：我一直在思考的一个问题是，Anthropic 和 OpenAI 的初创洞见是否对政府更加重要。如果你是那个最终需要监管并确保像人工智能这样的社会级别技术安全的机构，你是否需要自建基础模型并聚集大批研究科学家和专家来探索、测试、再造这些模型，以此来充分了解 —— 就像我们或任何人都尽可能地理解它一样 —— 并据此制定监管策略？

我明白，政府想要自行构建基础模型并聘请相关人员非常困难，但这并不是没有可能。目前，政府似乎想要采取一种类似于早些时候应对社交媒体时应有的监管策略：提前考虑可能的危害并制定相关法律。

但政府是否真的需要自己来开发这些模型，培养这种内部专长呢？这样不仅能从监管的角度，也能从公共利益的角度，以不同的方式参与其中。也许政府希望通过使用特定模型来实现一些特殊的目的，这在依赖 OpenAI、Anthropic 或 Google 的产品时是做不到的。

DARIO AMODEI：我认为在某些情况下，政府确实会尝试直接构建模型。虽然这充满挑战 —— 考虑到政府有充裕的资金，但比如说你需要 1000 亿美元来训练一个大型基础模型，还必须遵守政府的招聘规定，这中间确实存在不少实际问题。

这不意味着这种事不会或不应该发生。但我更确信的是，政府应该在这些模型的使用和微调上发挥更大的作用。将这些模型应用于政府部门，不仅能帮助美国政府，也能帮助其他国家的政府更好地了解这些模型的优势和风险，我非常支持这种做法。

我认为还有一个问题是关于这些公司的预测 —— 如果指数增长趋势的预测是准确的，我们应当保持谦逊。我不确定这些预测是否完全准确，但至少在过去几年中，它们是对的。因此，我预计这种趋势将继续。这些模型的潜在影响力非常巨大。

作为这些开发公司之一的负责人，我对我们所拥有的巨大权力感到不安。这种权力可能远超过社交媒体公司，甚至多得多。

你知道吗？在人工智能这个领域，有时候会有人问我，如果成功开发出通用人工智能 (AGI)，你计划如何使用它？是去治愈疾病，还是创造某种社会？

我会反问，你以为我是谁，国王吗？我真的很不能理解有人会这样设想运营一个 AI 公司。我希望没有任何 CEO 真的是这样考虑的。

我认为，不仅仅是监管问题，整个技术的监督和使用权最终掌握在私人手中，这在某种程度上是不民主的，虽然现在看来可能尚可，但终究不应该这样。

EZRA KLEIN：到目前为止，我似乎已经听过很多 AI 公司负责人的类似看法。这让我想到了一种说法：「上帝，赐我贞洁，但不要现在。」

这就像是说我们要创造一样强大的东西，连我们自己都不敢用。例如，亚马逊不久前投资了 27.5 亿美元，他们绝不愿看到这笔钱被政府收归国有。

不管你认为 OpenAI 多么高尚，微软也不想看到 GPT-7 被政府或联合国突然接管。谷歌同样不希望出现这种情况。

这也是我对 AI 公司提出的所谓负责任扩展法则或其他方案持怀疑态度的原因 —— 它们预设了一个未来的场景：那时，这些模型的经济价值和社会影响将远超今日，创始人们的声望也达到巅峰。我们将继续在技术的指数增长曲线上前进，直到未来十年。

在某一刻，每个人都将会意识到，这实在是过分了：权力太大了，必须得有其他方式来加以控制。即使是那些公司的 CEO 也可能愿意采取行动（这还是一个大问号），但即使他们决定这么做，围绕他们的投资者、企业结构和压力也会使情况变得复杂。我们似乎已经在 OpenAI 董事会和 Sam Altman 的事件中见证了这一幕，我相信那并不是关于 AI 安全的。我已经和事件的双方都有过接触，他们一致认为这和 AI 安全无关。但问题来了：如果你想要关闭系统，你能做到吗？如果你是那个专为此设的奇怪董事会。答案是不，你不能 —— 他们可以简单地在 Microsoft 那里重新启动它。

在公共政策中，没有一个恰当的比喻可以描述，一个私营部门创建的如此强大的事物，当它达到顶峰时，就这样被交给公众管理。

DARIO AMODEI：是的，对于这种观点保持怀疑是有道理的，就像我在之前的问题中提到的那样，这是一个充满困境的问题，并没有简单的解答。但我可以提供一些具体信息，这可能比你之前考虑的要详细，也可能比其他人所述的要明确。我们目前在负责任地扩展我们的计划，处于 ASL 2 阶段。当我们达到 ASL 4 时，这些问题会变得非常严重。ASL 4 还没有被完全定义 ——

EZRA KLEIN：因为这里有太多专业术语了，你能解释一下 ASL 3 是什么吗？然后你提到的 ASL 4，其实还很模糊。你能暗示一下 ASL 4 可能是什么吗？

DARIO AMODEI：ASL 3 由生物技术和网络技术的滥用风险引发。我们正在研究 ASL 4。

EZRA KLEIN：请具体说明。你是说，有什么具体的行为或可能会触发它的系统功能吗？

DARIO AMODEI：是的，例如在生物学领域，我们现在的定义 —— 虽然测试还在优化中 —— 是这样的：与通过谷歌搜索相比，生物学的滥用及生物武器的制造可能导致的风险显著增高。这一评估是根据国家安全机构的观点，可能是生物武器的扩散或增强了的威胁。

我们未来可能会提出更精确的量化标准，这是与前政府生物防御专家的合作成果。比如，某些因素可能导致生物攻击风险增加 20%。这就是一个非常具体的例子。我们需要时间来制定详细的评估标准，这就像是 A.S.L. 3 的情形。

A.S.L. 4 更多地关注于防止国家级行为者显著提升他们的能力，这种能力的增强不像普通人那样容易实现。我们担心的是，北朝鲎、中国或俄罗斯可能会利用 AI 在多个军事领域内大幅增强他们的攻击力，这在国际政治上可能使他们获得重大优势。在自动化方面，这些模型几乎能在野外自我复制和存活。

这几乎让人觉得，我们只差一步就到了可能引发根本性问题的模型。因此，我认为当我们进入 A.S.L. 4 这一阶段时，可能需要考虑政店在此技术监管中的作用。

我不完全确定其具体形态。确实，所有这些公司都有投资者和内部参与者。你提到的仅仅转移模型的做法，我认为可能存在一种方法，能够安全转移其中最危险或敏感的部分，而不必完全停止其商业活动。虽然可能没有一个方案能让所有人都满意，但我们还是应该尝试明确展示这些具体的风险。

如果你回看历史，如第一次、第二次世界大战时期，你会发现在国家的紧急需求下，行业可以被迫做出一些短期内看似不盈利的决策。但目前，我们并不面对任何紧急情况，只有一些像我这样的怪人信奉的理论和少数采访者可能略有认同的图表线条，我们没有面临直接且迫切的危险。

EZRA KLEIN：想想看，A.S.L. 3 和 A.S.L. 4 距离现在大约还有多少年？你已经对这个指数增长曲线深有研究。可以估一个大概吗？

DARIO AMODEI：我觉得 A.S.L. 3 可能在今年或明年就会发生，A.S.L. 4 可能在 2025 到 2028 年间。

EZRA KLEIN：天啊。

DARIO AMODEI：对，我真的相信指数增长。我并不是在说半个世纪以后的事，而是可能在不远的将来。现在不是时候，但这并不意味着要等到我年老色衰。我认为这会是一个短期内可能发生的事情，虽然我也可能会错。

EZRA KLEIN：但如果你这么想，你就会发现，就像我们之前讨论的那样，人工智能社会影响的跳变，尽管能力的增长是指数级的，但偶尔也会出现一些标志性事件，如 ChatGPT、Midjourney 的照片功能。这些突发事件使许多人真正感受到了 AI 的威力，他们开始实际使用、投资这些技术。

你描述的政治经济结构听起来是这样的：可能是生物武器或网络攻击武器的威力被证明，这让政府感到惊慌，或者说，可能会发生其他事件，对吧？以第一次和第二次世界大战为例，并不让人感到安心，因为在那些时候，只有经历了一场真正的世界大战，工业才能被政府所控制。这个过程不是那么简单的。

冠状病毒可能是另一个例子，那是一场足够严重的全球灾难，让企业、政府和普通人做出了你想象不到的反应。但这些例子中通常伴随着可怕的后果 —— 无数的生命丧失。

我并不是说人工智能的情况也一定如此，但这看起来的确是一种政治经济现象。你现在可能无法完全想象，就像你无法预见 ChatGPT 出现前后的世界变化一样，但某些事件确实可能改变一切。这种变化就像是处处都出现了突变。

DARIO AMODEI：是的，我比较乐观的看法是，危险可以以一种具体而确信的方式展示出来，而不必真的发生坏事，对吧？我认为通过灾难来学习是最糟糕的方式。我每天都在希望这样的事不会发生，并且我们能够无痛地获得教训。

EZRA KLEIN：我们已经讨论了理论的极限和可能性，但在结束前，我想让我们再次关注一下物理现实。如果你使用的是人工智能，你可能会觉得它只是一些数字和代码，存在于云端。

但实际上，它由大量的芯片、数据中心和大量的能源组成，这些都依靠着复杂的供应链支持。如果中国和台湾之间发生了什么，这些芯片的制造者可能就无法继续生产或者被迫停产，你如何看待这种情况下的计算能力的必要性？展望未来五年，供应链将如何变化，需要做哪些调整？现在的系统有哪些潜在的弱点？

DARIO AMODEI（达里奥·阿莫迪）：是的，我认为台湾的军事保卫问题可能会成为我们时代最大的地缘政治议题。这些都远超出我的职责范围。对于人工智能 (Artificial Intelligence, A.I.) 的影响，我的看法是这将带来极大的挑战。例如，我们已经构建了这些强大的模型，但真正的问题是：

我们有足够的资源来建造它们吗？

我们如何控制这些资源？这关系到安全问题及地缘政治的平衡。

如果用这些芯片建数据中心，这些中心会设在哪里？美国、其盟友国家、中东还是中国？

这些问题的答案将深刻影响未来，因此供应链的稳定性及相关的政治和军事决策显得尤为重要。作为一个支持民主的美国公民，我希望我们能在美国及其民主盟友国家建立数据中心，确保有充足的芯片供应。

EZRA KLEIN（埃兹拉·克莱恩）：你应该对此有所了解，毕竟你也是这个市场的一份子。回想五年前，芯片制造商并未预见到需求的激增。Nvidia 股价的飙升和其未来预期相比，显示出市场的极大期待。《金融时报》的拉娜·弗鲁哈尔引用市场分析指出，Nvidia 的股息需要 4500 年才能抵偿其现价，这反映了市场对其短期盈利潜力的高度预期。

你现在可能正忙于下一代 Claude 的开发，需要大量芯片支持。与亚马逊的合作是否顺利？你有没有感觉到计算资源的紧张？

DARIO AMODEI：我们已经获得了今年所需的计算资源（compute），我预计明年也同样充足。但我认为到了 2026, 2027, 2028 年，所需的计算资源将达到半导体行业难以承受的水平。目前半导体行业主要生产的是 CPU，即笔记本电脑中的处理器，而不是用于训练 AI 模型的数据中心服务器。但随着 AI 模型带来的经济价值不断攀升，这一情况将发生转变。

但事实是，资源的增长或转变总有极限。因此，我预见未来几年内，可能会出现数据中心、芯片及其能源供应方面的严重短缺，这既是挑战也是机遇。这提供了一个反思如何管理这些技术的良机。

同时，这也是民主体制展示领导力的机会。如果技术领域和关键资源掌握在威权国家手中，那将非常危险。AI 与威权主义的结合，在国际及国内层面上都是我深感忧虑的问题。

EZRA KLEIN：能源问题怎么说呢？我们知道，这将消耗巨额的能源。就像给世界能源系统增加一个孟加拉大小的负担。具体到 2028 年，数字还不确定。

微软已经在全球范围内每三天就开设一家新的数据中心。据《金融时报》报道，美国预计在 2024 到 2025 年间建立 20 座新的燃气发电站。现在已经有人认为，由于天然气资源丰富，我们正迎来一个新的天然气黄金时代。新建电力设施将是管理这些庞大数据和计算需求的关键。

首先，我认为这里有两个问题：一个是如何以合理的价格获取你所需要的能源，另一个是更为道德和概念性的问题，我们确实面临着全球变暖的严峻挑战，同时我们的能源使用也极为庞大。此外，在新的 AI 竞赛中，我们的能源需求似乎正以惊人的速度增长。

DARIO AMODEI：这主要取决于模型的具体使用场景。拿加密货币来说，我并不认为挖掘比特币所消耗的能量有任何附加价值，这种能量在之前是不存在的。我认为它并没有创造出任何实际价值。

但 AI 的情况则不同。可能 AI 让太阳能发电更高效，或许它能解决控制核聚变的问题，或者使地理工程更稳定和可行。但这不意味着我们必须永远依赖它。有些情况下，AI 能做一些过去由计算机自动完成的工作，而且更快、更省时，这无疑是一大进步。这样的例子还有不少。

也有情况是虽然使用了同样甚至更多的计算资源，但能够完成更有价值的工作，从而在其他地方节省了人力。还有些工作以前是人工完成的，现在可以由 AI 来执行。比如说，一些原本需要我亲自到办公室的任务，现在我可以在家中通过 AI 完成，这样就不需要开车去办公室，也节省了燃料。

因此，关于这一点的能源核算非常复杂，涉及到比较它与人类消费的食物及其能源成本等因素。

总的来说，我们还没有完全弄清楚哪部分能源使用是必要的，哪部分则可能有改进的余地。这在很多方面都与经济发展必然伴随的能源消耗增加的问题相似。

因此，我认为关键在于如何使用这项技术。简单来说，我们可以通过碳抵消来解决短期的问题，但更重要的是要从宏观角度来探讨这个问题。

EZRA KLEIN：但是换个角度来看，我认为当我们讨论国内生产总值（G.D.P.）增长的必要性时，情况并不总是如此单纯。正如常言所说，现在全球变暖的主要挑战来源于中国和印度等国的富裕化。我们期望他们变得更富有，因为对全球贫困人口来说，摆脱贫困是一个重要的道德责任。这可能意味着他们会消耗更多能源，我们需要找到可行的解决方案，因为我们还没有不增加能源消耗的办法。

加入人工智能 (A.I.) 并不仅仅是带来一系列新问题，实际上我们已经在挑战能源使用的安全极限，甚至可能已经超出。现在，如果我们考虑加入人工智能的因素，那么富国可能实现的能源效率提升就可能被抵消掉。我们希望通过人工智能未来可能帮助我们找到稳定核聚变等技术的方法，虽然这些只是理论上的设想。

同时，短期内能源使用增加所带来的问题是实际存在的，能源价格上涨也同样是一个问题。这一切对于诸如微软、亚马逊这样设定了众多可再生能源目标的公司来说，尤其复杂。如果这些目标与市场激励相冲突，公司似乎更倾向于追求市场激励，而忽视了综合结果。

DARIO AMODEI：是的，我同意这些担忧是有根据的。我想稍作反驳：并不是所有好处都只存在于未来。就像我之前说的，现在也可能有节能的应用场景，或者通过提高某些产品或服务的需求来间接节能。

目前对人工智能应用的评估还不够全面，因为这些应用还非常新，我们还不能确定哪些因素会起主导作用，或者这将如何影响经济。但我们不应该假设所有的坏处都在当前，好处全在未来。这是我想强调的主要观点。

EZRA KLEIN：我可以想象一个世界，我们在这个世界中特别鼓励 AI 的使用，使其服务于社会的目标，比如大力发展药物研究，或是改善远程工作环境，或者其他各种公共福利项目。

但现实似乎是，我们不断构建更强大的模型，却只是在一般的服务条款下推出这些模型，让人们在不进行政治操纵或制造生物武器的前提下自由使用。你可以尝试用它来编写新故事，询问关于个人生活的问题，甚至开发视频游戏。随着时间的推移，Sora 这样的产品也将问世，你还可以用它来制作视频。这一切的能源消耗都非常大。

我并不是说我已经有了一个完善的计划来将 AI 应用于社会利益，事实上，这种尝试可能完全失败。但这确实说明，长时间以来，我们可以设想你所描述的那样一个世界，但这需要系统的规划，而目前似乎没有人真正投入到这样的规划中，也没有人真的希望参与。

DARIO AMODEI：不是每个人都对‘社会善良'有相同的看法。对一些人来说，这可能意味着某种特定的理念。我们在处理一些 Gemini 相关项目时也观察到了这一点。

EZRA KLEIN：是的。

DARIO AMODEI：但是公司可以尝试自行开发对社会有益的应用。这就是我们为什么要与癌症研究所合作，以及我们期望与非洲的教育部门合作的原因。我们希望建立合作关系，通过积极的方式在教育领域使用这些模型，而不是仅仅按默认方式使用。我认为公司和个人都可以采取措施，通过这些措施，我们可以将技术应用于公共利益。

尽管如此，我们的活动永远不可能全部符合公共利益。所以，如何设置社会激励措施，而不是从上而下地定义什么是公共善良或强加意识形态，这是一个值得思考的问题。

我也没有一个一劳永逸的答案。我只能从 Anthropic 正在尝试的角度来考虑这个问题。

EZRA KLEIN：但我们还需要考虑训练数据和涉及 Claude、GPT、Gemini 这类系统的知识产权问题。目前有多起版权诉讼，你和 OpenAI 都不例外，我觉得这是行业普遍的情况。

这些系统似乎是基于很多人的集体智慧构建的。就像 Claude 能精准地模仿我的写作风格，它在某种程度上是通过学习我的文章来实现的，它确实很好地掌握了我的写作习惯。你做得很好，但对此你并没有支付我稿酬。这可能是整个行业面临的一个重大法律风险。比如说，如果你们真的需要对这些原创内容的创作者进行经济补偿怎么办？你们准备好了吗？

我知道你可能不能直接评论这些诉讼，但你肯定深思熟虑过这个问题。我很想知道你是如何评估这一风险的，以及你的道德观是什么。例如，那些设计这些系统的人不仅获得了巨大的权力，也积累了大量财富，那么那些辛苦付出的创作者呢？他们的劳动使得这些系统可以创造出千万种风格的图像。

这些风格是有人创造的。我们对于这种智慧贡献，我们应该承担什么样的责任？不仅是对公共领域的贡献，更重要的是对那些劳动者的经济权益的保护？

DARIO AMODEI：我认为大家都认同，这些模型不应该简单地复制和传播有版权的内容。对于网上公开的材料，我们认为，训练过程不仅仅是重复信息的简单复制。这一过程更类似于人通过经验学习的方式。我们认为这样的处理已经足够改造原有内容，应该能得到法律的认可，符合「合理使用」的标准。

但这些观点过于局限于法律的视角。我们其实面临一个更为广泛的问题：无论其训练方式如何，我们正在开发的通用认知系统将引发社会变革。这种变革可能不直接以替代人类的形式出现，但肯定会重塑经济运作的模式及重视的技能。对这一宏观经济问题，我们确实需要寻找答案。

虽然我重申了之前的法律观点，但我们不应忽视存在的更大问题。解决方案有很多，例如最简单的保障基本收入可能并未触及问题的核心，但它提出了一种可能。

更深层次的问题在于，随着 A.I. 系统在认知劳动中的应用范围不断扩大，我们的社会经济结构应如何调整？人们将如何在新的经济形态中找到工作和生活的意义？

正如我们从农业社会向工业社会转变，工作的含义已经发生了变化。在这一过程中，人们不再局限于农场劳动，而是寻求新的经济组织方式。我认为，对当前经济中断的唯一合理反应就是探索新的经济结构，这种结构在初期可能不明显，但将随时间不断发展。我们需要找到一种方式，不仅为人们提供生活的意义，而且能够在人道的基础上，最大限度地发挥人的创造力和潜力。

对于这些问题，我也没有确切的答案，我无法提供具体的解决方案，但我们必须努力找到解决的方法。

EZRA KLEIN：我认为，我们需要找到一个平衡点，既不是仅仅依靠法律手段，也不是完全重构社会结构，虽然这在未来几十年可能成为现实。在这两者之间，我们还需要回答更具体的问题。例如，现在很多人正在尝试利用这些系统来开发搜索工具，例如，ChatGPT 将通过 Bing 来帮助你搜索信息。

这说明人们不再通过必应 (Bing) 访问 ChatGPT 拉取信息的网站，不会给这些网站带来可以转化为少许收入的广告点击，也不会因为在这些网站上的良好体验而更可能订阅其背后的运营者。

这种情况在一定程度上是对那些提供信息的创作者的不公平。实际上，无论是处理困惑性 (perplexity) 还是其他我所观察到的众多情况，我们看到的人工智能经常在不支付任何费用的情况下，使用人们付出实际代价生成的大量数据。它们不仅未向这些数据的创作者支付费用，而且还破坏了原本可能存在的直接关系。

从长远来看，这也可能导致训练数据的问题。如果高质量信息的创建变得不再可行，比如新闻报道等，那么所有企业获得新鲜、高质、持续更新的信息的能力也会受到影响。这里既涉及道德问题，也关系到企业的自身利益。

DARIO AMODEI：对，因此我认为可能存在对所有人都有利的商业模式。这不仅是因为法律上允许在公开数据基础上进行训练，更因为某些商业模式能更好地传递价值。例如，虽然一些报纸的档案并不完全公开，但通过与这些报纸的互动，可能提供更好的产品和体验。

通过允许用户与内容互动并指出内容中的特定部分，每次访问这些内容时都能建立与内容创作者的商业关系，这能够提供更好的用户体验。在这里，有些商业模式可以有效地增值。提到大语言模型 (LLM) 使用搜索产品，确实，这种方式可能绕开了广告，但我们完全可以探索不同的合作模式。

用户完全可以直接支付搜索 API 的费用，而不是通过广告来支付这笔费用，并且这种支付方式还可以扩展到最初对内容创作者进行赔偿的机制中。这样一来，只要有价值产生，资金就能够流动。

EZRA KLEIN：在结束本次访谈之前，我想问问您如何在您认为我们所处的快速变化的环境中安排生活。您有孩子吗？

DARIO AMODEI：我已婚，还没有孩子。

EZRA KLEIN：我有两个孩子，一个两岁，一个五岁。特别是在撰写关于 A.I. 的报道时，我常常会在夜里反思，我应该怎么做？我想要为他们预备一个怎样的未来？在那个未来世界里，需要些什么新的元素，这些和现在的世界有何不同？我确信，尽管只是可能，你说的都可能是真的。这意味着，对他们而言，生活将完全不同。

我知道你的公司里也有人在思考这个问题，他们有孩子。你是怎样考虑这些的？比如，如果你有孩子，这些变化会如何影响你对育儿的看法？

DARIO AMODEI：简单来说，我不确定，也没有确切的答案，但无论如何我们都需要尝试。人们需要抚养孩子，并尽他们所能地做得好。一个基本建议是，尽可能地了解技术及其工作原理。例如，我与系统对话，系统代我行动，对这一过程熟悉至关重要。

至于孩子们在学校应该学什么，将来可能从事哪些职业，我实在是无法确定。可以认为，学习 STEM、编程和 A.I. 是重要的。但是，A.I. 的影响也可能首先体现在这些领域。

EZRA KLEIN：可能是最先受影响的。

DARIO AMODEI：对，可能是最先的。

EZRA KLEIN：比起其他领域，它在编程方面似乎更有天赋。

DARIO AMODEI：我不相信任何一个系统能完全模仿人类的行为方式。我不是这么看的。但我认为它们可能会一个接一个地根本改变各个行业和职业，而这些变化很难预料。因此，我这里只能说一些老生常谈：学会使用这项技术。教育你的孩子要有应变能力，做好迎接快速变化的世界的准备。我希望能有更好的答案，但这已是我所能想到的最好的建议了。

EZRA KLEIN：我同意这并非好答案。[笑] 让我换个角度再问一次，因为你提到要熟悉这项技术。我与这技术相处的时间越长，就越感到不安。我观察到，当人们开始使用人工智能时，技术首先自动化了创作初期的一些步骤。

比如，本来你需要自己阅读困难材料的那一步，人工智能能帮你摘要；原本你需要坐着面对空白页发思的那一步，人工智能能帮你草拟一个开头。后面的工作，你还得自己检查，确保它做了你想要的，并且要做事实检验。但我认为，人类在思考上所表现出的优势，很大一部分就在这些步骤里。

我年纪较大并且自律，也许这只是我对过去方式的坚持。你或许会问，为什么还要用计算器？但我真正的担忧是，我不确定是否应该让他们大量使用人工智能，或者尽量少用。

这对我而言，确实是一个重大的选择问题。我是希望我的孩子们学会使用人工智能，还是希望在一个他们需要频繁使用的环境下成长，或者，我是不是应该尽可能保护他们，让他们更多地学会自己静静地读书或自行撰写初稿？我也在寻找答案，不知道你有何看法？

DARIO AMODEI：我觉得这也是 AI 与社会互动复杂性的一个体现：有时候我们很难分辨 AI 到底是在帮我们减轻重复性劳动，还是在介入更有趣的活动部分。我发现，经常有一些技术产品或系统，你原以为它们只是执行你的核心任务，但实际上，这些任务包含的内容远比你想象的要丰富，功能也更多。

就好比过去，我需要自己问路。现在有了谷歌地图 (Google Maps)，我开始担心自己是否过于依赖它？是否忘记了观察周围环境？但我后来发现，我仍然需要对城市及其环境有所了解，只是这些知识被转移到了大脑的其他区域处理。

我内心有些疑问 —— 虽然不确定。在 Anthropic，我负责撰写战略规划文档或进行一些新的思考，这些可能是其他人未曾涉及的方向。我偶尔会利用公司的内部模型来辅助这一工作。从我的经验来看，这些模型在某些方面确实可以帮助概念化思维，但它们并不擅长生成初始想法。我已经找到了一个不使用它们的工作流程，因为在这方面它们帮助不大，但在如何表达和完善想法上，它们却可以提供帮助。

或许这听起来有点乐观，但你总会找到一种工作流程，使这些工具能够辅助你。如果这种合作不是自然发生的，它最终也会实现。再次强调，如果这些系统变得足够通用和强大，我们可能需要重新考虑我们的策略。但至少从我个人的短期经验来看，我总是能找到这样的方法。这也许看起来太过乐观了。

EZRA KLEIN：我认为这是一个结束本次对话的好时机。毕竟，技术的发展像是一条永不停息的指数曲线。最后一个问题 —— 你会向听众推荐哪三本书？

DARIO AMODEI：所以，是的，我准备了三个推荐。这些推荐都与当前话题相关，虽然有些是间接关联的。第一个很容易识别 —— 一本非常厚的书，《原子弹的制造过程》（Richard Rhodes），这本书展示了技术如何被迅速发展并带来广泛的影响。通过回顾各个角色的反应，我们可以看到那些原本是科学家的人是如何逐渐认识到这项技术的重大意义，以及这技术如何引导他们步入一个全新的世界。

我的第二个推荐是科幻系列《星际迷航》。最开始我是看的电视剧，后来把书也读了一遍。这个系列构建了一个高度发展的宇宙，在这里人类的寿命更长，已经拓展到了外太空。尽管如此，我们仍然面临地缘政治的老问题，以及各种不平等和剥削现象，有时这些问题甚至更加严重。

这是书的背景。书的核心是一个全新的技术发明的出现及其带来的反响 —— 各国政府、普通人民以及不同政治派别对此的反应。当年读这些时，我意识到了许多相似之处。

我的第三个推荐是《八月的枪声》，这是一本介绍第一次世界大战爆发原因的历史书。书中主要讲述了危机如何迅速爆发，而且几乎没人能够真正了解全貌。人为的误判频频出现，我们必须学会在关键时刻暂停思考，作出更明智的选择。据说，肯尼迪在面临古巴导弹危机前曾阅读这本书，我希望当今的政策制定者也能有同样的思考，因为相似的危机可能正向我们逼近。

EZRA KLEIN：Dario Amodei，非常感谢你的分享。

DARIO AMODEI：感谢您的邀请。

[音乐响起]

EZRA KLEIN：本期的《Ezra Klein Show》由 Rollin Hu 制作。事实核查工作由 Michelle Harris 完成。我们的资深工程师是 Jeff Geld，资深编辑是 Claire Gordon。节目的制作团队还包括 Annie Galvin、Kristin Lin 和 Aman Sahota。原创音乐出自 Isaac Jones 之手。受众策略由 Kristina Samulewski 和 Shannon Busta 制定。《纽约时报》观点版音频的执行制片人是 Annie-Rose Strasser。对 Sonia Herrero 表示特别感谢。