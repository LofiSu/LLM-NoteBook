原文链接：https://arxiv.org/abs/1706.03762
论文核心贡献
1. Transformer模型
- 抛弃了传统的序列网络（RNN、LSTM、CNN），完全基于自注意力机制（Self-Attention---一个算法）
- 通过多头注意力（Multi-Head Attention）进行信息捕捉，让模型学习更多不同特征。
比如翻译 “I love you” 这个输入序列。不同的人（线性层）分别从语法结构、词汇含义、情感倾向等不同角度去分析这几个单词，然后综合这些分析结果，就能更准确地生成对应的中文 “我爱你” ，也就是在输入和输出序列之间建立了更深度的联系，提高了翻译的准确性和质量。
- 采用位置编码（Positional Encoding） 解决无序问题、序列信息丢失问题。
2. 提升并行计算能力
- RNN 需要逐步处理序列而Transformer可以并行化计算
- 主要依赖于矩阵运算（矩阵乘法和softmax计算）适合GPU/TPU加速。
3. 提升翻译任务的效果
- 论文中的实验表明，Transformer 在 WMT 2014 英法翻译任务上超越了当时的 SOTA（State-of-the-Art）模型。
Transformer 模型架构
Transformer 由 编码器（Encoder）和解码器（Decoder） 组成，每个部分由 多个相同的子层（Sub-layer）堆叠 而成：
1. Encoder（编码器）
由 N 层相同的编码单元 组成，每个单元包含：
- 多头自注意力（Multi-Head Self-Attention）
- 前馈神经网络（Feed-Forward Network, FFN）
- 残差连接（Residual Connection）+ Layer Normalization
每个 Token 经过 自注意力层，关注整个输入序列的不同部分，然后进入前馈网络，最终经过 N 层叠加 形成编码表示。
2. Decoder（解码器）
类似于编码器，但每层多了一个：
- Masked Multi-Head Attention（掩码自注意力）
  - 目的是在训练时避免模型看到未来的 Token（防止信息泄露）。
解码器的作用是利用编码器的输出 逐步生成目标序列的词语（如翻译任务中的目标语言）。
关键技术
自注意力（Self-Attention）
自注意力的核心思想是：计算输入序列中每个 Token 与其他 Token 之间的相关性，然后根据权重重新加权输入表示。
计算过程：
1. 输入转换为 Query (Q), Key (K), Value (V)：
Q=XWq K=XWk  V=XWv
2. 计算注意力分数（Attention Scores）：
[图片]
- 通过 softmax 归一化，得到注意力权重：
[图片]

