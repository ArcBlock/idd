# /intent-assess

> Evaluate if IDD fits your project and learn about Intent-Driven Development

## Usage

```bash
/intent-assess
/intent-assess --learn    # Focus on IDD education
```

## Purpose

Before adopting IDD, this command helps you:

1. **Evaluate project fit** - Is IDD right for this project?
2. **Learn IDD methodology** - Understand the philosophy and practices
3. **Identify adoption path** - How to introduce IDD to existing projects

## When to Use

- Starting a new project and considering IDD
- Evaluating IDD for an existing codebase
- Onboarding team members to IDD concepts
- Deciding between IDD and traditional approaches

## Project Fit Criteria

### Good Candidates for IDD

| Factor | Why It Helps |
|--------|--------------|
| **New features/modules** | Clean slate for Intent-first design |
| **Complex business logic** | Intent clarifies requirements before code |
| **Team collaboration** | Intent as shared contract |
| **Long-term maintenance** | Intent survives developer turnover |
| **AI-assisted development** | LLMs work better with structured Intent |

### Less Suitable for IDD

| Factor | Why |
|--------|-----|
| Quick prototypes | Overhead not justified |
| One-off scripts | No long-term value |
| Pure refactoring | No new intent needed |
| Trivial changes | Simple enough without formal process |

## Output

The command provides:

1. **Fit Assessment**
   - Score based on project characteristics
   - Specific recommendations

2. **Learning Materials** (with `--learn`)
   - IDD philosophy overview
   - Comparison with TDD/SDD
   - Best practices

3. **Next Steps**
   - Recommended commands to run
   - Adoption strategy for your situation

## Example Session

```
> /intent-assess

Analyzing your project...

## Project Assessment

Based on the codebase analysis:

✓ Multiple modules detected - Good fit for Intent hierarchy
✓ Business logic present - Benefits from Intent clarity
✓ Tests exist - Can adopt TDD agents smoothly
△ Some legacy patterns - May need gradual adoption

## Recommendation: ADOPT

Start with one new feature using IDD, then expand.

## Suggested Next Steps

1. Run `/intent-init` to set up structure
2. Run `/intent-interview` for your next feature
```

## Related Commands

- [/intent-init](intent-init.md) - Initialize IDD structure
- [/intent-interview](intent-interview.md) - Create your first Intent

## See Also

- [IDD Workflow](../workflow.md) - Complete workflow guide
- [Methodology](../methodology.md) - IDD vs other approaches
