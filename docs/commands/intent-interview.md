# /intent-interview

> Create complete INTENT.md through structured interviewing

## Usage

```bash
/intent-interview
/intent-interview path/to/intent/
```

## Purpose

Transforms your ideas into a well-structured Intent document through a guided conversation. The interview ensures you capture all essential aspects before implementation.

## When to Use

- Starting a new feature or module
- Documenting existing functionality
- Clarifying requirements before coding
- When you have an idea but not a clear specification

## Interview Process

### Phase 1: Vision & Scope

Questions about:
- What problem are you solving?
- Who is the user/consumer?
- What's the core value proposition?

### Phase 2: Responsibilities

Questions about:
- What does this module/feature do?
- What does it explicitly NOT do?
- Where are the boundaries?

### Phase 3: Structure

Guidance on:
- Component breakdown
- Data flow
- ASCII diagram creation

```
Example output:

## Structure

\```
┌─────────────┐     ┌─────────────┐
│   Handler   │────▶│   Service   │
└─────────────┘     └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  Repository │
                    └─────────────┘
\```
```

### Phase 4: API Design

Questions about:
- Key functions/methods
- Parameters and return types
- Error conditions

### Phase 5: Examples

Guidance on:
- Input → Output pairs
- Edge cases
- Error scenarios

## Output

A complete INTENT.md file with:

```markdown
# [Feature Name] Intent

> One-line description

## Responsibilities

### What It Does
- Responsibility 1
- Responsibility 2

### What It Doesn't Do
- Explicit non-goal 1
- Explicit non-goal 2

## Structure

\```
[ASCII diagram]
\```

## API

### functionName(param1, param2)

**Parameters:**
- param1: Type - Description
- param2: Type - Description

**Returns:** Type - Description

**Errors:**
- ErrorType: When condition

## Examples

### Basic Usage

Input:
\```json
{ "field": "value" }
\```

Output:
\```json
{ "result": "success" }
\```

## Dependencies

- dependency1: Why needed

## Constraints

- Constraint 1
- Constraint 2
```

## Tips for Good Interviews

1. **Be specific** - "handles user data" → "validates email format and stores in database"
2. **Define boundaries** - What you won't do is as important as what you will
3. **Use ASCII diagrams** - A picture is worth a thousand words
4. **Include examples** - Every example becomes a test case
5. **Think about errors** - What can go wrong?

## Example Session

```
> /intent-interview

Starting Intent interview...

## Phase 1: Vision

What feature or module are you building?
> A rate limiter for API endpoints

Who will use this?
> Internal API handlers

What's the core goal?
> Prevent abuse by limiting requests per client

## Phase 2: Responsibilities

What specific actions will this perform?
> Track request counts per client IP
> Block requests when limit exceeded
> Reset counts after time window

What will this NOT do?
> Won't handle authentication
> Won't log blocked requests (caller's job)
> Won't persist counts across restarts

[Interview continues...]

## Interview Complete

Generated: intent/rate-limiter/INTENT.md

Next steps:
1. Review the generated Intent
2. Run /intent-critique to check for over-engineering
3. Run /intent-review to approve sections
```

## Related Commands

- [/intent-critique](intent-critique.md) - Review for over-engineering
- [/intent-review](intent-review.md) - Approve sections
- [/intent-build-now](intent-build-now.md) - Start implementation

## See Also

- [Intent Standard](../intent-standard.md) - File format specification
- [IDD Workflow](../workflow.md) - Where this fits in the process
