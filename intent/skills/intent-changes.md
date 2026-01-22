# Intent: /intent-changes

> 设计文档的结构化变更提案与协作 Review 工具

## 问题

设计文档的迭代常见两种极端：

1. **无结构修改**：直接改文档，难以追踪"改了什么、为什么改、谁同意的"
2. **过重流程**：用 PR review 代码的方式 review 文档，但 diff 对设计文档不友好

需要一种**轻量但结构化**的方式来：
- 提出具体变更建议
- 追踪每个变更的决策过程
- 支持多人异步协作
- 最终干净地 apply 到原文档

## 核心概念

### Change Proposal

每个变更是一个独立的提案，包含：

| 字段 | 说明 |
|------|------|
| **ID** | 唯一标识 (C001, C002...) |
| **Type** | ADD / MODIFY / REPLACE / DELETE |
| **Status** | PENDING / ACCEPTED / REJECTED |
| **Target** | 变更位置（Section 标题或行号范围） |
| **Before** | 原内容（MODIFY/REPLACE/DELETE 时） |
| **After** | 新内容（ADD/MODIFY/REPLACE 时） |
| **Reason** | 变更理由 |
| **Decision** | 决策记录 (reviewer, timestamp, comment) |

### Review Session

一个 Review Session 绑定一个源文档，产出一个 `.review.md` 文件：

```
source: intent/specs/kind-system-spec.md
review: .reviews/kind-system-spec.review.md
```

### Status Flow

```
PENDING  ──accept──>  ACCEPTED  ──finalize──>  Applied
    │                     │
    └──reject──>  REJECTED (archived)
```

## 文件结构

### Review 目录

```
.reviews/
├── kind-system-spec.review.md
├── tools-spec.review.md
└── ui-device-spec.review.md
```

采用扁平结构，文件名 = 源文件名 + `.review.md`

### Review 文件格式

```markdown
---
source: intent/specs/kind-system-spec.md
created: 2026-01-21
reviewers:
  - robmao
  - claude
status: active  # active | finalized | abandoned
---

# Review: kind-system-spec.md

## Summary

| Status | Count |
|--------|-------|
| PENDING | 3 |
| ACCEPTED | 5 |
| REJECTED | 2 |

---

## C001 [ADD] [ACCEPTED]

> 新增 Action 分类说明

**Target:** After "## Actions"

**After:**
```markdown
Actions 分为三类：
- Inline: 同步执行，决定 commit 成功与否
- Deferred: 异步执行，失败不影响 commit
- Observational: 只读，可以慢
```

**Decision:**
- ✓ @robmao (2026-01-21): "分类清晰，采纳"

---

## C002 [MODIFY] [PENDING]

> 修改 Kind 定义的措辞

**Target:** Section "## Kind 定义"

**Before:**
```markdown
Kind 是语义类型。
```

**After:**
```markdown
Kind 是自执行的语义单元，包含 validate/normalize/render 能力。
```

**Reason:** 原描述过于简单，未体现 Kind 的自包含特性。

---

## C003 [DELETE] [REJECTED]

> 删除示例代码

**Target:** Section "## 示例"

**Decision:**
- ✗ @robmao (2026-01-21): "示例对理解很重要，保留"
```

## 命令设计

### 启动 Review

```bash
/intent-changes start <file>
/intent-changes start intent/specs/kind-system-spec.md
```

行为：
1. 检查 `.reviews/` 是否已有该文件的 review
2. 有则恢复，无则创建新 review 文件
3. 显示当前状态

### 提出变更

```bash
/intent-changes propose
```

行为：
1. 读取源文档和当前 review
2. 与用户讨论需要变更的内容
3. 生成 Change Proposal（自动分配 ID）
4. 追加到 review 文件

### 决策操作

```bash
/intent-changes accept C001 [--comment "..."]
/intent-changes reject C002 --reason "..."
/intent-changes comment C003 "讨论一下这个改法"
```

