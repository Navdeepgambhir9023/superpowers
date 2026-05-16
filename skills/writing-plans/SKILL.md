---
name: writing-plans
description: Use when you have a spec or requirements for a multi-step task, before touching code
---

# Writing Plans

## Overview

Write comprehensive implementation plans assuming the engineer has zero context for our codebase. Document everything they need to know: which files to touch for each task, testing, docs they might need to check, and how to test it. Give them the whole plan as bite-sized tasks. Follow TDD principles while ensuring DRY and YAGNI practices, with frequent commits after each task.

**Code Formatting Guidelines:**
- **For new features:** Explain *what* we have to build and *why*, and include references to files we have to edit or create. Do NOT output large blocks of code in the plan file itself to save context tokens. Describe the logic and interfaces instead.
- **For existing debugging/modification:** Include code only in smaller chunks just to give an idea of where the problem is or what needs changing. Excessive code fills up the context too fast and results in higher token usage.

Assume they are a skilled developer, but know almost nothing about our toolset or problem domain. Assume they don't know good test design very well.

**Announce at start:** "I'm using the writing-plans skill to create the implementation plan."

**Context:** Development should happen in a standard in-place git branch named with the full day and date (e.g., `Monday-March-18-2026-feature-name`). Git worktrees are discouraged for this workflow unless explicitly requested.

**Save plans to:** A dedicated directory at `docs/nd/plans/Full Day & Date(for eg. Monday-March-18-2026 note. Do not keep spaces in dates use "-")-<topic>-plan/`
- Break the plan into smaller, manageable chunks (maximum 10 files).
- `00-overview.md`: Contains the Goals, Architecture, Tech Stack, and links/index of the phases.
- `01-<phase-name>.md`, `02-<phase-name>.md`, etc.: Phase-wise or feature-wise task checklists.
- (User preferences for plan location override this default directory)

## Scope Check

If the spec covers multiple independent subsystems, it should have been broken into sub-project specs during brainstorming. If it wasn't, suggest breaking this into separate plans — one per subsystem. Each plan should produce working, testable software on its own.

## File Structure & Decomposition Standards

Before defining tasks, map out which files will be created or modified and what each one is responsible for. This is where decomposition decisions get locked in.

**Strict Architectural Mandates:**
- **Zero God Files:** Design the plan specifically to prevent files from exceeding 250-300 lines of code. 
- **Separation of Concerns:** Enforce layered architecture. Feature plans MUST separate business logic from presentation/routing. For frontend, separate state/logic (`hooks/`, `utils/`) from UI (`components/`). For backend, separate routing/controllers from business logic (`services/`) and data access (`models/repositories/`). The plan MUST dictate building the logic layers before the presentation/routing layers.
- **DRY Design:** Ensure shared logic or repetitive lists are abstracted.
- Design units with clear boundaries and well-defined interfaces. Each file should have one clear responsibility.
- You reason best about code you can hold in context at once. Prefer smaller, focused files over large ones that do too much.
- Files that change together should live together. Split by responsibility, not by technical layer.
- In existing codebases, if a file you're modifying has grown unwieldy (>300 lines), including a split in the plan is REQUIRED. Do not let the agent add more weight to a God file.

This structure informs the task decomposition. Each task should produce self-contained changes that make sense independently.

## Bite-Sized Task Granularity

**Each step is one action (2-5 minutes):**
- "Write the failing test" - step
- "Run it to make sure it fails" - step
- "Implement the minimal code to make the test pass" - step
- "Run the tests and make sure they pass" - step
- "Commit" - step

## Plan Documents Structure

Every plan MUST be chunked into multiple files to make it easy to navigate and avoid context bloat.

### 1. The Overview File (`00-overview.md`)
Must start with this header:

```markdown
# [Feature Name] Implementation Plan Overview

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Follow the phase files in sequentially numbered order.

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

**Phases Index:**
- [Phase 1: Component Name](./01-component-name.md)
- [Phase 2: Next Component Name](./02-next-component.md)

---
```

### 2. The Phase Files (`01-<phase-name>.md`, etc.)
Must contain the bite-sized tasks structured using checkbox (`- [ ]`) syntax.

````markdown
# Phase N: [Phase Name]

### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`
- Test: `tests/exact/path/to/test.py`

- [ ] **Step 1: Write the failing test**
  - **Goal:** Verify that `function(input)` returns `expected`
  - *(Brief description or small code snippet if debugging)*

- [ ] **Step 2: Run test to verify it fails**
  Run: `pytest tests/path/test.py::test_name -v`
  Expected: FAIL with "function not defined"

- [ ] **Step 3: Write minimal implementation**
  - **What:** Create the `function(input)` returning `expected`. Details of the logic...
  - **Why:** To satisfy the exact requirement the test demands.
  - *(Brief description or small code snippet if debugging)*

- [ ] **Step 4: Run test to verify it passes**
  Run: `pytest tests/path/test.py::test_name -v`
  Expected: PASS

- [ ] **Step 5: Commit**
```bash
git add tests/path/test.py src/path/file.py
git commit -m "feat: add specific feature"
```
````

## No Placeholders

Every step must contain the actual content an engineer needs. These are **plan failures** — never write them:
- "TBD", "TODO", "implement later", "fill in details"
- "Add appropriate error handling" / "add validation" / "handle edge cases"
- "Write tests for the above" (without defining what tests to write)
- "Similar to Task N" (repeat the instructions — the engineer may be reading tasks out of order)
- References to types, functions, or methods not defined in any task

## Remember
- Exact file paths always
- Exact commands with expected output
- DRY, YAGNI, TDD, frequent commits

## Self-Review

After writing the complete plan, look at the spec with fresh eyes and check the plan against it. This is a checklist you run yourself — not a subagent dispatch.

**1. Spec coverage:** Skim each section/requirement in the spec. Can you point to a task that implements it? List any gaps.

**2. Placeholder scan:** Search your plan for red flags — any of the patterns from the "No Placeholders" section above. Fix them.

**3. Type consistency:** Do the types, method signatures, and property names you used in later tasks match what you defined in earlier tasks? A function called `clearLayers()` in Task 3 but `clearFullLayers()` in Task 7 is a bug.

If you find issues, fix them inline. No need to re-review — just fix and move on. If you find a spec requirement with no task, add the task.

## Execution Handoff

After saving the plan, offer execution choice:

**"Plan complete and saved to `docs/nd/plans/<filename>.md`. Two execution options:**

**1. Subagent-Driven (recommended)** - I dispatch a fresh subagent per task, review between tasks, fast iteration

**2. Inline Execution** - Execute tasks in this session using executing-plans, batch execution with checkpoints

**Which approach?"**

**If Subagent-Driven chosen:**
- **REQUIRED SUB-SKILL:** Use superpowers:subagent-driven-development
- Fresh subagent per task + two-stage review

**If Inline Execution chosen:**
- **REQUIRED SUB-SKILL:** Use superpowers:executing-plans
- Batch execution with checkpoints for review
