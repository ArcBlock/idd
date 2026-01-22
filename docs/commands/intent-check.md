# /intent-check

> Run validation and sync checks

## Usage

```bash
/intent-check
/intent-check --validate    # Only format validation
/intent-check --sync        # Only sync check
```

## Purpose

Runs automated checks to ensure Intent files are valid and consistent with implementation. Triggers the validation agents automatically.

## When to Use

- After modifying Intent files
- Before committing changes
- As part of CI/CD pipeline
- Regular health checks

## Checks Performed

### 1. Format Validation (`--validate`)

Triggered agent: `intent-validate`

| Check | Description |
|-------|-------------|
| Structure | Required sections present |
| Hierarchy | Correct nesting and organization |
| Format | Markdown syntax, ASCII diagrams |
| Markup | Section status markers valid |

### 2. Sync Check (`--sync`)

Triggered agent: `intent-sync`

| Check | Description |
|-------|-------------|
| API Match | Signatures match implementation |
| Structure Match | Diagram reflects actual architecture |
| Naming | Terms consistent with code |
| Dependencies | Listed deps match actual imports |

## Output Format

```
> /intent-check

Running IDD checks...

## Format Validation

Checking intent/INTENT.md...
✓ Structure: All required sections present
✓ Hierarchy: Correct nesting
✓ Format: Valid markdown
⚠ Markup: 1 section missing status marker

Checking intent/auth/INTENT.md...
✓ All checks passed

## Sync Check

Comparing intent/auth/INTENT.md with src/auth/...
✓ API signatures match
✓ Structure matches
⚠ Naming: Intent says "AuthService", code has "AuthenticationService"
✓ Dependencies match

## Summary

| File | Format | Sync | Status |
|------|--------|------|--------|
| intent/INTENT.md | ⚠ 1 warning | - | Needs attention |
| intent/auth/INTENT.md | ✓ Pass | ⚠ 1 warning | Needs attention |

Total: 2 warnings, 0 errors

Run /intent-sync to fix sync issues.
```

## Exit Codes

For CI/CD integration:

| Code | Meaning |
|------|---------|
| 0 | All checks passed |
| 1 | Warnings found |
| 2 | Errors found |

## CI/CD Integration

### GitHub Actions

```yaml
- name: Check Intent
  run: |
    claude /intent-check
    if [ $? -eq 2 ]; then
      echo "Intent check failed"
      exit 1
    fi
```

### Pre-commit Hook

```bash
#!/bin/bash
# .git/hooks/pre-commit

if git diff --cached --name-only | grep -q "intent/"; then
  claude /intent-check --validate
  if [ $? -eq 2 ]; then
    echo "Intent validation failed. Fix errors before committing."
    exit 1
  fi
fi
```

## Severity Levels

| Level | Icon | Meaning | Action |
|-------|------|---------|--------|
| Pass | ✓ | Check passed | None |
| Warning | ⚠ | Minor issue | Should fix |
| Error | ✗ | Critical issue | Must fix |

## Common Issues

### Format Issues

| Issue | Fix |
|-------|-----|
| Missing section | Add required section to Intent |
| Invalid status marker | Use `[draft]`, `[reviewed]`, or `[locked]` |
| Broken ASCII diagram | Fix diagram syntax |

### Sync Issues

| Issue | Fix |
|-------|-----|
| API mismatch | Run `/intent-sync` |
| Naming inconsistency | Update Intent or code to match |
| Missing dependency | Add to Intent dependencies section |

## Related Commands

- [/intent-sync](intent-sync.md) - Fix sync issues
- [/intent-review](intent-review.md) - Fix format issues
- [/intent-build-now](intent-build-now.md) - Validates before building

## See Also

- [Agents Overview](../agents/overview.md) - Validation agents
- [Intent Standard](../intent-standard.md) - Format specification
