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
│  │ /intent-interview │  │ /intent-review    │               │
│  │   Create Intent   │  │   Approve sections│               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Validation                                                  │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ /intent-check     │  │ intent-validate   │               │
│  │   Run checks      │  │   (auto agent)    │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Sync & Report                                               │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-sync       │  │ /intent-report    │               │
│  │   (auto agent)    │  │   Generate docs   │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Health & Share                                              │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-audit      │  │ /intent-story     │               │
│  │   (auto agent)    │  │   Share experience│               │
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
| `/intent-review` | Review and approve Intent sections (locked/reviewed/draft) |
| `/intent-check` | Run validation and sync checks (triggers agents) |
| `/intent-report` | Generate human-readable reports from Intent files |
| `/intent-story` | Share your IDD experience, create blog posts (multi-language) |

### Agents (Autonomous)

| Agent | Trigger | Output |
|-------|---------|--------|
| `intent-validate` | After Intent modification | Format compliance report |
| `intent-sync` | After implementation | Code-Intent diff report |
| `intent-audit` | Periodic check | Project health report |

## Workflow

```
/intent-assess            # 1. Evaluate project fit
    ↓
/intent-init              # 2. Initialize IDD structure
    ↓
/intent-interview         # 3. Create Intent from ideas
    ↓
/intent-review            # 4. Approve critical sections
    ↓
[Development]             # 5. Code (AI follows Intent)
    ↓
/intent-check             # 6. Validate consistency
    ↓
/intent-report            # 7. Generate documentation
    ↓
/intent-story             # 8. Share your experience (optional)
```

## Documentation

| Document | Description |
|----------|-------------|
| [docs/methodology.md](docs/methodology.md) | IDD vs SDD detailed comparison |
| [docs/intent-standard.md](docs/intent-standard.md) | Intent file format specification |
| [docs/intent-approval.md](docs/intent-approval.md) | Section approval mechanism |

## License

MIT
