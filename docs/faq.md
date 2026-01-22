# Frequently Asked Questions

## General

### What is IDD?

**Intent-Driven Development (IDD)** is a development methodology where Intent documents serve as the source of truth. Instead of code driving documentation, Intent drives code.

```
Traditional: Code → Documentation
IDD:         Intent → Tests → Code → Sync
```

### How is IDD different from TDD?

| Aspect | TDD | IDD |
|--------|-----|-----|
| Source of truth | Tests | Intent documents |
| Starting point | Write a test | Write Intent |
| Human review | Code review | Intent review |
| AI role | Assistance | Implementation |
| Documentation | After the fact | Built-in (Intent) |

IDD includes TDD as part of its workflow—tests are still written first before code, but they're derived from Intent.

### How is IDD different from SDD (Spec-Driven Development)?

| Aspect | SDD | IDD |
|--------|-----|-----|
| Organization | By requirement type | By module/layer |
| Core artifact | Text descriptions | Structure diagrams |
| Granularity | Split into user stories | Complete patterns |
| Task management | Separate task files | None - AI decomposes |
| LLM friendliness | Needs context assembly | Understands complete pattern |

### Do I need AI to use IDD?

IDD is designed for AI-assisted development but can be used without AI. The Intent documents still provide value as:
- Clear specifications
- Team communication
- Onboarding documentation

However, the full power of IDD comes from letting AI agents handle implementation while humans focus on Intent.

---

## Getting Started

### How do I start using IDD?

```bash
# 1. Install the plugin
npx add-skill arcblock/idd

# 2. Evaluate fit
/intent-assess

# 3. Initialize structure
/intent-init

# 4. Create your first Intent
/intent-interview

# 5. Start building
/intent-build-now
```

### Can I adopt IDD gradually?

Yes! Recommended approach:

1. **Start small** - Pick one new feature
2. **Don't retrofit everything** - Existing code can stay as-is
3. **Build confidence** - See the workflow work
4. **Expand** - Apply to more features

### What if my team doesn't want to change?

Start with yourself:
- Write Intent for your own features
- Show the benefits through results
- Share your Intent documents for review
- Let quality speak for itself

---

## Intent Documents

### What must an Intent document contain?

Minimum requirements:

```markdown
# [Name] Intent

> One-line description

## Responsibilities

### What It Does
- ...

### What It Doesn't Do
- ...

## Structure

\```
[ASCII diagram]
\```

## API

### functionName(params)
...
```

### Why ASCII diagrams instead of images?

1. **Version control** - Diffs are meaningful
2. **AI-readable** - LLMs understand text better
3. **Portable** - No external files needed
4. **Editable** - Anyone can modify inline

### How detailed should Intent be?

Enough for:
- AI to understand what to build
- Tests to be derived from it
- Another developer to implement it

Too little: "Make a payment system"
Too much: Line-by-line pseudocode
Just right: Clear API contracts, examples, boundaries

### Should I update Intent after implementation?

Yes! Use `/intent-sync` to:
- Capture final API signatures
- Document implementation decisions
- Keep Intent as accurate source of truth

---

## TDD Agents

### What are the TDD agents?

Four specialized agents that implement code from Intent:

| Agent | Role |
|-------|------|
| `idd-task-execution-master` | Breaks Intent into phases |
| `idd-test-master` | Designs tests before code |
| `idd-code-guru` | Implements to pass tests |
| `idd-e2e-test-queen` | Validates end-to-end |

### Can I skip agents?

Not recommended. The chain works together:
- Skipping test-master → code without tests
- Skipping code-guru → who implements?
- Skipping e2e-queen → no integration validation

### What if an agent makes mistakes?

Agents are not perfect. You can:
1. Review their output
2. Provide corrections
3. Re-run with clarifications

The Intent is your contract—if the agent deviates, the Intent helps you spot it.

### Can I use just some agents?

Yes. Common patterns:

- **Test-first only**: Use test-master, implement yourself
- **E2E only**: Use e2e-queen for verification
- **Full automation**: Let all agents work

---

## Workflow

### What's the difference between /intent-plan and /intent-build-now?

| Command | Output | Control |
|---------|--------|---------|
| `/intent-plan` | PLAN.md file | Manual execution |
| `/intent-build-now` | Automatic execution | Agent-driven |

Use `/intent-plan` when you want to review before executing.
Use `/intent-build-now` when you trust the process.

### How do I know if my Intent is ready?

Run `/intent-build-now` and it will tell you:
- What's missing
- How to fix it
- When it's ready

Or review yourself:
- [ ] Responsibilities defined?
- [ ] Structure diagram present?
- [ ] API signatures complete?
- [ ] Examples provided?

### What if implementation diverges from Intent?

1. **Small divergence**: Run `/intent-sync` to update Intent
2. **Large divergence**: Discuss with team, may need Intent revision
3. **Fundamental mismatch**: Stop, reassess, possibly restart

---

## Best Practices

### How do I write good Intent?

1. **Be specific** - "handles data" → "validates email format"
2. **Draw diagrams** - ASCII art is worth a thousand words
3. **Define boundaries** - What it doesn't do is important
4. **Include examples** - Every example becomes a test
5. **Think about errors** - What can go wrong?

### How do I review Intent?

Focus on:
1. **Clarity** - Could someone else understand this?
2. **Completeness** - Are all cases covered?
3. **Simplicity** - Is this over-engineered?
4. **Testability** - Can we verify this?

### When should I update Intent vs. create new?

**Update existing**:
- Bug fixes
- Minor enhancements
- Clarifications

**Create new**:
- New features
- Major changes in scope
- Different modules

---

## Troubleshooting

### "Intent validation failed"

Your Intent is missing required elements. Check:
- Does it have a Responsibilities section?
- Is there a Structure diagram?
- Are API signatures defined?

Run `/intent-build-now` to see specific gaps.

### "Tests are failing"

If tests fail after implementation:
1. **Don't modify tests** to pass
2. **Fix the implementation** instead
3. If tests are wrong, get test-master's approval to change them

### "Agent is stuck"

If an agent isn't progressing:
1. Check Intent clarity
2. Provide more specific context
3. Break the task into smaller pieces
4. Try running with more detailed prompt

### "Too much documentation overhead"

If Intent feels heavy:
1. Start smaller - one module at a time
2. Use `/intent-interview` to guide you
3. Remember: Intent replaces other docs, not adds to them

---

## Philosophy

### Why is "Intent the new source code"?

In AI-native development:
- Humans are better at defining what, AI at implementing how
- Code changes frequently, Intent is more stable
- Intent survives developer turnover
- AI can regenerate code from Intent

### Should humans review Intent or code?

**Humans review Intent** because:
- Intent is readable by non-developers
- Fewer lines to review
- Catches problems earlier
- Business logic is visible

**AI reviews code** because:
- AI is tireless and thorough
- Pattern matching at scale
- Consistency checking
- Tests validate correctness

### What's the future of IDD?

We believe:
- Intent will become standard project artifact
- AI will handle most implementation
- Human creativity focuses on Intent design
- Teams will be measured by Intent quality

---

## More Help

- [IDD Workflow](workflow.md) - Complete guide
- [Commands Reference](commands/) - All commands
- [Agents Documentation](agents/) - How agents work
- [Intent Standard](intent-standard.md) - File format
- [Methodology](methodology.md) - IDD philosophy
