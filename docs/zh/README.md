# IDD - Intent 驱动开发

> Intent 驱动开发的完整工具链

[English](../../README.md)

## 理念

```
传统开发：  Code → Test → Documentation
SDD：       Spec → Code → Test              (Spec 作为参考)
TDD：       Test → Code → Documentation     (Test 作为契约)
IDD：       Intent → Test → Code → Sync     (Intent 作为唯一真相)
```

**Intent 是新的源代码。** Code review 由 AI 完成，Intent review 由 Human 完成。

### 为什么不用 SDD？

| 维度 | SDD | IDD |
|------|-----|-----|
| 组织方式 | 按 requirement 类型（功能、UX、技术） | 按模块/层级 |
| 核心载体 | 文字描述 | 结构图 |
| 粒度 | 细分到 user story | 保持完整 pattern |
| Task 管理 | 独立 task 文件 | 不需要，AI 自主分解 |
| LLM 友好度 | 需要拼装上下文 | 一次性理解完整 pattern |

详见 [methodology.md](methodology.md)。

## 工具链概览

```
┌─────────────────────────────────────────────────────────────┐
│                      IDD 生命周期                             │
│                                                              │
│  准备阶段                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-assess    │  │ /intent-init      │               │
│  │   评估适配度       │  │   初始化 IDD      │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  创建阶段                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-interview │  │ /intent-critique  │               │
│  │   创建 Intent     │  │   设计质量审查    │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  审查阶段                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-review    │  │ /intent-changes   │               │
│  │   审批 sections   │  │   提议变更        │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  执行阶段                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-build-now │  │ /intent-plan      │               │
│  │   验证并构建       │  │   TDD 计划        │               │
│  └───────────────────┘  └───────────────────┘               │
│           │                                                  │
│           ▼                                                  │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  TDD Agent 团队（自主执行）                          │    │
│  │                                                     │    │
│  │  idd-task-execution-master ──→ 阶段规划             │    │
│  │           │                                         │    │
│  │           ▼                                         │    │
│  │  idd-test-master ──→ 测试优先设计                   │    │
│  │           │                                         │    │
│  │           ▼                                         │    │
│  │  idd-code-guru ──→ 优雅实现                         │    │
│  │           │                                         │    │
│  │           ▼                                         │    │
│  │  idd-e2e-test-queen ──→ E2E 验证                    │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  同步与验证                                                   │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-sync      │  │ /intent-check     │               │
│  │   同步回写        │  │   运行检查        │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  报告与分享                                                   │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-report    │  │ /intent-story     │               │
│  │   生成文档        │  │   分享经验        │               │
│  └───────────────────┘  └───────────────────┘               │
└─────────────────────────────────────────────────────────────┘
```

## 安装

```bash
# 快速安装
npx add-skill arcblock/idd

# 或手动安装
git clone https://github.com/ArcBlock/idd ~/path/to/idd
claude mcp add-plugin ~/path/to/idd
```

## 命令

### Skills（交互式）

| 命令 | 说明 |
|------|------|
| `/intent-assess` | 评估项目是否适合 IDD，学习 IDD 方法论 |
| `/intent-init` | 初始化项目 IDD 结构（检查现状，创建模板） |
| `/intent-interview` | 通过结构化访谈，从想法创建完整的 INTENT.md |
| `/intent-critique` | 设计质量批判，检查过度工程、YAGNI 违规、简化机会 |
| `/intent-changes` | 结构化变更提案，类似 PR 的审查体验 |
| `/intent-review` | 逐 Section 审批 Intent，标记 locked/reviewed/draft |
| `/intent-build-now` | **验证 Intent 完整性，然后启动 TDD 执行** |
| `/intent-plan` | 生成严格 TDD 的阶段性执行计划 |
| `/intent-sync` | 实现完成后，将最终细节同步回 Intent |
| `/intent-check` | 运行格式验证和同步检查（触发 agents） |
| `/intent-report` | 从 Intent 生成人类可读的报告文档 |
| `/intent-story` | 分享 IDD 使用经验，生成博客文章（多语言） |

### Agents（自主）

#### 验证 Agents

| Agent | 触发场景 | 产出 |
|-------|---------|------|
| `intent-validate` | Intent 修改后 | 格式合规报告 |
| `intent-sync` | 实现完成后 | 代码与 Intent 一致性检查 |
| `intent-audit` | 定期检查 | 项目级 Intent 健康报告 |

#### TDD 执行 Agents

| Agent | 角色 | 说明 |
|-------|------|------|
| `idd-task-execution-master` | 阶段规划 | 将 Intent 转换为阶段性 TDD 执行计划 |
| `idd-test-master` | 测试设计 | 在实现之前定义完整的测试规格 |
| `idd-code-guru` | 实现 | 编写能通过所有测试的优雅代码 |
| `idd-e2e-test-queen` | E2E 验证 | 设计并验证端到端测试 |

## 工作流程

```
/intent-assess            # 1. 评估项目适配度
    ↓
/intent-init              # 2. 初始化 IDD 结构
    ↓
/intent-interview         # 3. 从想法创建 Intent
    ↓
/intent-critique          # 4. 检查过度工程（可选）
    ↓
/intent-review            # 5. 审批关键 sections
    ↓
/intent-build-now         # 6. 验证并开始构建
    │
    ├──→ idd-task-execution-master（阶段规划）
    │         ↓
    ├──→ idd-test-master（测试优先设计）
    │         ↓
    ├──→ idd-code-guru（实现）
    │         ↓
    └──→ idd-e2e-test-queen（E2E 验证）
    ↓
/intent-sync              # 7. 将最终细节同步回 Intent
    ↓
/intent-check             # 8. 验证一致性
    ↓
/intent-report            # 9. 生成文档
    ↓
/intent-story             # 10. 分享你的经验（可选）
```

### 快速开始：从 Intent 到代码

```bash
# 已有 Intent？立即开始构建：
/intent-build-now

# 这将：
# 1. 验证 Intent 完整性
# 2. 报告任何需要修复的缺口
# 3. 准备就绪后，启动 TDD Agent 团队
```

## 文档

| 文档 | 说明 |
|------|------|
| [methodology.md](methodology.md) | IDD vs SDD 详细对比 |
| [intent-standard.md](intent-standard.md) | Intent 文件格式规范 |
| [intent-approval.md](intent-approval.md) | Section 审批机制 |

## 博客

| 文章 | 语言 |
|------|------|
| [Intent Is the New Source Code](../blog/idd-intent-is-new-source-code-en.md) | English |
| [AI 时代别再写需求文档了，写 Intent](../blog/idd-intent-is-new-source-code-zh.md) | 中文 |

## License

MIT
