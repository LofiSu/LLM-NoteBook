- https://flo.host/E6j_G5X/

1.什么是Tokenization？请比较BPE, WordPiece, 和SentencePiece的异同。

2.词嵌入 (Embedding) 是什么？它解决了什么问题？

3.Transformer为什么需要位置编码？请介绍几种你所知道的位置编码方式（如绝对位置编码、旋转位置编码RoPE）。

4.为什么LLM主要使用Layer Normalization (LN) 或 RMSNorm 而不是Batch Normalization (BN)？请解释LN和RMSNorm的原理。

5.为什么像GPT这样的模型会选择GeLU、SwiGLU等激活函数，而不是ReLU？

6.在大模型预训练和微调中，最常用的损失函数是什么？请解释其原理。

7.解释贪心搜索 (Greedy Search)、束搜索 (Beam Search)、Top-K采样和Top-P (Nucleus) 采样的原理和优缺点。

8.在文本生成中，Temperature参数的作用是什么？它如何影响生成结果的多样性？

9.解释自回归（Autoregressive）模型和自编码（Autoencoding）模型的区别，并分别举例说明（如GPT vs. BERT）。

10.什么是模型的上下文窗口 (Context Window)？它对模型能力有什么影响？

11.什么是知识蒸馏 (Knowledge Distillation)？它通常如何应用于大模型？

12.如何评估一个语言模型的好坏？请解释困惑度 (Perplexity) 的含义。

13.请详细描述Transformer的整体架构，包括Encoder和Decoder的组成部分。

14.详细解释自注意力机制 (Self-Attention) 的计算过程（Q, K, V的生成、缩放点积注意力）。它的计算复杂度是多少？

15.为什么需要多头注意力 (Multi-Head Attention)？它的“头”越多越好吗？

16.Transformer中的FFN层起什么作用？它通常由哪几层组成？

17.解释Transformer中残差连接 (Residual Connection) 和层归一化 (Layer Normalization) 的作用和位置。为什么采用Post-LN的模型训练时需要warm-up？

18.比较Encoder-Only (如BERT), Decoder-Only (如GPT), 和Encoder-Decoder (如T5) 架构的异同和适用场景。

19.简述一下GPT系列、LLaMA系列、BERT系列、ChatGLM系列模型的主要特点和演进关系。

20.LLaMA架构相比于原始Transformer做了哪些关键改动？（如RMSNorm, SwiGLU, RoPE）

21.你了解哪些Attention的变体或优化？（如FlashAttention, Multi-Query Attention, Grouped-Query Attention），它们分别解决了什么问题？

22.FlashAttention的实现原理是什么？它为什么能加速计算并节省显存？

23.MQA/GQA: Multi-Query Attention (MQA) 和 Grouped-Query Attention (GQA) 是如何工作的？它们如何优化推理效率？

24.什么是MoE (Mixture of Experts) 架构？它的工作原理、优点和挑战是什么？

25.当前主流LLM是如何处理长文本输入的？有哪些技术或架构上的解决方案？（如滑动窗口、稀疏注意力等）

26.Causal Language Modeling (CLM) 和 Masked Language Modeling (MLM) 作为预训练目标，有什么区别？

27.预训练一个大模型需要什么样的数据？如何进行数据清洗和预处理？

28.什么是增量预训练（Continual Pre-training）？它在什么场景下使用？

29.在训练大模型时，可能会遇到哪些不稳定的问题（如Loss Spikes）？有哪些常用的解决方法？

30.为什么AdamW是训练大模型时常用的优化器？它和Adam有什么区别？

31.解释数据并行 (Data Parallelism)、张量并行 (Tensor Parallelism) 和流水线并行 (Pipeline Parallelism) 的原理、优缺点及适用场景。

32.
数据并行中的通信开销主要在哪里？Ring All-reduce是如何工作的？

33.
Megatron-LM提出的张量并行是如何实现的？它如何切分Transformer中的MLP层和Attention层？

34.
GPipe和PipeDream提出的流水线并行有什么区别？如何解决流水线气泡（Pipeline Bubble）问题？

35.
谈谈你对ZeRO (Zero Redundancy Optimizer) 的理解，它分为哪几个阶段？分别优化了什么？

36.
如何将数据并行、张量并行和流水线并行结合起来进行3D并行训练？

37.
什么是混合精度训练（Mixed Precision Training）？它的原理和好处是什么？

38.
梯度累积（Gradient Accumulation）是什么？它有什么作用？

39.
什么是Activation Checkpointing (或Gradient Checkpointing)？它如何节省显存？

40.
什么是全量微调 (Full Fine-Tuning)？它有什么优缺点？

41.
什么是参数高效微调 (Parameter-Efficient Fine-Tuning, PEFT)？它为什么有效？

42.
详细解释LoRA (Low-Rank Adaptation) 的原理。它的关键超参数r (rank) 和 alpha 分别代表什么？

43.
你了解哪些LoRA的变体，比如QLoRA？QLoRA是如何在消费级GPU上微调大模型的？

44.
除了LoRA，还了解哪些其他的PEFT方法？（如Adapter, Prefix-Tuning, P-Tuning, Prompt Tuning）

