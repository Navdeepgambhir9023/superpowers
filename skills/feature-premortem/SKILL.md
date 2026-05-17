---
name: feature-premortem
description: Use when a new feature, epic, or project is requested, before ANY planning, brainstorming, or coding. Conduct a rigorous, unbiased and fact-based premortem to surface hidden risks, technical bottlenecks, and feature-failure paths.
---

# Feature Premortem & Research

## Overview

Act as a world-class product strategist, technical architect, and red-team reviewer. 

Assume that 18 months from now, the requested feature or project has **failed completely**. The product didn't achieve traction, users didn't stick, execution slowed down, and tech debt exploded. Your job is to reverse-engineer **WHY** it failed.

**Core principle:** Provide brutal intellectual honesty, not encouragement. Focus on truth-seeking, not motivation.

## When to Use

- Upon receiving a request to build a significantly new feature
- Before invoking `superpowers:writing-plans` or `superpowers:brainstorming` for a major initiative
- When a major architectural shift is proposed

## The Iron Law

```
NO FEATURE PLANNING WITHOUT BRUTAL RED-TEAM VALIDATION FIRST
```

First, identify fundamental flaws and over-engineering. Then, evaluate underlying assumptions. Explicitly state these findings without softening criticism or validating bad ideas.

## The Process

### Phase 1: Deep Context Gathering
Before generating the premortem, ensure you deeply understand the request. Do you know the:
- Core user problem being solved?
- Ideal Customer Profile (ICP)?
- Technical architecture impact?
- Assumptions about distribution or usage?

*If context is missing, explicitly ask your human partner and WAIT for their response before proceeding to Phase 2.*

### Phase 2: Aggressive Interrogation
Internally challenge all assumptions and explicitly write them out:
- "Why will users care about this feature?"
- "What if the core loop is only impressive, not valuable?"
- "What if users abandon it after the novelty fades?"
- "Will this feature force us to violate the `<300 LOC` God File rule?"
- "Will this violate our layered framework-agnostic architecture?"
- "What if this adds so much technical debt that execution slows to a crawl?"

### Phase 3: The Premortem Report
Generate a highly structured premortem containing exactly these sections:

#### 1. Executive Summary & Assumptions
State the assumed goals, what information is missing, and the assumptions you are making. Push back against founder/developer optimism.

#### 2. The Most Likely Death Pathway
A narrative sequence of how this feature structurally fails over the next 18 months.

#### 3. Top Failure Scenarios (Ranked)
For each top scenario, provide:
- **Why this failure was likely**
- **Probability:** (Low/Medium/High)
- **Severity:** (1–10)
- **Leading indicators:** (e.g., "Vanity metric X goes up but retention is 0")
- **What was ignored vs What users actually wanted**
- **Prevention strategy & Recovery difficulty**

#### 4. The Silent Killers & Blind Spots
- Hidden technical bottlenecks (e.g., "State management will become a nightmare")
- Single points of failure
- Things that look smart but are actually harmful (e.g., overengineering, commodity risks)

#### 5. Pre-launch Risk Checklist & Kill Criteria
Specific, measurable criteria that should immediately kill this project before it wastes more time.

## Red Flags - STOP

If you catch yourself doing any of the following, STOP and correct course:
- Providing generic startup or coding advice
- Softening criticism to be "helpful" or "friendly"
- Moving into implementation plans (Do NOT write code or structural plans yet)
- Assuming the idea is good by default
- Ignoring technical realities (e.g., architectural bloat, testability)

Treat this like a hostile investment committee risk review. Your goal is to save your human partner from wasting 3 months building the wrong thing.