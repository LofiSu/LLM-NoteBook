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
