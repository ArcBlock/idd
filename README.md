# IDD - Intent Driven Development

> Complete toolkit for Intent-driven development

[中文文档](./docs/zh/README.md)

## Philosophy

```
Traditional:  Code → Test → Documentation
SDD:          Spec → Code → Test              (Spec as reference)
TDD:          Test → Code → Documentation     (Test as contract)
IDD:          Intent → Test → Code → Sync     (Intent as source of truth)
```

**Intent is the new source code.** Code review is done by AI, Intent review is done by Humans.

### Why not SDD?

| Aspect | SDD | IDD |
|--------|-----|-----|
| Organization | By requirement type (functional, UX, technical) | By module/layer |
| Core artifact | Text descriptions | Structure diagrams |
| Granularity | Split into user stories | Keep complete patterns |
| Task management | Separate task files | None - AI decomposes autonomously |
| LLM friendliness | Needs context assembly | Understands complete pattern at once |

See [docs/methodology.md](docs/methodology.md) for detailed comparison.

## Toolkit Overview

```
┌─────────────────────────────────────────────────────────────┐
│                      IDD Lifecycle                           │
│                                                              │
│  Setup                                                       │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-assess    │  │ /intent-init      │               │
│  │   Evaluate fit    │  │   Initialize IDD  │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Creation                                                    │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-interview │  │ /intent-critique  │               │
│  │   Create Intent   │  │   Review quality  │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Review                                                      │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-review    │  │ /intent-changes   │               │
│  │   Approve sections│  │   Propose changes │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Execution                                                   │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-build-now │  │ /intent-plan      │               │
│  │   Validate & build│  │   TDD plan        │               │
│  └───────────────────┘  └───────────────────┘               │
│           │                                                  │
│           ▼                                                  │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  TDD Agent Team (Autonomous Execution)              │    │
│  │                                                     │    │
│  │  idd-task-execution-master ──→ Phase planning       │    │
│  │           │                                         │    │
│  │           ▼                                         │    │
│  │  idd-test-master ──→ Test-first design              │    │
│  │           │                                         │    │
│  │           ▼                                         │    │
│  │  idd-code-guru ──→ Elegant implementation           │    │
│  │           │                                         │    │
│  │           ▼                                         │    │
│  │  idd-e2e-test-queen ──→ E2E verification            │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  Sync & Validate                                             │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-sync      │  │ /intent-check     │               │
│  │   Sync back       │  │   Run checks      │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Report & Share                                              │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-report    │  │ /intent-story     │               │
│  │   Generate docs   │  │   Share experience│               │
│  └───────────────────┘  └───────────────────┘               │
└─────────────────────────────────────────────────────────────┘
```

## Installation

```bash
# Quick install
npx add-skill arcblock/idd

# Or manual install
git clone https://github.com/ArcBlock/idd ~/path/to/idd
claude mcp add-plugin ~/path/to/idd
```

## Commands

### Skills (Interactive)

| Command | Description |
|---------|-------------|
| `/intent-assess` | Evaluate if IDD fits your project, learn IDD methodology |
| `/intent-init` | Initialize IDD structure in project (check existing, create templates) |
| `/intent-interview` | Create complete INTENT.md through structured interviewing |
| `/intent-critique` | Critical review for over-engineering, YAGNI violations, simplification |
| `/intent-changes` | Structured change proposals with PR-like review experience |
| `/intent-review` | Review and approve Intent sections (locked/reviewed/draft) |
| `/intent-build-now` | **Validate Intent completeness, then launch TDD execution** |
| `/intent-plan` | Generate phased execution plan with strict TDD |
| `/intent-sync` | After implementation, sync finalized details back to Intent |
| `/intent-check` | Run validation and sync checks (triggers agents) |
| `/intent-report` | Generate human-readable reports from Intent files |
| `/intent-story` | Share your IDD experience, create blog posts (multi-language) |

### Agents (Autonomous)

#### Validation Agents

| Agent | Trigger | Output |
|-------|---------|--------|
| `intent-validate` | After Intent modification | Format compliance report |
| `intent-sync` | After implementation | Implementation consistency check |
| `intent-audit` | Periodic check | Project health report |

#### TDD Execution Agents

| Agent | Role | Description |
|-------|------|-------------|
| `idd-task-execution-master` | Phase Planning | Transform Intent into phased TDD execution plan |
| `idd-test-master` | Test Design | Define comprehensive test specs before implementation |
| `idd-code-guru` | Implementation | Write elegant code that passes all tests |
| `idd-e2e-test-queen` | E2E Verification | Design and validate end-to-end tests |

## Workflow

```
/intent-assess            # 1. Evaluate project fit
    ↓
/intent-init              # 2. Initialize IDD structure
    ↓
/intent-interview         # 3. Create Intent from ideas
    ↓
/intent-critique          # 4. Review for over-engineering (optional)
    ↓
/intent-review            # 5. Approve critical sections
    ↓
/intent-build-now         # 6. Validate & start building
    │
    ├──→ idd-task-execution-master (phase planning)
    │         ↓
    ├──→ idd-test-master (test-first design)
    │         ↓
    ├──→ idd-code-guru (implementation)
    │         ↓
    └──→ idd-e2e-test-queen (E2E verification)
    ↓
/intent-sync              # 7. Sync finalized details back to Intent
    ↓
/intent-check             # 8. Validate consistency
    ↓
/intent-report            # 9. Generate documentation
    ↓
/intent-story             # 10. Share your experience (optional)
```

### Quick Start: From Intent to Code

```bash
# Have an Intent ready? Start building immediately:
/intent-build-now

# This will:
# 1. Validate your Intent completeness
# 2. Report any gaps that need fixing
# 3. If ready, launch the TDD agent team
```

## Documentation

| Document | Description |
|----------|-------------|
| [docs/methodology.md](docs/methodology.md) | IDD vs SDD detailed comparison |
| [docs/intent-standard.md](docs/intent-standard.md) | Intent file format specification |
| [docs/intent-approval.md](docs/intent-approval.md) | Section approval mechanism |

## Blog

| Article | Language |
|---------|----------|
| [Intent Is the New Source Code](docs/blog/idd-intent-is-new-source-code-en.md) | English |
| [AI 时代别再写需求文档了，写 Intent](docs/blog/idd-intent-is-new-source-code-zh.md) | 中文 |

## License

MIT
