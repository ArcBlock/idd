# /intent-review

> Review and approve Intent sections

## Usage

```bash
/intent-review
/intent-review path/to/INTENT.md
```

## Purpose

Interactive section-by-section review and approval of Intent documents. Approved sections become implementation contracts that guide the TDD agents.

## When to Use

- After creating or modifying Intent
- Before starting implementation
- When preparing Intent for team handoff
- Before running `/intent-build-now`

## Section States

| State | Meaning | Icon |
|-------|---------|------|
| **draft** | Work in progress, not reviewed | |
| **reviewed** | Examined, may need changes | `[reviewed]` |
| **locked** | Approved, ready for implementation | `[locked]` |

## Review Process

```
┌─────────────────────────────────────────────────────────────┐
│                    Review Flow                               │
│                                                              │
│  Load Intent ──▶ Show Section ──▶ Review ──▶ Mark Status    │
│                       │                          │           │
│                       ▼                          ▼           │
│                  Discuss issues          draft/reviewed/locked│
│                  Ask questions                               │
│                       │                          │           │
│                       └──────────────────────────┘           │
│                                 │                            │
│                                 ▼                            │
│                          Next Section                        │
└─────────────────────────────────────────────────────────────┘
```

### What Gets Reviewed

1. **Responsibilities** - Clear scope and boundaries?
2. **Structure** - Diagram makes sense?
3. **API** - Signatures complete and correct?
4. **Examples** - Cover main cases?
5. **Constraints** - All limitations documented?

## Example Session

```
> /intent-review intent/auth/INTENT.md

Starting review of intent/auth/INTENT.md

## Section 1: Responsibilities [draft]

### What It Does
- Authenticates users via JWT tokens
- Manages refresh token rotation
- Validates token signatures

### What It Doesn't Do
- User registration (handled by user-service)
- Password reset flows

---

Review this section:
[l]ock  [r]eviewed  [d]raft  [c]omment  [n]ext  [q]uit

> l

✓ Section "Responsibilities" marked as [locked]

## Section 2: Structure [draft]

\```
┌─────────────┐     ┌─────────────┐
│  Middleware │────▶│  AuthService│
└─────────────┘     └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  TokenStore │
                    └─────────────┘
\```

Review this section:
[l]ock  [r]eviewed  [d]raft  [c]omment  [n]ext  [q]uit

> c

Comment: Where does the public key for signature validation come from?

Comment added. Continue reviewing?
[l]ock  [r]eviewed  [d]raft  [n]ext

> r

✓ Section "Structure" marked as [reviewed]

[...]

## Review Summary

| Section | Status |
|---------|--------|
| Responsibilities | [locked] |
| Structure | [reviewed] - 1 comment |
| API | [locked] |
| Examples | [draft] |

Ready for implementation: Partially
- 2 sections locked
- 1 section needs clarification
- 1 section still draft

Run /intent-review again after addressing comments.
```

## Marking in File

After review, sections are marked in the Intent file:

```markdown
## Responsibilities [locked]

...

## Structure [reviewed]

<!-- Comment: Where does the public key come from? -->

...
```

## Best Practices

1. **Lock critical sections first** - API and Responsibilities are most important
2. **Don't lock drafts** - If uncertain, mark as reviewed
3. **Use comments** - Document questions for later
4. **Review incrementally** - Don't try to lock everything at once

## Related Commands

- [/intent-interview](intent-interview.md) - Create Intent before review
- [/intent-critique](intent-critique.md) - Design review before approval
- [/intent-build-now](intent-build-now.md) - Start building after approval

## See Also

- [Intent Approval](../intent-approval.md) - Detailed approval mechanism
- [IDD Workflow](../workflow.md) - Review in context
