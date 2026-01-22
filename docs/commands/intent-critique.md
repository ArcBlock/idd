# /intent-critique

> Critical review of Intent design quality

## Usage

```bash
/intent-critique
/intent-critique path/to/INTENT.md
```

## Purpose

Reviews your Intent for design quality issues, focusing on:

- Over-engineering
- YAGNI (You Aren't Gonna Need It) violations
- Premature abstraction
- Unnecessary complexity

This is an interactive discussion to refine design decisions.

## When to Use

- After `/intent-interview` before approval
- When Intent feels too complex
- Before starting implementation of a large feature
- When you want a second opinion on design choices

## What It Checks

### Over-Engineering Detection

| Pattern | Example | Better |
|---------|---------|--------|
| Too many abstractions | 5 layers for simple CRUD | 2-3 layers max |
| Premature generalization | "supports any data type" | Start with specific types |
| Configuration overkill | 20 config options | Sensible defaults |
| Future-proofing | "in case we need X" | Build X when needed |

### YAGNI Violations

- Features not in current requirements
- Flexibility nobody asked for
- "Nice to have" disguised as requirements

### Complexity Analysis

- Cyclomatic complexity hints
- Dependency count
- Interface surface area

## Interactive Process

The critique is a discussion, not a report. It will:

1. **Identify concerns** - Point out potential issues
2. **Ask questions** - "Do you really need X?"
3. **Suggest simplifications** - "What if we just..."
4. **Seek justification** - "Why is this necessary?"

## Example Session

```
> /intent-critique intent/payment-processor/INTENT.md

Reviewing Intent for design quality...

## Concern 1: Abstraction Layer

Your Intent defines a PaymentProviderInterface with 15 methods.

Current requirements mention only Stripe integration.

**Question:** Do you have concrete plans for other providers?

> We might add PayPal later

**Suggestion:** Start with direct Stripe integration. Extract interface
when you actually add PayPal. The right abstraction will be clearer then.

## Concern 2: Configuration Complexity

Your Intent specifies 12 configuration options including:
- retryStrategy
- circuitBreakerThreshold
- customWebhookParser

**Question:** Are these driven by actual requirements or "just in case"?

> The retry strategy is important, others are nice-to-have

**Suggestion:** Keep retryStrategy. Remove others until needed.
Simpler config = fewer bugs.

## Concern 3: Event System

You've designed a full event bus for payment events.

Current use case: Send email on successful payment.

**Suggestion:** Direct function call is simpler. Add event bus when you
have 3+ subscribers.

## Summary

| Issue | Severity | Recommendation |
|-------|----------|----------------|
| PaymentProviderInterface | Medium | Defer abstraction |
| Config complexity | Low | Remove 10 of 12 options |
| Event system | Medium | Use direct calls |

Accept simplifications? [y/n/discuss]
```

## Critique Philosophy

> "The best code is no code. The second best is simple code."

The critique follows these principles:

1. **YAGNI** - Don't build what you don't need today
2. **Simple first** - Start simple, add complexity when proven necessary
3. **Concrete before abstract** - Real examples before generalizations
4. **Three strikes** - Extract abstraction after third similar case

## Related Commands

- [/intent-interview](intent-interview.md) - Create Intent first
- [/intent-review](intent-review.md) - Approve after critique
- [/intent-changes](intent-changes.md) - Propose specific changes

## See Also

- [IDD Workflow](../workflow.md) - Where critique fits
- [Methodology](../methodology.md) - IDD philosophy
