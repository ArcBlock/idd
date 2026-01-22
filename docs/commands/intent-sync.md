# /intent-sync

> Sync finalized implementation details back to Intent

## Usage

```bash
/intent-sync
/intent-sync path/to/INTENT.md
```

## Purpose

After implementation is complete and tests pass, this command syncs confirmed details back to the Intent document. This keeps Intent as the accurate source of truth.

## When to Use

- Implementation is complete
- All tests pass
- API signatures or data structures evolved during implementation
- Architecture decisions were made that should be documented

## What Gets Synced

| Category | Examples |
|----------|----------|
| **API Signatures** | Final parameter types, return types |
| **Data Structures** | Actual field names, types |
| **Naming Conventions** | Class names, function names as implemented |
| **Architecture Decisions** | Patterns chosen, libraries used |
| **Constraints Discovered** | Limitations found during implementation |

## Sync Process

```
┌─────────────────────────────────────────────────────────────┐
│                     /intent-sync                             │
│                                                              │
│  ┌────────────────────────────────────────────────────┐     │
│  │ Step 1: Analyze Implementation                     │     │
│  │ - Read source files                                │     │
│  │ - Extract signatures, types, structures            │     │
│  │ - Identify patterns used                           │     │
│  └────────────────────────┬───────────────────────────┘     │
│                           ▼                                  │
│  ┌────────────────────────────────────────────────────┐     │
│  │ Step 2: Compare with Intent                        │     │
│  │ - Find differences                                 │     │
│  │ - Categorize: addition, modification, removal      │     │
│  └────────────────────────┬───────────────────────────┘     │
│                           ▼                                  │
│  ┌────────────────────────────────────────────────────┐     │
│  │ Step 3: Present Changes                            │     │
│  │ - Show diff for each section                       │     │
│  │ - Ask for confirmation                             │     │
│  └────────────────────────┬───────────────────────────┘     │
│                           ▼                                  │
│  ┌────────────────────────────────────────────────────┐     │
│  │ Step 4: Apply Updates                              │     │
│  │ - Update Intent file                               │     │
│  │ - Mark sections as [synced]                        │     │
│  └────────────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────┘
```

## Example Session

```
> /intent-sync intent/auth/INTENT.md

Analyzing implementation...
Found: src/auth/service.ts, src/auth/middleware.ts

Comparing with Intent...

## Differences Found

### API Section

**Original Intent:**
\```
### validateToken(token)
Returns: boolean
\```

**Actual Implementation:**
\```typescript
validateToken(token: string): TokenValidationResult {
  // Returns object with isValid, userId, expiresAt
}
\```

**Proposed Update:**
\```
### validateToken(token)

**Parameters:**
- token: string - JWT token to validate

**Returns:** TokenValidationResult
- isValid: boolean
- userId: string | null
- expiresAt: Date | null

**Errors:**
- MalformedTokenError: When token format is invalid
\```

Apply this update? [y/n/edit]
> y

✓ API section updated

### Structure Section

**Addition detected:** Error handling layer

\```
Original:
┌─────────────┐     ┌─────────────┐
│  Middleware │────▶│  AuthService│
└─────────────┘     └─────────────┘

Proposed:
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Middleware │────▶│ ErrorHandler│────▶│  AuthService│
└─────────────┘     └─────────────┘     └─────────────┘
\```

Apply this update? [y/n/edit]
> y

✓ Structure section updated

## Sync Summary

| Section | Status |
|---------|--------|
| Responsibilities | No changes |
| Structure | Updated |
| API | Updated |
| Examples | No changes |

Intent synced successfully.
```

## Sync vs Original Intent

| Aspect | Original Intent | After Sync |
|--------|-----------------|------------|
| **Role** | Design document | Implementation record |
| **Accuracy** | Aspirational | Verified |
| **Source** | Human design | Code-derived |

## Best Practices

1. **Sync after tests pass** - Don't sync broken implementations
2. **Review each change** - Don't auto-apply everything
3. **Keep design intent** - Sync facts, preserve philosophy
4. **Document why** - If implementation differs significantly, note why

## Related Commands

- [/intent-build-now](intent-build-now.md) - Build before sync
- [/intent-check](intent-check.md) - Validate after sync
- [/intent-review](intent-review.md) - Re-review if major changes

## See Also

- [IDD Workflow](../workflow.md) - Sync in the lifecycle
- [Intent Standard](../intent-standard.md) - File format
