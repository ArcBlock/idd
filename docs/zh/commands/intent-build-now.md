# /intent-build-now

> 验证 Intent 完整性并启动 TDD 执行

## 用法

```bash
/intent-build-now
/intent-build-now path/to/INTENT.md
```

## 用途

连接 Intent 和实现的桥梁。此命令：

1. **验证** Intent 完整性和质量
2. **报告** 任何需要修复的缺口
3. 准备就绪时**启动** TDD Agent 团队

## 何时使用

- Intent 已批准，准备实现
- `/intent-review` 已锁定关键章节后
- 想让 AI 接管构建过程时

## 验证检查

### 必需章节

| 章节 | 为什么必需 |
|------|-----------|
| **职责** | 为 Agent 定义范围 |
| **结构** | 指导架构决策 |
| **API** | 测试设计的契约 |

### 质量检查

| 检查 | 标准 |
|------|------|
| **清晰度** | 无模糊术语 |
| **可测试性** | 示例映射到断言 |
| **边界** | 明确的"不做什么" |
| **依赖** | 列出外部依赖 |

### 对于多模块项目

- `intent/architecture/DEPENDENCIES.md` 存在
- 定义了模块依赖图
- 无循环依赖

## 执行流程

```
┌─────────────────────────────────────────────────────────────┐
│                   /intent-build-now                          │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ 步骤 1: 定位 Intent                                   │   │
│  │ - 检查 intent/INTENT.md                              │   │
│  │ - 检查当前目录                                        │   │
│  │ - 使用提供的路径                                      │   │
│  └────────────────────────┬─────────────────────────────┘   │
│                           ▼                                  │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ 步骤 2: 验证完整性                                    │   │
│  │ - 检查必需章节                                        │   │
│  │ - 验证质量标准                                        │   │
│  │ - 评估就绪状态                                        │   │
│  └────────────────────────┬─────────────────────────────┘   │
│                           │                                  │
│              ┌────────────┴────────────┐                    │
│              ▼                         ▼                    │
│  ┌───────────────────┐     ┌───────────────────────────┐   │
│  │ 不完整             │     │ 就绪                       │   │
│  │                   │     │                           │   │
│  │ 显示缺口           │     │ 启动 TDD Agent 团队        │   │
│  │ 解释修复方法       │     │ - task-execution-master   │   │
│  │ 推荐操作           │     │ - test-master             │   │
│  └───────────────────┘     │ - code-guru               │   │
│                            │ - e2e-test-queen          │   │
│                            └───────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

## 示例：准备好构建

```
> /intent-build-now

定位 Intent...
找到: intent/auth/INTENT.md

验证完整性...

## Intent 验证: 通过 ✓

你的 Intent 已准备好实现:

✓ 职责已定义
✓ 结构已记录（找到 ASCII 图）
✓ API 签名清晰（3 个函数）
✓ 提供了示例（5 个案例）
✓ 依赖已列出

启动 idd-task-execution-master...

## 执行计划

### 阶段 1: 核心认证
- 任务 1.1: Token 验证
- 任务 1.2: Token 生成
- 任务 1.3: 刷新 Token 轮换

### 阶段 2: 集成
- 任务 2.1: 中间件实现
- 任务 2.2: 错误处理

开始阶段 1...

[TDD Agent 接管]
```

## 示例：未准备好

```
> /intent-build-now

定位 Intent...
找到: intent/payment/INTENT.md

验证完整性...

## Intent 验证: 需要完善

你的 Intent 缺少关键元素:

### 缺失章节

❌ **结构** - 未找到 ASCII 图

添加组件图:
\```markdown
## 结构

\```
ComponentA ──▶ ComponentB
     │
     ▼
ComponentC
\```
\```

❌ **API** - 函数签名不完整

定义参数和返回值:
\```markdown
## API

### processPayment(amount, currency)

**参数:**
- amount: number - 支付金额（分）
- currency: string - ISO 货币代码

**返回:** PaymentResult

**错误:**
- InvalidAmount: 当 amount <= 0
\```

### 质量问题

⚠ **发现模糊术语:** "处理支付"
→ 指定: 验证？处理？记录？

⚠ **无示例章节**
→ 添加输入/输出示例

### 推荐操作

1. 添加带 ASCII 图的结构章节
2. 完成 API 签名
3. 添加示例章节
4. 再次运行 `/intent-build-now`

**Intent 完整之前不要继续实现。**
```

## TDD Agent 团队

验证通过后，协调这些 Agent:

| Agent | 角色 |
|-------|------|
| `idd-task-execution-master` | 创建阶段执行计划 |
| `idd-test-master` | 在实现前设计测试 |
| `idd-code-guru` | 实现代码以通过测试 |
| `idd-e2e-test-queen` | 用 E2E 测试验证 |

参见: [Agent 概述](../agents/overview.md)

## 相关命令

- [/intent-review](intent-review.md) - 构建前批准章节
- [/intent-plan](intent-plan.md) - 手动规划替代方案
- [/intent-sync](intent-sync.md) - 构建后同步

## 相关文档

- [IDD 工作流程](../workflow.md) - 上下文中的构建阶段
- [Agent 文档](../agents/) - Agent 如何工作
