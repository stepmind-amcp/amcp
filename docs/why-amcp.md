# Why AMCP? / 为什么是 AMCP？

A brief history of the problem and why existing solutions are insufficient.  
问题的简史，以及现有解决方案为何不够充分。

---

## The Stateless AI Problem / 无状态 AI 问题

Every AI conversation starts from zero.  
每次 AI 对话都从零开始。

This is not a coincidence. It reflects a deeper architectural reality: current AI models are **stateless functions**. They receive input, produce output, and retain nothing. The "memory" features in various chat products are workarounds — manually injected text, not a protocol.  
这不是巧合，它反映了更深层的架构现实：当前 AI 模型是**无状态函数**。它们接收输入，产生输出，不保留任何东西。各种聊天产品中的"记忆"功能是变通手段——手动注入的文本，而不是协议。

---

## Why Existing Solutions Fall Short / 现有解决方案的不足

### MCP (Model Context Protocol) / 模型上下文协议
Good: Standardizes how tools expose data to AI.  
好处：标准化了工具向 AI 暴露数据的方式。

Missing / 缺失:
- No binary wire format — "protocol violations" have no enforcement mechanism  
  没有二进制帧格式——"协议违规"没有执行机制
- No knowledge types — all context is equal, undifferentiated text  
  没有知识类型——所有上下文都是等同的、未分化的文本
- No causal consistency — no way to know if two nodes have the same knowledge  
  没有因果一致性——无法知道两个节点是否拥有相同的知识
- No distributed storage model — no concept of hot/warm/cold  
  没有分布式存储模型——没有热/暖/冷的概念

### Context window injection / 上下文窗口注入
Crams everything into the context window. No prioritization, no ROI ranking, no semantic routing.  
将所有内容塞入上下文窗口。没有优先级，没有 ROI 排序，没有语义路由。

### Vector databases / 向量数据库
Good: Semantic search over stored embeddings.  
好处：对存储的嵌入进行语义搜索。

Missing / 缺失:
- No wire protocol — every integration is custom code  
  没有线路协议——每个集成都是自定义代码
- No knowledge lifecycle — no decay, no supersession, no causality  
  没有知识生命周期——没有衰减、取代、因果关系
- No cross-AI consistency — different models embed differently  
  没有跨 AI 一致性——不同模型的嵌入方式不同

---

## AMCP's Design Decisions / AMCP 的设计决策

### Why a binary wire format? / 为什么用二进制帧格式？

Because "protocol" without enforcement is documentation.  
因为没有执行机制的"协议"只是文档。

The 50-byte AMCP frame header, with its magic bytes, CRC-32C, and `0x00FF` violation response, means protocol violations are detected and terminated at the transport layer — not discovered hours later as mysterious data corruption.  
50字节的 AMCP 帧头，含魔数、CRC-32C 和 `0x00FF` 违规响应，意味着协议违规在传输层就被检测和终止——而不是数小时后才作为神秘的数据损坏被发现。

### Why structured knowledge triples, not text? / 为什么用结构化三元组而非文本？

Because natural language is interpreted differently by different models.  
因为自然语言被不同模型的解读方式不同。

`"OKX TP/SL REQUIRES attachAlgoOrds"` as a triple is the same regardless of whether Claude, GPT-4, or Gemini reads it. As a natural language string, each model may parse the semantics differently.  
`"OKX TP/SL REQUIRES attachAlgoOrds"` 作为三元组，无论 Claude、GPT-4 还是 Gemini 读取，都是相同的。作为自然语言字符串，每个模型可能以不同方式解析其语义。

### Why content-addressed IDs? / 为什么用内容寻址ID？

Because knowledge should be globally deduplicated.  
因为知识应该在全球范围内去重。

`knowledge_id = SHA-256(content)` means the same fact discovered independently by two different AI nodes has the same ID. No central coordination needed.  
`knowledge_id = SHA-256(content)` 意味着两个不同 AI 节点独立发现的同一事实具有相同的 ID。无需中央协调。

### Why Apache 2.0 instead of Apache 2.0? / 为什么用 Apache 2.0 而非 Apache 2.0？

Because the community's work needs protection in its early years.  
因为社区的工作在早期需要保护。

Apache 2.0 is the right choice for a protocol standard. AMCP's real protection comes from three things that no license restriction can replicate: being first, owning the community, and controlling the "AMCP Certified" trademark. Any vendor can freely implement AMCP — but they cannot falsely claim official certification without passing our conformance test suite. Trademark law handles that more effectively than a commercial license restriction, without creating any friction for adopters.  
Apache 2.0 是协议标准的正确选择。AMCP 真正的护城河来自三件事，而非许可证限制：先发优势、社区归属、以及对"AMCP 官方认证"商标的控制。任何厂商都可以自由实现 AMCP——但未通过我们的一致性测试套件，就不能声称官方认证。商标法比商业许可证限制更有效地处理这个问题，同时对采用者不产生任何摩擦。

---

*StepMind Community · stepmind.org*
