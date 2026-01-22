# CLAUDE.md - IDD Plugin

## 项目定位

IDD (Intent Driven Development) 是 AINE 方法论的核心实践工具，提供 Intent 驱动开发的完整工具链。

## 核心理念

> **Intent 是新的源代码。Code review 由 AI 完成，Intent review 由 Human 完成。**

```
传统:  Code → Test → Docs
TDD:   Test → Code → Docs
IDD:   Intent → Test → Code → Sync
```

## 组件

### Skills（交互式）

| 命令 | 文件 | 说明 |
|------|------|------|
| `/intent-interview` | `skills/intent-interview/` | 从想法创建 INTENT.md |
| `/intent-critique` | `skills/intent-critique/` | 设计质量批判与简化 |
| `/intent-review` | `skills/intent-review/` | Section 级别审批 |

### Subagents（自主分析）

| Agent | 文件 | 说明 |
|-------|------|------|
| `intent-validate` | `agents/intent-validate.md` | 格式合规检查 |
| `intent-sync` | `agents/intent-sync.md` | 实现一致性检查 |
| `intent-audit` | `agents/intent-audit.md` | 项目级健康报告 |

### 规范文档

| 文档 | 说明 |
|------|------|
| `docs/intent-standard.md` | Intent 文件结构规范 |
| `docs/intent-approval.md` | Section 审批机制 |

## 开发此 Plugin

```bash
# 测试 skill
claude --skill intent-review

# 测试 agent
claude --agent intent-validate --input '{"path": "test.md"}'
```

## 目录结构

```
idd/
├── claude-plugin.json      # Plugin 配置
├── CLAUDE.md               # 本文件
├── README.md               # 用户文档
├── skills/
│   ├── intent-interview/   # 创建 Intent
│   │   └── SKILL.md
│   └── intent-review/      # 审批 Intent
│       └── SKILL.md
├── agents/
│   ├── intent-validate.md  # 格式检查
│   ├── intent-sync.md      # 一致性检查
│   └── intent-audit.md     # 健康报告
└── docs/
    ├── intent-standard.md  # 结构规范
    └── intent-approval.md  # 审批机制
```
