---
name: generating-project-rules
description: Use when bringing Superpowers to a new repository, bootstrapping a new project, or when requested to write global AI rules. Creates or updates the CLAUDE.md file to hardcode global non-negotiable architectural constraints so they apply even when explicit skills aren't invoked.
---

# Generating Project Rules

## Overview

AI coding assistants rely on global instruction files (like `CLAUDE.md`, `.cursorrules`, or `AGENTS.md`) as their baseline system prompt. If these files don't explicitly enforce our codebase mandates, the AI will drift into bad habits (producing monolithic God Files, skipping tests, making massive bundled commits) whenever it is executing tasks without a specific skill invoked.

**Core principle:** Bake the constraints into the environment itself so the AI cannot "forget" the rules between sessions.

## When to Use

- At the start of a completely new project.
- When moving to an unconfigured or poorly-configured repository.
- When asked to "write a claude.md file" or initialize workspace rules.
- Before beginning major feature planning in a repo without global constraints.

## The Process

### 1. Analyze the Workspace
Quickly assess the project's tech stack (React, Node, Python, TS, etc.) to tailor the architectural guidelines specifically to the frameworks being used. Check if a `CLAUDE.md` already exists to avoid overwriting existing user-specific rules.

### 2. Generate the Rules (`CLAUDE.md`)
Create or append to the `CLAUDE.md` file in the root of the repository. The file **MUST** explicitly state the following Non-Negotiable "Iron Laws":

#### Fundamental AI Execution Mandates:
- **Zero God Files (< 250-300 LOC Limit):** The absolute highest priority. No source file, test file, or plan file may exceed 300 lines of code. If logic requires expanding a file beyond this, the logic MUST be extracted into a new, smaller single-responsibility module first.
- **Atomic, Isolated Git Workflow:** All development and debugging must physically take place on context-specific branches (e.g., `YYYY-MM-DD-feature-name`). You must make frequent, atomic functional commits using standard prefixes (`feat:`, `fix:`, `chore:`). Never commit unverified broken code attempting to sync.
- **Layered Architecture (Separation of Concerns):** Strictly segregate concerns based on the stack. (e.g., UI components separated from state/hooks in React; routing/controllers separated from business logic/services in backends).
- **Test-Driven Development (TDD):** The Red-Green-Refactor cycle is mandatory. No execution code is written without a failing test first. `testing-anti-patterns` apply (no monolithic God Test files).
- **Verification Before Completion:** Never claim a task, phase, or build is successful without executing the commands (tests, builds, linters) and independently verifying the output. Confidence is not proof.
- **Persistent Tracking (`tracking.md`):** During multi-step feature implementation, execution state MUST be recorded manually in a `tracking.md` file using markdown checkboxes so progress isn't lost across sessions or context windows.

### 3. Formatting
Ensure the rules are written assertively with clear markdown headers. The AI reading this file in the future should immediately recognize these as absolute constraints, not gentle suggestions.

```markdown
# Example CLAUDE.md Structure
## Global Constraints
(Include the <300 LOC rule, Atomic Commits, Layered Architecture)

## Development Workflow
(Include TDD, Verification Gate, `tracking.md` usage)

## Project Specifics
(Add any stack-specific instructions observed from the repo)
```