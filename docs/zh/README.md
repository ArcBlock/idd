# IDD - Intent 驱动开发

> Intent 驱动开发的完整工具链

[English](../../README.md)

## 理念

```
传统开发：  Code → Test → Documentation
TDD：       Test → Code → Documentation
IDD：       Intent → Test → Code → Sync
```

**Intent 是新的源代码。** Code review 由 AI 完成，Intent review 由 Human 完成。

## 工具链概览

```
┌─────────────────────────────────────────────────────────────┐
│                    IDD 生命周期                               │
│                                                              │
│  创建层                                                       │
│  ┌───────────────────┐                                       │
│  │ /intent-interview │ → 从想法创建 INTENT.md                 │
│  └───────────────────┘                                       │
│                                                              │
│  质量层                                                       │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-validate   │  │ /intent-review    │               │
│  │   (subagent)      │  │   格式校验 + 审批   │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  同步层                                                       │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-sync       │  │ intent-audit      │               │
│  │   实现一致性检查    │  │   项目级健康报告   │               │
│  │   (subagent)      │  │   (subagent)      │               │
│  └───────────────────┘  └───────────────────┘               │
└─────────────────────────────────────────────────────────────┘
```

## 安装

```bash
# 添加到 Claude Code settings
claude mcp add-plugin ~/path/to/idd
```

## 命令

### Skills（交互式）

| 命令 | 说明 |
|------|------|
| `/intent-interview` | 通过结构化访谈，从想法创建完整的 INTENT.md |
| `/intent-review` | 逐 Section 审批 Intent，标记 locked/reviewed/draft |

### Subagents（自主分析）

| Agent | 触发场景 | 产出 |
|-------|---------|------|
| `intent-validate` | Intent 修改后 | 格式合规报告 |
| `intent-sync` | 实现完成后 | 代码与 Intent 差异报告 |
| `intent-audit` | 定期检查 | 项目级 Intent 健康报告 |

## Intent 文件规范

见 [intent-standard.md](intent-standard.md)

## Section 审批机制

见 [intent-approval.md](intent-approval.md)

## 与 AINE 的关系

IDD 是 [AINE (AI Native Engineering)](https://github.com/ArcBlock/aine) 方法论的核心实践之一。

```
AINE 方法论
├── IDD (Intent Driven Development)  ← 本 plugin
├── Contract 三态语义
├── TDD 先行
├── Chamber 架构
└── Human-in-the-loop
```

## License

MIT
