# /intent-build-now

> Validate Intent completeness and launch TDD execution

## Usage

```bash
/intent-build-now
/intent-build-now path/to/INTENT.md
```

## Purpose

The bridge between Intent and implementation. This command:

1. **Validates** Intent completeness and quality
2. **Reports** any gaps that need fixing
3. **Launches** the TDD agent team when ready

## When to Use

- Intent is approved and ready for implementation
- After `/intent-review` has locked key sections
- When you want AI to take over the build process

## Validation Checks

### Required Sections

| Section | Why Required |
|---------|--------------|
| **Responsibilities** | Defines scope for agents |
| **Structure** | Guides architecture decisions |
| **API** | Contracts for test design |

### Quality Checks

| Check | Criteria |
|-------|----------|
| **Clarity** | No ambiguous terms |
| **Testability** | Examples map to assertions |
| **Boundaries** | Clear "what it doesn't do" |
| **Dependencies** | External deps listed |

### For Multi-Module Projects

- `intent/architecture/DEPENDENCIES.md` exists
- Module dependency graph defined
- No circular dependencies

## Execution Flow

```
┌─────────────────────────────────────────────────────────────┐
│                   /intent-build-now                          │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ Step 1: Locate Intent                                │   │
│  │ - Check intent/INTENT.md                             │   │
│  │ - Check current directory                            │   │
│  │ - Use provided path                                  │   │
│  └────────────────────────┬─────────────────────────────┘   │
│                           ▼                                  │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ Step 2: Validate Completeness                        │   │
│  │ - Check required sections                            │   │
│  │ - Verify quality criteria                            │   │
│  │ - Assess readiness                                   │   │
│  └────────────────────────┬─────────────────────────────┘   │
│                           │                                  │
│              ┌────────────┴────────────┐                    │
│              ▼                         ▼                    │
│  ┌───────────────────┐     ┌───────────────────────────┐   │
│  │ INCOMPLETE        │     │ READY                     │   │
│  │                   │     │                           │   │
│  │ Show gaps         │     │ Launch TDD Agent Team     │   │
│  │ Explain fixes     │     │ - task-execution-master   │   │
│  │ Recommend actions │     │ - test-master             │   │
│  └───────────────────┘     │ - code-guru               │   │
│                            │ - e2e-test-queen          │   │
│                            └───────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

## Example: Ready to Build

```
> /intent-build-now

Locating Intent...
Found: intent/auth/INTENT.md

Validating completeness...

## Intent Validation: PASSED ✓

Your Intent is ready for implementation:

✓ Responsibilities defined
✓ Structure documented (ASCII diagram found)
✓ API signatures clear (3 functions)
✓ Examples provided (5 cases)
✓ Dependencies listed

Launching idd-task-execution-master...

## Execution Plan

### Phase 1: Core Authentication
- Task 1.1: Token validation
- Task 1.2: Token generation
- Task 1.3: Refresh token rotation

### Phase 2: Integration
- Task 2.1: Middleware implementation
- Task 2.2: Error handling

Starting Phase 1...

[TDD agents take over]
```

## Example: Not Ready

```
> /intent-build-now

Locating Intent...
Found: intent/payment/INTENT.md

Validating completeness...

## Intent Validation: NEEDS WORK

Your Intent is missing critical elements:

### Missing Sections

❌ **Structure** - No ASCII diagram found

Add a component diagram:
\```markdown
## Structure

\```
ComponentA ──▶ ComponentB
     │
     ▼
ComponentC
\```
\```

❌ **API** - Function signatures incomplete

Define parameters and returns:
\```markdown
## API

### processPayment(amount, currency)

**Parameters:**
- amount: number - Payment amount in cents
- currency: string - ISO currency code

**Returns:** PaymentResult

**Errors:**
- InvalidAmount: When amount <= 0
\```

### Quality Issues

⚠ **Ambiguous term found:** "handles payments"
→ Specify: validate? process? record?

⚠ **No examples section**
→ Add input/output examples

### Recommended Actions

1. Add Structure section with ASCII diagram
2. Complete API signatures
3. Add Examples section
4. Run `/intent-build-now` again

**Do not proceed with implementation until Intent is complete.**
```

## TDD Agent Team

When validation passes, these agents are orchestrated:

| Agent | Role |
|-------|------|
| `idd-task-execution-master` | Creates phased execution plan |
| `idd-test-master` | Designs tests before implementation |
| `idd-code-guru` | Implements code to pass tests |
| `idd-e2e-test-queen` | Validates with E2E tests |

See: [Agents Overview](../agents/overview.md)

## Related Commands

- [/intent-review](intent-review.md) - Approve sections before build
- [/intent-plan](intent-plan.md) - Manual planning alternative
- [/intent-sync](intent-sync.md) - Sync back after build

## See Also

- [IDD Workflow](../workflow.md) - Build phase in context
- [Agents Documentation](../agents/) - How agents work
