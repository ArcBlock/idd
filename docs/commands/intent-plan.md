# /intent-plan

> Generate phased execution plan with strict TDD

## Usage

```bash
/intent-plan
/intent-plan path/to/INTENT.md
```

## Purpose

Transforms an approved Intent into a structured, executable development plan with strict TDD discipline. Unlike `/intent-build-now`, this generates a plan for manual execution rather than automatic agent orchestration.

## When to Use

- Want to review the plan before execution
- Prefer manual control over implementation
- Need to share plan with team
- Learning IDD workflow step by step

## Plan Structure

```
Phase 1: [Phase Name]
├── Step 1.1: [Feature/Component]
│   ├── Unit 1: Write Tests
│   │   ├── Happy path cases
│   │   ├── Bad path cases
│   │   ├── Edge cases
│   │   ├── Security tests
│   │   ├── Data leak tests
│   │   └── Data damage tests
│   └── Unit 2: Implementation
│       └── Make all tests pass
├── Step 1.2: [Next Feature]
│   └── ...
└── Phase Gate: E2E Verification
    └── CLI/Script based validation

Phase 2: [Phase Name]
└── ...
```

## Test Categories

Every step requires comprehensive test coverage:

| Category | Purpose | Examples |
|----------|---------|----------|
| **Happy Path** | Normal usage | Valid inputs, correct sequences |
| **Bad Path** | Error conditions | Wrong types, missing fields |
| **Edge Cases** | Boundary conditions | Empty inputs, max values |
| **Security** | Vulnerability prevention | Injection, auth bypass |
| **Data Leak** | Information exposure | Sensitive data in logs |
| **Data Damage** | Data integrity | Partial writes, corruption |

## Output: PLAN.md

```markdown
# Implementation Plan for [Project/Feature]

Generated from: `intent/[name]/INTENT.md`
Date: 2024-01-21

## Overview

- Total Phases: 3
- Complexity: Medium
- Key Dependencies: auth-service, database

## Phase 1: Core Functionality

**Goal**: Basic payment processing works

### Step 1.1: Payment Validation

**Unit 1: Tests** (Do First)

| Category | Test Cases |
|----------|------------|
| Happy Path | Valid amount processes successfully |
| Bad Path | Negative amount rejected |
| Bad Path | Zero amount rejected |
| Edge Cases | Maximum amount (system limit) |
| Security | SQL injection in metadata |
| Data Leak | Card number not in logs |

**Unit 2: Implementation**

- [ ] Implement validatePayment()
- [ ] Ensure all tests pass

### Step 1.2: Payment Processing

[...]

### Phase 1 Gate: E2E Verification

\```bash
# Verify payment flow
curl -X POST http://localhost:3000/api/payments \
  -H "Content-Type: application/json" \
  -d '{"amount": 1000, "currency": "USD"}' | jq .
\```

**Success Criteria:**
- [ ] Payment created successfully
- [ ] Correct status returned
- [ ] Database record exists

---

## Phase 2: Error Handling

[...]
```

## Example Session

```
> /intent-plan intent/payment/INTENT.md

Reading Intent...
Analyzing scope and complexity...

## Execution Plan Generated

### Phase Overview

| Phase | Objective | Tasks |
|-------|-----------|-------|
| 1 | Core Processing | 3 |
| 2 | Error Handling | 2 |
| 3 | Integration | 2 |

### Phase 1: Core Processing

Step 1.1: Payment Validation
- 12 test cases identified
- Implementation scope: 1 file

Step 1.2: Payment Execution
- 8 test cases identified
- Implementation scope: 2 files

Step 1.3: Receipt Generation
- 6 test cases identified
- Implementation scope: 1 file

Phase Gate: Verify via CLI that a payment can be processed

[Full plan continues...]

Plan saved to: intent/payment/PLAN.md

Next steps:
1. Review the plan
2. Start Phase 1, Step 1.1
3. Write tests first, then implement
4. Run phase gate verification before Phase 2
```

## vs /intent-build-now

| Aspect | /intent-plan | /intent-build-now |
|--------|--------------|-------------------|
| Output | PLAN.md file | Automatic execution |
| Control | Manual | Agent-driven |
| Use case | Review first | Trust the process |
| Learning | Better for beginners | Better for experienced |

## Best Practices

1. **Right-size phases** - Each completable in 1-3 days
2. **Clear dependencies** - Note step prerequisites
3. **Specific test cases** - "Test 404 response" not "test errors"
4. **Automatable gates** - CLI verification preferred

## Related Commands

- [/intent-build-now](intent-build-now.md) - Automatic execution
- [/intent-review](intent-review.md) - Approve before planning
- [/intent-sync](intent-sync.md) - Sync after execution

## See Also

- [IDD Workflow](../workflow.md) - Planning in context
- [Agents Overview](../agents/overview.md) - TDD agent team
