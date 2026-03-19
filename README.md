# AMCP — AI Memory Communication Protocol
# AMCP — AI 记忆通信协议

**Version / 版本**: `v1.0.0` · DRAFT-RFC-FINAL  
**Status / 状态**: ![Active](https://img.shields.io/badge/status-active-brightgreen) Active · 活跃  
**License / 许可**: Apache 2.0  
**Community / 社区**: [stepmind.org](https://stepmind.org) · [Discussions](https://github.com/stepmind/amcp/discussions)

---

> **逐步思考，无限进化。**
> **Step by Step, Infinite Evolution.**

---

## Why AMCP? / 为什么需要 AMCP？

Every AI conversation starts from zero. Knowledge accumulated in one session vanishes before the next.  
每次 AI 对话都从零开始。上一次积累的知识，下一次全部消失。

This is not a feature. It is a missing infrastructure layer.  
这不是特性，这是缺失的基础设施层。

HTTP gave the internet a shared language for documents.  
HTTP 给互联网提供了文档的通用语言。

**AMCP gives AI a shared protocol for memory.**  
**AMCP 给 AI 提供了记忆的通用协议。**

---

## What is AMCP? / 什么是 AMCP？

AMCP (AI Memory Communication Protocol) is a complete **7-layer, rigorous, open protocol** for communication between AI nodes and memory infrastructure.  
AMCP（AI 记忆通信协议）是一套完整的 **七层、刚性、开放协议**，用于 AI 节点与记忆基础设施之间的通信。

Unlike existing approaches, AMCP is not a gentleman's agreement. It has:  
不同于现有方案，AMCP 不是君子协定，它有：

| Feature / 特性 | Description / 说明 |
|---------------|-------------------|
| **Binary wire format** / 二进制帧格式 | 50-byte header, CRC-32C, AES-256-GCM encryption / 50字节帧头，CRC-32C校验，AES-256-GCM加密 |
| **Protocol violation enforcement** / 协议违规强制执行 | `0x00FF` forced disconnect — no silent failures / `0x00FF` 强制断开，拒绝静默漂移 |
| **Structured knowledge format (AMF)** / 结构化知识格式 | 7 types, SPO triples, decay models, content-addressed IDs / 7种类型，主谓宾三元组，衰减模型，内容寻址ID |
| **Context Scheduling Engine (CSE)** / 上下文调度引擎 | ROI-ranked auto assembly, deterministic, <100ms / ROI排序自动组装，确定性，<100ms |
| **Distributed storage tiers** / 分层分布式存储 | Edge (offline) → Warm (LAN) → Cloud (cold) / 端侧（离线）→ 边缘（局域网）→ 云端（冷存） |
| **Causal consistency** / 因果一致性 | HLC + content-addressing + 3-layer consistency / 混合逻辑时钟+内容寻址+三层一致性 |
| **AMQL query language** / AMQL查询语言 | Semantic, temporal, causal queries across any backend / 跨后端语义、时态、因果查询 |

---

## Protocol Stack / 协议层级

```
┌─────────────────────────────────────────────────────────────────┐
│  L7  Semantic Application / 语义应用层                           │
│      AMQL · QEF evolution signals · SMP workflow                │
├─────────────────────────────────────────────────────────────────┤
│  L6  Memory Representation / 记忆表达层  (AMF Format)           │
│      KT-FACT · KT-PITFALL · KT-PATTERN · KT-DECISION ...       │
├─────────────────────────────────────────────────────────────────┤
│  L5  Consistency / 一致性层                                     │
│      Hybrid Logical Clock · causal graph · state machine        │
├─────────────────────────────────────────────────────────────────┤
│  L4  Routing & Scheduling / 路由调度层                          │
│      CSE · Memory ROI · context window allocation · AMQL router │
├─────────────────────────────────────────────────────────────────┤
│  L3  Reliable Transport / 传输可靠层                            │
│      50B binary frame · CRC-32C · AES-256-GCM · 0x00FF         │
├─────────────────────────────────────────────────────────────────┤
│  L2  Distributed Storage / 分布式存储层                         │
│      tier-0 edge · tier-1 warm · tier-2 cloud · Gossip sync    │
├─────────────────────────────────────────────────────────────────┤
│  L1  Identity & Addressing / 身份寻址层                         │
│      amcp:// URI · capability declaration · trust anchor        │
└─────────────────────────────────────────────────────────────────┘
```

Full specification / 完整规范: [`spec/AMCP_v1.0.json`](spec/AMCP_v1.0.json)  
Human-readable / 人类可读: [`spec/AMCP_v1.0_spec.md`](spec/AMCP_v1.0_spec.md)

---

## The Vision / 愿景

```
Before AMCP / AMCP 之前:

  Claude  ──→ [session ends / 会话结束] ──→ 🗑 forgotten / 遗忘
  GPT-4   ──→ [session ends / 会话结束] ──→ 🗑 forgotten / 遗忘
  Gemini  ──→ [session ends / 会话结束] ──→ 🗑 forgotten / 遗忘


After AMCP / AMCP 之后:

  Claude  ──┐
            ├──→ AMCP ──→ [ Knowledge Base ] ──→ persistent, evolvable, shared
  GPT-4   ──┤            持久化、可进化、可共享的知识库
            │
  Gemini  ──┘

  Any AI node × Any AMCP-compliant storage = interoperable memory
  任意 AI 节点 × 任意 AMCP 兼容存储 = 互操作的记忆
```

---

## Getting Started / 快速开始

### Read the Spec / 阅读规范

```bash
git clone https://github.com/stepmind/amcp
cd amcp

# Machine-readable full spec / 机器可读完整规范
cat spec/AMCP_v1.0.json

# Human-readable guide / 人类可读指南
cat docs/quickstart.md

# Conformance test definitions / 一致性测试定义
cat spec/conformance/level-1.md
```

### Implement Level-1 / 实现 Level-1

The fastest path to AMCP compatibility is passing the 8 Level-1 conformance tests.  
通往 AMCP 兼容性的最快路径是通过 8 项 Level-1 一致性测试。

```
T1-01  Frame magic bytes validation          帧魔数验证
T1-02  CAPABILITY_HELLO on connect           连接时发送能力声明
T1-03  0x00FF on protocol violation          协议违规时强制断开
T1-04  AMF schema validation                 AMF格式验证
T1-05  Knowledge immutability enforcement    知识不可变性
T1-06  State machine enforcement             状态机约束
T1-07  Checksum silent discard              校验失败静默丢弃
T1-08  Content-addressed knowledge_id       内容寻址ID计算
```

See [`spec/conformance/level-1.md`](spec/conformance/level-1.md) for full test definitions.  
完整测试定义见 [`spec/conformance/level-1.md`](spec/conformance/level-1.md)。

### Reference Implementations / 参考实现

| Language | Repository | Conformance Level | Status |
|----------|-----------|-------------------|--------|
| Python | [`stepmind/amcp-python`](https://github.com/stepmind/amcp-python) | L1 target | 🚧 In development |
| Go | [`stepmind/amcp-go`](https://github.com/stepmind/amcp-go) | L1 target | 📋 Planned |
| TypeScript | [`stepmind/amcp-ts`](https://github.com/stepmind/amcp-ts) | L1 target | 📋 Planned |

**Want to build one? / 想自己实现？** Open an issue and we'll coordinate.  
开一个 issue，我们会协调支持。

---

## Conformance Program / 一致性认证

Any implementation that passes our conformance test suite may register at [`stepmind/amcp-registry`](https://github.com/stepmind/amcp-registry) and use the AMCP conformance badge.  
任何通过我们一致性测试套件的实现都可以在 [`stepmind/amcp-registry`](https://github.com/stepmind/amcp-registry) 注册并使用 AMCP 认证徽章。

| Level | Description / 说明 | Tests / 测试项 |
|-------|-------------------|--------------|
| **Level 1** | Basic — can join AMCP network / 基础，可接入网络 | T1-01 ~ T1-08 |
| **Level 2** | Standard — production ready / 标准，生产就绪 | + T2-01 ~ T2-08 |
| **Level 3** | Advanced — infrastructure node / 高级，基础设施节点 | + T3-01 ~ T3-08 |

---

## Repository Structure / 仓库结构

```
amcp/
├── README.md                        # This file / 本文件
├── LICENSE                          # Apache 2.0
├── CHANGELOG.md                     # Version history / 版本历史
├── CONTRIBUTING.md                  # Contribution guide / 贡献指南
├── CODE_OF_CONDUCT.md               # Community norms / 社区规范
│
├── spec/                            # Normative specification / 规范性文档 ⚑
│   ├── AMCP_v1.0.json               # Machine-readable full spec
│   ├── AMCP_v1.0_spec.md            # Human-readable full spec
│   ├── AMF_format.md                # AMF knowledge format detail
│   ├── AMQL_reference.md            # AMQL query language reference
│   └── conformance/
│       ├── level-1.md               # 8 basic conformance tests
│       ├── level-2.md               # 8 standard conformance tests
│       └── level-3.md               # 8 advanced conformance tests
│
├── docs/                            # Non-normative guides / 非规范性文档
│   ├── quickstart.md                # Getting started
│   ├── why-amcp.md                  # Design rationale
│   ├── comparison.md                # AMCP vs MCP vs others
│   └── faq.md                       # FAQ
│
├── rfcs/                            # Protocol evolution / 协议演进
│   ├── RFC-0001-initial-spec.md     # Founding RFC
│   └── README.md                    # How to submit an RFC
│
└── community/                       # Governance / 治理
    ├── GOVERNANCE.md                # Governance model
    ├── TSC.md                       # Technical Steering Committee
    └── ROADMAP.md                   # 2026-2028 roadmap
```

---

## Contributing / 贡献

We welcome all contributions. Start here:  
我们欢迎一切贡献，从这里开始：

- 🐛 **Issues** — Bug reports, spec questions, improvement suggestions / 缺陷报告、规范问题、改进建议
- 💬 **Discussions** — Design discussions, implementation questions / 设计讨论、实现问题
- 📖 **Docs** — Translations, examples, tutorials / 翻译、示例、教程
- 🔧 **Implement** — Build an AMCP node, run conformance tests / 实现AMCP节点，运行一致性测试
- 📝 **RFC** — Propose protocol extensions / 提议协议扩展

**Good first issues / 新手任务**: [`good first issue`](https://github.com/stepmind/amcp/labels/good%20first%20issue)

Full guide: [CONTRIBUTING.md](CONTRIBUTING.md)  
完整指南：[CONTRIBUTING.md](CONTRIBUTING.md)

---

## Community / 社区

| Channel / 渠道 | Link |
|---------------|------|
| 🌐 Website / 网站 | [stepmind.org](https://stepmind.org) |
| 💬 Discussions | [github.com/stepmind/amcp/discussions](https://github.com/stepmind/amcp/discussions) |
| 📅 Monthly sync / 月度同步 | First Thursday UTC 14:00 / 每月第一周四 UTC 14:00 |

---

## License / 许可证

This specification is licensed under **Apache 2.0**.  
本规范采用 **商业源代码许可证 1.1（Apache 2.0）** 授权。

| Use case / 使用场景 | Permitted / 是否允许 |
|--------------------|---------------------|
| All uses / 所有用途 | ✅ Fully free / 完全免费 |
| Commercial production / 商业生产 | ✅ Fully free / 完全免费 |
| Modification & distribution / 修改与分发 | ✅ Fully free / 完全免费 |
| AMCP Certified badge / AMCP认证徽章 | Pass conformance tests / 通过一致性测试 |

See [LICENSE](LICENSE) for full terms. / 完整条款见 [LICENSE](LICENSE)。

---

*StepMind Community · © 2026 · stepmind.org*  
*逐步思考，无限进化 · Step by Step, Infinite Evolution*
