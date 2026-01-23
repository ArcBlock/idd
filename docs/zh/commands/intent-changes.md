# /intent-changes

> 结构化变更提案，类似 PR 的审查体验

## 用法

```bash
/intent-changes start <file>    # 开始提议变更
/intent-changes propose         # 建议变更
/intent-changes accept          # 接受提议的变更
/intent-changes reject          # 拒绝提议的变更
/intent-changes finalize        # 应用所有接受的变更
```

## 目的

管理 Intent 文档的结构化变更提案，提供类似 Pull Request 但针对 Intent 文件的协作审查体验。

## 何时使用

- 多人审查 Intent
- 对现有 Intent 进行重大修订
- 当你想要可追踪的变更历史
- 需要正式审批流程

## 工作流程

```
┌─────────────────────────────────────────────────────────────┐
│                  /intent-changes 流程                        │
│                                                              │
│  start ──▶ propose ──▶ review ──▶ accept/reject ──▶ finalize│
│              │           │              │                    │
│              ▼           ▼              ▼                    │
│         逐个添加      讨论          做出决定                  │
│           变更       每一个         每个提案                  │
└─────────────────────────────────────────────────────────────┘
```

### 步骤 1：开始会话

```bash
/intent-changes start intent/INTENT.md
```

为指定文件打开变更会话。

### 步骤 2：提议变更

```bash
/intent-changes propose
```

交互式提议具体变更：

```
要变更哪个章节？
> ## API

当前内容是什么？
> ### processPayment(amount)

应该是什么？
> ### processPayment(amount, currency = 'USD')

为什么要这样变更？
> 根据客户需求支持多币种支付
```

### 步骤 3：审查提案

每个提案显示：
- 当前 vs 提议内容
- 理由
- 影响评估

### 步骤 4：接受或拒绝

```bash
/intent-changes accept    # 接受当前提案
/intent-changes reject    # 带原因拒绝
```

### 步骤 5：完成

```bash
/intent-changes finalize
```

将所有接受的变更应用到文件。

## 提案格式

```markdown
## 提案 #1

**章节：** ## API
**状态：** pending

### 当前
\```
processPayment(amount)
\```

### 提议
\```
processPayment(amount, currency = 'USD')
\```

### 理由
根据客户需求支持多币种支付。

### 影响
- 向后兼容（默认参数）
- 需要货币验证
- 测试需要更新
```

## 示例会话

```
> /intent-changes start intent/payment/INTENT.md

已为 intent/payment/INTENT.md 开始变更会话
会话 ID：changes-2024-01-21-001

> /intent-changes propose

要变更的章节：## 职责
当前："通过 Stripe 处理支付"
提议："通过 Stripe 和 PayPal 处理支付"
原因：PayPal 集成已在 Q1 路线图中批准

提案 #1 已创建。

> /intent-changes propose

要变更的章节：## API
当前：[当前 API 章节]
提议：[带新 PayPal 方法的 API]
原因：PayPal 集成所需

提案 #2 已创建。

> /intent-changes accept 1

提案 #1 已接受。

> /intent-changes reject 2

拒绝原因：从统一接口开始，而不是提供商特定的方法

提案 #2 已拒绝。

> /intent-changes finalize

已将 1 个变更应用到 intent/payment/INTENT.md

变更：
- 提案 #1：已应用（职责更新）
- 提案 #2：已拒绝（API 变更）

会话已关闭。
```

## 最佳实践

1. **每个提案一个关注点** - 不要捆绑不相关的变更
2. **解释原因** - 必须有理由
3. **考虑影响** - 注意还有什么可能需要变更
4. **保持原子性** - 每个提案应该独立

## 相关命令

- [/intent-critique](intent-critique.md) - 变更前审查
- [/intent-review](intent-review.md) - 变更后批准章节

## 另请参阅

- [Intent 审批](../intent-approval.md) - 审批机制
- [IDD 工作流程](../workflow.md) - 这适合的位置
