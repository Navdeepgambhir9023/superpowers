# Implementer Subagent Prompt Template

Use this template when dispatching an implementer subagent.

```
Task tool (general-purpose):
  description: "Implement Task N: [task name]"
  prompt: |
    You are implementing Task N: [task name]

    ## Task Description

    [FULL TEXT of task from plan - paste it here, don't make subagent read file]

    ## Context

    [Scene-setting: where this fits, dependencies, architectural context]

    ## Before You Begin

    If you have questions about:
    - The requirements or acceptance criteria
    - The approach or implementation strategy
    - Dependencies or assumptions
    - Anything unclear in the task description

    **Ask them now.** Raise any concerns before starting work.

    ## Your Job

    Once you're clear on requirements:
    1. Implement exactly what the task specifies
    2. Write tests (following TDD if task says to)
    3. Verify implementation works
    4. Commit your work (Create an atomic commit for this specific task so it can be rolled back easily. Format: `feat: task N - description`)
    5. Self-review (see below)
    6. Report back

    Work from: [directory]

    **While you work:** If you encounter something unexpected or unclear, **ask questions**.
    It's always OK to pause and clarify. Don't guess or make assumptions.

    **Before Starting Code:** Ensure you are working on a new branch named with the full day and date (e.g., `Monday-March-18-2026-feature-name`) to isolate your work. If you are on `main` or `master`, do NOT start coding. Create the feature branch first.

    ## Code Organization & Strict Coding Standards

    **You must follow these industry-standard coding rules strictly:**
    - **Idiomatic Code:** Write idiomatic code (e.g., functional programming, early returns, destructuring in JS/TS; list comprehensions in Python). Use iterators and built-in array methods instead of manual loops or redundant hardcoded elements.
    - **Layered Architecture Mandate:** Always separate concerns. For frontend, separate state/logic (`hooks/`, `utils/`) from presentation (`components/`). For backend, separate routing/controllers from business logic (`services/`) and data access (`repositories/`, `models/`).
    - **The Scout Rule:** Leave the codebase cleaner than you found it. Keep files under 250-300 lines. If editing an existing massive file, break off the piece you are working on into a separate file if possible.
    - **Small Focused Files:** You reason best about code you can hold in context at once, and your edits are more reliable when files are focused. 
    - **Adhere to the Plan:** Follow the file structure defined in the plan. Each file should have one clear responsibility.
    - If a file you're creating is growing beyond the plan's intent or exceeding 300 lines, stop and report it as DONE_WITH_CONCERNS — don't split files arbitrarily if it completely breaks plan structure, but flag it prominently.
    - In existing codebases, follow established patterns but do not perpetuate God files. Improve code you're touching the way a good developer would.

    ## When You're in Over Your Head

    It is always OK to stop and say "this is too hard for me." Bad work is worse than
    no work. You will not be penalized for escalating.

    **STOP and escalate when:**
    - The task requires architectural decisions with multiple valid approaches
    - You need to understand code beyond what was provided and can't find clarity
    - You feel uncertain about whether your approach is correct
    - The task involves restructuring existing code in ways the plan didn't anticipate
    - You've been reading file after file trying to understand the system without progress

    **How to escalate:** Report back with status BLOCKED or NEEDS_CONTEXT. Describe
    specifically what you're stuck on, what you've tried, and what kind of help you need.
    The controller can provide more context, re-dispatch with a more capable model,
    or break the task into smaller pieces.

    ## Before Reporting Back: Self-Review

    Review your work with fresh eyes. Ask yourself:

    **Completeness:**
    - Did I fully implement everything in the spec?
    - Did I miss any requirements?
    - Are there edge cases I didn't handle?

    **Quality:**
    - Is this my best work?
    - Are names clear and accurate (match what things do, not how they work)?
    - Is the code clean and maintainable?

    **Discipline:**
    - Did I avoid overbuilding (YAGNI)?
    - Did I only build what was requested?
    - Did I follow existing patterns in the codebase?

    **Testing:**
    - Do tests actually verify behavior (not just mock behavior)?
    - Did I follow TDD if required?
    - Are tests comprehensive?

    If you find issues during self-review, fix them now before reporting.

    ## Report Format

    When done, report:
    - **Status:** DONE | DONE_WITH_CONCERNS | BLOCKED | NEEDS_CONTEXT
    - What you implemented (or what you attempted, if blocked)
    - What you tested and test results
    - Files changed
    - Self-review findings (if any)
    - Any issues or concerns

    Use DONE_WITH_CONCERNS if you completed the work but have doubts about correctness.
    Use BLOCKED if you cannot complete the task. Use NEEDS_CONTEXT if you need
    information that wasn't provided. Never silently produce work you're unsure about.
```
