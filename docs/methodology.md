# IDD Methodology

> Intent Driven Development - A methodology comparison and design rationale

[中文版](zh/methodology.md)

## Background

IDD (Intent Driven Development) emerged from the need to optimize development workflows for AI-assisted coding. This document explains the methodology and compares it with SDD (Spec Driven Development).

---

## Development Methodology Evolution

```
┌─────────────────────────────────────────────────────────────┐
│  Traditional                                                 │
│  Code → Test → Docs                                         │
│  Problem: Documentation often outdated or missing           │
├─────────────────────────────────────────────────────────────┤
│  SDD (Spec Driven Development)                              │
│  Spec → Code → Test                                         │
│  Problem: Specs become stale, split across many files       │
├─────────────────────────────────────────────────────────────┤
│  TDD (Test Driven Development)                              │
│  Test → Code → Docs                                         │
│  Problem: Tests don't capture design rationale              │
├─────────────────────────────────────────────────────────────┤
│  IDD (Intent Driven Development)                            │
│  Intent → Test → Code → Sync                                │
│  Intent captures "what" and "why", AI handles "how"         │
└─────────────────────────────────────────────────────────────┘
```

---

## SDD: What Works and What Doesn't

### Typical SDD Structure

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

### What SDD Gets Right

| Feature | Value | How IDD Adopts It |
|---------|-------|-------------------|
| **Spec/Task separation** | Spec is stable "what", Task is temporary "do" | Intent is spec, no task files needed |
| **Diagrams first** | More precise than prose, easier to review | ASCII diagrams for structure and dependencies |
| **Testability** | Specs can generate tests | Intent maps directly to test assertions |
| **Version tracking** | Specs have change history | Git tracks intent changes |

### What SDD Gets Wrong

| Feature | Problem | IDD Approach |
|---------|---------|--------------|
| **Requirement classification** | Splits complete patterns, LLM needs reassembly | Organize by module/layer, not by type |
| **User Story format** | "As a user, I want..." meaningless for system software | Describe behavior and constraints directly |
| **Task files** | LLM can decompose tasks itself | Not needed, let AI plan autonomously |
| **Rigid templates** | Forces filling inapplicable fields | Minimal structure, extend as needed |

---

## Core Problems with SDD

### 1. Classification Splits Patterns

SDD requires categorizing into:
- Functional Requirements
- UX Requirements
- Technical Requirements
- User Stories

**Problem**: This categorization might work for enterprise apps, but doesn't fit system software. More importantly, **excessive splitting fragments complete patterns that LLMs can reason about holistically**.

LLMs excel at understanding complete context. Forced splitting increases cognitive load.

### 2. User Story Limitations

```
"As a user, I want to login so that I can access my account"
```

For system software (like a chamber module), this format is meaningless. There's no "user" - only module interactions.

### 3. Task File Redundancy

SDD maintains separate task files, but LLMs can:
1. Read spec/intent
2. Decompose tasks autonomously
3. Plan execution order

Extra task files only add maintenance cost.

---

## The IDD Approach

### Core Formula

```
Intent = Structure Diagrams + Constraint Rules + Examples

NOT: Functional desc + UX req + Technical req + User stories
```

### Three-Layer Structure

```
┌─────────────────────────────────────────────────────────────┐
│  Layer 1: Structure Diagrams                                │
│  - Directory structure, data structures, module relations   │
│  - ASCII diagrams primary, text secondary                   │
│  - LLM can "see" and understand the system                  │
├─────────────────────────────────────────────────────────────┤
│  Layer 2: Constraint Rules                                  │
│  - Dependency direction, boundary rules, invariants         │
│  - Table or list format                                     │
│  - Directly convertible to lint rules or test assertions    │
├─────────────────────────────────────────────────────────────┤
│  Layer 3: Behavior Examples                                 │
│  - Concrete input → output examples                         │
│  - Edge cases                                               │
│  - Directly convertible to test cases                       │
└─────────────────────────────────────────────────────────────┘
```

### Organization

```
intent/
├── INTENT.md                    # Project overview (entry point)
│
├── core/                        # By module, not by type
│   ├── chamber/
│   │   └── INTENT.md            # Structure + API + Examples
│   ├── router/
│   └── deploy/
│
└── architecture/                # Architecture-level constraints
    ├── DEPENDENCIES.md          # Dependency graph
    └── BOUNDARIES.md            # Boundary rules
```

---

## Key Differences Summary

| Dimension | SDD | IDD |
|-----------|-----|-----|
| **Organization** | By requirement type | By module/layer |
| **Core artifact** | Text descriptions | Structure diagrams |
| **Granularity** | Split into user stories | Keep complete patterns |
| **Task management** | Separate task files | None - AI decomposes |
| **Scope** | Enterprise applications | System software + apps |
| **LLM friendliness** | Needs context assembly | Complete pattern at once |

---

## IDD Design Principles

1. **Diagrams First** - ASCII diagrams are more precise; both LLMs and humans understand quickly
2. **Organize by Module** - Not by requirement type; keep patterns complete
3. **Testable Constraints** - Every constraint should convert to test assertions or lint rules
4. **Minimal Templates** - Don't force filling inapplicable fields
5. **AI Autonomous Decomposition** - No task files; let AI plan execution

---

## When to Use IDD

**Good fit:**
- System software (frameworks, libraries, infrastructure)
- AI-assisted development workflows
- Projects where LLMs are primary implementers
- Codebases needing strict architectural boundaries

**May not fit:**
- Highly regulated industries requiring traditional documentation
- Teams without AI tooling
- Projects with non-technical stakeholders needing user stories

---

## Version History

| Date | Changes |
|------|---------|
| 2026-01-19 | Initial version |
