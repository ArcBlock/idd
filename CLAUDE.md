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
| `/intent-assess` | `skills/intent-assess/` | 评估项目是否适合 IDD，学习 IDD 方法论 |
| `/intent-init` | `skills/intent-init/` | 初始化项目 IDD 结构 |
| `/intent-interview` | `skills/intent-interview/` | 从想法创建 INTENT.md |
| `/intent-critique` | `skills/intent-critique/` | 设计质量批判与简化 |
| `/intent-changes` | `skills/intent-changes/` | 结构化变更提案与协作 Review |
| `/intent-review` | `skills/intent-review/` | Section 级别审批 |
| `/intent-build-now` | `skills/intent-build-now/` | 验证 Intent 完整性并启动构建 |
| `/intent-plan` | `skills/intent-plan/` | 生成严格 TDD 的阶段性执行计划 |
| `/intent-sync` | `skills/intent-sync/` | 实现完成后同步细节回 Intent |
| `/intent-check` | `skills/intent-check/` | 运行格式验证和同步检查 |
| `/intent-report` | `skills/intent-report/` | 从 Intent 生成人类可读报告 |
| `/intent-story` | `skills/intent-story/` | 分享 IDD 使用经验，生成博客 |

### Subagents（自主分析）

| Agent | 文件 | 说明 |
|-------|------|------|
| `intent-validate` | `agents/intent-validate.md` | 格式合规检查 |
| `intent-sync` | `agents/intent-sync.md` | 实现一致性检查 |
| `intent-audit` | `agents/intent-audit.md` | 项目级健康报告 |

### Subagents（TDD 执行）

| Agent | 文件 | 说明 |
|-------|------|------|
| `idd-task-execution-master` | `agents/idd-task-execution-master.md` | 将 Intent 转换为阶段性执行计划 |
| `idd-test-master` | `agents/idd-test-master.md` | 测试优先设计，定义完整测试规格 |
| `idd-code-guru` | `agents/idd-code-guru.md` | 基于测试实现优雅代码 |
| `idd-e2e-test-queen` | `agents/idd-e2e-test-queen.md` | E2E 测试设计与验证 |

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
├── .claude-plugin/
│   └── plugin.json         # Plugin 配置
├── CLAUDE.md               # 本文件
├── README.md               # 用户文档
├── intent/                 # 新 Skill 的 Intent 文档
│   └── skills/
├── skills/
│   ├── intent-assess/      # 评估项目适配度
│   ├── intent-init/        # 初始化 IDD 结构
│   ├── intent-interview/   # 创建 Intent
│   ├── intent-critique/    # 设计质量批判
│   ├── intent-changes/     # 变更提案 Review
│   ├── intent-review/      # Section 审批
│   ├── intent-build-now/   # 验证并启动构建
│   ├── intent-plan/        # TDD 执行计划
│   ├── intent-sync/        # 同步实现细节
│   ├── intent-check/       # 运行检查
│   ├── intent-report/      # 生成报告
│   └── intent-story/       # 分享经验
├── agents/
│   ├── intent-validate.md  # 格式检查
│   ├── intent-sync.md      # 一致性检查
│   ├── intent-audit.md     # 健康报告
│   ├── idd-task-execution-master.md  # 阶段性执行计划
│   ├── idd-test-master.md            # 测试规格设计
│   ├── idd-code-guru.md              # 代码实现
│   └── idd-e2e-test-queen.md         # E2E 验证
└── docs/
    ├── intent-standard.md  # 结构规范
    └── intent-approval.md  # 审批机制
```
