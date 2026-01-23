# /intent-review

> 审查和批准 Intent 章节

## 用法

```bash
/intent-review
/intent-review path/to/INTENT.md
```

## 目的

对 Intent 文档进行交互式逐章审查和批准。批准的章节成为指导 TDD Agent 的实现契约。

## 何时使用

- 创建或修改 Intent 之后
- 开始实现之前
- 准备将 Intent 移交给团队时
- 运行 `/intent-build-now` 之前

## 章节状态

| 状态 | 含义 | 图标 |
|------|------|------|
| **draft** | 进行中，未审查 | |
| **reviewed** | 已检查，可能需要修改 | `[reviewed]` |
| **locked** | 已批准，准备实现 | `[locked]` |

## 审查流程

```
┌─────────────────────────────────────────────────────────────┐
│                    审查流程                                   │
│                                                              │
│  加载 Intent ──▶ 显示章节 ──▶ 审查 ──▶ 标记状态              │
│                       │                    │                 │
│                       ▼                    ▼                 │
│                  讨论问题          draft/reviewed/locked     │
│                  提出疑问                                    │
│                       │                    │                 │
│                       └────────────────────┘                 │
│                                 │                            │
│                                 ▼                            │
│                          下一章节                            │
└─────────────────────────────────────────────────────────────┘
```

### 审查内容

1. **职责** - 范围和边界清晰吗？
2. **结构** - 图表有意义吗？
3. **API** - 签名完整且正确吗？
4. **示例** - 覆盖主要情况吗？
5. **约束** - 所有限制都记录了吗？

## 示例会话

```
> /intent-review intent/auth/INTENT.md

开始审查 intent/auth/INTENT.md

## 章节 1：职责 [draft]

### 做什么
- 通过 JWT 令牌认证用户
- 管理刷新令牌轮换
- 验证令牌签名

### 不做什么
- 用户注册（由 user-service 处理）
- 密码重置流程

---

审查此章节：
[l]ock  [r]eviewed  [d]raft  [c]omment  [n]ext  [q]uit

> l

✓ 章节 "职责" 标记为 [locked]

## 章节 2：结构 [draft]

\```
┌─────────────┐     ┌─────────────┐
│  Middleware │────▶│  AuthService│
└─────────────┘     └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  TokenStore │
                    └─────────────┘
\```

审查此章节：
[l]ock  [r]eviewed  [d]raft  [c]omment  [n]ext  [q]uit

> c

评论：签名验证的公钥从哪里来？

评论已添加。继续审查？
[l]ock  [r]eviewed  [d]raft  [n]ext

> r

✓ 章节 "结构" 标记为 [reviewed]

[...]

## 审查总结

| 章节 | 状态 |
|------|------|
| 职责 | [locked] |
| 结构 | [reviewed] - 1 条评论 |
| API | [locked] |
| 示例 | [draft] |

准备实现：部分就绪
- 2 个章节已锁定
- 1 个章节需要澄清
- 1 个章节仍是草稿

处理评论后再次运行 /intent-review。
```

## 文件中的标记

审查后，章节在 Intent 文件中标记：

```markdown
## 职责 [locked]

...

## 结构 [reviewed]

<!-- 评论：公钥从哪里来？ -->

...
```

## 最佳实践

1. **先锁定关键章节** - API 和职责最重要
2. **不要锁定草稿** - 如果不确定，标记为 reviewed
3. **使用评论** - 记录问题供以后处理
4. **增量审查** - 不要试图一次锁定所有内容

## 相关命令

- [/intent-interview](intent-interview.md) - 审查前创建 Intent
- [/intent-critique](intent-critique.md) - 批准前设计审查
- [/intent-build-now](intent-build-now.md) - 批准后开始构建

## 另请参阅

- [Intent 审批](../intent-approval.md) - 详细审批机制
- [IDD 工作流程](../workflow.md) - 审查在上下文中的位置
