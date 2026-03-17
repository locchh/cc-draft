# CLAUDE.md Best Practices

## What is CLAUDE.md

CLAUDE.md is a critical file for providing project-specific context to Claude Code. It serves as an onboarding guide for AI to your project requirements and codebase.

## File Location

CLAUDE.md file is typically placed in the root of the project repository. For example, if you're working with the React web app, you should have this structure.

```
project-root/
├── CLAUDE.md
├── package.json
├── README.md
├── src/
├── components/
└── ...
```

## File Format

The file itself is structured in markdown format (.md stands for markdown).

```markdown
## Project Overview

Short explanation of what the project is.

## Tech Stack

- TypeScript
- Next.js
- Tailwind
- ShadCN

## Architecture

Explain folders and patterns.
```

## Common Sections

Include in a file the following sections:

1. Project overview
2. Tech stack
3. Architecture
4. Coding conventions
5. UI and design system rules
6. Content and copy guidance
7. Testing and quality bar
8. File and component placement rules
9. Safe-change rules
10. Specific Commands

---

## 01 — Project Overview

This is the highest-value section that creates context for Claude. In this section, you should explain in plain language:

- What the product is
- Who it is for
- What the app is trying to optimize for
- Most important business or UX constraints

## 02 — Tech Stack

This section prevents a lot of bad assumptions. Without this section, Claude may introduce libraries that are technically valid but wrong for your project.

State the actual technologies in use:

- frameworks
- programming language
- styling system
- etc

## 03 — Architecture

This is where you teach Claude how the repo is organized.

You need to describe:

- major directories
- responsibilities of each area
- data flow
- separation of concerns
- where new code should go

## 04 — Coding Conventions

Along with the project overview, this is the second most important section in the whole file because it has a direct impact on the quality of code output produced by Claude. It defines whether the code is readable and clear for anyone who will read it.

You need to include anything that impacts day-to-day code generation.

## 05 — UI & Design System Rules

For front-end projects, this section is gold.

Define:

- visual style
- spacing philosophy
- typography approach
- interaction patterns
- responsiveness
- accessibility expectations
- component usage rules

## 06 — Content and Copy Guidance

This section is underrated, especially for landing pages and product work.

State how copy should sound:

- concise or detailed
- technical or plain language
- aspirational or practical
- sentence length
- headline style
- forbidden patterns

## 07 — Testing and Quality Bar

Claude should know how finished work is validated.

Define:

- what tests to add
- when tests are required
- lint/typecheck expectations
- what "done" means

## 08 — File Placement Rules

This deserves its own section because it stops repo drift. The section is especially useful in mature repos where duplicate components become a problem fast.

You need to define rules for:

- where to create new files
- when to edit existing files
- when to create abstractions
- naming patterns

## 09 — Safe-Change Rules

Very valuable for real projects. It's a good idea to tell Claude what it should avoid changing casually. It reduces "technically smart but operationally risky" edits that will lead to pricey refactoring.

## 10 — Specific Commands

Anthropic recommends giving Claude concrete project context, and commands are part of that operational context.

Add the actual commands Claude should use (like install, dev, build, lint, test, format, storybook (if relevant), SQL database commands if safe).

Of course, only include commands that are real and current.
