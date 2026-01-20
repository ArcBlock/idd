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
│  Creation                                                    │
│  ┌───────────────────┐                                       │
│  │ /intent-interview │ → Create INTENT.md from ideas         │
│  └───────────────────┘                                       │
│                                                              │
│  Quality                                                     │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-validate   │  │ /intent-review    │               │
│  │   (subagent)      │  │   Review & Approve │               │
│  └───────────────────┘  └───────────────────┘               │
│                                                              │
│  Sync                                                        │
│  ┌───────────────────┐  ┌───────────────────┐               │
│  │ intent-sync       │  │ intent-audit      │               │
│  │   Code consistency │  │   Project health  │               │
│  │   (subagent)      │  │   (subagent)      │               │
│  └───────────────────┘  └───────────────────┘               │
└─────────────────────────────────────────────────────────────┘
```

## Installation

```bash
# Add to Claude Code settings
claude mcp add-plugin ~/path/to/idd
```

## Commands

### Skills (Interactive)

| Command | Description |
|---------|-------------|
| `/intent-interview` | Create complete INTENT.md through structured interviewing |
| `/intent-review` | Review and approve Intent sections (locked/reviewed/draft) |

### Subagents (Autonomous)

| Agent | Trigger | Output |
|-------|---------|--------|
| `intent-validate` | After Intent modification | Compliance report |
| `intent-sync` | After implementation | Code-Intent diff report |
| `intent-audit` | Periodic check | Project health report |

## Intent File Structure

See [docs/intent-standard.md](docs/intent-standard.md)

## Section Approval Mechanism

See [docs/intent-approval.md](docs/intent-approval.md)

## Relationship to AINE

IDD is a core practice of the [AINE (AI Native Engineering)](https://github.com/ArcBlock/aine) methodology.

```
AINE Methodology
├── IDD (Intent Driven Development)  ← This plugin
├── Contract Semantics (satisfied/violated/degraded)
├── TDD First
├── Chamber Architecture
└── Human-in-the-loop
```

## License

MIT