多头注意力（Multi-Head Attention）
普通的自注意力可能关注的信息有限，多头注意力通过多个不同的注意力头（Head） 学习不同的表示：
[图片]
每个头独立执行自注意力，然后拼接结果。
位置编码（Positional Encoding）
由于 Transformer 没有循环结构，需要手动注入序列信息：
这样可以让模型感知到词序。
[图片]
训练细节(还没搞懂）
- 优化器：Adam + Warmup
- 损失函数：交叉熵（Cross-Entropy Loss）
- 正则化：Dropout, Label Smoothing
Transformer 与 RNN 的对比
RNN（包括LSTM和GRU）可以处理序列数据，但它有如下问题：
1. 无法并行化：RNN需要按时间同步（Time Step）逐步计算，每一步的计算依赖于前一步的隐藏状态，无法进行并行计算，导致训练速度较慢。
2. 长距离依赖问题：RNN 主要依赖隐藏状态传递信息，但随着序列变长，早期的信息会被遗忘，尤其是标准 RNN 中的梯度消失问题严重。
3. 难以捕捉远程依赖关系：LSTM 和 GRU 通过门控机制缓解了梯度消失问题，但仍然无法完全解决长距离依赖问题。

Transformer vs. RNN
暂时无法在飞书文档外展示此内容
结论：Transformer 在大多数 NLP 任务中优于 RNN，成为主流架构。

---
4. Transformer 的优化
5. 改进计算复杂度：
  - Transformer 的 自注意力计算复杂度是 O(T2)O(T^2)，对于长序列计算量较大。
  - 改进方案：Longformer、BigBird 等提出了稀疏注意力（Sparse Attention），降低计算复杂度。
6. 更高效的架构：
  - BERT：基于 Transformer 双向预训练，提高文本理解能力。
  - GPT：基于 Transformer 单向解码器，用于生成任务。

- RNN 适用于短序列任务，但训练速度慢，难以捕捉长距离信息。
- Transformer 采用自注意力机制，能够高效建模长距离依赖，并支持并行计算，大幅提高 NLP 任务的性能。
GPT & BERT 详解：Transformer 在 NLP 任务中的核心架构
Transformer 诞生后，研究者基于其编码器（Encoder） 和 解码器（Decoder） 分别发展出了两个重要的 NLP 预训练模型：
- GPT（Generative Pre-trained Transformer）：基于 Transformer 解码器（Decoder），用于生成任务（如文本生成）。
- BERT（Bidirectional Encoder Representations from Transformers）：基于 Transformer 编码器（Encoder），用于理解任务（如文本分类、问答等）。
这两个模型都采用了预训练 + 微调（Pretraining + Fine-tuning） 的方式，大幅提升了 NLP 任务的性能。

---
1. GPT（Generative Pre-trained Transformer）
GPT 是由 OpenAI 提出的生成式预训练模型，它使用 Transformer 的解码器（Decoder）结构，主要用于自然语言生成（NLG）任务。
1.1 GPT 结构
GPT 主要由多个 Transformer Decoder 层 堆叠而成，每层包含：
- Masked 自注意力层（Masked Self-Attention）
- 前馈神经网络（Feed Forward Network, FFN）
- 残差连接 + 层归一化（LayerNorm）
与原始 Transformer Decoder 的区别：
- 没有 Encoder-Decoder Attention（因为不需要编码器）
- Masked Self-Attention：确保模型只能看到过去的信息，防止“偷看”未来的词。
[图片]
1.2 GPT 的训练方式
GPT 采用 自回归（Auto-Regressive） 方式进行预训练：
- 给定一个文本序列 X = (x₁, x₂, ..., xₙ)，GPT 通过 最大化下一个单词的概率 进行训练：
- P(xt∣x1,x2,...,xt−1)P(x_t | x_1, x_2, ..., x_{t-1})
- 训练目标是 最小化负对数似然（Negative Log-Likelihood, NLL）：
- L=−∑t=1nlog⁡P(xt∣x1,x2,...,xt−1)L = - \sum_{t=1}^{n} \log P(x_t | x_1, x_2, ..., x_{t-1})
1.3 GPT 的特点
- 单向（Left-to-Right）：
  - 仅依赖于前面的单词，适合生成任务（如 ChatGPT）。
- 基于解码器（Decoder）：
  - 没有编码器，完全靠解码器 进行序列建模。
- 适用于自然语言生成（NLG）任务：
  - 文本生成（如文章写作、代码生成）。
  - 机器翻译（Auto-regressive 方式）。
  - 对话系统（如 ChatGPT）。
1.4 GPT 的演化
暂时无法在飞书文档外展示此内容

---
2. BERT（Bidirectional Encoder Representations from Transformers）
BERT 由 Google 在 2018 年提出，它基于 Transformer 编码器（Encoder），用于自然语言理解（NLU）任务。
2.1 BERT 结构
BERT 由多个 Transformer Encoder 层 组成，每层包含：
- 自注意力层（Self-Attention）
- 前馈神经网络（FFN）
- 残差连接 + 层归一化（LayerNorm）
与 GPT 最大的区别：
- BERT 采用 Transformer 编码器（Encoder），是 双向（Bidirectional） 结构。
- GPT 采用 Transformer 解码器（Decoder），是 单向（Left-to-Right） 结构。
[图片]
2.2 BERT 的训练方式
BERT 采用 自监督学习（Self-Supervised Learning） 进行预训练，使用了两种训练任务：
(1) 掩码语言模型（Masked Language Model, MLM）
- 在输入序列中，随机掩盖 15% 的词，让模型预测这些被遮挡的词：
"The [MASK] is playing in the park." → "The dog is playing in the park."
- 计算损失：
- L=−∑t∈maskedlog⁡P(xt∣x1,...,xn)L = - \sum_{t \in \text{masked}} \log P(x_t | x_1, ..., x_n)
- 优点：MLM 让 BERT 能够看到整个序列的上下文信息（双向建模）。
(2) 下一句预测（Next Sentence Prediction, NSP）
- 让模型判断两个句子是否有逻辑关系：
  - 正样本："I love books." → "Reading is my hobby."
  - 负样本："I love books." → "The sun is bright."
- 目标：预测是否为相邻句子。
注意：BERT 之后的升级版本（如 RoBERTa）发现 NSP 任务效果不佳，因此被去掉。
2.3 BERT 的特点
- 双向（Bidirectional）：
  - 能够同时看到左侧和右侧的上下文，更适合文本理解任务。
- 适用于自然语言理解（NLU）任务：
  - 句子分类（如情感分析）。
  - 句子配对（如问答任务）。
  - 词向量表示（用于下游任务）。
2.4 BERT 的演化
暂时无法在飞书文档外展示此内容

---
3. GPT vs. BERT 对比
暂时无法在飞书文档外展示此内容

---
4. 总结
- GPT 适用于 自然语言生成（NLG）任务，如 ChatGPT、文本生成等。
- BERT 适用于 自然语言理解（NLU）任务，如问答系统、情感分析等。
- 未来的发展：
  - GPT 进化为 ChatGPT（更强的对话能力）。
  - BERT 进化为 RoBERTa、T5（更强的理解能力）。
如果你想深入了解 GPT-4 或 BERT 的具体应用，欢迎继续探讨！🚀
