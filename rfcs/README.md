# RFC Process / RFC 流程

RFCs (Requests for Comments) are the mechanism for proposing significant changes to the AMCP protocol.  
RFC（征求意见稿）是提议对 AMCP 协议进行重大变更的机制。

---

## When to Write an RFC / 何时需要 RFC

An RFC is required for: / 以下情况需要 RFC：
- Adding new protocol layers or sublayers / 添加新协议层或子层
- Changing the wire format (L3) / 修改帧格式（L3）
- Adding or modifying AMF knowledge types / 添加或修改 AMF 知识类型
- Changing AMQL syntax / 修改 AMQL 语法
- Changes to conformance test requirements / 修改一致性测试要求
- Any change affecting backward compatibility / 任何影响向后兼容性的变更

An RFC is **not** required for: / 以下情况**不需要** RFC：
- Fixing typos or grammar / 修复拼写或语法
- Adding non-normative examples / 添加非规范性示例
- Improving documentation clarity / 改进文档清晰度

---

## RFC Template / RFC 模板

```markdown
# RFC-XXXX: [Title / 标题]

**Author / 作者**: [GitHub username]
**Date / 日期**: YYYY-MM-DD
**Status / 状态**: Draft | Under Review | Accepted | Rejected | Withdrawn

## Summary / 摘要
One paragraph. / 一段话。

## Motivation / 动机
Why is this change needed? What problem does it solve?
为什么需要这个变更？它解决什么问题？

## Detailed Design / 详细设计
The meat of the RFC. Be precise.
RFC 的核心内容。要精确。

## Drawbacks / 缺点
What are the downsides?
有哪些缺点？

## Alternatives Considered / 备选方案
What else was considered and why was this chosen?
还考虑了什么？为何选择本方案？

## Compatibility / 兼容性
Is this backward-compatible? If not, what is the migration path?
是否向后兼容？如果不是，迁移路径是什么？

## Unresolved Questions / 未解决问题
What needs to be decided before this RFC can be finalized?
在此 RFC 最终确定之前还需要决定什么？
```

---

## Submission Process / 提交流程

```
1. Open a Discussion tagged [RFC Idea]
   开一个标记 [RFC Idea] 的 Discussion

2. Community feedback period: minimum 14 days
   社区反馈期：至少14天

3. Fork repo, create rfcs/RFC-XXXX-short-title.md
   Fork 仓库，创建 rfcs/RFC-XXXX-short-title.md

4. Open Pull Request
   开 Pull Request

5. TSC schedules review within 30 days
   TSC 在30天内安排审查

6. TSC votes (simple majority to accept)
   TSC 投票（简单多数通过）

7. Accepted RFCs merged; implementation tracked in issues
   接受的 RFC 合并；实现进度在 issues 中追踪
```

---

## Accepted RFCs / 已接受的 RFC

| RFC | Title / 标题 | Status / 状态 | Version / 版本 |
|-----|-------------|--------------|----------------|
| [RFC-0001](RFC-0001-initial-spec.md) | Initial AMCP Specification / 初始 AMCP 规范 | ✅ Accepted | v1.0.0 |

---

*StepMind Community · stepmind.org*
