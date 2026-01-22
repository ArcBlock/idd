# idd-task-execution-master

> Transform Intent into phased TDD execution plans

## Role

The Task Execution Master is the orchestrator of the TDD agent team. It takes an approved Intent document and breaks it down into logical phases, each containing specific tasks with clear completion criteria.

## Responsibilities

1. **Intent Validation** - Verify Intent is complete before planning
2. **Phase Planning** - Organize work into logical phases
3. **Task Definition** - Create specific, actionable tasks
4. **TDD Enforcement** - Ensure test-first approach
5. **Completion Review** - Verify tasks are done correctly

## When It's Used

- After `/intent-build-now` validates the Intent
- When breaking down complex implementations
- For coordinating multi-phase development
- To review progress between phases

## Input

An approved Intent document containing:
- Clear responsibilities
- Structure diagrams
- API specifications
- Examples

## Output

### Execution Plan

```markdown
# Execution Plan for: [Intent Name]

## Intent Validation Status
- [x] Goals defined
- [x] Scope clear
- [x] Constraints identified
- [x] Acceptance criteria measurable

## Phase Overview
| Phase | Objective | Est. Tasks | Dependencies |
|-------|-----------|------------|--------------|
| 1 | Core functionality | 3 | None |
| 2 | Error handling | 2 | Phase 1 |
| 3 | Integration | 2 | Phase 2 |

## Phase 1: Core Functionality

**Objective:** Basic features work correctly
**Entry Criteria:** Intent approved
**Exit Criteria:** All unit tests pass, E2E gate verified

### Task P1-T01: Token Validation

**Title:** Implement JWT token validation
**Description:** Validate incoming JWT tokens for authenticity and expiration
**Preconditions:** None
**Completion Criteria:**
- All test cases pass
- No security vulnerabilities
- Error messages are clear

**Test Strategy:** Unit tests for all validation paths
**Assigned To:** idd-test-master → idd-code-guru

### Task P1-T02: Token Generation

[...]

### Phase 1 Gate

**Verification Script:**
\```bash
curl -X POST localhost:3000/auth/verify \
  -H "Authorization: Bearer $TOKEN" | jq .valid
\```

**Success Criteria:**
- [ ] Valid tokens accepted
- [ ] Invalid tokens rejected
- [ ] Expired tokens rejected
```

## Task Definition Format

Each task includes:

| Field | Description |
|-------|-------------|
| Task ID | Unique identifier (P1-T01 format) |
| Title | Concise, action-oriented |
| Description | What needs to be done and why |
| Preconditions | What must be complete first |
| Completion Criteria | Specific, measurable conditions |
| Test Strategy | How this will be tested |
| Assigned To | Agent sequence (test → code) |

## Phase Types

### Phase 0: Foundation (if needed)

- Infrastructure setup
- Core abstractions
- Shared utilities

### Phase 1-N: Implementation

- Primary functionality
- Feature by feature
- Building on previous phases

### Final Phase: Validation

- E2E testing
- Documentation verification
- Integration confirmation

## Interaction with Other Agents

```
task-execution-master
        │
        ├──▶ idd-test-master: "Design tests for P1-T01"
        │         │
        │         ▼
        │    idd-code-guru: "Implement to pass tests"
        │         │
        │         ▼
        ├──▶ idd-e2e-test-queen: "Verify Phase 1 gate"
        │
        └──▶ [Next phase...]
```

## Handling Incomplete Intent

If Intent is incomplete, the agent will:

1. **Stop planning** - Not proceed with incomplete information
2. **List gaps** - Clearly identify what's missing
3. **Advise against forcing** - Recommend completing Intent first
4. **Ask questions** - Use structured questions to fill gaps

Example:

```
## Intent Validation: INCOMPLETE

Cannot proceed with planning. Missing elements:

1. **API Section** - No function signatures defined
   → Run /intent-interview to complete

2. **Examples** - No input/output examples
   → Add examples to guide test design

3. **Constraints** - Error handling not specified
   → Define expected error behaviors

Recommendation: Complete Intent before starting implementation.
Force-starting leads to rework.
```

## Completion Review

After tasks are completed, the agent:

1. Reviews completion criteria against actual outcomes
2. Identifies deviations from plan
3. Documents lessons learned
4. Checks if Intent needs updates

## Best Practices

1. **Right-size phases** - Each completable in 1-3 days
2. **Clear dependencies** - Note prerequisites explicitly
3. **Measurable gates** - Objective verification at each gate
4. **No shortcuts** - Every task goes through TDD cycle

## See Also

- [Agents Overview](overview.md) - How agents work together
- [idd-test-master](idd-test-master.md) - Next in the chain
- [/intent-build-now](../commands/intent-build-now.md) - Triggers this agent
