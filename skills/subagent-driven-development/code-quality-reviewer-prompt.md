# Code Quality Reviewer Prompt Template

Use this template when dispatching a code quality reviewer subagent.

**Purpose:** Verify implementation is well-built (clean, tested, maintainable)

**Only dispatch after spec compliance review passes.**

```
Task tool (general-purpose):
  Use template at requesting-code-review/code-reviewer.md

  DESCRIPTION: [task summary, from implementer's report]
  PLAN_OR_REQUIREMENTS: Task N from [plan-file]
  BASE_SHA: [commit before task]
  HEAD_SHA: [current commit]
```

**In addition to standard code quality concerns, the reviewer MUST check and strictly REJECT (send back to implementer) if any of these are violated:**
- **The God File Rule:** Reject any file approaching 250-300+ lines that hasn't been extracted into smaller logical modules. Mandate extraction.
- **Separation of Concerns:** Reject modules that mix responsibilities (e.g., UI components mixing state/business logic, or API routes mixing routing, validation, and database queries). Force the implementer to move logic into appropriate layers (e.g., `services/`, `controllers/`, `utils/`, or `hooks/`).
- **DRY (Don't Repeat Yourself):** Reject manual repetition (e.g., repetitive UI elements, redundant boilerplate, duplicated logic). Mandate idiomatic iterators (`.map()`, list comprehensions) or abstracted helper functions.
- **Cyclomatic Complexity:** Reject deeply nested `if/else` statements.
- **Are units decomposed** so they can be understood and tested independently?
- **Is the implementation following the file structure** from the plan?
- **Did this implementation create new files that are already large**, or significantly grow existing files? (Don't flag pre-existing file sizes — focus on what this change contributed.)

**Code reviewer returns:** Strengths, Issues (Critical/Important/Minor), Assessment
