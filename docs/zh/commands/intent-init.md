# /intent-init

> 在项目中初始化 IDD 结构

## 用法

```bash
/intent-init
/intent-init --force    # 覆盖现有结构
```

## 目的

在项目中设置 Intent 目录结构和模板，为 Intent 驱动开发做准备。

## 何时使用

- 在新项目中启动 IDD
- 为现有代码库添加 IDD
- 重置 Intent 结构（使用 `--force`）

## 创建的内容

### 基本结构

```
project/
└── intent/
    ├── INTENT.md              # 项目级 Intent（模板）
    └── architecture/          # （多模块时创建）
        ├── DEPENDENCIES.md    # 模块依赖图
        └── BOUNDARIES.md      # 边界规则
```

### INTENT.md 模板

```markdown
# [项目名称] Intent

> 一句话项目描述

## 愿景

这个项目旨在实现什么。

## 职责

### 做什么
-

### 不做什么
-

## 结构

\```
[组件的 ASCII 图]
\```

## 模块

| 模块 | 位置 | 描述 |
|------|------|------|
| | | |

## 依赖

-

## 约束

-
```

## 行为

### 新项目

创建带有模板的完整结构。

### 现有项目

1. 检查现有的 `intent/` 目录
2. 报告已存在的内容
3. 提供添加缺失部分的选项
4. 不使用 `--force` 不会覆盖

### 多模块检测

如果项目有多个包/模块，还会创建：
- `intent/architecture/DEPENDENCIES.md`
- `intent/architecture/BOUNDARIES.md`

## 示例会话

```
> /intent-init

检查项目结构...

## 当前状态

- intent/ 目录：未找到
- 包结构：包含 3 个包的 Monorepo

## 操作

创建 IDD 结构...

✓ 已创建 intent/INTENT.md
✓ 已创建 intent/architecture/DEPENDENCIES.md
✓ 已创建 intent/architecture/BOUNDARIES.md

## 下一步

1. 编辑 intent/INTENT.md 填写项目愿景
2. 运行 /intent-interview 交互式填充细节
3. 为每个模块创建模块级 Intent：
   - packages/core/intent/INTENT.md
   - packages/api/intent/INTENT.md
   - packages/cli/intent/INTENT.md
```

## 选项

| 选项 | 描述 |
|------|------|
| `--force` | 覆盖现有 Intent 文件 |

## 相关命令

- [/intent-assess](intent-assess.md) - 先评估项目适配性
- [/intent-interview](intent-interview.md) - 交互式填充 Intent

## 另请参阅

- [Intent 标准](../intent-standard.md) - 文件格式规范
- [IDD 工作流程](../workflow.md) - 完整工作流程指南
