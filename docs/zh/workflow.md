# IDD 工作流程指南

> 从想法到实现的 Intent 驱动开发

## 概述

IDD（Intent 驱动开发）遵循一个结构化的工作流程，其中 **Intent 是唯一真相来源**。与传统的代码驱动开发不同，IDD 将人类可读的 Intent 文档置于核心，由 AI 处理实现细节。

```
┌─────────────────────────────────────────────────────────────────────┐
│                         IDD 工作流程                                 │
│                                                                      │
│   定义            细化             构建            维护              │
│                                                                      │
│  ┌──────┐       ┌──────┐        ┌──────┐         ┌──────┐          │
│  │ 评估 │──────▶│ 创建 │───────▶│ 构建 │────────▶│ 同步 │          │
│  └──────┘       └──────┘        └──────┘         └──────┘          │
│                                                                      │
│  IDD 适合吗？   编写 Intent     TDD 执行        保持同步            │
│  设置项目       审查质量        Agent 团队      验证健康度          │
│                 批准章节                                            │
└─────────────────────────────────────────────────────────────────────┘
```

## 阶段一：定义

### 步骤 1.1：评估项目适配性

在采用 IDD 之前，评估它是否适合你的项目。

```bash
/intent-assess
```

**适合 IDD 的情况：**
- 新功能或新模块
- 复杂业务逻辑
- 需要团队协作
- 预期长期维护

**不太适合的情况：**
- 快速原型
- 一次性脚本
- 纯机械性重构

参见：[/intent-assess 命令](commands/intent-assess.md)

### 步骤 1.2：初始化 IDD 结构

在项目中设置 Intent 目录结构。

```bash
/intent-init
```

创建的结构：
```
project/
└── intent/
    └── INTENT.md    # 你的第一个 Intent 文件
```

参见：[/intent-init 命令](commands/intent-init.md)

## 阶段二：细化

### 步骤 2.1：创建 Intent

通过引导式访谈将想法转化为结构化的 Intent 文档。

```bash
/intent-interview
```

访谈涵盖：
- **职责**：做什么和不做什么
- **结构**：组件图（ASCII 艺术）
- **API**：函数签名和契约
- **示例**：输入 → 输出 映射

参见：[/intent-interview 命令](commands/intent-interview.md)

### 步骤 2.2：审查设计（可选）

检查 Intent 是否存在过度工程和 YAGNI 违规。

```bash
/intent-critique
```

可以发现：
- 过早抽象
- 不必要的复杂性
- 你不需要的功能

参见：[/intent-critique 命令](commands/intent-critique.md)

### 步骤 2.3：审查和批准

批准 Intent 章节，将它们锁定为实现契约。

```bash
/intent-review
```

章节状态：
- **draft**：进行中，未审查
- **reviewed**：已检查，可能需要修改
- **locked**：已批准，可以实现

参见：[/intent-review 命令](commands/intent-review.md)

### 步骤 2.4：提议变更（按需）

用于类似 PR 体验的协作审查。

```bash
/intent-changes
```

参见：[/intent-changes 命令](commands/intent-changes.md)

## 阶段三：构建

### 步骤 3.1：验证并开始构建

连接 Intent 和实现的关键命令。

```bash
/intent-build-now
```

此命令：
1. **验证** Intent 完整性
2. **报告** 任何需要修复的缺口
3. 准备就绪时**启动** TDD Agent 团队

参见：[/intent-build-now 命令](commands/intent-build-now.md)

### 步骤 3.2：TDD Agent 团队执行

一旦 `/intent-build-now` 验证了你的 Intent，它会协调四个专门的 Agent：

```
┌─────────────────────────────────────────────────────────────┐
│                    TDD Agent 团队                            │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-task-execution-master                          │    │
│  │  将 Intent 分解为带有明确交付物的阶段                 │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        ▼                                     │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-test-master                                    │    │
│  │  在实现之前设计全面的测试                            │    │
│  │  - 正常路径、异常路径、边界条件                      │    │
│  │  - 安全测试、数据泄露测试、数据损坏测试              │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        ▼                                     │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-code-guru                                      │    │
│  │  实现能通过所有测试的优雅代码                        │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        ▼                                     │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-e2e-test-queen                                 │    │
│  │  端到端验证                                          │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

参见：[Agent 概述](agents/overview.md)

### 替代方案：手动规划

如果你倾向于手动控制，可以生成计划而不自动执行：

```bash
/intent-plan
```

参见：[/intent-plan 命令](commands/intent-plan.md)

## 阶段四：维护

### 步骤 4.1：同步实现细节

实现完成后，将确认的细节同步回 Intent。

```bash
/intent-sync
```

捕获的内容：
- 最终 API 签名
- 实际数据结构
- 实现决策

参见：[/intent-sync 命令](commands/intent-sync.md)

### 步骤 4.2：验证一致性

运行检查以确保 Intent 和实现保持一致。

```bash
/intent-check
```

这会自动触发验证 Agent。

参见：[/intent-check 命令](commands/intent-check.md)

### 步骤 4.3：生成报告

从 Intent 文件创建人类可读的文档。

```bash
/intent-report
```

参见：[/intent-report 命令](commands/intent-report.md)

### 步骤 4.4：分享经验（可选）

为他人记录你的 IDD 之旅。

```bash
/intent-story
```

参见：[/intent-story 命令](commands/intent-story.md)

## 快速参考

### 典型的新功能流程

```bash
/intent-interview     # 从你的想法创建 Intent
/intent-critique      # 检查是否过度工程
/intent-review        # 批准关键章节
/intent-build-now     # 验证并开始 TDD 执行
/intent-sync          # 完成后同步回来
```

### 现有项目采用

```bash
/intent-assess        # 评估适配性
/intent-init          # 设置结构
/intent-interview     # 记录现有模块
```

### 健康检查

```bash
/intent-check         # 运行所有验证
```

## 下一步

- [命令参考](commands/) - 每个命令的详细文档
- [Agent 文档](agents/) - TDD Agent 如何工作
- [常见问题](faq.md) - 常见问题与解答
- [Intent 标准](intent-standard.md) - 文件格式规范
