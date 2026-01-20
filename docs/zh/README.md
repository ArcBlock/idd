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
│                    IDD 生命周期                               │
│                                                              │
│  准备阶段                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-assess    │  │ /intent-init      │               │
│  │   评估适配度       │  │   初始化 IDD      │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  创建阶段                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-interview │  │ /intent-review    │               │
│  │   创建 Intent     │  │   审批 sections   │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  验证阶段                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-check     │  │ intent-validate   │               │
│  │   运行检查        │  │   (自动 agent)    │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  同步与报告                                                   │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-sync       │  │ /intent-report    │               │
│  │   (自动 agent)    │  │   生成文档        │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  健康检查与分享                                               │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-audit      │  │ /intent-story     │               │
│  │   (自动 agent)    │  │   分享经验        │               │
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
| `/intent-review` | 逐 Section 审批 Intent，标记 locked/reviewed/draft |
| `/intent-check` | 运行格式验证和同步检查（触发 agents） |
| `/intent-report` | 从 Intent 生成人类可读的报告文档 |
| `/intent-story` | 分享 IDD 使用经验，生成博客文章（多语言） |

### Agents（自主）

| Agent | 触发场景 | 产出 |
|-------|---------|------|
| `intent-validate` | Intent 修改后 | 格式合规报告 |
| `intent-sync` | 实现完成后 | 代码与 Intent 差异报告 |
| `intent-audit` | 定期检查 | 项目级 Intent 健康报告 |

## 工作流程

```
/intent-assess            # 1. 评估项目适配度
    ↓
/intent-init              # 2. 初始化 IDD 结构
    ↓
/intent-interview         # 3. 从想法创建 Intent
    ↓
/intent-review            # 4. 审批关键 sections
    ↓
[开发]                    # 5. 写代码（AI 遵循 Intent）
    ↓
/intent-check             # 6. 验证一致性
    ↓
/intent-report            # 7. 生成文档
    ↓
/intent-story             # 8. 分享你的经验（可选）
```

## 文档

| 文档 | 说明 |
|------|------|
| [methodology.md](methodology.md) | IDD vs SDD 详细对比 |
| [intent-standard.md](intent-standard.md) | Intent 文件格式规范 |
| [intent-approval.md](intent-approval.md) | Section 审批机制 |

## License

MIT
