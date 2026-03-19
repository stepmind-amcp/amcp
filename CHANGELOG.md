# Changelog / 变更日志

All notable changes to the AMCP specification are documented here.  
所有 AMCP 规范的重要变更均记录于此。

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).  
格式遵循 [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)。

---

## [1.0.0] — 2026-03-18

### Added / 新增
- **L1 Identity & Addressing** — `amcp://` URI format, capability declaration, trust anchor hierarchy  
  身份寻址层 — `amcp://` URI格式、能力声明、信任锚点体系
- **L2 Distributed Storage** — 3-tier storage model (edge/warm/cloud), solidification rules, Gossip sync  
  分布式存储层 — 三层存储模型（端侧/边缘/云端）、固化规则、Gossip同步
- **L3 Reliable Transport** — 50-byte binary frame, CRC-32C, AES-256-GCM, `0x00FF` protocol violation  
  传输可靠层 — 50字节二进制帧、CRC-32C、AES-256-GCM、`0x00FF`协议违规处理
- **L4 Routing & Scheduling** — CSE with Memory ROI formula, AMQL query language, context window allocation  
  路由调度层 — 带记忆ROI公式的CSE、AMQL查询语言、上下文窗口分配
- **L5 Consistency** — Hybrid Logical Clock (HLC), causal graph, 3-layer consistency, session state machine  
  一致性层 — 混合逻辑时钟、因果图、三层一致性、会话状态机
- **L6 Memory Representation (AMF)** — 7 knowledge types (KT-FACT, KT-PITFALL, KT-PATTERN, KT-CONTEXT, KT-DECISION, KT-PRINCIPLE, KT-SIGNAL), SPO triples, decay models, content-addressed IDs  
  记忆表达层（AMF）— 7种知识类型、主谓宾三元组、衰减模型、内容寻址ID
- **L7 Semantic Application** — AMQL, QEF evolution signals, standard AI workflow  
  语义应用层 — AMQL、QEF量化进化信号、标准AI工作流
- **Conformance test suite v1.0** — 24 tests across 3 levels  
  一致性测试套件 v1.0 — 跨3个级别共24项测试
- **AMCP status codes** — 2xx/3xx/4xx/5xx/7xx + `0x00FF` protocol layer  
  AMCP状态码 — 2xx/3xx/4xx/5xx/7xx + `0x00FF`协议层

---

*Versions are tagged in git: `git tag v1.0.0`*  
*版本在 git 中打标签：`git tag v1.0.0`*
