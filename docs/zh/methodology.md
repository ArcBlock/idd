# IDD 方法论

> Intent 驱动开发 - 方法论对比与设计原理

[English](../methodology.md)

## 背景

IDD (Intent Driven Development) 源于优化 AI 辅助编码工作流的需求。本文解释该方法论并与 SDD (Spec Driven Development) 进行对比。

---

## 开发方法论演进

```
┌─────────────────────────────────────────────────────────────┐
│  传统方式                                                    │
│  Code → Test → Docs                                         │
│  问题：文档经常过时或缺失                                     │
├─────────────────────────────────────────────────────────────┤
│  SDD (Spec Driven Development)                              │
│  Spec → Code → Test                                         │
│  问题：Spec 容易过时，分散在多个文件中                         │
├─────────────────────────────────────────────────────────────┤
│  TDD (Test Driven Development)                              │
│  Test → Code → Docs                                         │
│  问题：测试无法捕捉设计理由                                   │
├─────────────────────────────────────────────────────────────┤
│  IDD (Intent Driven Development)                            │
│  Intent → Test → Code → Sync                                │
│  Intent 捕捉 "做什么" 和 "为什么"，AI 处理 "怎么做"           │
└─────────────────────────────────────────────────────────────┘
```

---

## SDD：哪些可取，哪些不可取

### SDD 典型结构

```
specs/
├── functional/
│   ├── user-authentication.md
│   └── payment-processing.md
├── ux/
│   └── checkout-flow.md
├── technical/
│   └── database-schema.md
└── stories/
    └── US-001-login.md

tasks/
├── TASK-001-implement-login.md
└── TASK-002-add-payment.md
```

### SDD 值得借鉴的

| 特性 | 价值 | IDD 如何借鉴 |
|-----|------|-------------|
| **Spec/Task 分离** | Spec 是稳定的 "是什么"，Task 是临时的 "做什么" | Intent 是 spec，不需要 task 文件 |
| **结构图优先** | 比文字更精确，更易 review | ASCII 图描述结构和依赖 |
| **可测试性** | Spec 可以生成测试 | Intent 直接映射到测试断言 |
| **版本追踪** | Spec 有变更历史 | Git 追踪 intent 变更 |

### SDD 不可取的

| 特性 | 问题 | IDD 做法 |
|-----|------|---------|
| **Requirement 分类** | 割裂完整 pattern，LLM 需要重新拼装 | 按模块/层级组织，不按类型 |
| **User Story 格式** | "As a user, I want..." 对系统软件无意义 | 直接描述行为和约束 |
| **Task 文件** | LLM 可以自己分解任务 | 不需要，让 AI 自主规划 |
| **过细的模板** | 强制填写不适用的字段 | 最小化结构，按需扩展 |

---

## SDD 的核心问题

### 1. 强制分类割裂 Pattern

SDD 要求划分：
- Functional Requirements
- UX Requirements
- Technical Requirements
- User Stories

**问题**：这种划分在企业应用场景下可能 OK，但不适用于系统软件。更重要的是，**过度划分割裂了 LLM 可以一体化思考和解决的完整 pattern**。

LLM 擅长理解完整上下文，强制拆分反而增加认知负担。

### 2. User Story 的局限

```
"As a user, I want to login so that I can access my account"
```

对于系统软件（如 chamber 模块），这种格式毫无意义。没有 "user"，只有模块间的交互。

### 3. Task 文件的冗余

SDD 维护独立的 task 文件，但 LLM 完全可以：
1. 阅读 spec/intent
2. 自主分解任务
3. 规划执行顺序

额外的 task 文件只增加维护成本。

---

## IDD 的做法

### 核心公式

```
Intent = 结构图 + 约束规则 + 示例

不是：功能描述 + UX 需求 + 技术需求 + 用户故事
```

### 三层结构

```
┌─────────────────────────────────────────────────────────────┐
│  Layer 1: 结构图 (Structure)                                │
│  - 目录结构、数据结构、模块关系                               │
│  - ASCII 图为主，文字为辅                                    │
│  - LLM 可以 "看图" 理解系统                                  │
├─────────────────────────────────────────────────────────────┤
│  Layer 2: 约束规则 (Constraints)                            │
│  - 依赖方向、边界规则、不变式                                 │
│  - 表格或列表形式                                            │
│  - 可以直接转化为 lint 规则或测试断言                         │
├─────────────────────────────────────────────────────────────┤
│  Layer 3: 行为示例 (Examples)                               │
│  - 输入 → 输出 的具体例子                                    │
│  - 边界情况                                                  │
│  - 可以直接转化为测试用例                                     │
└─────────────────────────────────────────────────────────────┘
```

### 组织方式

```
intent/
├── INTENT.md                    # 项目概述（入口）
│
├── core/                        # 按模块组织，不按类型
│   ├── chamber/
│   │   └── INTENT.md            # 结构 + API + 示例
│   ├── router/
│   └── deploy/
│
└── architecture/                # 架构级约束
    ├── DEPENDENCIES.md          # 依赖图
    └── BOUNDARIES.md            # 边界规则
```

---

## 关键区别总结

| 维度 | SDD | IDD |
|-----|-----|-----|
| **组织方式** | 按 requirement 类型 | 按模块/层级 |
| **核心载体** | 文字描述 | 结构图 |
| **粒度** | 细分到 user story | 保持完整 pattern |
| **Task 管理** | 独立 task 文件 | 不需要，AI 自主分解 |
| **适用范围** | 企业应用 | 系统软件 + 应用 |
| **LLM 友好度** | 需要拼装上下文 | 一次性理解完整 pattern |

---

## IDD 设计原则

1. **结构图优先** - ASCII 图比文字更精确，LLM 和人类都能快速理解
2. **按模块组织** - 不按 requirement 类型，保持 pattern 完整性
3. **约束可测试** - 每条约束都应能转化为测试断言或 lint 规则
4. **最小化模板** - 不强制填写不适用的字段
5. **AI 自主分解** - 不维护 task 文件，让 AI 规划执行

---

## 适用场景

**适合 IDD：**
- 系统软件（框架、库、基础设施）
- AI 辅助开发工作流
- LLM 是主要实现者的项目
- 需要严格架构边界的代码库

**可能不适合：**
- 高度监管行业需要传统文档
- 没有 AI 工具的团队
- 有非技术利益相关者需要 user story 的项目

---

## 版本历史

| 日期 | 变更 |
|------|------|
| 2026-01-19 | 初始版本 |
