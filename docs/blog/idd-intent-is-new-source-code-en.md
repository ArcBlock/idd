# Stop Writing Requirements Docs in the AI Era, Write Intent

We've open-sourced a methodology and toolkit called IDD (Intent Driven Development). The core idea in one sentence: **Tell AI "what you want," not "what to do."**

As AI-assisted programming becomes routine, traditional requirements documents, user stories, and technical specs feel increasingly out of place. They were designed for human-to-human collaboration. When applied to human-AI collaboration, you write a bunch of documents but AI still frequently misunderstands, leading to round after round of corrections. IDD takes a different approach: instead of telling AI how to do something, make clear what you want and let AI plan the implementation. This article explains why we took this approach and how it works in practice.

## SDD vs IDD

Software engineering has seen many attempts to solve the "think before you code" problem. SDD (Spec Driven Development) is one of them - the core idea is to write detailed specifications first, then implement according to the spec. Sounds reasonable, but it exposes problems in the AI era.

| Method | Flow | Problem |
|--------|------|---------|
| Traditional | Code → Test → Docs | Documentation often outdated or missing |
| SDD | Spec → Code → Test | Specs become stale, scattered across files |
| TDD | Test → Code → Docs | Tests can't express design intent |
| **IDD** | **Intent → Test → Code → Sync** | Intent expresses "what" and "why," AI handles "how" |

I have firsthand experience with SDD's formalism. Years ago at a major Seattle software company, there was a PM on the team who would turn anything into an endless formal document - something that could be explained in a few sentences would be split into a dozen user stories, perfectly formatted, watertight, but after reading it you still didn't know what the thing was supposed to do. When I tried Amazon's Kiro last year, that familiar feeling returned. Kiro is a typical SDD tool - it generates a bunch of spec files with nice structure, but the "writing for writing's sake" vibe is overwhelming. This isn't a tool problem, it's a mindset problem - taking traditional software engineering practices and transplanting them directly to the AI era. The tools changed but the thinking didn't.

The problem with SDD is that it still organizes information the traditional way: by requirement type (functional, UX, technical), split into user stories, with separate task files. This classification makes sense for human collaboration - product managers read functional requirements, designers read UX requirements, architects read technical requirements. But for AI, this classification fragments the complete context. AI needs to understand the full picture of a module, not piece together information from five different files. The finer you split things the traditional way, the more effort AI needs to reassemble them, and when it gets it wrong, you're back to endless corrections.

IDD thinks differently: organize by module rather than requirement type, maintaining complete context; don't write task files, let AI decompose tasks itself; Intent operates at a higher abstraction level, describing "what effect" rather than "how to implement." Compared to TDD, IDD adds an Intent layer before Test; compared to SDD, IDD doesn't prescribe implementation details, giving AI room to plan better solutions.

## Why IDD Works

You might ask: without detailed specs, how does AI know what to do? Here's a counterintuitive fact: **In many domains, AI knows "how to do it" better than humans.**

Recently I wanted to implement a 6502 CPU Emulator. This kind of task is traditionally considered "hardcore" - you need to understand CPU architecture, register design, instruction encoding and decoding, and the design phase alone requires poring over technical manuals. With the SDD approach, I'd need to write dozens of pages documenting every instruction and addressing mode - the spec might not even be finished before the project dies. But I just told AI: I need a 6502 Emulator that can correctly execute the standard instruction set with basic debugging capabilities. That's it.

The result made me realize something: the 6502 is a chip from 1975 that powered the Apple II and NES. The technical documentation and open-source implementations around it are countless - LLMs have seen more emulator code than any human expert. AI's module design was cleaner than what I would have come up with myself, and combined with TDD requirements, the whole implementation came together smoothly. Tasks that used to require the most senior engineers are actually easy for AI, because these classic problems have the most comprehensive coverage in training data.

This is the foundation of why IDD works: in domains well-covered by AI training data, you don't need to tell it how to do things - you just need to clearly state what you want. AI has seen more patterns than we have; its planned solution might be more reasonable than what we'd come up with ourselves. Human value lies in judging "what is the right thing to want" - that's the part that truly requires human wisdom.

