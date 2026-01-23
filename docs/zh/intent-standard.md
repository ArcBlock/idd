# Intent 设计规范

> 适用于多项目、多 repo 的通用标准
> 版本: 1.0

## 设计目标

1. **Agent 区域自治** - 每个模块/chamber 有独立 intent，agent 在自己范围内自主规划
2. **层级清晰** - 项目级、模块级、架构级各有分工
3. **结构图优先** - ASCII 图比文字更精确
4. **可测试性** - Intent 直接映射到测试断言

---

## 目录结构

### 标准布局

```
project/
├── intent/                      # 项目级 intent
│   ├── INTENT.md                # 入口：愿景 + 索引
│   ├── architecture/            # 架构级约束
│   │   ├── DEPENDENCIES.md      # 模块依赖图
│   │   └── BOUNDARIES.md        # 边界规则
│   └── specs/                   # 结构规范
│       └── *.md                 # 各类结构图
│
├── src/
│   ├── core/                    # 核心模块
│   │   └── intent/
│   │       └── INTENT.md        # core 模块 intent
│   │
│   ├── platforms/               # 多平台
│   │   ├── web/
│   │   │   └── intent/
│   │   │       └── INTENT.md
│   │   └── cli/
│   │       └── intent/
│   │           └── INTENT.md
│   │
│   └── chambers/                # 独立 chambers
│       ├── terminal/
│       │   └── intent/
│       │       └── INTENT.md
│       └── portal/
│           └── intent/
│               └── INTENT.md
│
└── docs/
    └── engineering/             # 工程方法论
        └── intent-standard.md   # 本文档
```

---

## 层级职责

```
┌─────────────────────────────────────────────────────────────┐
│  项目级 intent/                                              │
│  - 愿景和目标                                                │
│  - 模块索引                                                  │
│  - 架构约束 (依赖、边界)                                      │
│  - 全局结构规范                                              │
├─────────────────────────────────────────────────────────────┤
│  模块级 intent/                                              │
│  - 模块职责                                                  │
│  - API 签名                                                  │
│  - 内部结构                                                  │
│  - 本模块特有规范                                            │
│                                                              │
│  ⚠️ Agent 在此范围内自主工作，不越界                          │
└─────────────────────────────────────────────────────────────┘
```

### 项目级 vs 模块级

| 内容 | 项目级 | 模块级 |
|-----|-------|-------|
| 愿景目标 | ✓ | - |
| 模块索引 | ✓ | - |
| 依赖关系 | ✓ | - |
| 边界规则 | ✓ | - |
| 模块职责 | - | ✓ |
| API 签名 | - | ✓ |
| 内部结构 | - | ✓ |
| 测试断言 | - | ✓ |

---

## 文件格式

### INTENT.md (入口)

```markdown
# <模块名> Intent

> 一句话定位

## 职责

- 做什么
- 不做什么

## 结构

\```
目录/数据结构图
\```

## API

### functionName(params)

**参数:** ...
**返回:** ...
**约束:** ...

## 示例

输入 → 输出
```

### DEPENDENCIES.md (依赖图)

```markdown
# 模块依赖

## 依赖图

\```
    API Layer
        │
   ┌────┴────┐
   ▼         ▼
 Deploy   Router
   │         │
   └────┬────┘
        ▼
    Chamber
        │
        ▼
       FS
\```

## 依赖矩阵

|          | Chamber | Deploy | Router | FS |
|----------|---------|--------|--------|-----|
| API      | ✓       | ✓      | ✓      | ✗   |
| Deploy   | ✓       | -      | ✗      | ✗   |
| Router   | ✓       | ✗      | -      | ✗   |
| Chamber  | -       | ✗      | ✗      | ✓   |

✓ 允许依赖  ✗ 禁止依赖  - 自身
```

### BOUNDARIES.md (边界规则)

```markdown
# 边界规则

## 原则

- 依赖单向：上层 → 下层
- 不越级访问
- 通过 API 通信，不直接访问内部

## 禁止模式

| 文件 | 禁止 | 原因 |
|-----|------|------|
| api.js | `join(appsDir, ...)` | 必须通过 Chamber API |
| deploy.js | `import.*route-engine` | 不允许跨模块 |

## 检查方法

\```bash
# 检测违规 import
grep -r "join.*appsDir" src/platforms/
\```
```

### Structure Spec (结构规范)

```markdown
# <名称> 结构规范

## 目录结构

\```
apps/my-app/
├── .chamber.yaml         # 说明
└── branches/
    └── <branch>/
        └── public/
\```

## 配置格式

### .chamber.yaml
\```yaml
default: main
\```

## 状态机 (如有)

\```
[created] → [running] → [stopped]
\```
```

---

## Agent 工作模式

### 区域自治

```
┌──────────────────────────────────────────────────────────────┐
│                     项目级 Agent                              │
│  - 读取 intent/INTENT.md 理解全局                             │
│  - 根据任务分配到具体模块                                      │
│  - 不直接修改模块内部代码                                      │
└──────────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│  Core Agent      │ │  Terminal Agent  │ │  CLI Agent       │
│                  │ │                  │ │                  │
│  读取:           │ │  读取:           │ │  读取:           │
│  core/intent/    │ │  terminal/intent/│ │  cli/intent/     │
│                  │ │                  │ │                  │
│  工作范围:       │ │  工作范围:       │ │  工作范围:       │
│  core/src/       │ │  terminal/src/   │ │  cli/src/        │
│  core/tests/     │ │  terminal/tests/ │ │  cli/tests/      │
└──────────────────┘ └──────────────────┘ └──────────────────┘
```

### 关键规则

1. **Agent 只在自己区域工作** - 不越界修改其他模块
2. **Agent 自主分解任务** - 不需要外部 task 文件
3. **Agent 遵循本地 intent** - 先读 intent，再规划
4. **跨模块需求上报** - 需要修改其他模块时，生成跨模块请求

---

## 最小化原则

### 必须有

- `intent/INTENT.md` - 项目入口
- `<module>/intent/INTENT.md` - 每个独立模块

### 按需添加

- `intent/architecture/` - 有多模块依赖时
- `intent/specs/` - 有复杂结构规范时
- `<module>/intent/*.md` - 模块内部有多个设计文档时

### 不需要

- Task 文件 - Agent 自主分解
- User Story 文件 - 直接描述行为
- 按 requirement 类型分类 - 按模块组织

---

## 演进路径

```
阶段 1: 最小化
├── intent/INTENT.md              # 项目入口
└── module/intent/INTENT.md       # 各模块

阶段 2: 添加架构约束
├── intent/
│   ├── INTENT.md
│   └── architecture/
│       ├── DEPENDENCIES.md       # 模块多了需要依赖图
│       └── BOUNDARIES.md

阶段 3: 添加结构规范
├── intent/
│   ├── INTENT.md
│   ├── architecture/
│   └── specs/
│       └── directory-structure.md  # 复杂结构需要规范
```

---

## 相关文档

- [intent-approval.md](intent-approval.md) - Section 级别的审批机制
- [methodology.md](methodology.md) - Intent vs SDD 方法论对比

---

## 版本历史

| 版本 | 日期 | 变更 |
|-----|------|------|
| 1.0 | 2026-01-19 | 初始版本 |
