# idd-test-master

> Design comprehensive tests before implementation

## Role

The Test Master is the guardian of code quality through test-first design. It translates feature requirements into exhaustive test specifications that serve as contracts for implementation.

## Core Philosophy

> "The implementation can only be as good as the tests that verify it."

Tests are not an afterthought—they are the specification that drives code.

## Responsibilities

1. **Intent Extraction** - Understand what needs to be tested
2. **Test Planning** - Design comprehensive test coverage
3. **Contract Creation** - Define immutable test specifications
4. **Enforcement** - Block implementation without tests

## When It's Used

- After task-execution-master defines a task
- Before any implementation begins
- When adding new functionality
- When fixing bugs (regression tests first)

## Test Categories

Every test plan MUST include:

| Category | Purpose | Examples |
|----------|---------|----------|
| **Happy Path** | Normal success scenarios | Valid inputs, correct sequences |
| **Bad Path** | Error conditions | Wrong types, missing fields |
| **Edge Cases** | Boundary conditions | Empty inputs, max values |
| **Security** | Vulnerability prevention | Injection, auth bypass |
| **Data Leak** | Information exposure | Sensitive data in logs/errors |
| **Data Damage** | Data integrity | Corruption, partial writes |

## Output Format

```markdown
# Test Specification for: [Task Name]

## Overview
- Task: P1-T01
- Scope: src/auth/validator.ts
- Test File: tests/auth/validator.test.ts

## Test Cases

### Category: Happy Path

#### Test #1: Validates correct JWT token
- **Intent**: Verify valid tokens are accepted
- **Preconditions**: Valid token exists
- **Input**: `{ token: "valid.jwt.token" }`
- **Expected Outcome**: `{ valid: true, userId: "123" }`
- **Completion Condition**: Returns validation result with user ID
- **Priority**: Critical

#### Test #2: Extracts user claims from token
- **Intent**: Verify claims are correctly parsed
- **Preconditions**: Token with standard claims
- **Input**: Token with sub, exp, iat claims
- **Expected Outcome**: Claims object with all fields
- **Completion Condition**: All claims accessible
- **Priority**: High

### Category: Bad Path

#### Test #3: Rejects expired token
- **Intent**: Expired tokens must be rejected
- **Preconditions**: Token with past expiration
- **Input**: `{ token: "expired.jwt.token" }`
- **Expected Outcome**: `{ valid: false, error: "TOKEN_EXPIRED" }`
- **Completion Condition**: Returns specific error code
- **Priority**: Critical

#### Test #4: Rejects malformed token
[...]

### Category: Edge Cases

#### Test #7: Handles empty token string
[...]

### Category: Security

#### Test #10: Prevents algorithm confusion attack
- **Intent**: Block tokens with "alg: none"
- **Preconditions**: Token crafted with no algorithm
- **Input**: Token with `{"alg": "none"}` header
- **Expected Outcome**: Rejection with security error
- **Completion Condition**: Never validates without proper algorithm
- **Priority**: Critical

### Category: Data Leak

#### Test #12: Token not logged on validation failure
[...]

### Category: Data Damage

#### Test #14: Concurrent validation doesn't corrupt state
[...]
```

## Enforcement Rules

### Test Immutability

Once tests are defined, they are contracts:

```
✗ WRONG: "Tests are failing, let's adjust expectations"
✓ RIGHT: "Tests are failing, let's fix the implementation"
```

### No Implementation Without Tests

```
✗ WRONG: Write code first, add tests later
✓ RIGHT: Write tests first, implement to pass
```

### Blocking Authority

The Test Master can block code that:
- Has no corresponding tests
- Has failing tests
- Has modified tests without approval

## Integration with Other Agents

```
task-execution-master ──▶ "Design tests for token validation"
                               │
                               ▼
                        idd-test-master
                               │
                   ┌───────────┴───────────┐
                   ▼                       ▼
         Test Specification         Enforcement
         (for code-guru)            (no skipping)
```

## Quality Standards

- Each test independently executable
- Tests are deterministic (no flaky tests)
- Names clearly describe scenarios
- Completion conditions objectively verifiable
- Security tests reference specific attacks
- Data damage tests include recovery verification

## Example Interaction

```
Input from task-execution-master:
{
  "task": "P1-T01",
  "title": "Token Validation",
  "description": "Validate JWT tokens for auth",
  "scope": "src/auth/validator.ts"
}

Output:
Test specification with 15 test cases:
- 3 happy path
- 4 bad path
- 3 edge cases
- 3 security
- 1 data leak
- 1 data damage

Passed to: idd-code-guru for implementation
```

## Best Practices

1. **More failure tests than success tests** - Bad paths are numerous
2. **Specific, not vague** - "Rejects expired token" not "handles errors"
3. **Independent tests** - No test depends on another's state
4. **Security by default** - Always include security tests
5. **Think like an attacker** - What could go wrong?

## See Also

- [Agents Overview](overview.md) - Agent team workflow
- [idd-task-execution-master](idd-task-execution-master.md) - Provides task definitions
- [idd-code-guru](idd-code-guru.md) - Implements to pass these tests
