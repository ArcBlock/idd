# Intent Approval Mechanism

> Intent is the new source code.
> Code review is done by AI, Intent review is done by Humans.

[中文版](zh/intent-approval.md)

## Design Principles

1. **Progressive Enhancement** - Plain markdown readable without tools, better experience with tools
2. **Section Granularity** - Approval at section level, not entire file
3. **Visible Status** - See at a glance which areas need attention

---

## Approval Levels

```
┌─────────────────────────────────────────────────────────────┐
│  🔒 LOCKED (Constitutional)                                  │
│                                                              │
│  Core principles, modification requires explicit human       │
│  decision                                                    │
│  - Module boundary rules                                     │
│  - Core data structures                                      │
│  - Security constraints                                      │
│                                                              │
│  On modification: Must have human review with clear reason   │
├─────────────────────────────────────────────────────────────┤
│  ✓ REVIEWED (Accepted)                                       │
│                                                              │
│  Human has reviewed and accepted, modification needs         │
│  human attention                                             │
│  - API signatures                                            │
│  - Configuration formats                                     │
│  - Critical flows                                            │
│                                                              │
│  On modification: Notify human, can review afterwards        │
├─────────────────────────────────────────────────────────────┤
│  📝 DRAFT (Proposed)                                         │
│                                                              │
│  Design draft, Agent can freely iterate and optimize         │
│  - Implementation details                                    │
│  - Example code                                              │
│  - Supplementary explanations                                │
│                                                              │
│  On modification: No notification needed, human can          │
│  optionally review                                           │
└─────────────────────────────────────────────────────────────┘
```

---

## Markup Syntax

### Fenced Div Format

Use `:::` to wrap sections and mark status:

```markdown
::: locked
## Module Boundary Rules

Deploy module cannot directly access Router internals...
:::

::: reviewed {by=robert date=2026-01-19}
## API Signatures

### create(chamberPath, config, appsDir)

Creates a chamber...
:::

::: draft
## Implementation Suggestions

Consider using cache optimization...
:::
```

### Attribute Format

```
::: <status> {key=value key=value}
```

| Attribute | Description | Example |
|-----------|-------------|---------|
| by | Approver | by=robert |
| date | Approval date | date=2026-01-19 |
| reason | Lock reason | reason="Core architecture" |
| ticket | Related issue | ticket=#123 |

---

## Rendering

### Without Tools (GitHub/Editor)

```
::: locked
## Module Boundary Rules

Content...
:::
```

Plain text readable, section boundaries clear.

### With Tools (Intent Viewer)

```
┃🔒│ ## Module Boundary Rules         │
┃  │                                  │ LOCKED
┃  │ Deploy module cannot directly... │ Core architecture
┃  │                                  │
├──┼──────────────────────────────────┤
┃✓ │ ## API Signatures                │
┃  │                                  │ REVIEWED
┃  │ ### create(...)                  │ robert, 2026-01-19
┃  │                                  │
├──┼──────────────────────────────────┤
┃  │ ## Implementation Suggestions    │
┃  │                                  │ DRAFT
┃  │ Consider using...                │
```

---

## Toolchain Vision

### Layer 0: Plain Text (Current)

- Readable in GitHub/any editor
- `git diff` works
- `grep` can search for `::: locked` etc.

### Layer 1: Intent Viewer

- Render sidebar status markers
- Section background/border highlighting
  - locked = red border
  - reviewed = green border
  - draft = gray border
- Collapse/expand sections
- Status statistics (N locked, M reviewed, K draft)

### Layer 2: Intent Approver

- Interactive approval interface
- Click to mark reviewed/locked
- Auto-add by/date
- Batch approval

### Layer 3: Intent Diff

- Compare changes by section
- Highlight locked section modifications (⚠️ needs attention)
- Show status changes (draft → reviewed)
- Ignore minor changes in draft sections

### Layer 4: Intent History

- Timeline view
- Evolution history of each section
- Who approved what and when
- Link to git commits

---

## Agent Behavior Rules

### Modifying LOCKED Section

```
1. Detect modification to locked section
2. Pause, generate modification reason
3. Request human review
4. Wait for human confirmation before continuing
```

### Modifying REVIEWED Section

```
1. Allow modification
2. Record change
3. Notify human (can be async)
4. Human can review afterwards
```

### Modifying DRAFT Section

```
1. Modify freely
2. No notification needed
```

---

## Parsing Example

When agent parses intent file:

```javascript
const sections = parseIntent(content);

// sections = [
//   {
//     id: 'module-boundaries',
//     status: 'locked',
//     title: 'Module Boundary Rules',
//     content: '...',
//     meta: { reason: 'Core architecture' }
//   },
//   {
//     id: 'api-signature',
//     status: 'reviewed',
//     title: 'API Signatures',
//     content: '...',
//     meta: { by: 'robert', date: '2026-01-19' }
//   },
//   ...
// ]
```

---

## Version History

| Date | Changes |
|------|---------|
| 2026-01-19 | Initial design |