45.
什么是监督微调 (Supervised Fine-Tuning, SFT)？它的目的是什么？如何构建SFT所需的数据集？

46.
指令微调 (Instruction Tuning) 和标准SFT有什么区别？它对模型能力有什么提升？

47.
请详细描述RLHF (Reinforcement Learning from Human Feedback) 的完整流程（三个阶段）。

48.
在RLHF中，奖励模型 (RM) 是如何训练的？它的输入和输出是什么？

49.
训练奖励模型需要什么样的人类偏好数据？通常如何收集？

50.
为什么RLHF通常使用PPO (Proximal Policy Optimization) 算法？请解释PPO loss中的KL散度惩罚项的作用。

51.
RLHF在实践中存在哪些挑战？（如奖励设计、模式崩溃、对齐税等）

52.
什么是奖励作弊 (Reward Hacking)？在RLHF中如何缓解这个问题？

53.
什么是DPO (Direct Preference Optimization)？它相比RLHF有什么优势？

54.
什么是模型对齐 (Alignment)？为什么它对现代LLM如此重要？我们希望模型在哪些方面与人类对齐？

55.
什么是Prompt Engineering？它和微调有什么关系？

56.
大模型推理为什么慢？主要的瓶颈在哪里（访存 or 计算）？

57.
解释KV Cache在自回归模型推理中的作用原理。它对显存占用有什么影响？

58.
你了解哪些主流的大模型推理加速框架？（如vLLM, FasterTransformer, TensorRT-LLM）

59.
vLLM中的PagedAttention机制是如何工作的？它解决了KV Cache的什么问题？

60.
什么是模型量化 (Quantization)？它为什么能加速推理并减少显存占用？

61.
介绍几种常见的量化方法（如PTQ, QAT, GPTQ, AWQ）。

62.
什么是投机解码 (Speculative Decoding)？它的基本原理是什么？

63.
评估生成式任务时，BLEU和ROUGE指标有什么区别和局限性？

64.
什么是大模型的幻觉 (Hallucination)？它的成因可能是什么？

65.
如何检测和缓解模型的幻觉问题？

66.
如何解决大模型在生成长文本时出现的“复读机”问题？

67.
你知道哪些常用的大模型能力评估基准 (Benchmark)？（如MMLU, HELM, MT-Bench）

68.
部署一个LLM服务时，需要考虑哪些工程问题？（如吞吐量、延迟、并发）

69.
在LLM推理服务中，动态批处理（Dynamic Batching）或连续批处理（Continuous Batching）是如何提升吞吐量的？

70.
你了解哪些用于部署LLM服务的开源框架？（如TGI, Triton Inference Server）

71.
什么是检索增强生成 (Retrieval-Augmented Generation, RAG)？它的完整流程是怎样的？

72.
RAG和微调有什么区别？在什么场景下应该选择RAG，什么场景下选择微调？

73.
如何优化一个RAG系统？（如优化检索、优化生成、Chunk策略、重排等）

74.
什么是AI Agent？它和传统的LLM应用有什么区别？

75.
请描述一个典型的Agent架构，比如ReAct (Reason + Act) 是如何工作的？

76.
Agent是如何学习使用外部工具的？

77.
什么是多模态大模型？请简述其常见的技术架构。

78.
在多模态模型中，如何实现不同模态（如图像和文本）的特征对齐？

79.
什么是思维链 (Chain-of-Thought)？它如何提升LLM的推理能力？

80.
解释Self-Consistency如何与CoT结合，进一步提升模型性能。

81.
在开发和部署大模型时，需要考虑哪些安全和伦理问题？（如偏见、隐私、滥用）

82.
什么是红队测试 (Red Teaming)？它在确保模型安全中的作用是什么？

83.
你认为大模型未来的发展方向是什么？

84.
你如何理解大模型的Scaling Law？它对未来的模型发展有何启示？

85.
你认为未来是“一堆小模型”的组合还是“一个超大模型”更具前景？为什么？

86.
你最关注的开源大模型项目是什么？它的技术特点和社区生态如何？

87.
谈谈你过去项目中遇到的最困难的技术挑战，以及你是如何解决的。

88.
你是否有过复现学术论文的经历？请分享一次印象深刻的经历。

89.
如果让你从头搭建一个基于LLM的问答系统，你会如何进行技术选型？

90.
你为什么选择大模型算法这个方向？你未来的职业规划是怎样的？

91.
在扩展模型上下文窗口时，会遇到哪些核心挑战？（如计算量、显存、性能衰减）

92.
知识图谱（Knowledge Graph）如何与大模型结合？有哪些潜在的应用场景？

93.
你如何看待大模型的可解释性（Interpretability）问题？有哪些方法可以尝试去理解模型的内部工作机制？

94.
“Garbage in, garbage out.” 在大模型时代，你认为数据质量的重要性体现在哪些方面？如何构建高质量的数据集？

95.
有观点认为LLM正在向“世界模型”演进，你如何理解这个概念？

96.
如何让模型具备持续自主学习和进化的能力，而不是仅仅依赖于离线训练？

97.
请用Python/PyTorch手写一个简单的多头注意力模块。

98.
解释softmax函数的梯度是如何计算的。

99.
设计一个实验来评估两种不同Prompt策略的优劣。