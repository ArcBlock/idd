# IDD Workflow Guide

> From idea to implementation with Intent-Driven Development

## Overview

IDD (Intent-Driven Development) follows a structured workflow where **Intent is the source of truth**. Unlike traditional development where code drives everything, IDD puts human-readable Intent documents at the center, with AI handling the implementation details.

```
┌─────────────────────────────────────────────────────────────────────┐
│                         IDD Workflow                                 │
│                                                                      │
│   DEFINE          REFINE           BUILD            MAINTAIN         │
│                                                                      │
│  ┌──────┐       ┌──────┐        ┌──────┐         ┌──────┐          │
│  │Assess│──────▶│Create│───────▶│Build │────────▶│ Sync │          │
│  └──────┘       └──────┘        └──────┘         └──────┘          │
│                                                                      │
│  Is IDD right?   Write Intent    TDD execution    Keep in sync      │
│  Setup project   Review quality  Agent team       Validate health   │
│                  Approve sections                                    │
└─────────────────────────────────────────────────────────────────────┘
```

## Phase 1: Define

### Step 1.1: Assess Project Fit

Before adopting IDD, evaluate if it's right for your project.

```bash
/intent-assess
```

**Good fit:**
- New features or modules
- Complex business logic
- Team collaboration needed
- Long-term maintenance expected

**Less suitable:**
- Quick prototypes
- One-off scripts
- Purely mechanical refactoring

See: [/intent-assess command](commands/intent-assess.md)

### Step 1.2: Initialize IDD Structure

Set up the Intent directory structure in your project.

```bash
/intent-init
```

This creates:
```
project/
└── intent/
    └── INTENT.md    # Your first Intent file
```

See: [/intent-init command](commands/intent-init.md)

## Phase 2: Refine

### Step 2.1: Create Intent

Transform your ideas into a structured Intent document through guided interviewing.

```bash
/intent-interview
```

The interview covers:
- **Responsibilities**: What it does and doesn't do
- **Structure**: Component diagrams (ASCII art)
- **API**: Function signatures and contracts
- **Examples**: Input → Output mappings

See: [/intent-interview command](commands/intent-interview.md)

### Step 2.2: Critique Design (Optional)

Review your Intent for over-engineering and YAGNI violations.

```bash
/intent-critique
```

This catches:
- Premature abstractions
- Unnecessary complexity
- Features you won't need

See: [/intent-critique command](commands/intent-critique.md)

### Step 2.3: Review and Approve

Approve Intent sections to lock them as implementation contracts.

```bash
/intent-review
```

Section states:
- **draft**: Work in progress
- **reviewed**: Examined but not finalized
- **locked**: Approved, ready for implementation

See: [/intent-review command](commands/intent-review.md)

### Step 2.4: Propose Changes (When Needed)

For collaborative review with PR-like experience.

```bash
/intent-changes
```

See: [/intent-changes command](commands/intent-changes.md)

## Phase 3: Build

### Step 3.1: Validate and Start Building

The key command that bridges Intent to implementation.

```bash
/intent-build-now
```

This command:
1. **Validates** Intent completeness
2. **Reports** any gaps that need fixing
3. **Launches** the TDD agent team when ready

See: [/intent-build-now command](commands/intent-build-now.md)

### Step 3.2: TDD Agent Team Execution

Once `/intent-build-now` validates your Intent, it orchestrates four specialized agents:

```
┌─────────────────────────────────────────────────────────────┐
│                    TDD Agent Team                            │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-task-execution-master                          │    │
│  │  Breaks Intent into phases with clear deliverables  │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        ▼                                     │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-test-master                                    │    │
│  │  Designs comprehensive tests BEFORE implementation  │    │
│  │  - Happy path, Bad path, Edge cases                 │    │
│  │  - Security, Data leak, Data damage tests           │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        ▼                                     │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-code-guru                                      │    │
│  │  Implements elegant code that passes all tests      │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        ▼                                     │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  idd-e2e-test-queen                                 │    │
│  │  Validates with end-to-end tests                    │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

See: [Agents Overview](agents/overview.md)

### Alternative: Manual Planning

If you prefer manual control, generate a plan without automatic execution:

```bash
/intent-plan
```

See: [/intent-plan command](commands/intent-plan.md)

## Phase 4: Maintain

### Step 4.1: Sync Implementation Details

After implementation, sync confirmed details back to Intent.

```bash
/intent-sync
```

This captures:
- Finalized API signatures
- Actual data structures
- Implementation decisions

See: [/intent-sync command](commands/intent-sync.md)

### Step 4.2: Validate Consistency

Run checks to ensure Intent and implementation stay aligned.

```bash
/intent-check
```

This triggers validation agents automatically.

See: [/intent-check command](commands/intent-check.md)

### Step 4.3: Generate Reports

Create human-readable documentation from Intent files.

```bash
/intent-report
```

See: [/intent-report command](commands/intent-report.md)

### Step 4.4: Share Experience (Optional)

Document your IDD journey for others.

```bash
/intent-story
```

See: [/intent-story command](commands/intent-story.md)

## Quick Reference

### Typical New Feature Flow

```bash
/intent-interview     # Create Intent from your idea
/intent-critique      # Check for over-engineering
/intent-review        # Approve key sections
/intent-build-now     # Validate and start TDD execution
/intent-sync          # Sync back when done
```

### Existing Project Adoption

```bash
/intent-assess        # Evaluate fit
/intent-init          # Set up structure
/intent-interview     # Document existing modules
```

### Health Check

```bash
/intent-check         # Run all validations
```

## Next Steps

- [Command Reference](commands/) - Detailed documentation for each command
- [Agent Documentation](agents/) - How the TDD agents work
- [FAQ](faq.md) - Common questions and answers
- [Intent Standard](intent-standard.md) - File format specification
