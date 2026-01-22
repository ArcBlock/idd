# IDD Agents Overview

> Autonomous agents that power Intent-Driven Development

## What Are IDD Agents?

IDD agents are specialized AI agents that work autonomously to validate, implement, and verify code based on Intent documents. Unlike interactive skills (commands), agents work in the background with minimal user intervention.

## Agent Categories

### Validation Agents

These agents ensure Intent quality and consistency:

| Agent | Purpose | Trigger |
|-------|---------|---------|
| [intent-validate](intent-validate.md) | Format compliance | After Intent modification |
| [intent-sync](intent-sync.md) | Implementation consistency | After code changes |
| [intent-audit](intent-audit.md) | Project health | Periodic / on-demand |

### TDD Execution Agents

These agents form the TDD team that builds code from Intent:

| Agent | Role | In Workflow |
|-------|------|-------------|
| [idd-task-execution-master](idd-task-execution-master.md) | Phase planning | First: breaks Intent into phases |
| [idd-test-master](idd-test-master.md) | Test design | Second: writes tests before code |
| [idd-code-guru](idd-code-guru.md) | Implementation | Third: implements to pass tests |
| [idd-e2e-test-queen](idd-e2e-test-queen.md) | E2E verification | Fourth: validates end-to-end |

## TDD Agent Team Workflow

```
┌─────────────────────────────────────────────────────────────────────┐
│                        TDD Agent Team                                │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                 idd-task-execution-master                     │   │
│  │                                                               │   │
│  │  Input: Approved Intent document                              │   │
│  │  Output: Phased execution plan with tasks                     │   │
│  │                                                               │   │
│  │  • Validates Intent completeness                              │   │
│  │  • Breaks work into logical phases                            │   │
│  │  • Defines completion criteria                                │   │
│  │  • Coordinates other agents                                   │   │
│  └───────────────────────────┬──────────────────────────────────┘   │
│                              │                                       │
│                              ▼                                       │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                     idd-test-master                           │   │
│  │                                                               │   │
│  │  Input: Task definition from execution-master                 │   │
│  │  Output: Comprehensive test specification                     │   │
│  │                                                               │   │
│  │  • Happy path tests                                           │   │
│  │  • Bad path tests (detailed, comprehensive)                   │   │
│  │  • Edge case tests                                            │   │
│  │  • Security tests                                             │   │
│  │  • Data leak tests                                            │   │
│  │  • Data damage tests                                          │   │
│  └───────────────────────────┬──────────────────────────────────┘   │
│                              │                                       │
│                              ▼                                       │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                      idd-code-guru                            │   │
│  │                                                               │   │
│  │  Input: Test specification from test-master                   │   │
│  │  Output: Elegant implementation that passes all tests         │   │
│  │                                                               │   │
│  │  • Clean, maintainable code                                   │   │
│  │  • Follows project patterns                                   │   │
│  │  • No code duplication                                        │   │
│  │  • Proper naming and structure                                │   │
│  └───────────────────────────┬──────────────────────────────────┘   │
│                              │                                       │
│                              ▼                                       │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                   idd-e2e-test-queen                          │   │
│  │                                                               │   │
│  │  Input: Completed phase implementation                        │   │
│  │  Output: E2E validation results                               │   │
│  │                                                               │   │
│  │  • End-to-end test design                                     │   │
│  │  • CLI-based verification preferred                           │   │
│  │  • Phase gate validation                                      │   │
│  │  • Integration testing                                        │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

## Key Principles

### 1. Tests First, Always

The TDD agents enforce strict test-first development:

```
WRONG: Code → Tests → Fix
RIGHT: Tests → Code → Verify
```

No agent will write implementation code before tests exist.

### 2. Immutable Test Contracts

Tests designed by `idd-test-master` are contracts:

- Cannot be modified to make code pass
- Code must be fixed, not tests
- Exceptions require explicit approval

### 3. Phase Gates

Each phase ends with E2E verification:

```
Phase 1: Core ──────▶ E2E Gate ──────▶ Phase 2: Integration
                         │
                         ▼
                    All tests pass?
                    ├── Yes: Continue
                    └── No: Fix first
```

### 4. Agent Autonomy

Agents work within their scope:

- Task-execution-master: Planning only
- Test-master: Test design only
- Code-guru: Implementation only
- E2E-test-queen: Verification only

No agent crosses into another's domain.

## Triggering Agents

### Automatic (via /intent-build-now)

```bash
/intent-build-now
```

This validates Intent and orchestrates the full agent team.

### Manual (via Task tool)

```bash
# Launch specific agent
Task: idd-test-master
Prompt: "Design tests for the authentication module based on this Intent: ..."
```

### Via /intent-check

```bash
/intent-check
```

Triggers validation agents automatically.

## Agent Communication

Agents pass structured information:

```
task-execution-master ──▶ test-master
{
  "task": "P1-T01",
  "title": "Token Validation",
  "scope": "src/auth/validator.ts",
  "requirements": [...]
}

test-master ──▶ code-guru
{
  "task": "P1-T01",
  "tests": [
    { "name": "validates correct token", "type": "happy" },
    { "name": "rejects expired token", "type": "bad" },
    ...
  ],
  "testFile": "tests/auth/validator.test.ts"
}
```

## Best Practices

### 1. Trust the Process

Let agents work autonomously. Intervene only when asked.

### 2. Provide Complete Intent

Agents work best with complete, unambiguous Intent documents.

### 3. Review Phase Gates

Check E2E results before proceeding to next phase.

### 4. Don't Skip Agents

The chain works together. Skipping test-master undermines the whole process.

## Next Steps

- [idd-task-execution-master](idd-task-execution-master.md) - Phase planning
- [idd-test-master](idd-test-master.md) - Test design
- [idd-code-guru](idd-code-guru.md) - Implementation
- [idd-e2e-test-queen](idd-e2e-test-queen.md) - E2E verification

## See Also

- [IDD Workflow](../workflow.md) - Agents in context
- [/intent-build-now](../commands/intent-build-now.md) - Launching agents
