## **GPT & BERT 详解：Transformer 在 NLP 任务中的核心架构**

Transformer 诞生后，研究者基于其**编码器（Encoder）** 和 **解码器（Decoder）** 分别发展出了两个重要的 NLP 预训练模型：
- **GPT（Generative Pre-trained Transformer）**：基于 **Transformer 解码器（Decoder）**，用于生成任务（如文本生成）。
- **BERT（Bidirectional Encoder Representations from Transformers）**：基于 **Transformer 编码器（Encoder）**，用于理解任务（如文本分类、问答等）。

这两个模型都采用了**预训练 + 微调（Pretraining + Fine-tuning）** 的方式，大幅提升了 NLP 任务的性能。

---

# **1. GPT（Generative Pre-trained Transformer）**
GPT 是由 OpenAI 提出的生成式预训练模型，它使用 **Transformer 的解码器（Decoder）结构**，主要用于**自然语言生成（NLG）任务**。

## **1.1 GPT 结构**
GPT 主要由多个 **Transformer Decoder 层** 堆叠而成，每层包含：
- **Masked 自注意力层（Masked Self-Attention）**
- **前馈神经网络（Feed Forward Network, FFN）**
- **残差连接 + 层归一化（LayerNorm）**

与原始 Transformer **Decoder** 的区别：
- **没有 Encoder-Decoder Attention**（因为不需要编码器）
- **Masked Self-Attention**：确保**模型只能看到过去的信息**，防止“偷看”未来的词。

![](https://miro.medium.com/v2/resize:fit:1400/1*FHDQAjFjZOT9yrJ-icWE-w.png)

## **1.2 GPT 的训练方式**
GPT 采用 **自回归（Auto-Regressive）** 方式进行预训练：
- 给定一个文本序列 **X = (x₁, x₂, ..., xₙ)**，GPT 通过 **最大化下一个单词的概率** 进行训练：
  \[
  P(x_t | x_1, x_2, ..., x_{t-1})
  \]
- 训练目标是 **最小化负对数似然（Negative Log-Likelihood, NLL）**：
  \[
  L = - \sum_{t=1}^{n} \log P(x_t | x_1, x_2, ..., x_{t-1})
  \]

### **1.3 GPT 的特点**
- **单向（Left-to-Right）**：
  - 仅依赖于**前面的单词**，适合生成任务（如 ChatGPT）。
- **基于解码器（Decoder）**：
  - 没有编码器，完全靠**解码器** 进行序列建模。
- **适用于自然语言生成（NLG）任务**：
  - 文本生成（如文章写作、代码生成）。
  - 机器翻译（Auto-regressive 方式）。
  - 对话系统（如 ChatGPT）。
  
### **1.4 GPT 的演化**
| **模型版本** | **参数量** | **特点** |
|-------------|----------|---------|
| **GPT-1**（2018） | 1.17 亿 | 训练在 BooksCorpus（8GB 数据）。 |
| **GPT-2**（2019） | 15 亿 | **更强的生成能力**，支持长文本生成。 |
| **GPT-3**（2020） | 1750 亿 | **Few-shot Learning**，不需要微调即可执行多种任务。 |
| **GPT-4**（2023） | 未公布 | **多模态能力**，能处理文本、图像等。 |

---

# **2. BERT（Bidirectional Encoder Representations from Transformers）**
BERT 由 Google 在 2018 年提出，它基于 **Transformer 编码器（Encoder）**，用于**自然语言理解（NLU）任务**。

## **2.1 BERT 结构**
BERT 由多个 **Transformer Encoder 层** 组成，每层包含：
- **自注意力层（Self-Attention）**
- **前馈神经网络（FFN）**
- **残差连接 + 层归一化（LayerNorm）**

与 GPT 最大的区别：
- **BERT 采用 Transformer 编码器（Encoder），是** **双向（Bidirectional）** 结构。
- **GPT 采用 Transformer 解码器（Decoder），是** **单向（Left-to-Right）** 结构。

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*U_SeyA1b4B7iLxl06CSuAg.png)

## **2.2 BERT 的训练方式**
BERT 采用 **自监督学习（Self-Supervised Learning）** 进行预训练，使用了两种训练任务：
### **(1) 掩码语言模型（Masked Language Model, MLM）**
- 在输入序列中，**随机掩盖 15% 的词**，让模型预测这些被遮挡的词：
  ```
  "The [MASK] is playing in the park." → "The dog is playing in the park."
  ```
- 计算损失：
  \[
  L = - \sum_{t \in \text{masked}} \log P(x_t | x_1, ..., x_n)
  \]
- **优点**：MLM 让 BERT **能够看到整个序列的上下文信息**（双向建模）。
  
### **(2) 下一句预测（Next Sentence Prediction, NSP）**
- 让模型判断两个句子是否有逻辑关系：
  - **正样本**："I love books." → "Reading is my hobby."
  - **负样本**："I love books." → "The sun is bright."
- **目标**：预测是否为相邻句子。

> **注意**：BERT 之后的升级版本（如 RoBERTa）发现 NSP 任务效果不佳，因此被去掉。

## **2.3 BERT 的特点**
- **双向（Bidirectional）**：
  - 能够**同时看到左侧和右侧的上下文**，更适合文本理解任务。
- **适用于自然语言理解（NLU）任务**：
  - 句子分类（如情感分析）。
  - 句子配对（如问答任务）。
  - 词向量表示（用于下游任务）。

### **2.4 BERT 的演化**
| **模型版本** | **参数量** | **特点** |
|-------------|----------|---------|
| **BERT-Base**（2018） | 1.1 亿 | 标准 12 层 Transformer Encoder。 |
| **BERT-Large**（2018） | 3.4 亿 | 更深的网络（24 层）。 |
| **RoBERTa**（2019） | 3.4 亿 | **去除 NSP 任务，增强预训练**。 |
| **ALBERT**（2019） | 3.4 亿 | **参数量更少，但效果更好**。 |
| **T5**（2020） | 110 亿 | **文本到文本（Text-to-Text）** 框架。 |

---

# **3. GPT vs. BERT 对比**
| **对比项** | **GPT（生成式）** | **BERT（理解式）** |
|-----------|----------------|----------------|
| **结构** | Transformer **解码器（Decoder）** | Transformer **编码器（Encoder）** |
| **方向性** | **单向（左到右）** | **双向（左右都看）** |
| **训练任务** | 预测下一个词（Auto-Regressive） | MLM（预测被遮挡词）+ NSP |
| **适用任务** | 生成（如文本生成、对话） | 理解（如文本分类、问答） |
| **下游任务** | GPT-3 适用于开放领域对话 | BERT 适用于分类、匹配、阅读理解 |
| **计算开销** | 训练高效，但推理慢 | 训练慢，但推理快 |

---

# **4. 总结**
- **GPT** 适用于 **自然语言生成（NLG）任务**，如 ChatGPT、文本生成等。
- **BERT** 适用于 **自然语言理解（NLU）任务**，如问答系统、情感分析等。
- **未来的发展**：
  - **GPT 进化为 ChatGPT（更强的对话能力）**。
  - **BERT 进化为 RoBERTa、T5（更强的理解能力）**。

如果你想深入了解 **GPT-4** 或 **BERT 的具体应用**，欢迎继续探讨！🚀
