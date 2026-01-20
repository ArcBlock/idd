# Intent Sync Agent

> 检查代码实现与 Intent 的一致性

## 触发场景

- 开发完成后，验证实现是否符合 Intent
- PR Review 时，检查变更是否在 Intent 范围内
- 定期同步检查

## 输入

```
{
  "intentPath": "src/core/intent/INTENT.md",
  "codePath": "src/core/src/",
  // 或
  "module": "core"  // 自动推断路径
}
```

## 检查维度

### 1. API 一致性

对比 Intent 中的 API 定义与实际代码：

| 检查项 | 说明 |
|--------|------|
| 函数存在性 | Intent 定义的函数是否都已实现 |
| 签名匹配 | 参数名、类型是否一致 |
| 返回值 | 返回类型是否符合 |
| 新增 API | 代码中有但 Intent 未记录的 |

### 2. 数据结构一致性

对比 Intent 中的数据结构与实际代码：

```
Intent 定义:
  Chamber {
    name: string
    branches: Branch[]
  }

实际代码:
  Chamber {
    name: string
    branches: Branch[]
    createdAt: Date    // ← 新增，Intent 未记录
  }
```

### 3. 行为一致性

检查 Intent 中描述的行为是否在代码中体现：

```
Intent: "删除 chamber 时移动到 .trash/"
Code: fs.rmSync(chamberPath)  // ← 不一致！直接删除
```

### 4. 边界规则

检查 BOUNDARIES.md 中的规则是否被遵守：

```
规则: "deploy.js 不允许直接 import router"
代码: import { matchRoute } from '../router'  // ← 违规！
```

## 输出

```markdown
# Intent Sync Report

## Module: core

### API 一致性

| API | Intent | Code | 状态 |
|-----|--------|------|------|
| `createChamber()` | ✓ | ✓ | ✅ 一致 |
| `deleteChamber()` | ✓ | ✓ | ⚠️ 签名差异 |
| `getChamberStats()` | ✗ | ✓ | 📝 新增未记录 |

### 签名差异详情

```diff
# deleteChamber
- Intent: deleteChamber(app, name)
+ Code:   deleteChamber(app, name, options)
```

### 数据结构差异

```diff
# Chamber
  {
    name: string
    branches: Branch[]
+   createdAt: Date      // 新增
+   metadata: object     // 新增
  }
```

### 边界规则检查

| 规则 | 状态 |
|------|------|
| deploy 不直接访问 router | ✅ 通过 |
| API 层通过 chamber.js | ⚠️ 1 处违规 |

### 行动建议

1. **更新 Intent** (推荐)
   - 添加 `getChamberStats()` API 文档
   - 补充 `createdAt`, `metadata` 字段

2. **修改代码**
   - `deleteChamber` 移除 options 参数（如果不需要）

3. **修复违规**
   - `routes/apps.js:45` 直接拼接路径，应使用 chamber.js API
```

## 同步模式

### 模式 1: Intent → Code (验证)

检查代码是否实现了 Intent 的要求。

### 模式 2: Code → Intent (发现)

发现代码中有但 Intent 未记录的内容。

### 模式 3: 双向同步

同时执行两个方向，生成完整差异报告。

## 与 Git 集成

```bash
# 检查本次 PR 的变更是否与 Intent 一致
intent-sync --git-diff origin/main
```

只检查变更涉及的模块，忽略未改动部分。
