# /intent-check

> 运行验证和同步检查

## 用法

```bash
/intent-check
/intent-check --validate    # 只做格式验证
/intent-check --sync        # 只做同步检查
```

## 目的

运行自动检查以确保 Intent 文件有效且与实现一致。自动触发验证 Agent。

## 何时使用

- 修改 Intent 文件后
- 提交变更前
- 作为 CI/CD 流水线的一部分
- 定期健康检查

## 执行的检查

### 1. 格式验证（`--validate`）

触发的 Agent：`intent-validate`

| 检查 | 描述 |
|------|------|
| 结构 | 必需章节是否存在 |
| 层级 | 正确的嵌套和组织 |
| 格式 | Markdown 语法，ASCII 图 |
| 标记 | 章节状态标记是否有效 |

### 2. 同步检查（`--sync`）

触发的 Agent：`intent-sync`

| 检查 | 描述 |
|------|------|
| API 匹配 | 签名与实现匹配 |
| 结构匹配 | 图表反映实际架构 |
| 命名 | 术语与代码一致 |
| 依赖 | 列出的依赖与实际导入匹配 |

## 输出格式

```
> /intent-check

运行 IDD 检查...

## 格式验证

检查 intent/INTENT.md...
✓ 结构：所有必需章节存在
✓ 层级：正确嵌套
✓ 格式：有效 markdown
⚠ 标记：1 个章节缺少状态标记

检查 intent/auth/INTENT.md...
✓ 所有检查通过

## 同步检查

比较 intent/auth/INTENT.md 与 src/auth/...
✓ API 签名匹配
✓ 结构匹配
⚠ 命名：Intent 写的是 "AuthService"，代码是 "AuthenticationService"
✓ 依赖匹配

## 总结

| 文件 | 格式 | 同步 | 状态 |
|------|------|------|------|
| intent/INTENT.md | ⚠ 1 警告 | - | 需要注意 |
| intent/auth/INTENT.md | ✓ 通过 | ⚠ 1 警告 | 需要注意 |

总计：2 警告，0 错误

运行 /intent-sync 修复同步问题。
```

## 退出码

用于 CI/CD 集成：

| 代码 | 含义 |
|------|------|
| 0 | 所有检查通过 |
| 1 | 发现警告 |
| 2 | 发现错误 |

## CI/CD 集成

### GitHub Actions

```yaml
- name: Check Intent
  run: |
    claude /intent-check
    if [ $? -eq 2 ]; then
      echo "Intent 检查失败"
      exit 1
    fi
```

### Pre-commit Hook

```bash
#!/bin/bash
# .git/hooks/pre-commit

if git diff --cached --name-only | grep -q "intent/"; then
  claude /intent-check --validate
  if [ $? -eq 2 ]; then
    echo "Intent 验证失败。提交前请修复错误。"
    exit 1
  fi
fi
```

## 严重性级别

| 级别 | 图标 | 含义 | 操作 |
|------|------|------|------|
| 通过 | ✓ | 检查通过 | 无 |
| 警告 | ⚠ | 小问题 | 应该修复 |
| 错误 | ✗ | 严重问题 | 必须修复 |

## 常见问题

### 格式问题

| 问题 | 修复 |
|------|------|
| 缺少章节 | 向 Intent 添加必需章节 |
| 无效状态标记 | 使用 `[draft]`、`[reviewed]` 或 `[locked]` |
| ASCII 图损坏 | 修复图表语法 |

### 同步问题

| 问题 | 修复 |
|------|------|
| API 不匹配 | 运行 `/intent-sync` |
| 命名不一致 | 更新 Intent 或代码使其匹配 |
| 缺少依赖 | 添加到 Intent 依赖章节 |

## 相关命令

- [/intent-sync](intent-sync.md) - 修复同步问题
- [/intent-review](intent-review.md) - 修复格式问题
- [/intent-build-now](intent-build-now.md) - 构建前验证

## 另请参阅

- [Agent 概述](../agents/overview.md) - 验证 Agent
- [Intent 标准](../intent-standard.md) - 格式规范
