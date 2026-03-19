# RFC-0001: Initial AMCP Specification / 初始 AMCP 规范

**Author / 作者**: StepMind Community  
**Date / 日期**: 2026-03-18  
**Status / 状态**: ✅ Accepted — Implemented in v1.0.0

---

## Summary / 摘要

This RFC defines the initial AMCP (AI Memory Communication Protocol) specification, a complete 7-layer protocol for communication between AI nodes and memory infrastructure.  
本 RFC 定义了初始 AMCP（AI 记忆通信协议）规范，这是一套完整的七层协议，用于 AI 节点与记忆基础设施之间的通信。

## Motivation / 动机

Current AI systems have no standardized protocol for persistent memory. Every session resets. Knowledge does not accumulate. This is a missing infrastructure layer, analogous to the absence of TCP/IP before the internet.  
当前 AI 系统没有持久记忆的标准化协议。每次会话都会重置，知识无法积累。这是一个缺失的基础设施层，类似于互联网出现前 TCP/IP 的缺失。

## Specification / 规范

The full specification is in [`spec/AMCP_v1.0.json`](../spec/AMCP_v1.0.json).  
完整规范见 [`spec/AMCP_v1.0.json`](../spec/AMCP_v1.0.json)。

Key design decisions: / 关键设计决策：

1. **7-layer stack** modeled after OSI, each layer independently implementable  
   **七层协议栈** 仿照 OSI 模型，每层可独立实现

2. **Binary wire format** with 50-byte header for protocol rigidity  
   **二进制帧格式** 含50字节帧头以保证协议刚性

3. **Content-addressed knowledge IDs** (SHA-256) for global deduplication  
   **内容寻址知识ID**（SHA-256）实现全局去重

4. **Apache 2.0 → Apache 2.0** license model to protect community while enabling ecosystem  
   **Apache 2.0 → Apache 2.0** 许可证模式，在保护社区的同时赋能生态

5. **AMF structured knowledge format** using SPO triples for semantic consistency across AI models  
   **AMF 结构化知识格式** 使用主谓宾三元组确保跨 AI 模型的语义一致性

## Status / 状态

Accepted and implemented as AMCP v1.0.0.  
已接受并实现为 AMCP v1.0.0。
