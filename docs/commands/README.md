# IDD Command Reference

> Complete list of all IDD skill commands

## Command Overview

### Setup Phase

| Command | Description |
|---------|-------------|
| [/intent-assess](intent-assess.md) | Evaluate if IDD fits your project, learn IDD methodology |
| [/intent-init](intent-init.md) | Initialize IDD structure in project |

### Creation Phase

| Command | Description |
|---------|-------------|
| [/intent-interview](intent-interview.md) | Create complete INTENT.md through structured interviewing |
| [/intent-critique](intent-critique.md) | Critical review for over-engineering, YAGNI violations |

### Review Phase

| Command | Description |
|---------|-------------|
| [/intent-review](intent-review.md) | Review and approve Intent sections (locked/reviewed/draft) |
| [/intent-changes](intent-changes.md) | Structured change proposals with PR-like review |

### Execution Phase

| Command | Description |
|---------|-------------|
| [/intent-build-now](intent-build-now.md) | **Validate Intent completeness, then launch TDD execution** |
| [/intent-plan](intent-plan.md) | Generate phased execution plan with strict TDD |

### Maintenance Phase

| Command | Description |
|---------|-------------|
| [/intent-sync](intent-sync.md) | Sync finalized details back to Intent after implementation |
| [/intent-check](intent-check.md) | Run validation and sync checks (triggers agents) |

### Report & Share

| Command | Description |
|---------|-------------|
| [/intent-report](intent-report.md) | Generate human-readable reports from Intent files |
| [/intent-story](intent-story.md) | Share your IDD experience, create blog posts (multi-language) |

## Common Workflows

### New Feature Development

```bash
/intent-interview     # 1. Create Intent from idea
/intent-critique      # 2. Check for over-engineering (optional)
/intent-review        # 3. Approve key sections
/intent-build-now     # 4. Validate and start TDD build
/intent-sync          # 5. Sync when done
/intent-check         # 6. Validate consistency
```

### Adopting IDD in Existing Project

```bash
/intent-assess        # 1. Evaluate fit
/intent-init          # 2. Set up structure
/intent-interview     # 3. Create Intent for existing modules
```

### Quick Health Check

```bash
/intent-check         # Run all validations
```

## Command Categories

### Interactive Skills

Commands requiring user interaction:

- `/intent-assess` - Q&A evaluation
- `/intent-interview` - Guided interview
- `/intent-critique` - Discussion-based review
- `/intent-review` - Section-level approval
- `/intent-changes` - Change proposals
- `/intent-story` - Experience interview

### Automated Commands

Commands that run to completion:

- `/intent-init` - Creates structure
- `/intent-build-now` - Launches agent team
- `/intent-plan` - Generates plan
- `/intent-sync` - Syncs changes
- `/intent-check` - Runs checks
- `/intent-report` - Generates reports

## See Also

- [IDD Workflow](../workflow.md) - Complete workflow guide
- [Agents Overview](../agents/overview.md) - TDD agent team
- [FAQ](../faq.md) - Common questions
