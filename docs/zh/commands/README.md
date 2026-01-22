# IDD 命令参考

> 所有 IDD 技能命令的完整列表

## 命令概览

### 设置阶段

| 命令 | 描述 |
|------|------|
| [/intent-assess](intent-assess.md) | 评估 IDD 是否适合你的项目，学习 IDD 方法论 |
| [/intent-init](intent-init.md) | 在项目中初始化 IDD 结构 |

### 创建阶段

| 命令 | 描述 |
|------|------|
| [/intent-interview](intent-interview.md) | 通过结构化访谈创建完整的 INTENT.md |
| [/intent-critique](intent-critique.md) | 批判性审查过度工程、YAGNI 违规和简化机会 |

### 审查阶段

| 命令 | 描述 |
|------|------|
| [/intent-review](intent-review.md) | 审查和批准 Intent 章节（locked/reviewed/draft） |
| [/intent-changes](intent-changes.md) | 结构化变更提案，类似 PR 的审查体验 |

### 执行阶段

| 命令 | 描述 |
|------|------|
| [/intent-build-now](intent-build-now.md) | **验证 Intent 完整性，然后启动 TDD 执行** |
| [/intent-plan](intent-plan.md) | 生成严格 TDD 的阶段执行计划 |

### 维护阶段

| 命令 | 描述 |
|------|------|
| [/intent-sync](intent-sync.md) | 实现后将最终细节同步回 Intent |
| [/intent-check](intent-check.md) | 运行验证和同步检查（触发 Agent） |

### 报告与分享

| 命令 | 描述 |
|------|------|
| [/intent-report](intent-report.md) | 从 Intent 文件生成人类可读的报告 |
| [/intent-story](intent-story.md) | 分享你的 IDD 体验，创建博客文章（多语言） |

## 常用工作流

### 新功能开发

```bash
/intent-interview     # 1. 从想法创建 Intent
/intent-critique      # 2. 检查过度工程（可选）
/intent-review        # 3. 批准关键章节
/intent-build-now     # 4. 验证并开始 TDD 构建
/intent-sync          # 5. 完成后同步
/intent-check         # 6. 验证一致性
```

### 现有项目采用 IDD

```bash
/intent-assess        # 1. 评估适配性
/intent-init          # 2. 设置结构
/intent-interview     # 3. 为现有模块创建 Intent
```

### 快速健康检查

```bash
/intent-check         # 运行所有验证
```

## 命令分类

### 交互式技能

需要用户交互的命令：

- `/intent-assess` - 问答评估
- `/intent-interview` - 引导式访谈
- `/intent-critique` - 讨论式审查
- `/intent-review` - 章节级批准
- `/intent-changes` - 变更提案
- `/intent-story` - 经验访谈

### 自动化命令

运行后自动完成的命令：

- `/intent-init` - 创建结构
- `/intent-build-now` - 启动 Agent 团队
- `/intent-plan` - 生成计划
- `/intent-sync` - 同步变更
- `/intent-check` - 运行检查
- `/intent-report` - 生成报告

## 相关文档

- [IDD 工作流程](../workflow.md) - 完整流程指南
- [Agent 概述](../agents/overview.md) - TDD Agent 团队
- [常见问题](../faq.md) - FAQ
