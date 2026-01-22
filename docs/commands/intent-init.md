# /intent-init

> Initialize IDD structure in your project

## Usage

```bash
/intent-init
/intent-init --force    # Overwrite existing structure
```

## Purpose

Sets up the Intent directory structure and templates in your project, preparing it for Intent-Driven Development.

## When to Use

- Starting IDD in a new project
- Adding IDD to an existing codebase
- Resetting Intent structure (with `--force`)

## What It Creates

### Basic Structure

```
project/
└── intent/
    ├── INTENT.md              # Project-level Intent (template)
    └── architecture/          # (created if multi-module)
        ├── DEPENDENCIES.md    # Module dependency graph
        └── BOUNDARIES.md      # Boundary rules
```

### INTENT.md Template

```markdown
# [Project Name] Intent

> One-line project description

## Vision

What this project aims to achieve.

## Responsibilities

### What It Does
-

### What It Doesn't Do
-

## Structure

\```
[ASCII diagram of components]
\```

## Modules

| Module | Location | Description |
|--------|----------|-------------|
| | | |

## Dependencies

-

## Constraints

-
```

## Behavior

### New Project

Creates the full structure with templates.

### Existing Project

1. Checks for existing `intent/` directory
2. Reports what already exists
3. Offers to add missing pieces
4. Never overwrites without `--force`

### Multi-Module Detection

If the project has multiple packages/modules, also creates:
- `intent/architecture/DEPENDENCIES.md`
- `intent/architecture/BOUNDARIES.md`

## Example Session

```
> /intent-init

Checking project structure...

## Current State

- intent/ directory: Not found
- Package structure: Monorepo with 3 packages

## Actions

Creating IDD structure...

✓ Created intent/INTENT.md
✓ Created intent/architecture/DEPENDENCIES.md
✓ Created intent/architecture/BOUNDARIES.md

## Next Steps

1. Edit intent/INTENT.md with your project vision
2. Run /intent-interview to fill in details interactively
3. For each module, create module-level Intent:
   - packages/core/intent/INTENT.md
   - packages/api/intent/INTENT.md
   - packages/cli/intent/INTENT.md
```

## Options

| Option | Description |
|--------|-------------|
| `--force` | Overwrite existing Intent files |

## Related Commands

- [/intent-assess](intent-assess.md) - Evaluate project fit first
- [/intent-interview](intent-interview.md) - Fill Intent interactively

## See Also

- [Intent Standard](../intent-standard.md) - File format specification
- [IDD Workflow](../workflow.md) - Complete workflow guide
