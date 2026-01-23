# /intent-report

> 从 Intent 文件生成人类可读的报告

## 用法

```bash
/intent-report
/intent-report --format html
/intent-report --format pdf
/intent-report --output docs/
```

## 目的

将技术性 Intent 规格转换为可读文档，供利益相关者、团队成员或项目文档使用。

## 何时使用

- 与非技术利益相关者分享 Intent
- 创建项目文档
- 生成 API 文档
- 团队入职材料

## 输出格式

| 格式 | 用例 |
|------|------|
| **markdown** | 默认，用于文档网站 |
| **html** | 独立网页 |
| **pdf** | 可打印文档 |

## 报告结构

```markdown
# [项目/功能] 规格

从 Intent 文件生成于 [日期]

## 执行摘要

[从愿景章节自动生成]

## 做什么

[来自职责 - 做什么]

## 不做什么

[来自职责 - 不做什么]

## 架构

[结构图转换为图像或保留为代码块]

## API 参考

[API 章节格式化为文档]

### 函数名

**目的：** [从上下文提取]

**参数：**
| 名称 | 类型 | 描述 |
|------|------|------|
| ... | ... | ... |

**返回：** ...

**示例：**
\```
[来自示例章节]
\```

## 依赖

[依赖章节作为表格]

## 约束与限制

[约束章节]

---
*由 IDD /intent-report 生成*
```

## 示例会话

```
> /intent-report intent/payment/INTENT.md --format html

生成报告...

读取 Intent 文件：
- intent/payment/INTENT.md
- intent/payment/architecture/DEPENDENCIES.md

处理章节...
✓ 愿景已提取
✓ 职责已格式化
✓ 结构图已处理
✓ API 文档已生成
✓ 示例已格式化

输出：docs/payment-specification.html

报告生成成功。

预览：file:///path/to/docs/payment-specification.html
```

## 选项

| 选项 | 描述 | 默认值 |
|------|------|--------|
| `--format` | 输出格式（markdown/html/pdf） | markdown |
| `--output` | 输出目录 | 当前目录 |
| `--include-private` | 包含草稿章节 | false |
| `--toc` | 生成目录 | true |

## 多文件报告

用于项目级报告：

```bash
/intent-report intent/ --format html
```

这会生成一个组合报告，包含：
- 来自 `intent/INTENT.md` 的项目概述
- 每个模块 Intent 的模块章节
- 来自架构文件的依赖图

## 自定义

### 报告模板

将自定义模板放在 `intent/.templates/`：

```
intent/
├── .templates/
│   ├── report-header.md
│   ├── report-footer.md
│   └── section-api.md
└── INTENT.md
```

### 排除章节

添加到 Intent frontmatter：

```markdown
---
report:
  exclude:
    - internal-notes
    - draft-ideas
---
```

## 用例

### 利益相关者文档

```bash
/intent-report --format pdf --output stakeholder-docs/
```

### API 文档网站

```bash
/intent-report intent/api/ --format html --output docs/api/
```

### 团队入职

```bash
/intent-report intent/ --format markdown --output wiki/
```

## 相关命令

- [/intent-interview](intent-interview.md) - 创建要报告的 Intent
- [/intent-story](intent-story.md) - 分享经验，而非规格

## 另请参阅

- [Intent 标准](../intent-standard.md) - 源格式
- [IDD 工作流程](../workflow.md) - 报告在上下文中的位置
