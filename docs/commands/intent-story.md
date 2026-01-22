# /intent-story

> Share your IDD adoption story

## Usage

```bash
/intent-story
/intent-story --lang zh    # Chinese output
/intent-story --lang en    # English output
```

## Purpose

Through structured interviewing, creates blog posts or articles about your Intent-Driven Development experiences, lessons learned, and best practices.

## When to Use

- Completed a project using IDD
- Want to share learnings with the community
- Writing internal case studies
- Contributing to IDD knowledge base

## Interview Process

The command conducts a structured interview covering:

### 1. Context

- What project did you use IDD for?
- What was the team size and experience?
- What development approach were you using before?

### 2. Adoption Journey

- What motivated trying IDD?
- How did you introduce it to the team?
- What was the initial reaction?

### 3. Experiences

- What worked well?
- What was challenging?
- Any surprises?

### 4. Results

- Measurable improvements?
- Team feedback?
- Would you use it again?

### 5. Advice

- Tips for others adopting IDD?
- What would you do differently?

## Output Formats

### Blog Post

```markdown
# How We Adopted Intent-Driven Development for [Project]

*By [Author] | [Date]*

## The Challenge

[Context from interview]

## Why We Tried IDD

[Motivation from interview]

## Our Journey

[Adoption story from interview]

## What We Learned

[Lessons from interview]

## Results

[Outcomes from interview]

## Advice for Others

[Tips from interview]

---
*This story was created with IDD /intent-story*
```

### Case Study

More formal format with metrics and structured sections.

### Quick Post

Shorter format suitable for social media or internal updates.

## Example Session

```
> /intent-story

Let's capture your IDD story!

## Context

What project did you use IDD for?
> Our payment processing system refactor

How large was the team?
> 4 developers

What were you using before IDD?
> Traditional user stories with Jira

## Adoption

What made you try IDD?
> We kept having misunderstandings between product and engineering.
> The Intent concept of "source of truth" appealed to us.

How did you introduce it?
> Started with one new module as a pilot

## Experience

What worked well?
> The structured interview process was great. It forced us to think
> through edge cases before writing code.
> The TDD agents caught issues we would have missed.

What was challenging?
> Getting the team to write ASCII diagrams took practice.
> Some resistance to "more documentation"

## Results

Any measurable improvements?
> 40% fewer bugs in code review
> Onboarding new devs is much faster with Intent docs

## Advice

What would you tell others starting with IDD?
> Start small. Pick one new feature.
> Don't try to retrofit everything at once.

---

Generating story...

Output: blog/idd-story-payment-system.md

Preview the story and edit as needed.
```

## Multi-Language Support

```bash
/intent-story --lang zh
```

Generates the story in Chinese, naturally written (not translated).

## Output Files

| Language | File |
|----------|------|
| English | `blog/idd-story-[project]-en.md` |
| Chinese | `blog/idd-story-[project]-zh.md` |

## Publishing

The generated story can be:
- Posted to your blog
- Shared internally
- Submitted to IDD community
- Added to project documentation

## Related Commands

- [/intent-report](intent-report.md) - Technical documentation
- [/intent-check](intent-check.md) - Validate before sharing

## See Also

- [Methodology](../methodology.md) - IDD philosophy to reference
- [IDD Workflow](../workflow.md) - The process you're documenting