## Intent Is the New Source Code

What this means is: **Code review can be done by AI, Intent review must be done by humans.**

AI excels at checking whether code follows conventions, has security vulnerabilities, or adheres to project style. But AI cannot judge "is this feature really what we want" - only humans can make that judgment. So human effort should focus on reviewing Intent, not line-by-line reviewing AI-generated code.

The difference between Intent and traditional requirements:

| Traditional Requirements | IDD Intent |
|--------------------------|------------|
| Organized by type (functional/technical/UX) | Organized by module |
| Describes "what to do" | Describes "what you want" |
| Written for humans | Written for AI + humans |
| Easily outdated after writing | Continuously synced with code |

Intent operates at a higher abstraction level. You don't need to tell AI what technology to use or how to layer things - let AI plan that. What you need to do is clearly describe: what's the end result, what are the constraints, how to handle edge cases.

## Intent File Structure

IDD Intent files use a three-layer structure:

**1. Structure Diagrams** - ASCII diagrams showing module relationships and data flow. Diagrams are more precise than text, and LLMs can directly "see" them.

**2. Constraint Rules** - Restrictions that must be followed, like dependency directions and boundary rules. Can be directly converted to lint rules or test assertions.

**3. Behavior Examples** - Concrete inputs and outputs, including edge cases. Can be directly converted to test cases.

Design principle: **Every layer must be verifiable.** Not vague descriptions, but constraints that can be checked with code.

## Toolkit

We built a Claude Code plugin:

| Command | Function |
|---------|----------|
| `/intent-assess` | Evaluate if IDD fits your project |
| `/intent-init` | Initialize IDD directory structure |
| `/intent-interview` | Transform ideas into INTENT.md through interviewing |
| `/intent-review` | Approve critical Intent sections |
| `/intent-plan` | Generate phased execution plan with strict TDD (test first, then implement) |
| `/intent-sync` | After implementation, sync finalized interfaces and structures back to Intent |
| `/intent-check` | Verify code-Intent consistency |
| `/intent-report` | Generate documentation from Intent |

`/intent-plan` transforms Intent into an executable phased plan. Every step enforces TDD: write tests first (including happy path, bad path, edge cases, security cases, data leak cases, etc. - bad cases should be detailed), then implement based on tests. Each phase ends with e2e verification, preferring CLI/script automation.

`/intent-sync` runs after implementation is complete, tests pass, and user confirms. It writes back the finalized interfaces, data structures, and naming conventions to Intent, making Intent the true single source of truth.

Complete workflow:

```
/intent-assess        # Evaluate fit
    ↓
/intent-init          # Initialize structure
    ↓
/intent-interview     # Create Intent
    ↓
/intent-review        # Approve critical parts
    ↓
/intent-plan          # Generate TDD execution plan
    ↓
[Execute: Test → Implement cycles]
    ↓
/intent-sync          # Sync back finalized details
    ↓
/intent-check         # Verify consistency
```

Installation:

```bash
npx add-skill arcblock/idd
```

## When to Use

**Good fit for IDD:**
- AI-assisted development is your primary workflow
- System software, frameworks, infrastructure
- Projects requiring strict architectural boundaries

**May not fit:**
- Highly regulated industries requiring traditional documentation formats
- Teams without AI tooling
- Projects needing user stories for non-technical stakeholders

## Closing Thoughts

Back to the opening question: What should humans tell AI? I believe the answer is tell it "what you want," not "how to do it." Spec-driven approaches easily become formalism in the AI era - you write piles of documents but AI still doesn't understand what you want. IDD takes a different direction: instead of specifying how to do things in detail, make clear what you want and let AI plan the implementation.

We've been using this approach ourselves for a while, and it feels like the right direction. Open-sourcing it in hopes it helps other teams too.

GitHub: [github.com/ArcBlock/idd](https://github.com/ArcBlock/idd)
