## 20250209Group-Relative-Policy-Optimization-GRPO-Illustrated-Breakdown-Explanation

[Group Relative Policy Optimization (GRPO) Illustrated Breakdown & Explanation | by Ebrahim Pichka | Jan, 2025 | Towards AI](https://pub.towardsai.net/group-relative-policy-optimization-grpo-illustrated-breakdown-explanation-684e71b8a3f2)

A simplified intro to GRPO, an efficient policy optimization method used for LLM reasoning training

Ebrahim Pichka

Towards AI

Ebrahim Pichka

Jan 31, 2025

### 01. Introduction

介绍

Reinforcement Learning (RL) has emerged as a powerful tool for enhancing Large Language Models (LLMs) after their initial training, particularly in reasoning-intensive tasks. DeepSeek’s recent breakthroughs with DeepSeek-Math [2] and DeepSeek-R1 [3] models have demonstrated the remarkable potential of RL in improving mathematical reasoning and problem-solving abilities of LLMs.

强化学习（RL）已经成为增强大语言模型（LLM）的有力工具，尤其是在初始训练之后，对于推理密集型任务的提升效果显著。DeepSeek 近期发布的 DeepSeek-Math [2] 和 DeepSeek-R1 [3] 模型，充分展示了 RL 在提升 LLM 的数学推理和问题解决能力方面的巨大潜力。

These achievements were made possible through an innovative RL approach called Group Relative Policy Optimization (GRPO), which addresses the unique challenges of applying RL to language models. In this post, we’ll dive deep into how GRPO works and why it represents a significant advancement in LLM training.

这些成就得益于一种创新的强化学习（Reinforcement Learning，RL）方法 —— 组相对策略优化（Group Relative Policy Optimization，GRPO）。该方法有效应对了将强化学习应用于语言模型时遇到的特殊挑战。本文将深入探讨 GRPO 的工作原理，以及它如何成为大语言模型训练领域的重要进展。

### 02. PPO vs GRPO

Proximal Policy Optimization (PPO) [1] has been the go-to algorithm for RL fine-tuning of language models. At its core, PPO is a policy gradient method that uses clipping to limit policy updates (gradients), preventing destructive large policy changes. The objective function for PPO can be written as:

近端策略优化（Proximal Policy Optimization，PPO）[1] 是对语言模型进行强化学习微调时常用的算法。从本质上讲，PPO 是一种策略梯度方法，它通过裁剪来限制策略的更新幅度（梯度），以此避免可能造成破坏性影响的策略突变。PPO 的目标函数可以表示为：

$$
J_{PPO}(\Theta)= E[s \sim P(S), a \sim \pi_{\theta_{old}}(A \mid s)]
\min \left[ \frac{\pi_{\theta}(a \mid s)}{\pi_{\theta_{old}}(a \mid s)} A(s, a), \operatorname{clip}\left(\frac{\pi_{\theta}(a \mid s)}{\pi_{\theta_{old}}(a \mid s)}, 1-\epsilon, 1+\epsilon\right) A(s, a) \right]
$$

GRPO — first introduced in [2] — builds upon PPO’s foundation but introduces several key innovations that make it more efficient and better suited for language models:

GRPO，首次在 [2] 中提出，它以 PPO 为基础，但引入了几项关键创新，使其效率更高，更适合用于语言模型：

1 Eliminates the need for a value network, hence less memory/compute usage

无需价值网络，从而减少内存 / 计算消耗

2 Uses group sampling for more efficient stable advantage estimation

使用组采样，来实现更高效、更稳定的优势函数

3 Uses a more conservative update mechanism through further penalizing both the objective and the rewards

估计采用更保守的更新机制，通过进一步惩罚目标函数和奖励来实现

### 03. GRPO: A Closer Look

GRPO：深入解析

LLM as a Policy

大语言模型（LLM）作为策略

In GRPO, the language model serves as the policy network (actor), taking a question q as input observation s and producing a sequence of tokens as actions. The policy distribution factors across tokens:

在 GRPO 中，大语言模型充当策略网络（行动者 actor），它接收问题 q 作为输入观察 s，并生成一系列 token 作为动作。策略的分布可以分解为每个 token 的条件概率，也就是说，模型会依次预测每个 token ，从而构成完整的动作序列。

$\pi_\theta(a \mid q) = \prod_{t=1}^{N} \pi_\theta(a_t \mid q, a_{< t})$

Note: In the original paper [2], they use o_t to denote the output token at timestep t. Whereas we use a_t instead to conform with standard RL notation of action.

注意：在原始论文 [2] 中，作者使用 o_t 来表示 *t* 时刻输出的 Token。为了与强化学习中动作（action）的标准表示法保持一致，我们使用 a_t 来表示。

### 04. Sequential Token Generation

序列化 Token 生成

The generation process is inherently sequential because of auto-regressive nature of transformers/LLMs:

由于 Transformer / 大语言模型（LLM）的自回归特性，生成过程本质上是序列化的：

1 Each token is generated conditionally on previous tokens

每个 Token 的生成都依赖于之前的 Token

2 The policy network (LLM) maintains a running context

策略网络（大语言模型）维护着一个动态的上下文

3 Each token generation step can be viewed as an action a_t in the RL framework

在强化学习（RL）框架中，每个 Token 的生成步骤都可以被视为一个动作 a\_t

### 05. Reward and Advantage Calculation

奖励和优势计算

For each generated sequence, GRPO computes per-token rewards as follows:

对于每个生成的序列，GRPO 按照以下方式计算每个 Token 的奖励：

$r_{+} = r_{\phi}(s, a_{\le t}) - \beta \log \frac{\pi_{\theta}(a_t \mid s, a_{< t})}{\pi_{ref}(a_t \mid s, a_{< t})}$

Instead of using a value network, GRPO estimates baseline advantages A by normalizing a group (batch) of rewards obtained from sampling multiple different outputs from the reference policy produced in response to the same question as input:

GRPO 并没有使用价值网络，而是采用了一种不同的方法来估计基线优势 A（Advantage）。它通过对一批奖励进行归一化来实现，这些奖励是通过参考策略对同一输入问题进行多次采样，从而获得多个不同的输出。

$\hat{A}_{i,t} = \tilde{r}_i = \frac{r_i - mean(\mathbf{r})}{std(\mathbf{r})}$

The GRPO Objective

GRPO 目标

for each question 𝑞, GRPO samples a group of outputs {𝑜1, 𝑜2, · · · , 𝑜𝐺} from the old policy 𝜋𝜃𝑜𝑙𝑑 and then optimizes the policy model by maximizing the GRPO objective. The complete GRPO objective brings everything together:

对于每一个问题 𝑞，GRPO 会从旧的策略 𝜋𝜃𝑜𝑙𝑑 中采样一组输出 {𝑜1，𝑜2,···，𝑜𝐺}，然后通过最大化 GRPO 目标函数来优化策略模型。完整的 GRPO 目标函数将所有要素整合如下：

$$
J_{GRPO}(\Theta) = E[s \sim P(S), a \sim \pi_{\theta_{old}}(A \mid s)] \\
\frac{1}{G} \sum_{i=1}^{G} \left\{ \min \left[ \frac{\pi_{\theta}(a_i \mid s)}{\pi_{\theta_{old}}(a_i \mid s)} \hat{A}_i, \operatorname{clip}\left(\frac{\pi_{\theta}(a_i \mid s)}{\pi_{\theta_{old}}(a_i \mid s)}, 1-\epsilon, 1+\epsilon\right) \hat{A}_i \right] - \beta D_{KL}[\pi_\theta || \pi_{ref}] \right\}
$$

This objective:

这个目标：

1 Averages over both groups and sequence lengths

对两组数据和序列长度进行平均；

2 Uses clipping for conservative updates

采用裁剪（clipping）方法进行保守更新；

3 Includes an estimate of the KL divergence as a penalty to prevent large deviations from the reference model

引入 KL 散度（KL divergence）的估计，作为一种惩罚项，以避免与参考模型产生过大的偏差。

$$
J_{GRPO}(\Theta) = E[s \sim P(S), \{\mathbf{a}_i\}_{i=1}^G \sim \pi_{\theta_{old}}(A \mid s)] \\
\frac{1}{G} \sum_{i=1}^{G} \frac{1}{|\mathbf{a}_i|} \sum_{t=1}^{|\mathbf{a}_i|} \left\{ \min \left[ \frac{\pi_{\theta}(a_{i,t} \mid s, \mathbf{a}_{i,<t})}{\pi_{\theta_{old}}(a_{i,t} \mid s, \mathbf{a}_{i,<t})} \hat{A}_{i,t}, \operatorname{clip}\left(\frac{\pi_{\theta}(a_{i,t} \mid s, \mathbf{a}_{i,<t})}{\pi_{\theta_{old}}(a_{i,t} \mid s, \mathbf{a}_{i,<t})}, 1-\epsilon, 1+\epsilon\right) \hat{A}_{i,t} \right] - \beta D_{KL}[\pi_\theta || \pi_{ref}] \right\}
$$

=>

$$
D_{KL}[\pi_\theta || \pi_{ref}] = \frac{\pi_{ref}(a_{i,t} | q, a_{i,< t})}{\pi_\theta(a_{i,t} | q, a_{i,<t})} - \log \frac{\pi_{ref}(a_{i,t} | q, a_{i,< t})}{\pi_\theta(a_{i,t} | q, a_{i,< t})} - 1
$$

### 06. Conclusion

结论

GRPO represents a significant advancement in applying RL to language models. By eliminating the need for a value network and introducing group-relative advantage estimation, it provides a more efficient and stable training process. The success of DeepSeek-Math and DeepSeek-R1 demonstrates the practical benefits of this approach.

GRPO 代表了在将强化学习（Reinforcement Learning，RL）应用于语言模型方面的一项重大进步。它无需价值网络，并引入了组相对优势估计，从而提供了一个更高效、更稳定的训练过程。DeepSeek-Math 和 DeepSeek-R1 的成功，充分展示了这种方法在实践中的优势。

The key innovations of GRPO — group sampling, relative advantage estimation, and the elimination of the value network — provide a blueprint for future developments in LLM training. As we continue to push the boundaries of what language models can achieve, techniques like GRPO will be crucial in unlocking their full potential.

GRPO 的几项关键创新 —— 组采样（group sampling）、相对优势估计（relative advantage estimation）以及去除价值网络（elimination of the value network)—— 为大语言模型（LLM/Large Language Model）训练的未来发展方向奠定了基础。随着我们不断探索语言模型的能力边界，GRPO 这类技术将在充分挖掘其潜力方面发挥关键作用。

### References

[1] Schulman, John, et al. Proximal Policy Optimization Algorithms. arXiv:1707.06347, arXiv, 28 Aug. 2017. arXiv.org, https://doi.org/10.48550/arXiv.1707.06347.

[2] Shao, Zhihong, et al. DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models. arXiv:2402.03300, arXiv, 27 Apr. 2024. arXiv.org, https://doi.org/10.48550/arXiv.2402.03300.

[3] DeepSeek-AI, et al. DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning. arXiv:2501.12948, arXiv, 22 Jan. 2025. arXiv.org, https://doi.org/10.48550/arXiv.2501.12948.