行为：
1. 找到对应提案
2. 更新 status 和 decision
3. 记录 reviewer 和 timestamp

### 查看状态

```bash
/intent-changes status
/intent-changes status --detail
```

输出：
```
Review: kind-system-spec.md

PENDING (3):
  C002 - 修改 Kind 定义的措辞
  C004 - 新增性能章节
  C005 - 调整目录结构

ACCEPTED (5):
  C001 - 新增 Action 分类说明
  ...

REJECTED (2):
  C003 - 删除示例代码
  ...
```

### 完成 Review

```bash
/intent-changes finalize
```

行为：
1. 显示所有 ACCEPTED 的变更
2. **交互确认**：逐个询问是否 apply
3. Apply 到源文档
4. 标记 review 为 finalized
5. 生成变更摘要

交互流程：
```
即将 Apply 5 个变更：

[1/5] C001: 新增 Action 分类说明
      Target: After "## Actions"

      Apply this change? [Y/n/view]
      > y
      ✓ Applied

[2/5] C002: 修改 Kind 定义的措辞
      Target: Section "## Kind 定义"

      Apply this change? [Y/n/view]
      > view

      [显示 before/after diff]

      Apply this change? [Y/n]
      > n
      ⊘ Skipped (remains ACCEPTED but not applied)

...

Summary:
- Applied: 4
- Skipped: 1
- Source file updated: intent/specs/kind-system-spec.md
```

## 协作模式

### Reviewer 署名

每个决策记录操作者：

```markdown
**Decision:**
- ✓ @robmao (2026-01-21): "LGTM"
- ? @alice (2026-01-21): "需要讨论一下边界情况"
- ✓ @alice (2026-01-22): "讨论后同意"
```

### 获取当前 Reviewer

按优先级：
1. `--reviewer` 参数
2. git config `user.name`
3. 环境变量 `USER`

## 边界

### 做什么

- ✓ 结构化管理变更提案
- ✓ 追踪决策过程
- ✓ 支持多 reviewer 署名
- ✓ 交互式 apply

### 不做什么

- ✗ 不做格式校验（intent-validate 的职责）
- ✗ 不做 section 级审批（intent-review 的职责）
- ✗ 不做设计质量判断（intent-critique 的职责）
- ✗ 不做实现一致性检查（intent-sync 的职责）

## 与其他 IDD 工具的关系

```
intent-interview → 创建 Intent
        ↓
intent-critique → 质疑设计，产出 change 建议
        ↓
/intent-changes → 管理变更提案和 review 流程  ← 本 Skill
        ↓
intent-review → 锁定已 finalize 的 sections
        ↓
intent-plan → 开始实现
```

## 未来扩展（不在 MVP）

- 版本历史：`.reviews/kind-system-spec/` 目录存放历史 review
- 统计报告：accepted/rejected 比例分析
- Comment 线程：支持对单个 proposal 的讨论串
- @ 提及：通知特定 reviewer

## 示例场景

### 场景 1：独立 Review

```bash
# 开始
/intent-changes start intent/specs/tools-spec.md

# 阅读后提出几个建议
/intent-changes propose
# [交互式生成 C001, C002, C003]

# 自己接受部分
/intent-changes accept C001
/intent-changes accept C002
/intent-changes reject C003 --reason "想了想不需要"

# 应用
/intent-changes finalize
```

### 场景 2：协作 Review

```bash
# A 开始并提出建议
/intent-changes start spec.md
/intent-changes propose  # 生成 C001-C005

# B 来 review
/intent-changes status
/intent-changes accept C001 --comment "Good"
/intent-changes reject C002 --reason "不同意这个改法"

# A 看到反馈，继续讨论
/intent-changes comment C002 "那这样改呢？"
/intent-changes propose  # 生成 C006 作为 C002 的替代

# B 接受新方案
/intent-changes accept C006

# 最终 apply
/intent-changes finalize
```
