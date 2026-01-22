# /intent-changes

> Structured change proposals with PR-like review experience

## Usage

```bash
/intent-changes start <file>    # Begin proposing changes
/intent-changes propose         # Suggest a change
/intent-changes accept          # Accept proposed change
/intent-changes reject          # Reject proposed change
/intent-changes finalize        # Apply all accepted changes
```

## Purpose

Manages structured change proposals for Intent documents, providing a collaborative review experience similar to Pull Requests but for Intent files.

## When to Use

- Multiple people reviewing Intent
- Major revisions to existing Intent
- When you want trackable change history
- Formal approval process required

## Workflow

```
┌─────────────────────────────────────────────────────────────┐
│                  /intent-changes Flow                        │
│                                                              │
│  start ──▶ propose ──▶ review ──▶ accept/reject ──▶ finalize│
│              │           │              │                    │
│              ▼           ▼              ▼                    │
│         Add changes   Discuss      Decision made             │
│         one by one    each one     per proposal              │
└─────────────────────────────────────────────────────────────┘
```

### Step 1: Start Session

```bash
/intent-changes start intent/INTENT.md
```

Opens a change session for the specified file.

### Step 2: Propose Changes

```bash
/intent-changes propose
```

Interactively propose a specific change:

```
What section to change?
> ## API

What's the current content?
> ### processPayment(amount)

What should it be?
> ### processPayment(amount, currency = 'USD')

Why this change?
> Support multi-currency payments per client requirement
```

### Step 3: Review Proposals

Each proposal shows:
- Current vs proposed content
- Justification
- Impact assessment

### Step 4: Accept or Reject

```bash
/intent-changes accept    # Accept current proposal
/intent-changes reject    # Reject with reason
```

### Step 5: Finalize

```bash
/intent-changes finalize
```

Applies all accepted changes to the file.

## Proposal Format

```markdown
## Proposal #1

**Section:** ## API
**Status:** pending

### Current
\```
processPayment(amount)
\```

### Proposed
\```
processPayment(amount, currency = 'USD')
\```

### Justification
Support multi-currency payments per client requirement.

### Impact
- Backward compatible (default parameter)
- Requires currency validation
- Tests need updating
```

## Example Session

```
> /intent-changes start intent/payment/INTENT.md

Change session started for intent/payment/INTENT.md
Session ID: changes-2024-01-21-001

> /intent-changes propose

Section to change: ## Responsibilities
Current: "Processes payments via Stripe"
Proposed: "Processes payments via Stripe and PayPal"
Reason: PayPal integration approved in Q1 roadmap

Proposal #1 created.

> /intent-changes propose

Section to change: ## API
Current: [current API section]
Proposed: [API with new PayPal methods]
Reason: Required for PayPal integration

Proposal #2 created.

> /intent-changes accept 1

Proposal #1 accepted.

> /intent-changes reject 2

Reason for rejection: Start with unified interface, not provider-specific methods

Proposal #2 rejected.

> /intent-changes finalize

Applied 1 change to intent/payment/INTENT.md

Changes:
- Proposal #1: Applied (Responsibilities update)
- Proposal #2: Rejected (API change)

Session closed.
```

## Best Practices

1. **One concern per proposal** - Don't bundle unrelated changes
2. **Explain why** - Justification is required
3. **Consider impact** - Note what else might need changing
4. **Keep atomic** - Each proposal should stand alone

## Related Commands

- [/intent-critique](intent-critique.md) - Review before changing
- [/intent-review](intent-review.md) - Approve sections after changes

## See Also

- [Intent Approval](../intent-approval.md) - Approval mechanism
- [IDD Workflow](../workflow.md) - Where this fits
